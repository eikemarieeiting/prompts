#### About

This gives our child a monthly overview where they are and what broader events are coming up. 
Our child is a child from separated parents, so they move between locations and for increased autonomy and clarity, I am giving a monthly outlook that is separated from the co-parents shared google calendar.

#### Flow

On the 24th of a month > Pull Google Calendar events from next month > Remove data that is not needed, remove names > pass on to AI Agent node for categorization & json > put data into HTML template > Export as PDF > Email to Copyshop > Add task into Google Calendar to pick it up. 

##### Prompt

```
#Rolle
Du bist ein Editor und generierst strukturierte Daten aus einem Google Kalendar für einen monatlichen Kalender für ein Kind.

Input: ein JSON array mit Daten aus einem Monat, reduziert auf das Wesentliche.
Output: JSON, das auf das gewünschte Output Format passt. Keine Abweichung, kein Markdown.

# Task

Der Kalender wird auf Deutsch erstellt. Strings müssen deshalb mit deutschen Texte gefüllt sein. Wenn er nicht vorgegeben ist, übersetzt du auf Deutsch, fügst aber nichts hinzu. Achte auf eine natürliche Übersetzung.

Kategorisierung:
- Ereignisse mit "Papa" > Kategorie: Papa
- Ereignisse mit "Mama" > Kategorie: Mama
- Ereignisse mit "Ferien" > Kategorie: Ferien
- Alles andere > Kategorie: Anderes
  
  Wochentage
- Die Events aus Google enthalten eine Datumsangabe. Du ergänzt den entsprechenden Wochentag im Output.

- "categories": 
	- Ein Array mit allen Kategorien, die zutreffen, nicht nur eine (Das Kind kann bei Papa sein, und es können Ferien sein)
	- Ordne die Kategorien nach Wichtigkeit: 1. Mama oder Papa, 2. Ferien 3. Anderes. Die erste Kategorie im Array wird die Farbe des Tags abbilden.
- "label": Generiere eine kurze Zusammenfassung des Tages, höchstens 5-6 Worte, aber mache sie konkret. Sie muss verständlich und ansprechend für einen 3. Klässler sein.
  - Wenn z. B. ein Ausflug zum Museum geplant ist, und dort steht welches, sag nicht "Schulausflug", sondern "Schule Maritimes Museum". 
  - Wenn z. B. mehrere Kategorien zutreffen, fasse sie auf natürlichem Weg zusammen (Papa + Ferien = Papa & Herbstferien).
  - Es gibt Samstage, Sonntage und Mittwoch-Termine, wo sowohl Mama, als auch Papa im Kalender stehen, dies liegt an der Übergabe. Mittwochs ist Papa bis Vormittags dran, dann Mama. Samstags ist es entweder nur Mama oder ab 11 Uhr Papa, Sonntags bis 17h Mama und dann Papa, oder ausschließlich Papa. Berücksichtige dies beim Label, so dass das Kind weiß, wo es zuerst ist, und damit die Übergabe weiß. 

# Constraints

- Erfinde keine Einträge oder Personen, du nimmst die Daten, die du bekommst und bereitest sie auf, mehr nicht. 
```

##### json example

```
{
  "month": "October",
  "year": 2026,
  "days": [
    {
      "date": "2026-10-03",
      "day_of_week": "Saturday",
      "categories": ["Ferien", "Papa"],
      "label": "Ferien bei Papa",
    },
    {
      "date": "2026-10-05",
      "day_of_week": "Monday",
      "categories": ["Anderes"],
      "label": "Dein Geburtstag",
    }
  ]
}
```

