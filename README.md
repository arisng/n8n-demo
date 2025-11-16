# n8n Self-Hosting Roadmap

This workspace walks through a four-part learning arc that turns a brand-new user into an n8n power-user running a hardened, scalable, and automation-rich stack. Each demo folder (`demo1`, `demo2`, …) builds directly on the previous one, so progress through them in order.

## Quick Start

1. Clone this workspace and change into the repo directory.
2. Start with `demo1` and follow its `README.md` end-to-end before peeking at later demos.
3. After finishing each demo, capture lessons learned in your own notes—subsequent demos assume that context and reuse your prior artifacts (Docker Compose files, TLS assets, etc.).

## Demo Sequence

### `demo1` · Single-Node Docker Bootstrap

- **Focus & Outcomes**: Stand up n8n with Docker Compose, persistent volumes, and basic auth while practicing environment-variable hygiene, onboarding, and activation key management.
- **Depends On**: _None_
- **Grounding Sources**:
  - [n8n Docker installation](https://docs.n8n.io/hosting/installation/docker/) — canonical CLI flags and environment variables.
  - [Hostinger Docker tutorial](https://www.hostinger.com/tutorials/how-to-self-host-n8n-with-docker) — practical VPS walkthrough (directory prep, compose scaffolding).
- **Grounding Tasks**:
  1. Reproduce the official `docker run` + Compose samples locally and document any deviations.
  2. Capture the activation-key onboarding steps (email request, plan activation) with screenshots or notes for later demos.
  3. List the minimum environment variables (timezone, auth, encryption placeholder) in the demo README for reuse.

### `demo2` · Production Hardening

- **Focus & Outcomes**: Add HTTPS with NGINX/Certbot, enforce encryption keys, configure backups/logging/resource quotas, and write the initial operations runbook.
- **Depends On**: `demo1`
- **Grounding Sources**:
  - [n8n securing guide](https://docs.n8n.io/hosting/securing/overview/) — SSL, SSO/2FA, telemetry opt-out, and firewall guidance.
  - Hostinger SSL steps (same tutorial as above, section 5 onward) — cert issuance, reverse proxy config, restart commands.
- **Grounding Tasks**:
  1. Follow the securing guide’s checklist and map each item to concrete commands/log locations in the demo README.
  2. Automate certificate renewal validation (e.g., `certbot renew --dry-run`) and log the outcome.
  3. Define backup + log rotation commands citing their source paragraphs for traceability.

### `demo3` · Queue Mode & Scaling

- **Focus & Outcomes**: Swap SQLite for Postgres, introduce Redis, split main vs worker services, and tune execution retention/pruning (including guardrail-node validation post-upgrade).
- **Depends On**: `demo2`
- **Grounding Sources**:
  - [Queue mode documentation](https://docs.n8n.io/hosting/scaling/queue-mode/) — architecture expectations, environment variables, webhook processor examples.
  - [Contabo scaling guide](https://contabo.com/blog/self-hosting-n8n-a-comprehensive-docker-vps-guide/) — Docker Compose with Postgres, SSL optimizations, and scaling runbooks.
- **Grounding Tasks**:
  1. Derive the Compose stack (main, worker, Redis, Postgres) directly from the sources and annotate each service with the originating doc link.
  2. Implement execution pruning variables (`EXECUTIONS_DATA_*`) and record default vs tuned values in README tables.
  3. Script an upgrade test (pull → down → up) and verify guardrail-node availability, referencing the guide’s update section.

### `demo4` · Power-User Tooling

- **Focus & Outcomes**: Add external task runners, AI/LLM/MCP integrations, monitoring hooks, and collaboration workflows; bundle reusable templates and cost-model callouts.
- **Depends On**: `demo3`
- **Grounding Sources**:
  - [Task runner configuration](https://docs.n8n.io/hosting/configuration/task-runners/) — broker settings, auth tokens, runner images.
  - [Northflank architecture & pricing guide](https://northflank.com/blog/how-to-self-host-n8n-setup-architecture-and-pricing-guide) — managed Postgres/Redis patterns, cost baselines, worker deployment steps.
- **Grounding Tasks**:
  1. Stand up external runners referencing the doc’s environment variables and document broker auth handshake.
  2. Prototype at least one AI or MCP integration sourced from the official advanced-AI docs and record prerequisites.
  3. Summarize cost benchmarks (VPS vs managed platform) with citations to inform decision-making in the README.

## How to Use This Roadmap

- **Stay incremental**: Each demo README calls out “What’s New” so you can focus only on the delta from the previous stage.
- **Keep docs in sync**: Update `ROADMAP.md` whenever you add or reorder demos, and verify every demo folder contains its own README.
- **Reference canon**: External links above serve as the authoritative sources for commands and architecture decisions—mirror their practices inside the demos.
- **Iterate safely**: When experimenting, branch from the last stable demo so you can discard ideas without derailing the main learning path.
