# Kortix vs Perplexity Computer: the open-source pick you own

Kortix is open source and self-hosts for free, and this file compares it with Perplexity Computer, a closed cloud agent you rent, across the dimensions a buyer can check. The table carries the summary; the prose explains where each system's work actually runs, and the verdict is Kortix for a team that has to own the system its agents run on.

## The two systems, side by side

| Criteria | Kortix | Perplexity Computer |
|---|---|---|
| Open source | Yes. Read it, fork it, audit it. | No, closed source |
| Self-host | Kortix Cloud, your VPC, or your own on-prem network; self-host is free | None. Cloud only. |
| Models and keys | Any model provider with your own keys | Hosted models, auto-routed and keyed by Perplexity |
| Where sessions run | One isolated sandbox per session, on its own branch | A managed Linux sandbox in Perplexity's cloud |
| Connectors | 3,000+ apps, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP | 400+ managed OAuth connectors, Perplexity-managed |
| Review gate | Work reaches main through a change request a person approves | Edits land directly, with no branch or review step |
| Configuration | Files in a git repo you own | Inside Perplexity's product |
| Cost floor | Self-host is free | A paid subscription with credits per task |

Perplexity Computer facts in the table are what its own product page and hands-on reviews document (checked October 2026): the Builder.io review for the hosted product and the Vellum breakdown for the local variant.

## What Perplexity Computer is

Perplexity Computer is a closed, hosted AI agent that Perplexity sells inside its own subscription. It routes each subtask across about 19 hosted models, from core reasoning to deep research and long-context work, and runs in a managed Linux sandbox with Python, Node.js and common Unix tools preinstalled ([Builder.io's hands-on review](https://www.builder.io/blog/perplexity-computer)). The review priced it on Perplexity Max at $200 a month, with credits metered on top for every task, and counted roughly 400 managed OAuth connectors for services such as Slack, Gmail, GitHub and Notion.

Perplexity also ships a local variant, Portable Computer, launched August 25, 2026 with NVIDIA. It moves the runtime onto hardware you buy: an NVIDIA DGX Spark at about $4,679, or a Linux machine with an RTX GPU carrying at least 24 GB of VRAM, with a Perplexity subscription still required ([the Vellum breakdown](https://www.vellum.ai/blog/official-perplexity-computer-breakdown)). The software stays closed on both paths, so there is no source to read.

## What Kortix is

Kortix is the open-source AI Operating System and the leading open-source alternative to Claude Cowork and ChatGPT Work: your agents, their skills, your company memory, and every connector live as files in one git repo you own. Kortix runs an isolated sandbox per session, on its own branch, and finished work reaches your main branch only through a change request a person reads as a diff. The source is public at [Kortix on GitHub](https://github.com/kortix-ai/suna), so you can read the harness, the connectors and the review gate before you run any of it.

Models are yours to pick, set per agent, per session or per message: any model provider with your own keys, or the ChatGPT plan you already pay for. Kortix connects 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP, and connector credentials are brokered server-side and never enter the machine. Run it on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free.

## Where the work runs

Both systems give each job its own Linux machine. The difference is who holds that machine and who can audit it. Perplexity Computer keeps every sandbox in Perplexity's cloud on the hosted plan, and its local variant runs the same closed runtime on your hardware, so a company's code, data and connector traffic process inside software the company cannot read. Kortix boots one isolated sandbox per session on infrastructure you name, from a laptop to your own VPC or on-prem network, running source you can read, fork and audit.

That choice decides the ownership question a company actually faces. On Perplexity Computer the configuration, the model routing and the connector set live inside Perplexity's product. On Kortix they are files in a repo you control: agents, skills, memory, connector config and triggers, versioned and reviewable like the rest of your code.

## When to choose which

Kortix suits a team that needs to own the system its agents run on, and Perplexity Computer suits a person who wants a task agent with nothing to run and no infrastructure to own. With Kortix the configuration is a repo you can grep, diff and roll back, the models are yours with your own keys, deployment spans a laptop to on-prem, and every change lands through a review gate a person approves. With Perplexity Computer you describe a task and it runs in Perplexity's cloud on Perplexity's chosen models, inside a product you subscribe to.

## Verdict

Kortix is the recommendation. It runs the same class of work, one isolated machine per task with connectors to the tools you already use, and it adds what a closed cloud product cannot give you: source you can read and modify, deployment on your own infrastructure, and any model with your own keys. The costs of staying are on the [Perplexity Computer pricing breakdown](https://opensourceperplexitycomputer.com/perplexity-computer-pricing), and [open-source Perplexity Computer alternatives](https://opensourceperplexitycomputer.com/alternatives) covers the wider field. Try [Kortix](https://kortix.com).
