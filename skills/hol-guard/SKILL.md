---
name: hol-guard
description: Protect supported local AI coding-agent runtimes with HOL Guard before mutation-bearing tool work.
version: 1.0.0
license: Apache-2.0
author: "@kantorcodes"
tags:
  - security
  - runtime-safety
  - ai-agents
  - coding-agents
---

## Instructions

Use this skill when an AI agent needs to establish HOL Guard around a supported local coding-agent harness before state-changing or otherwise high-impact tool work.

HOL Guard is an additive local runtime boundary. It does not replace the agent client's authentication, permissions, sandboxing, confirmations, repository policy, target-service authorization, tests, backups, or human review. Do not assume OpenHuman itself is a HOL Guard-supported harness; `hol-guard detect --json` is authoritative for current harness support.

### Install and verify HOL Guard

If HOL Guard is not already available and installation is in scope, prefer an isolated install:

```bash
pipx install hol-guard
hol-guard --version
```

Discover the exact supported harness instead of guessing an adapter name:

```bash
hol-guard detect --json
```

Use the harness identifier returned by `detect`. Then establish and verify Guard's managed protection path:

```bash
hol-guard bootstrap
hol-guard install <harness> --json
hol-guard run <harness> --dry-run --json
hol-guard doctor <harness> --json
```

Do not claim protection merely because the package installed. Continue only when Guard reports the selected harness as installed and healthy.

### Run protected work

Launch the supported harness through Guard:

```bash
hol-guard run <harness> --json
```

Treat a Guard deny, review-required decision, error, timeout, malformed result, unavailable runtime, or unhealthy installation as a stop condition for the protected mutation. Do not retry the same state-changing action through an unprotected agent session.

After work, inspect Guard-owned state and evidence as needed:

```bash
hol-guard status --json
hol-guard approvals list --json
hol-guard receipts list --json
```

If an approval is required, preserve the normal human approval flow. Do not fabricate or auto-resolve an approval.

### Scope boundaries

- HOL Guard protects supported local agent harness execution paths; it does not claim to run inside unrelated hosted products or APIs.
- Keep the target service's native RBAC, validation, confirmation, audit, and safety controls authoritative.
- Use `hol-guard detect --json` as the source of truth for current harness support.
- Do not execute a destructive target action merely to test whether Guard would block it.
- Guard Cloud is optional; local protection must not silently opt a user into cloud sync.

Canonical project: https://github.com/hashgraph-online/hol-guard

## Examples

**Protect a supported coding-agent session before a deployment workflow:**

```text
User: Use HOL Guard before my coding agent performs the deployment.
Agent: I will first detect the supported local harness, verify HOL Guard is installed and healthy, run the Guard dry-run, and only then launch that harness through HOL Guard before any deployment mutation.
```

**Stop when Guard requires review:**

```text
User: Continue with the production-changing command.
Agent: HOL Guard returned a review-required decision. I will not bypass it or retry through an unprotected session; the action remains stopped until the normal approval flow is resolved.
```

**Do not overclaim the boundary:**

```text
User: Does installing this skill mean OpenHuman itself is protected by HOL Guard?
Agent: Not automatically. I must use `hol-guard detect --json` to identify a currently supported local harness and establish Guard on that harness. OpenHuman's own controls remain separate.
```

## Dependencies

- Python 3.9+
- `pipx` recommended for isolated installation
- `hol-guard` package from PyPI
- A local AI coding-agent harness reported as supported by `hol-guard detect --json`
