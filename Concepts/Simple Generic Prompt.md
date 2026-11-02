---
tags:
  - concept
publish: "true"
---

# Simple Generic Prompt Structure

**What it is**
1. ****Instruction**** — What exactly should the system do?
2. ****Context**** — Who is this for, and what situation should the system understand?
3. ****Input data**** — What information does the system need from you?
4. ****Output format**** — What should the answer look like?

You can define this also by approaching with a similar set of questions, if you still lack the clarity:

1. *What do you give the AI?* This defines the input.
2. *What should it give back?* This defines the output.
3. *How do you know it's good?* Here the TDD thought comes in, you find out by testing with a valid input, one that tests the boundary (see question #4), one that doesn't have the valid input)
4. *What must it **never** do?* Here you define constraints, or where the human takes over.

**When to use it**
This is a great clear prompt structure for clear topics. It forces you to have clarity about what you want to do and helps you define it. It's not great if the topic is unclear or very complex, then you'll need other prompts or techniques to first clarify the Job to be done.

**Example**
- [[Example Prompt]]

**Common mistake**
(the one thing people get wrong with this)

**Related**
- [[Constraints-vs-Instructions]]
