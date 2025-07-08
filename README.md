# Workflow Engine

A flexible workflow execution engine that supports API calls, AI interactions, and human-in-the-loop processes through YAML configuration files.

## Folder Structure

```plaintext
src/
├── engine/
│   ├── executor.ts          # Executes each workflow step
│   ├── parser.ts           # Parses YAML workflow definitions
│   ├── context.ts          # Shares data between workflow steps
│   └── stateManager.ts     # Manages and persists step state
├── config/
│   └── step_definitions.yml # Global step templates and configs
├── workflows/
│   └── clientA.yaml        # Example workflow for a client
└── index.ts                # Main entry point
```


---

## 🧩 Step Definition YAML Schema

Each step in your workflow is defined with the following structure:

| Field                | Required | Type    | Description                                      |
|---------------------|----------|---------|--------------------------------------------------|
| `id`                | ✅       | string  | Unique step identifier                           |
| `type`              | ✅       | enum    | Step type: `api`, `ai`, `human`                  |
| `requires_user_input` | ✅    | boolean | Whether the step requires user input to proceed  |
| `execution_name`    | optional | string  | Human-friendly label shown in UI or logs         |
| `input_schema`      | optional | object  | JSON schema for inputs                           |
| `output_schema`     | optional | object  | JSON schema for outputs                          |

---

## 🌐 API Endpoints

| Method | Endpoint    | Purpose                            |
|--------|-------------|------------------------------------|
| POST   | `/start`    | Start a workflow by ID or file     |
| POST   | `/stop`     | Stop a running workflow            |
| GET    | `/status`   | View current workflow state        |

---

## ⚙️ Getting Started

1. Define global steps in `config/step_definitions.yml`  
2. Create client workflows in the `workflows/` directory  
3. Run your engine:
   * bun run index.ts *
  # or
   * bun start *

## Example Usage
```bash
config/step_definitions.yml

steps:
  - id: say_hello
    type: api
    requires_user_input: false
    execution_name: "Say Hello"
    input_schema:
      type: object
      properties:
        name:
          type: string
    output_schema:
      type: object
      properties:
        greeting:
          type: string
  - id: say_bye
    type: api
    requires_user_input: false
    execution_name: "Say Goodbye"
    input_schema:
      type: object
      properties:
        name:
          type: string
    output_schema:
      type: object
      properties:
        farewell:
          type: string

workflows/example.yaml

workflow_id: hello-world
steps:
  - id: say_hello
    type: SYNC
    priority: 1
  - id: say_bye
    type: SYNC
    priority: 2


