# Assignment 3 — A Degree-Planning Agent

CSCI 395.32: AI Agents · Hunter College, CUNY · Fall 2026

Work in pairs. You build the **Riverview College degree-planning assistant**, a tool-using agent that answers students' questions about the Spring 2027 term: whether they can take a course, which sections are offered, whether two sections conflict, and how far they are from graduating. You write two of the agent's tools and its policy, test it on public cases and on six cases of your own, and improve it until it passes them.

Riverview College is fictional. Its data does not describe Hunter College or CUNY policy.

## Start here

1. Follow [`SETUP.md`](SETUP.md) to install the environment (about 15 minutes). This assignment runs locally, not in Colab.
2. Open `Assignment03_Degree_Planning_Agent.ipynb` and run the setup check, its first code cell.
3. Work through the notebook in order.

## What is in this folder

| File or folder | Contents |
|---|---|
| `Assignment03_Degree_Planning_Agent.ipynb` | the notebook you complete and submit |
| `data/` | the Riverview data (`catalog.json`, `sections.json`, `requirements.json`, `students.json`), the public cases (`public_cases.json`), and `README.md` with the rules every tool follows |
| `pyproject.toml`, `uv.lock`, `.python-version` | the environment definition, used by `uv sync` |
| `.env.example` | a template for your `.env` file with your OpenRouter key |
| `SETUP.md` | installation steps and troubleshooting |

Keep the notebook next to the `data/` folder: the notebook reads the data from there.

## What you submit

- The completed notebook, with its saved outputs.
- `results.json`, which the notebook writes in §11.

Do not submit your `.env` file or your API key.
