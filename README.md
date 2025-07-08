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
