---
publish: "true"
tags:
  - concept
---


# Constraints vs. Instructions

**What it is**
This dictate behavior, instructions tell an AI system which rules to follow, constraints define what to avoid. 

**When to use it**
- Consistency, defines i.e. a set format
- Relevance: Narrows down i.e. a topic or role to exclude everything else
- Safety & Compliance: blocks harmful or defines a more compliant response i.e. use a specific terminology or adding a legal disclaimer. 

**Example**
```
**Rolle:** Du bist ein professioneller Copywriter für eine Fitnessmarke.  
**Aufgabe:** Schreibe einen Werbetext für die neuen "ProFit Earbuds".

📋 **Constraints (Was die KI tun MUSS):**

- Nutze eine strukturierte **Bullet-Point-Liste** für die Hauptfeatures.
- Halte den Gesamttext unter **150 Wörtern**.
- Verwende einen **motivierenden und energiegeladenen Tonfall**.
- Nenne die Akkulaufzeit von **24 Stunden**.

🚫 **Restrictions (Was die KI NICHT tun DARF):**

- Verwende **keinen technischen Fachjargon** (z. B. keine Frequenzkurven oder Bluetooth-Protokolle nennen).
- Erwähne **keine Konkurrenzmarken** (wie Apple, Sony oder Bose).
- Nutze **keine Floskeln** wie „Das beste Produkt auf dem Markt“ oder „Revolutionär“.
```

**Common mistake**
- zu unspezifisch
- Besser: Instructions "Erwähne" vs. "Erwähne nicht"

**Related**
- [[Role-Prompting]]
