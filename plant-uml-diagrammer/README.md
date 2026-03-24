# plant-uml-diagrammer

A Claude Code skill that generates [PlantUML](https://plantuml.com) diagrams from a plain-text description and saves them to a `diagrams/` folder.

## Usage

```
/plant-uml-diagrammer <description of artifacts and relationships>
```

**Example:**

```
/plant-uml-diagrammer A user logs in via the web app, which calls an auth service that checks a database and returns a JWT token
```

## What it does

1. **Fetches PlantUML documentation** for relevant diagram types to ensure valid syntax.
2. **Analyses your description** to identify entities, relationships, and flow.
3. **Selects the most appropriate diagram type** from:
   - Sequence — messages between actors/services over time
   - State machine — states, transitions, and events
   - Activity / Data flow — data moving through processing steps
   - Class — classes, attributes, methods, inheritance
   - Component / Deployment — deployed services, containers, nodes
   - C4 / Archimate — high-level people, systems, and relationships
4. **Generates a `.puml` file** with valid PlantUML syntax.
5. **Saves the file** to the `diagrams/` folder in your project (creates it if it doesn't exist).
6. **Reports back** with the diagram type chosen, file path, and any assumptions made.

## Output

A `.puml` file saved to `<project-root>/diagrams/<diagram-name>.puml`, ready to render with any PlantUML-compatible tool (VS Code extension, IntelliJ plugin, the PlantUML online server, etc.).
