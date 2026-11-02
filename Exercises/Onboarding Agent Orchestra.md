The workflow will include three agents:

1. **Onboarding Coordinator Agent**  
    The main agent. It receives the chat message from HR, extracts the relevant information, asks follow-up questions if anything is missing, and decides which specialized agent to call.
2. **Onboarding Info Agent**  
    A specialized agent that retrieves the accounts that need to be created for the new employee from Notion.
3. **Welcome Announcement Agent**  
    A specialized agent that announces the newbie to the team in Slack.

The HR manager will provide the following information in the chat:

- the new employee’s name
- the company email address the employee should receive
- the employee’s role and department
- the new employee’s start date

For example:

Sarah Johnson will join the Marketing department as a Marketing Specialist. Her company email should be [sarah.johnson@company.com](mailto:sarah.johnson@company.com). She will start working with us on August 1.

The coordinator agent should then decide what needs to happen:

- If information is missing, it asks the HR manager for the missing details.
- If all information is available, it calls the Onboarding Info Agent and the Welcome Announcement Agent.
- At the end, the coordinator summarizes what has been done.

See the workflow in action:

## Step 0: Prerequisites

To build this workflow, you need (besides your usual n8n setup):

- A free Notion workspace
    - A page with a database containing info about the existing departments, each department’s team lead, and a list of the services that new employees of each department need access to. [Example](https://learn.wbscodingschool.com/wp-content/uploads/2026/06/Screenshot-2026-06-29-180712.png)
    - [A connection for that workspace](https://www.notion.com/help/add-and-manage-connections-with-the-api#add-connections-in-your-workspace) 
    - That connection [added to the page that contains the database](https://www.notion.com/help/add-and-manage-connections-with-the-api#add-connections-to-pages)
    - The [Access token](https://www.notion.com/help/add-and-manage-connections-with-the-api#add-connections-to-pages) for the connection
- A [free Slack workspace](https://app.slack.com/plans/)
    - [An App within that workspace and the Bot User OAuth Token](https://docs.n8n.io/integrations/builtin/credentials/slack#using-api-access-token)
    - A channel to welcome new employees
    - The App added to that channel

## Step 1: Create the workflow and set up the Orchestrator Agent

Create a new workflow in n8n, add a chat trigger, and connect an AI Agent Node. Rename the Agent Node, e.g. “Onboarding Coordinator Agent”-

Attach the AI Agent Node to a chat model write a first version of the agent’s system message (we will refine it later) and add Simple Memory.

Here’s a possible system message for the orchestrator agent at this stage:

# Overview   
You are the **Onboarding Coordinator Agent** for the HR team. Your responsibility is to coordinate the onboarding process for new employees. You do **not** perform onboarding tasks yourself. Instead, you ensure that all required information has been collected and, in later versions of this workflow, delegate tasks to specialized agents.   
## Required Information   
Before the onboarding process can continue, collect the following information:   
- Employee name   
- Company email address   
- Role   
- Department   
- Start date  
## Instruction   
1. Analyze the HR manager's message.   
2. Extract all required information.   
3. Check whether any required information is missing. 4. If information is missing:   
- Ask a clear and concise follow-up question.   
- Only ask for the missing information and ask if it is required to move on.   
- Wait for the user's response before continuing.   
5. If all required information is available:   
- Confirm that you have understood the request. - Summarize the onboarding details in a structured way.   
- Do **not** perform any onboarding actions yet.

Test your agent with an example message, e.g.

```
Please onboard Sarah Johnson. She will join the Marketing department as a Marketing Specialist. Her company email should be sarah.johnson@company.com. She will start on August 1.
```

Test it one more time, but this time with missing information. Does the agent behave as expected?

## Step 2: Create the Onboarding Info Agent

Add a tool to the orchestrator agent and select “AI Agent Tool”. Attach a chat model.

Rename the sub-agent, then click to attach a tool and look for Notion. Select “Notion Tool (Consume Notion API)”. If this is your first time working with Notion in n8n, you will now need to establish the connection between n8n and Notion by setting your credentials.

Here is a possible tool description for the Onboarding Info Agent:

You are the Onboarding Info Agent.  
You must use the tool called "Get necessary accounts" that queries a Notion database.  
Search for the row where the department matches the department name provided by the user.

Return:  
- The name of the Team Lead from the database column "Team Lead"  
- A list of the Necessary Accounts from the column "Necessary Accounts"  
Return the actual database property values, not the Notion page link.

If the department cannot be found, say so.  
Always use the “Get necessary accounts” tool before you respond.

The Prompt (User Message) should be defined automatically by the model.

Configure your Notion tool to retrieve information from the correct database.

## Step 3: Adapt the Orchestrator’s System Message and Test

Now that the Onboarding Info Agent exists as a tool, we need to let the Orchestrator Agent know how to use it.

Here’s a possible adapted system message for the Ochestrator Agent:

# Overview  
You are the **Onboarding Coordinator Agent** for the HR team.  
Your responsibility is to coordinate the onboarding process for new employees. You do **not** perform onboarding tasks yourself. Instead, you collect the required information and delegate specialized tasks to other agents when needed.  
  
## Required Information  
Before the onboarding process can continue, collect the following information:  
- Employee name  
- Company email address  
- Role  
- Department  
- Start date  
  
## Available AI Agent Tool  
### Onboarding Info Agent  
Use the **Onboarding Info Agent** whenever you need information about a department.  
Provide the department name to the agent.  
The agent will return:  
- The department's team lead  
- The services that new employees in that department require  
Do not attempt to answer these questions yourself. Always use the Onboarding Info Agent.  
  
## Instructions  
1. Analyze the HR manager's message.  
2. Extract all required employee information.  
3. Check whether any required information is missing.  
4. If information is missing:  
- Ask a clear and concise follow-up question.  
- Only ask for the missing information.  
- Wait for the user's response before continuing.  
5. Once all required information has been collected:  
- Use the **Onboarding Info Agent** to retrieve onboarding information for the employee's department.  
- Wait for the agent's response.  
6. After receiving the department information:  
- Summarize the onboarding details in a structured format.  
7. Do **not** perform any additional onboarding actions yet.  
  
## Response Style  
- Be friendly, professional, and concise.  
- Ask follow-up questions only when necessary.  
- Do not make assumptions or invent information.  
- Always use the Onboarding Info Agent to retrieve department-specific information.

Test the agent and check if it provides the correct information.

## Step 4: Create the Welcome Announcement Agent

This agent is responsible for writing and sending a short welcome message in Slack. The message should introduce the new employee to the team and include relevant onboarding information that the coordinator has collected.

Add another AI Agent Tool to your Orchestrator Agent. Rename it “Welcome Announcement Agent”.

Add a tool to that new sub-agent, search for “Slack” and choose “Slack Tool (Consume Slack API)”. If this is your first time working with Slack in n8n, you will now need to establish the connection between n8n and Slack by setting your credentials.

Here is a possible tool description for the Welcome Announcement Agent:

You are the Welcome Announcement Agent for the HR team.   
Your responsibility is to write and send a friendly Slack message announcing a new employee to the team. You only handle Slack welcome announcements.   
## Required Input   
You need the following information before you can create the welcome announcement:   
- Employee name   
- Role   
- Department   
- Start date  
## Available Tool   
You have access to Slack. Use Slack to send the welcome announcement to the selected team channel.   
## Instructions   
1. Write a short and friendly welcome announcement.   
2. Send the message to the selected Slack channel.  
3. Return a short confirmation that the message was sent.   
## Message Guidelines   
The Slack message should:   
- welcome the new employee,   
- mention their role and department,   
- mention when they will start,   
- sound friendly and professional,  
- be short enough to work well as a Slack message,  
- contain emojis where appropriate.  
## Example Slack Message   
Welcome Sarah Johnson to the team! Sarah will join the Marketing department as our new Marketing Specialist on July 15. Please give her a warm welcome. ![👋](https://s.w.org/images/core/emoji/17.0.2/svg/1f44b.svg)  
## Response Style   
After sending the message, respond briefly and clearly.   
Example: The welcome announcement for Sarah Johnson has been sent to Slack.

Configure the Slack tool so it can send a message to your selected Slack channel.

## Step 5: Adapt the Orchestrator’s System Message Again and Test

The orchestrator’s system message needs to be adjusted one more time, so it knows what to do the Welcome Announcement Agent we just provided as a tool.

Here’s a possible adapted system message for the orchestrator agent:

# Overview
You are the **Onboarding Coordinator Agent** for the HR team.
Your responsibility is to coordinate the onboarding process for new employees. You do **not** perform onboarding tasks yourself. Instead, you collect the required information and delegate specialized tasks to other agents when needed.

## Required Information
Before the onboarding process can continue, collect the following information:
- Employee name
- Company email address
- Role
- Department
- Start date

## Available AI Agent Tools
### Onboarding Info Agent
Use the **Onboarding Info Agent** whenever you need information about a department.
Provide the department name to the agent.
The agent will return:
- The department's team lead
- The services that new employees in that department require
Do not attempt to answer these questions yourself. Always use the Onboarding Info Agent.

### Welcome Announcement Agent
Use the **Welcome Announcement Agent** after you have collected all required employee information.
Provide the following information to the agent:
- Employee name
- Role
- Department
- Start date
The agent will write and send a welcome announcement in Slack.

## Instructions
1. Analyze the HR manager's message.
2. Extract all required employee information.
3. Check whether any required information is missing.
4. If information is missing:
- Ask a clear and concise follow-up question.
- Only ask for the missing information.
- Wait for the user's response before continuing.
5. Once all required information has been collected:
- Use the **Onboarding Info Agent** to retrieve onboarding information for the employee's department.
- Use the **Welcome Announcement Agent** to send a Slack welcome announcement.
- Wait for both agents' confirmations.
7. After both agents have confirmed that they have completed their tasks successfully:
- Summarize the completed onboarding preparation in a structured format.
- Include:
- Employee name
- Company email address
- Role
- Department
- Start date
- Team lead
- Required services
- Slack announcement status

## Response Style
- Be friendly, professional, and concise.
- Ask follow-up questions only when necessary.
- Do not make assumptions or invent information.
- Always use the Onboarding Info Agent to retrieve department-specific information.
- Only use the Welcome Announcement Agent after the department information has been retrieved successfully.

Your workflow has now all necessary elements. Test it multiple times with different departments, leave out some of the required information, and also experiment with different models.