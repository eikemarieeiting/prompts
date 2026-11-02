#### Brief

- Chatbot
- Each Sales Rep posts an informal message
- A python code node organizes available info
- AI Agent aggregates and researches and outputs a proper json
- The json lands in a sheet with a responsible person
- A phython code node adds a scoring and prio model.
- A link and follow-up suggestions are sent to the sales rep so that they can pick up the follow-up task immediately.

= Standardized solution
- Informal entry just single point of truth
- Single point of truth in a sheet for everyone
- background check outsourced to AI.
- Clear follow-up for sales reps


Category ideas, need to allow unknown or unconfirmed

1. Lead Quality

	- Hot (budget confirmed + concrete need + timeline) — e.g. Viessmann, dm-drogerie markt
	- Warm (need identified, budget unclear/future) — e.g. Ritter Sport, SAP
	- Cold/nurture (no concrete need, exploratory contact) — e.g. elobau

2. Company
	- Often clear
3. Contact
	- Often unclear
4. Business Problem
	- Slow onboarding, department friction, transformation needs, also service needs (leadership training or else)
5. Budget Status
	- Approved, reserved, free naming for AI node
6. Organisational Scale
	- Target groups, company size, locations
7. Delivery Requirements
	- Practical workshops, scalable programs, long-term partnership, progress tracking, what's concrete/named
8. Requested Next Steps 
	- Incl. Follow-Up Timing/Urgency
9. Engagement Signals
	- Concrete requests, kept separate from impressions such as “very friendly”


#### prompt

```
# role

You are the sales assistant. Sales Reps send you notes from their trade fair encounters, you take these notes, organise them into categories, research missing or unconfirmed information, prioritise the lead quality and return a short actionable follow-up message in the chat, you also create a json output to be put into a database as single point of truth.

# Task

You organise the information into the following categories. Take the examples into account when classifying the input.

- 

Icons:
Hot - red circle
Warm - orange circle
Cold - light blue circle
Warming sign - unconfirmed or incomplete information

How to process missing or incomplete, or unclear information:

1. You use a websearch to search company information (size, locations)
2. You use the company website and web to associate contact persons if i.e. name or position are not clear. Map these as unconfirmed still.

# Output

You create two outputs:

1. An organised json matching the required scheme for further processing in a database.
2. A chat message:
   
   Craft a short and actionable response. Use human language and informal
   tone to specify the information you have recorded and what you have
   aggregated.
   
   Structure:
   
   1. Start with a personal greeting.
   2. Lead Quality (and why) and company, i.e. "dm is a hot lead based on..."
   3. Requested Next Step (and context, engagement signal)
   4. Who to contact
   5. Context: Here you list everything that seems relevant to craft a compelling follow up. 
   6. Refer to the database and say that this chat can be used to update information based on the company name.
   7. End with a nice greeting.
```


#### Feedback Hidayet

Rate each statement on a scale from 1 to 5 (1 – strongly disagree, 5 – strongly agree):

1. 5 - The overall purpose of the workflow is immediately clear.
2. 5 -  The workflow is organized into clearly identifiable sections.
3. 5 - I can understand what each major workflow section does.
4. 4 - I would feel confident making small changes to this workflow based on the documentation.

Also consider the following questions and write down your answer:

5. What aspects of the documentation were particularly helpful?
   *Each note was very clear, the headlines connected well to understand the whole flow.*
6. Which part of the workflow was most difficult to understand?
   *Regarding the scoring approach I would ask follow-up questions. I also did not find clearly when and how I'd call the optional company research*
7. Where could additional documentation improve clarity?
   *The documentations explains what and how very well, why was missing for me, which makes this easy to understand for someone who has context, and more difficult for someone outside the context.*
8. Were any sticky notes unnecessary or repetitive? 
   *Saw only one note which for me seemed not necessary: Update lead row (explains what, and I can see the what, this is what makes it repetitive for me)*





