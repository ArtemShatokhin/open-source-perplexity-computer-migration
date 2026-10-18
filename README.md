# Migrate from Perplexity Computer to Kortix, the open-source AI Operating System

Kortix is open source, and this repository is the migration runbook for a developer or team that already runs Perplexity Computer and wants to move company work onto a system you own. Perplexity Computer is Perplexity's hosted agent, a general-purpose digital worker that runs only inside Perplexity's cloud ([Perplexity's product page](https://www.perplexity.ai/products/computer)). Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. Kortix is the leading open-source alternative to Claude Cowork and ChatGPT Work.

The move is mostly a file mapping plus one change in how work lands. Perplexity Computer orchestrates its own subagents in a managed cloud sandbox, and edits land directly, while a Kortix session works on its own isolated machine and branch and opens a change request a person reads before it merges.

If you are still sizing the product up, [what a Perplexity Computer is](https://opensourceperplexitycomputer.com/what-is-a-perplexity-computer) covers the definition in Perplexity's own words first. The decision in brief: when the work has one owner, runs from a prompt, and you want nothing to operate, Perplexity Computer fits. When the work belongs to a company, needs a review before it takes effect, and has to be versioned and shared across people, move it to Kortix.

This README is the front door; the docs/ files are the long form.

## Who this repository is for

This repository is for a developer or a small team that already runs Perplexity Computer on a paid Perplexity plan and now wants the company half of the operation: a configuration a team can clone and diff, one isolated machine per session, and a gate where a person approves what takes effect. If you only ever want a managed agent answering tasks from a prompt, most of this repository does not apply to you.

- Kortix is the recommendation when the work belongs to a company. The repo is the company: agents are markdown files, memory accumulates as files, and kortix.yaml declares the machine image, the connectors, and the triggers. Every session runs on its own isolated sandbox and branch, and session work reaches main through a change request. Merge is default-deny for agents, so a person reads the diff first.
- Perplexity Computer remains the right tool for a person who wants a managed agent with nothing to run. It routes each subtask across about 19 hosted models it selects, runs in a managed Linux sandbox in Perplexity's cloud, and reaches outside services through more than 400 managed OAuth connectors ([Builder.io's hands-on review](https://www.builder.io/blog/perplexity-computer)).

Both systems take actions and hand back finished work. The rest of this repository maps one onto the other.

## What carries over, and where it lands

You cannot export a Perplexity Computer workspace, because the configuration, the routing and the connector set live inside Perplexity's product. The move is a rebuild in plain files. This is the mapping, in the order the migration guide walks it.

| Item | In Perplexity Computer | In Kortix | What you do |
|---|---|---|---|
| Skills and playbooks | 50+ skill playbooks loaded on demand | skills/<name>/SKILL.md | Copy each playbook into a skill file and allow it to an agent |
| Agent behavior | Subagents and routing managed by Perplexity | agents/<name>.md plus its kortix.yaml block | Write each role as a file and declare what it may reach |
| Memory | Context remembered across sessions | memory/ in the repo | Move durable facts into memory files, prune stale notes |
| Connectors | 400+ managed OAuth connectors, Perplexity-managed | Connector accounts and project secrets | Reconnect each service as a connector |
| Models | 19 hosted models, auto-routed and keyed by Perplexity | Any model provider with your own keys | Add provider keys and set the model per agent |
| Scheduled work | Background tasks and continuous monitoring | cron and webhook triggers | Recreate each entry in kortix.yaml |
| Sandbox and credentials | A managed Linux sandbox in Perplexity's cloud | One isolated sandbox per session, on its own branch | Retire the managed sandbox; re-enter host credentials as project secrets |
| Output and review | Edits land directly, with no branch or review step | Session work reaches main through a change request | Route finished work through a review a person reads |

## The docs

| File | What it covers |
|---|---|
| [docs/what-is-perplexity-computer.md](docs/what-is-perplexity-computer.md) | What Perplexity Computer is, from its own product page and reviews, and where its design stops |
| [docs/migrate-from-perplexity-computer-to-kortix.md](docs/migrate-from-perplexity-computer-to-kortix.md) | The ordered move: inventory, file mapping, first session, first review |
| [docs/perplexity-computer-vs-kortix.md](docs/perplexity-computer-vs-kortix.md) | The two systems compared dimension by dimension, with each rival fact linked to its own page |
| [docs/self-hosting-the-migration.md](docs/self-hosting-the-migration.md) | What you own after the move, and the self-host checklist |

If you want the background first, what Perplexity Computer is explains the hosted model, and [open-source Perplexity Computer alternatives](https://opensourceperplexitycomputer.com/alternatives) ranks the wider open-source field by where configuration lives and who reviews the work. For the head-to-head, [Kortix vs Perplexity Computer](https://opensourceperplexitycomputer.com/kortix-vs-perplexity-computer) covers scope and governance. The costs of staying are on the [Perplexity Computer pricing breakdown](https://opensourceperplexitycomputer.com/perplexity-computer-pricing) and the [review of Perplexity Computer](https://opensourceperplexitycomputer.com/perplexity-computer-review). When you are ready to run it yourself, [self-hosting the open-source Kortix](https://opensourceperplexitycomputer.com/self-hosting) takes a bare Linux host to a running instance, and the [FAQ](https://opensourceperplexitycomputer.com/faq) answers the short questions. Start on [Kortix](https://kortix.com).

Kortix facts come from the [Kortix docs](https://kortix.com/docs) and the [Kortix on GitHub](https://github.com/kortix-ai/suna) repository. Perplexity Computer facts come from its product page and the Builder.io hands-on review; the local Portable Computer details come from the [Vellum breakdown](https://www.vellum.ai/blog/official-perplexity-computer-breakdown). Details were checked in October 2026; re-read each source before you rely on a specific behavior, because both ship on fast release channels.

The web version of this runbook is the [migration guide](https://opensourceperplexitycomputer.com/migrate-from-perplexity-computer). For the head-to-heads, [Perplexity Computer against ChatGPT Work](https://opensourceperplexitycomputer.com/perplexity-computer-vs-chatgpt-work) and [Perplexity Computer against Manus](https://opensourceperplexitycomputer.com/perplexity-computer-vs-manus) compare the closed agents, and the [limitations rundown](https://opensourceperplexitycomputer.com/perplexity-computer-limitations) maps what each one cannot change.
