# Codex Development Template

![Codex Development Template](./.assets/cover.png)

A clean, orchestration-first starter for teams building with [Codex](https://openai.com/codex/).

Use it in two ways:
- **as a GitHub template** to start a new project with docs, prompts, skills, and structure already in place
- **as a Codex plugin** to make the included skills available across any Codex session

Run **`start`** after cloning or generating a repo, and Codex guides the setup before implementation begins.

---

## Install as a Plugin

To make the bundled skills available globally in Codex:

```bash
git clone https://github.com/hdtinh57/codex-orchestrated-project-template
ln -sf "$(pwd)/codex-orchestrated-project-template/.codex" ~/.codex/plugins/codex-orchestrated-project-template
```

That's it. The eleven domain skills (`frontend`, `backend`, `database`, `mobile`, `design`, `content`, `quality`, `docs`, `cicd`, `docker`, `planning`) will appear in your Codex skill list immediately.

To update:

```bash
cd codex-orchestrated-project-template && git pull
```

The symlink means you always run from the latest version.

---

## Use as a Project Template

### 1. Create a new repository from this template

Click **"Use this template"** -> **"Create a new repository"** on GitHub.

Or with the GitHub CLI:

```bash
gh repo create my-project --template https://github.com/hdtinh57/codex-orchestrated-project-template --private --clone && cd my-project
```

### 2. Authenticate the GitHub CLI (optional)

```bash
gh auth login
```

Agents use `gh` directly for GitHub operations. One-time setup - persists across sessions. Skip if you don't need GitHub integration.

### 3. Open in Codex and run `start`

Codex reads `START_HERE.md` and begins the onboarding sequence - gathering project details, filling in documentation placeholders, and building the initial backlog from your requirements. At the end, `start` self-installs the plugin.

### 4. Start building

Once onboarding completes, `START_HERE.md` is deleted. Use `TODO.md` for the backlog, or run `status` for a full project health overview.

---

## What This Is

An opinionated project scaffold that gives Codex everything it needs to act as a coherent development team from day one:

- **5 consolidated agents** covering all disciplines - each thin by design, invoking domain skills rather than carrying knowledge in their system prompts
- **11 domain skills** encoding craft knowledge: working protocols, decision frameworks, checklists, anti-patterns - loaded on demand, never bloating the base context
- **Optional Codex hooks** you can wire into `hooks.json` for guardrails like destructive-command blocking, formatting, and completion checks
- **MCP servers** pre-configured for live library documentation and structured reasoning - shared across the team via a committed `.mcp.json`
- **File-scoped rules** that inject TypeScript, migration, and test standards only when the relevant file type is open
- **Living documentation** that agents keep current as the project evolves
- **A product requirements document** protected from accidental edits
- **A backlog** agents consult when you ask "what should we work on next?"

---

## Prompt Packs

### `start`

Run once after creating a new project. Codex reads `START_HERE.md`, gathers project details, copies templates into place, fills in every placeholder, builds the initial backlog, and self-installs the plugin.

### `orchestrate <task description>`

Hand off a multi-agent task and let Codex coordinate execution. The orchestrator analyzes the task, identifies which agents are needed, determines execution order (parallel where safe, sequential where dependencies require it), registers work in the backlog, creates a feature branch, and runs agents wave by wave.

```
orchestrate add user authentication with email and password
```

Presents a wave plan for approval before anything runs. Stops and asks if a wave fails.

### `status`

Renders a live project health card: current branch, in-progress tasks, recent commits, open PRs, blockers. Read-only - completes in seconds.

### `sync-template`

Pull the latest `.codex/` directory from the upstream template into your project. Shows a diff and asks for confirmation. Local-only files are never deleted.

---

## Agents

Five consolidated agents, each invoking domain skills before starting work.

| Agent | Model | Role | Invokes |
|-------|-------|------|---------|
| `planner` | Codex | Backlog governance, sprint planning, architecture decisions, ADRs | `planning` skill |
| `builder` | Codex | All application code - frontend, backend, database, mobile | `frontend` / `backend` / `database` / `mobile` skill by task |
| `designer` | Codex | UX flows, design system, landing copy, SEO strategy | `design` / `content` skill by task |
| `quality` | Codex | E2E tests, test strategy, user guide, post-feature docs | `quality` / `docs` skill by task |
| `infra` | Codex | CI/CD workflows, Dockerfiles, container configuration | `cicd` / `docker` skill by task |

---

## Domain Skills

Eleven skills encoding domain craft - invokable in any session once the plugin is installed.

| Skill | What it covers |
|-------|----------------|
| `planning` | ICE scoring, dependency graphs, sprint health signals, C4 model, architecture patterns, ADR format, NFR checklist |
| `frontend` | Server vs. Client Component decisions, state management, Core Web Vitals, component patterns, form handling |
| `backend` | DDD building blocks, API design principles, OWASP security checklist, caching strategy, background jobs |
| `database` | Index decision framework, zero-downtime migration patterns, query optimisation, transaction isolation |
| `mobile` | Expo Managed vs. Bare decision, navigation architecture, JS thread performance, platform-specific patterns |
| `design` | Design decision framework, visual hierarchy, cognitive load principles, assets discovery protocol |
| `content` | AIDA/PAS/FAB frameworks, brand voice, keyword intent, on-page SEO checklist, JSON-LD templates |
| `quality` | Test pyramid strategy, Playwright fixtures, flakiness prevention, accessibility testing, CI optimisation |
| `docs` | Diataxis framework, conciseness discipline, USER_GUIDE structure, changelog format |
| `cicd` | Pipeline design, security scanning, release automation, deployment strategies, reusable workflows |
| `docker` | Multi-stage builds, BuildKit cache mounts, security hardening, docker-compose standards |

---

## What's Inside

```
|-- AGENTS.md                          # Master Codex instructions (auto-loaded every session)
|-- PRD.md                             # Product Requirements Document - agents read, never modify
|-- TODO.md                            # Prioritized backlog - humans curate, agents consult
|-- START_HERE.md                      # Onboarding protocol - deleted after setup
|-- .mcp.json                          # MCP server config (sequential-thinking, context7)
|-- .codex/
|   |-- .codex-plugin/
|   |   `-- plugin.json                # Plugin manifest - makes skills installable
|   |-- agents/                        # 5 consolidated agents
|   |   |-- planner.md                 # Backlog & architecture (Codex)
|   |   |-- builder.md                 # All application code (Codex)
|   |   |-- designer.md                # UX & content (Codex)
|   |   |-- quality.md                 # Testing & documentation (Codex)
|   |   `-- infra.md                   # CI/CD & containers (Codex)
|   |-- skills/                        # 11 domain skills (SKILL.md per directory)
|   |   |-- planning/                  # Project management & architecture craft
|   |   |-- frontend/                  # React/Next.js implementation patterns
|   |   |-- backend/                   # API & business logic patterns
|   |   |-- database/                  # Schema design & migration patterns
|   |   |-- mobile/                    # React Native & Expo patterns
|   |   |-- design/                    # UX design process & visual hierarchy
|   |   |-- content/                   # Copywriting frameworks & SEO
|   |   |-- quality/                   # Testing strategy & Playwright patterns
|   |   |-- docs/                      # Documentation writing (Diataxis)
|   |   |-- cicd/                      # Pipeline design & release automation
|   |   `-- docker/                    # Container architecture & security
|   |-- prompts/
|   |   |-- orchestrate.md             # orchestrate - multi-agent task execution
|   |   |-- status.md                  # status - live project health card
|   |   |-- start.md                   # start - onboarding protocol
|   |   `-- sync-template.md           # sync-template - pull latest .codex/ from upstream
|   |-- rules/                         # File-scoped rules - injected when matching files are open
|   |   |-- typescript.md              # *.ts, *.tsx - no any, strict null, explicit returns
|   |   |-- migrations.md              # *.sql, migrations/** - reversible, naming convention
|   |   `-- tests.md                   # *.spec.ts, *.test.ts - POM, data-testid, no test.only
|   |-- hooks.json                     # Lifecycle hook configuration
|   `-- templates/                     # Blank doc templates - synced from upstream
|-- .github/
|   `-- PULL_REQUEST_TEMPLATE.md
|-- .tasks/                            # Detailed task files - one per TODO item
`-- docs/                              # Created during onboarding from .codex/templates/
    |-- user/USER_GUIDE.md
    |-- technical/
    |   |-- ARCHITECTURE.md
    |   |-- DESIGN_SYSTEM.md
    |   |-- API.md
    |   |-- DATABASE.md
    |   `-- DECISIONS.md
    `-- content/
        `-- CONTENT_STRATEGY.md
```

---

## Key Conventions

**Commits** - [Conventional Commits](https://www.conventionalcommits.org/):
```
feat(auth): add OAuth2 login with Google
fix(api): handle null response from payment provider
```

**Branches**:
```
feature/<ticket-id>-short-description
fix/<ticket-id>-short-description
```

**PRD is read-only** - `PRD.md` is protected by a three-layer mechanism (warning block, AGENTS.md rule, agent system prompts). Agents will refuse to modify it without explicit human instruction.

**Documentation stays current** - Agents must update the relevant `docs/` file before marking any implementation task complete.

**Conventions are enforced, not advisory** - Hooks fire at the tool-call level: `guard-destructive.sh` blocks dangerous commands before they run; `format-on-write.sh` runs the project formatter on every save. File-scoped rules in `.codex/rules/` inject standards only when the matching file type is active.

---

## Design Principles

- **Skills over system prompts** - domain craft lives in invokable skills, not embedded in agent definitions; agents stay thin, knowledge stays reusable
- **Design before code** - `planner` produces specs and ADRs; `builder` implements
- **Copy before implementation** - `designer` defines page copy and keyword targets before `builder` builds marketing pages
- **Document ownership** - every `docs/` file has a declared owner agent; others don't overwrite
- **Append-only ADRs** - architectural decisions are never silently revised; a new ADR supersedes an old one
- **Tests map to requirements** - `quality` writes tests against FR-XXX items in the PRD, not implementation details
- **Hooks over instructions** - destructive command blocking, auto-formatting, and completion checks are shell scripts that fire 100% of the time

---

## License

[MIT](LICENSE)


