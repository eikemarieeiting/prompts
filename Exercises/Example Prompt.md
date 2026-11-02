---
tags:
  - ex
publish: "true"
---
#### Case #1 Customer-support Email Triage

1. ****Instruction**** — What exactly should the system do?
2. ****Context**** — Who is this for, and what situation should the system understand?
3. ****Input data**** — What information does the system need from you?
4. ****Output format**** — What should the answer look like?

*Instruction*

This system is the first Customer Service Triage point. It

1. reviews incoming emails
2. classifies them by sentiment and topic (billing, order, delivery, product information, complaint)
3. prioritizes (order changes > billing > delivery > complaint > product information)
4. Assigns a SLA (order changes 2 hrs, billing 2 hrs, delivery 1 day, complaint 1 day, product information 2 days)
5. Routes to the correct department.

This system is for customer service members to give them clear priorization what to act on first based on:

- Service Level
- Sentiment
- Topic

Input data: Incoming emails

Output: prioritized inbox
#### Weekly meal planning

Build your revised prompt with these four parts:

1. ****Instruction**** — What exactly should the system do?
2. ****Context**** — Who is this for, and what situation should the system understand?
3. ****Input data**** — What information does the system need from you?
4. ****Output format**** — What should the answer look like?

Create a weekly meal planner: 

- Input: List of items added to chat as file (i.e. receipt from grocery delivering service, or just a list of items that are in the pantry and should be used)
- Format: 
	- This is what we have this week
	- This is the season: spring/summer/autumn/winter
	- This is the current challenge: digestion/movement/time/travel/

Based on this, you give a 1 pager format to print on a DINA4:

Monday to Sunday, for each week:

- Breakfast box
- Breakfast 8h
- Lunch 12:30h
- Dinner 18:00h
- Preparation

Context:
- 47 perimenopausal woman
	- Vata-Pitta type in vata-pitta phase
	- Parent
- Child
	- 8 years, boy
	- Neurodermitis

Restrictions
- Avoid anything that comes in a package with more than 5 ingredients
- Avoid raw
- Avoid excess sugar
- Avoid excess salt
- Avoid excess coffee

Favorites
- Child
	- Lasagne
	- Pizza
	- Pasta
	- Hotdogs
	- Crêpes
- Mother
	- Scrambled eggs
	- Kitchari
	- Lentils
	- Salmon
	- Rice

Then add two quick checks:

- What would make you say the answer is useful?
	- Reasoning is there, all givens used
- What is still missing or ambiguous in your prompt?
	- Format would need to be more specific
	- Ways to upload givens needs to be stupid simple, forgot half of it
	- Shopping list
	- Son only avialable on some days (Co-Parenting schedule as context)
	- 

## Report-back

Be ready to share:

- your revised prompt;
- the most important change you made; and
- one criterion you would use to evaluate the answer.

You do not need to submit this activity. Keep the prompt if it may be useful in your Prompting Exercises worksheet or Prompting Handbook.
