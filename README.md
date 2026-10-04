# Ro Claude Plugins

Marketplace for Claude Desktop (Chat / Cowork / Projects) and claude.ai.
Generated - do not edit here. Source of truth is the Cursor command pack in the
Ro AI Base meta launcher (`template/.cursor/commands` + meta `.cursor/commands`),
built by `scripts/build-claude-plugin.ps1`.

## Install (once)

1. Claude Desktop -> **Customize** -> **Plugins** -> **Add marketplace**
2. Enter `https://github.com/RohmeoTheDev/ro-claude-plugins` (full HTTPS URL, not SSH)
3. Install **Ro Slash Commands** (id `ro`). Skills are slash-only: type `/ro:` in Chat or Cowork.

## Update

Cowork caches on the marketplace entry `version`. The build script bumps it
whenever any generated `SKILL.md` changes and pushes. In Desktop: marketplace
**Update** (or let *Sync automatically* run), then fully quit and reopen.

## Why this exists

Claude Code and the Desktop *Code* tab read `~/.claude/commands` and
`~/.claude/skills`. Desktop **Chat / Cowork / Projects** and claude.ai only load
skills and plugins enabled on the account - they never read `~/.claude`.

## Ro Slash Commands (`ro`) - v1.00 - 33 skills

| Skill | Description | Source |
|---|---|---|
| `/ro:audit-skills` | Sweep the global skills pool for staleness, duplication, and unsafe code | `.cursor/commands/audit-skills.md` |
| `/ro:boot` | Set up this new project — interview you, then write AGENTS.md and the workspace files | `template/.cursor/commands/boot.md` |
| `/ro:discover-skills` | Sweep trending agent skills across discovery sites; never install | `.cursor/commands/discover-skills.md` |
| `/ro:james-code-assess-debt` | Scan codebase for technical debt; prioritize remediation with ROI roadmap | `template/.cursor/commands/james-code-assess-debt-v1.00.md` |
| `/ro:james-code-explain-code` | Explain complex code with narratives, diagrams, step-by-step breakdowns | `template/.cursor/commands/james-code-explain-code-v1.00.md` |
| `/ro:james-code-implement` | Implement features via subagent, following existing patterns | `template/.cursor/commands/james-code-implement-v1.00.md` |
| `/ro:james-code-migrate` | Plan and execute code migrations (framework upgrades, language ports) | `template/.cursor/commands/james-code-migrate-v1.00.md` |
| `/ro:james-code-refactor` | Analyze code smells/SOLID violations; refactor for maintainability | `template/.cursor/commands/james-code-refactor-v1.00.md` |
| `/ro:james-code-scaffold-api` | Scaffold production-ready APIs with models, auth, tests, Docker, CI/CD | `template/.cursor/commands/james-code-scaffold-api-v1.00.md` |
| `/ro:james-debugging-analyze-bug` | Systematic bug analysis: 5 Whys, classification, root cause, fix plan | `template/.cursor/commands/james-debugging-analyze-bug-v1.00.md` |
| `/ro:james-debugging-debug-issue` | Set up debugging: logging, tracing, profiling, error tracking | `template/.cursor/commands/james-debugging-debug-issue-v1.00.md` |
| `/ro:james-debugging-trace-error` | Analyze production error traces, identify patterns, recommend fixes | `template/.cursor/commands/james-debugging-trace-error-v1.00.md` |
| `/ro:james-devops-check-deployment` | Pre/post-deployment checklist: code quality, infra, security, rollback | `template/.cursor/commands/james-devops-check-deployment-v1.00.md` |
| `/ro:james-devops-optimize-docker` | Optimize Dockerfiles for size, build speed, security, runtime | `template/.cursor/commands/james-devops-optimize-docker-v1.00.md` |
| `/ro:james-devops-setup-monitoring` | Set up monitoring: metrics, logging, tracing, health checks, alerting | `template/.cursor/commands/james-devops-setup-monitoring-v1.00.md` |
| `/ro:james-docs-create-issue` | Create well-structured GitHub issues with reproduction steps | `template/.cursor/commands/james-docs-create-issue-v1.00.md` |
| `/ro:james-docs-enhance-pr` | Create/improve PRs with descriptions, evidence, testing checklists | `template/.cursor/commands/james-docs-enhance-pr-v1.00.md` |
| `/ro:james-docs-generate-docs` | Generate API docs, user guides, developer docs, config reference | `template/.cursor/commands/james-docs-generate-docs-v1.00.md` |
| `/ro:james-security-audit-accessibility` | WCAG 2.1 accessibility audit covering POUR principles and remediation | `template/.cursor/commands/james-security-audit-accessibility-v1.00.md` |
| `/ro:james-security-audit-dependencies` | Audit dependencies for CVEs, outdated packages, license compliance | `template/.cursor/commands/james-security-audit-dependencies-v1.00.md` |
| `/ro:james-security-scan-security` | Full security scan against OWASP Top 10, auth, input validation | `template/.cursor/commands/james-security-scan-security-v1.00.md` |
| `/ro:james-testing-generate-tests` | Generate full testing strategy and harness (unit/integration/e2e) | `template/.cursor/commands/james-testing-generate-tests-v1.00.md` |
| `/ro:james-testing-test-args` | Echo `$ARGUMENTS` — dev utility to verify argument passing | `template/.cursor/commands/james-testing-test-args-v1.00.md` |
| `/ro:james-testing-write-tests` | Write comprehensive tests via subagent (AAA pattern, multi-category) | `template/.cursor/commands/james-testing-write-tests-v1.00.md` |
| `/ro:new-project` | Create a new project from the lean Ro AI Base template (Flow A launcher) | `.cursor/commands/new-project.md` |
| `/ro:ro-agent-onboard` | Orient a fresh agent session in this workspace before it starts work | `template/.cursor/commands/ro-agent-onboard-v1.00.md` |
| `/ro:ro-workflow-agent-handover` | Sync docs, capture session state, produce paste-ready handover prompt for next session | `template/.cursor/commands/ro-workflow-agent-handover-v1.00.md` |
| `/ro:ro-workflow-docs-update` | Refresh all internal docs to match current code state; sync agent files | `template/.cursor/commands/ro-workflow-docs-update-v1.00.md` |
| `/ro:ro-workflow-git-sync` | Auto git sync: pull when clean, commit/push when dirty (no force-push) | `template/.cursor/commands/ro-workflow-git-sync-v1.00.md` |
| `/ro:ro-workflow-new-project-setup` | Orient agent in a new workspace: read docs, report understanding, wait | `template/.cursor/commands/ro-workflow-new-project-setup-v1.00.md` |
| `/ro:ro-workflow-session-close` | End-of-session wrap: sync docs, rewrite STATE.md, stamp SESSION_LOG.md (archive-safety) | `template/.cursor/commands/ro-workflow-session-close-v1.00.md` |
| `/ro:sync-claude-plugin` | Publish the Cursor slash-command pack as Claude account skills (Desktop Chat / Cowork / claude.ai) via the ro-claude-plugins marketplace | `.cursor/commands/sync-claude-plugin.md` |
| `/ro:sync-skills` | Sync skills from catalog/SKILLS.md into the global Cursor and Claude Code pools | `.cursor/commands/sync-skills.md` |