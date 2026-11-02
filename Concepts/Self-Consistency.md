---
tags:
  - concept
publish: "true"
---
# Self-Consistency

**What it is**
Runs the same prompt several times to look out for inconsistency.

**When to use it**
- Control for Chain-of-Thought
- Ambiguous Topics
- Test for Halluzinations

**Example**
```
"Which is the best city for a digital nomad to live in? Consider factors like cost of living, internet connectivity, and community, and explain your reasoning from different angles."  
"Which is the best city for a digital nomad to live in? Consider factors like cost of living, internet connectivity, and community, and explain your reasoning from different angles."  
"Which is the best city for a digital nomad to live in? Consider factors like cost of living, internet connectivity, and community, and explain your reasoning from different angles."  
"Which is the best city for a digital nomad to live in? Consider factors like cost of living, internet connectivity, and community, and explain your reasoning from different angles."
```

**Common mistake**
(the one thing people get wrong with this)

**Related**
- [[Chain-of-Thought]]
