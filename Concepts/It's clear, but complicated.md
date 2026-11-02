---
tags:
  - concept
publish: "true"
---
# Strategies for when it's clear, and complicated

#### What works
When it's clear, and complex, this is great, because we can be more specific than in an unknown scenario. Here it is not so much about expanding the insight and surfacing information, it is about making sure the AI system follows the clarity. 

- [[Constraints-vs-Instructions]] help to make explicit what is clear.
- [[Self-Consistency]] helps to show whether the AI system reaches a reliable result consistency, if it handles the complicated situation, or even one that is complex in parts, correctly.

**Example**
```
# CONTEXT
Wir haben 3 Produkt-Ideen: Idee 1 Idee 2 Idee 3 

# TASK
Bewerte jede nach:

# INSTRUCTION
Problemrelevanz, Umsetzbarkeit in 1 Tag, KI-Mehrwert

# CHAIN-OF-THOUGHT
Empfiehl eine und begründe es in 3 Sätzen.

---

Wir haben 3 Produkt-Ideen: Idee 1 Idee 2 Idee 3 Bewerte jede nach:

Problemrelevanz, Umsetzbarkeit in 1 Tag, KI-Mehrwert [INSTRUCTIONS & CONSTRAINTS]. Empfiehl eine und begründe es in 3 Sätzen [CHAIN-OF-THOUGHT].

---

Wir haben 3 Produkt-Ideen: Idee 1 Idee 2 Idee 3 Bewerte jede nach:

Problemrelevanz, Umsetzbarkeit in 1 Tag, KI-Mehrwert [INSTRUCTIONS & CONSTRAINTS]. Empfiehl eine und begründe es in 3 Sätzen [CHAIN-OF-THOUGHT].
```

