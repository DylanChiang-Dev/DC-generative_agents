# 生成式代理人模擬專案 - 作業展示 Agent Notes

## Start Here

- Read this file first, then `RULES.md`, then the top policy section and latest entries in `MEMORY.md`.
- Keep `README.md` as the human-facing project overview; do not turn it into an agent log.
- Use `MEMORY.md` for durable collaboration notes, decisions, deployment facts, and gotchas.
- Do not write secrets, tokens, private keys, or `.env` values into repository files or logs.

## Repository

- Owner: `DylanChiang-Dev`
- Repository: `generative_agents`
- Origin: `https://github.com/DylanChiang-Dev/generative_agents`
- Local path: `/Users/dc/Documents/github/DylanChiang-Dev/generative_agents`
- Main branch: `main`
- Private: `False`

## Tech Stack

- No package manifest detected at repository root

## Common Commands

- No standard build command detected; inspect README before running project-specific commands.

## Work Rules

- Before editing, inspect the relevant source files and existing style.
- Keep changes small and reviewable; avoid unrelated refactors.
- Run the fastest relevant check after changes.
- Commit completed work with a clear Chinese commit message unless the user asks otherwise.
- Push only after the local verification for the change has passed.

## Documentation Map

- `README.md`: project overview for humans.
- `AGENTS.md`: current agent entrypoint and operating notes.
- `RULES.md`: stable repository-specific rules.
- `MEMORY.md`: progressive collaboration memory and historical notes.

## Migrated From `AGENTS.md`

```markdown
# 生成式代理人模擬專案 - 作業展示 Agent Notes

## Start Here

- Read this file first, then `RULES.md`, then the top policy section and latest entries in `MEMORY.md`.
- Keep `README.md` as the human-facing project overview; do not turn it into an agent log.
- Use `MEMORY.md` for durable collaboration notes, decisions, deployment facts, and gotchas.
- Do not write secrets, tokens, private keys, or `.env` values into repository files or logs.

## Repository

- Owner: `DylanChiang-Dev`
- Repository: `generative_agents`
- Origin: `https://github.com/DylanChiang-Dev/generative_agents`
- Local path: `/Users/dc/Documents/github/DylanChiang-Dev/generative_agents`
- Main branch: `main`
- Private: `False`

## Tech Stack

- No package manifest detected at repository root

## Common Commands

- No standard build command detected; inspect README before running project-specific commands.

## Work Rules

- Before editing, inspect the relevant source files and existing style.
- Keep changes small and reviewable; avoid unrelated refactors.
- Run the fastest relevant check after changes.
- Commit completed work with a clear Chinese commit message unless the user asks otherwise.
- Push only after the local verification for the change has passed.

## Documentation Map

- `README.md`: project overview for humans.
- `AGENTS.md`: current agent entrypoint and operating notes.
- `RULES.md`: stable repository-specific rules.
- `MEMORY.md`: progressive collaboration memory and historical notes.

## Migrated From `CLAUDE.md`

```markdown
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

### Setup
- **Install Dependencies**: `pip install -r requirements.txt` (Python 3.9.12 recommended).
- **Configuration**: `reverie/backend_server/utils.py` contains API configuration:
  - `openai_api_key`, `openai_api_base`: API credentials and endpoint
  - `model_id`: Chat/completion model
  - `embedding_model_id`: Embedding model for memory retrieval
  - Currently configured for Doubao/Volcengine; modify for other OpenAI-compatible providers.

### Running the Simulation
Requires two concurrent servers:

1. **Environment Server** (Django):
   ```bash
   cd environment/frontend_server
   python3 manage.py runserver
   ```
   Access at: http://localhost:8000/

2. **Simulation Server**:
   ```bash
   cd reverie/backend_server
   python3 reverie.py
   ```

### Simulation Commands
At the `Enter option:` prompt:
- `run <step-count>` — Advance simulation (e.g., `run 100`). One step = 10 game seconds.
- `exit` — Quit without saving.
- `fin` — Save and exit.
- `call -- load history the_ville/<file>.csv` — Load agent memory history.

### Base Simulations
Fork from these when starting:
- `base_the_ville_n25` — 25 agents
- `base_the_ville_isabella_maria_klaus` — 3 agents (Isabella, Maria, Klaus)

### Utilities
- **Compress for Demo**: Edit target in `reverie/compress_sim_storage.py`, then:
  ```bash
  python3 reverie/compress_sim_storage.py
  ```
- **Test API Connection**: `python3 reverie/backend_server/test.py`

## Architecture

This project simulates "Generative Agents" using a dual-server architecture:

1.  **Environment/Frontend (`environment/frontend_server`)**:
    -   **Django Application**: Handles the visualization and environment state serving.
    -   **Static Assets**: `static_dirs/assets` contains maps, characters, and visuals.
    -   **Storage**: `storage/` stores simulation states; `temp_storage/` is used for runtime exchange.

2.  **Simulation/Backend (`reverie/backend_server`)**:
    -   **Core Logic**: `reverie.py` is the main entry point driving the agent behavior loop.
    -   **Persona (`persona/`)**: Contains cognitive modules for agents.
        -   `persona.py`: Main agent class.
        -   `cognitive_modules/`: Plan, Reflect, Retrieve, Perceive, Execute, Converse.
        -   `memory_structures/`: Associative memory, Spatial memory, Scratch (short-term).
    -   **World**: `maze.py` and `path_finder.py` handle spatial reasoning and movement.
    -   **LLM Interface**: `persona/prompt_template/gpt_structure.py` handles API calls to the LLM.

### Data Flow
- The simulation server (`reverie.py`) calculates agent actions and updates the state.
- State is persisted to the file system (`storage` directories).
- The frontend server reads this state to visualize the simulation in the browser.
- Communication between backend and frontend happens via file polling in `environment/frontend_server/temp_storage`.
```
```
