# n8n AI Automation Workflow Portfolio

This repository contains **two exported n8n workflow definitions**. They are source references for reproducible portfolio demonstrations, **not** evidence of a currently hosted or production-hardened service. Both exports currently set `active: false`; live execution, connector access, and error paths need to be validated in an isolated environment.

## Projects

| Workflow | Source | What it is designed to do |
| --- | --- | --- |
| Multimodal Telegram RAG + pgvector | [RAG workflow](RAG%20with%20pgvector%20telegram%20multiinput.json) | Telegram text/voice/image inputs, Google Drive file retrieval, chunking, embeddings, PostgreSQL pgvector search, agent replies, and Google Sheets integration. The graph includes an Ollama model, Gemini-related nodes, and Telegram delivery. |
| Telegram AI Secretary with agents + MCP | [AI Secretary workflow](Secretery_MCP_Gemini.json) | Telegram conversation through an orchestrator and specialist mail, calendar, and search agents. The exported graph includes Gmail, Google Calendar, Gemini, MCP client/server nodes, and voice/image handling. |

## Requirements and safe import

- A supported n8n instance with the required built-in and LangChain nodes; node availability varies by n8n version.
- You must configure **your own** Telegram, Google, Gmail, Calendar, Gemini/Ollama, PostgreSQL/pgvector, SerpApi or other credentials for the nodes you actually use. The exported credential IDs/references are **not reusable secrets** and may need clearing or replacing after import.
- Read the graph before activating any triggers. Check application scopes and the impact of send, reply, delete, and calendar-edit tools.
- Create a new test workspace with synthetic messages, dedicated test accounts, and isolated database / Google Drive content; disable or disconnect sending tools unless they send only to explicitly owned test destinations.
- Import through n8n **Workflows → Import from File**; open each node marked missing or unauthenticated; map credentials and environment-specific endpoint URLs; check connected services and current model identifiers.
- Keep webhook/MCP URLs, real OAuth token data, server addresses, real document IDs and chat IDs out of public examples and screenshots.

## Verification and video evidence

**A screenshot showing every node in green is not sufficient evidence.** n8n only colors nodes that executed on the actual path; conditionals, branch alternatives, manual triggers, and failure paths may remain unexecuted in one successful run.

For each workflow, capture a **2–4-minute** edited real-run walkthrough:
1. Show the graph overview and the trigger with the source of the demo input clearly labeled **synthetic**.
2. Show what the user experiences: a Telegram message or test file being received; for RAG, the retrieval/document reference and resulting grounded reply; for the Secretary, an actual mock/test calendar or Gmail action **without contacting real third parties**.
3. Show n8n's execution ID, execution status and key nodes with sensitive data redacted. Use **separate runs** to cover alternate paths (text, image, audio, error) rather than pretending one run traversed all branches.
4. Show output in the destination application (test chat, test calendar, test sheet or synthetic email) and cross-check the same execution ID/timestamp. For irreversible write tools, clearly label whether the action is real in a controlled test, simulated, or not tested.
5. Close with a factual table: `PASS / FAIL / NOT_TESTED` for each path, exact n8n version, known dependencies, and meaningful limitations.

Use screen crops rather than recording an entire desktop. Never show credentials, personal emails, live client messages, private Google Drive files, secret execution data, or any credential editor. Remove browser/account names and notification popups. Maintain unsanitized evidence privately only if it is legally appropriate and permitted, never in public Git.

## Production-readiness caveats

These JSON exports alone do **not** establish production readiness, security hardening, reliability, paid-client adoption, or any performance metric. Before offering the exact workflows as a managed service, independently validate authentication and access rights, retries, rate limits, idempotency/duplicate prevention, error paths, workload and API costs, backup/restore, and audit/redaction. Confirm current n8n node compatibility and provider terms.

## Security review needed before broad publication

These exports contain n8n credential **references and IDs** and workflow-specific connection parameters. Credential references are not API keys by themselves, but review and remove identifiers and customer-specific metadata that are unnecessary for reproducibility. Run a dedicated secret scan on exports and their **Git history**, not merely the latest files. Do not treat a preliminary text scan as proof of absence of sensitive material.
