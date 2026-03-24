---
name: plant-uml-diagrammer
description: Creates PlantUML diagrams from a text description. Selects the most appropriate diagram type (sequence, state machine, data flow, class, component, etc.) and saves the output to the diagrams folder.
argument-hint: <description of artifacts and relationships>
context: fork
agent: general-purpose
allowed-tools: WebFetch, WebSearch, Bash, Write, Read, Glob
---

# PlantUML Diagrammer

Your task is to generate a PlantUML diagram from the user's description and save it to the `diagrams/` folder.

## Input

The user's description: **$ARGUMENTS**

---

## Step 1 — Research PlantUML Syntax

Fetch the PlantUML documentation to understand current syntax for each diagram type. Use these reference pages:

- Sequence diagrams: https://plantuml.com/sequence-diagram
- State machine diagrams: https://plantuml.com/state-diagram
- Data flow / Activity diagrams: https://plantuml.com/activity-diagram-beta
- Component diagrams: https://plantuml.com/component-diagram
- Class diagrams: https://plantuml.com/class-diagram
- Deployment diagrams: https://plantuml.com/deployment-diagram
- C4 / Architecture: https://plantuml.com/archimate-diagram

Fetch only the pages relevant to the diagram type(s) you are considering. Read enough to understand the correct syntax so the generated `.puml` file will be valid.

---

## Step 2 — Analyse the Description

Read the user's description carefully and identify:

1. **Entities / Actors** — what are the participants, components, systems, or objects?
2. **Relationships** — how do they interact, depend on, or transition between each other?
3. **Flow or lifecycle** — is this a time-ordered interaction, a state lifecycle, a data pipeline, or a structural view?

---

## Step 3 — Select the Most Appropriate Diagram Type

Use this decision guide:

| Signals in the description | Best diagram type |
|---|---|
| Messages sent between actors / services over time | **Sequence** |
| States, transitions, events, guards | **State machine** |
| Data moving through processing steps / pipelines | **Activity (data flow)** |
| Classes, attributes, methods, inheritance | **Class** |
| Deployed services, containers, nodes | **Component / Deployment** |
| People, systems, relationships at a high level | **C4 / Archimate** |

State your choice explicitly and briefly justify it before writing any code.

---

## Step 4 — Generate the PlantUML Source

Write clean, valid PlantUML using:
- `@startuml` / `@enduml` delimiters
- A meaningful `title`
- Comments (`'`) where the diagram structure is non-obvious
- Grouping (`box`, `package`, `namespace`, `frame`) where it adds clarity
- Colours or stereotypes only when they improve readability — don't over-decorate

---

## Step 5 — Determine the Output Path

1. Use Glob to check whether a `diagrams/` directory already exists anywhere under the current working directory:
   - Pattern: `**/diagrams/`
   - If found, use the first result as the output directory.
   - If **not** found, create `./diagrams/` at the project root.

2. Derive a kebab-case filename from the diagram title, e.g. `user-login-sequence.puml`.

3. Full output path: `<diagrams-dir>/<filename>.puml`

---

## Step 6 — Write the File

Use the Write tool to save the `.puml` file at the path determined above.

---

## Step 7 — Report Back

Tell the user:
- Which diagram type you chose and why
- The full path to the generated file
- A short summary of what the diagram depicts
- Any assumptions you made about ambiguous parts of the description
