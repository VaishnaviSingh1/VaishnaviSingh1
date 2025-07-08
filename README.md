

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

```bash
bun run index.ts
# or
bun start
