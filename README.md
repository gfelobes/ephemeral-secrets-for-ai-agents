# Ephemeral Secrets for AI Agents

A demo of issuing short-lived credentials to agents that call external APIs, using Vault or a cloud secret manager.

## Features

- Integration with Vault or GCP Secret Manager
- Short-lived token generation for external API calls
- Runtime token injection into agent execution
- Automatic token expiry and renewal
- Per-tenant secret segregation

## Tech Stack

- Python, FastAPI
- Vault or GCP Secret Manager
- httpx / requests

## Getting Started

```bash
docker-compose up -d   # optional: start Vault dev server
pip install -r requirements.txt
uvicorn src.services.api:app --reload
```

## Demo Scenario
- Request an agent run via API.
- Observe the agent requesting a short-lived token.
- Use the token to call the external mock API.
- Show token expiry and renewed token on next run.

## Security Notes
See docs/threat-model.md for assumptions, risks, and mitigations.


ephemeral-secrets-for-ai-agents/
├─ src/
│  ├─ auth/
│  │  ├─ token_issuer.py
│  │  └─ vault_client.py
│  ├─ agents/
│  │  └─ external_api_agent.py
│  ├─ services/
│  │  └─ api.py
│  └─ config/
│     └─ settings.py
├─ tests/
│  └─ test_token_flow.py
├─ docs/
│  ├─ architecture.md
│  └─ threat-model.md
├─ docker-compose.yml   # optional Vault
├─ README.md
└─ requirements.txt
