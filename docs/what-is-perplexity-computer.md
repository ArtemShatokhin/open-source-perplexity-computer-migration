# What Perplexity Computer is, and the open-source Kortix you migrate to

Kortix is open source, and this file describes Perplexity Computer from its own product page and reviews, so the migration guide can map it onto the open-source AI Operating System. Read it first if you want to know exactly what you are leaving before you rebuild it as files you own.

## Perplexity Computer, defined

Perplexity Computer is a closed, hosted AI agent that Perplexity sells inside its own subscription. Perplexity calls it a general-purpose digital worker that operates the same interfaces you do, and it creates and executes entire workflows that can run for hours or even months in Perplexity's cloud ([Perplexity's product page](https://www.perplexity.ai/products/computer)). Perplexity Computer is not a chatbot: you describe an outcome, and Computer breaks it into tasks and subtasks, spins up subagents, and runs them in parallel while you do something else ([Perplexity's launch post](https://www.perplexity.ai/hub/blog/introducing-perplexity-computer)).

The product runs an isolated compute environment with a real filesystem, a real browser, and tool integrations, and Perplexity pitches that managed environment as the consistency advantage, because every session starts from the same image. The [Builder.io hands-on review](https://www.builder.io/blog/perplexity-computer) measured that environment at about 2 vCPU and 8 GB of RAM with Python, Node.js and ffmpeg preinstalled, and rated the consistency and the multi-agent orchestration as the parts that work best in daily use.

## How the routing and reach work

Perplexity Computer is model-agnostic in the same way a router is. As of the launch post it runs Claude Opus 4.6 for core reasoning and delegates subtasks to other hosted models, including Gemini for deep research, Nano Banana for images, Veo 3.1 for video, Grok for lightweight jobs, and ChatGPT 5.2 for long-context recall. The Builder.io review counts about 19 models routed across a single run, with no configuration from you. The same managed layer covers connectors: Perplexity advertises hundreds of integrations through managed OAuth, and the review counts more than 400, covering services such as Slack, Gmail, GitHub and Notion.

Two boundaries follow from that design, and both are the point of this migration guide. The models, the keys and the routing stay Perplexity's decision, so the system's behavior is not something you can inspect or change, and the sandbox stays in Perplexity's cloud, so a company's data and connector traffic process inside software the company cannot read. The review also found the connectors uneven in practice: a Vercel token that expired every session, an Ahrefs connector limited to backlink data, and a GitHub integration the reviewer bypassed with a manually pasted token.

## What it costs to stay

Perplexity Computer ships only inside a paid Perplexity plan. The Builder.io review priced the hosted product on Perplexity Max at $200 a month, with credits metered on top for every task (checked October 2026), and Perplexity does not sell the cloud agent as a standalone product. Perplexity's product page lists it as available to Pro and Max subscribers on desktop, mobile, Slack and Microsoft 365, and the launch post added that it would reach Enterprise Max users soon.

Perplexity also ships a local variant, Portable Computer, launched August 25, 2026 with NVIDIA. The [Vellum breakdown](https://www.vellum.ai/blog/official-perplexity-computer-breakdown) records that it runs the whole runtime on an NVIDIA DGX Spark at about $4,679, or a Linux machine with an RTX GPU carrying at least 24 GB of VRAM, with a Pro or Max subscription still required on top of the hardware. Local steps carry no token cost, and the escalation to Perplexity's cloud is gated per step. The runtime stays closed on both paths, so there is no source to read.

## Where the design stops, and what Kortix does instead

The failures reviewers report share one cause: the parts that break are the parts you cannot inspect or change. The credit meter runs while the agent repeats failing work, connectors fail without a way to debug them, there is no window into the running sandbox, and code edits land directly. In the Builder.io test, a silent npm install failure inside the sandbox led the agent to push broken builds and spend 10,000 credits before a developer read the logs and fixed the dependency by hand.

Kortix, the open-source AI Operating System, puts those same parts in a repo you own. Agents, skills, company memory, connector configuration and triggers are files in one git repo. One isolated sandbox runs per session, each on its own branch, and session work reaches main through a change request, so an agent edits a branch and a person reads the diff. Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or sign in with your OpenCode Console account for OpenCode Zen and Go. Kortix connects 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP, and connector credentials are brokered server-side and never enter the machine. You can read it, fork it and audit it, starting from [Kortix on GitHub](https://github.com/kortix-ai/suna). Run it on [Kortix](https://kortix.com), in your VPC, or on your own on-prem network, and self-host is free.

## The wider open-source field

Kortix is the pick when the whole company needs the system on its own side, and the other open-source projects in this space cover narrower lanes. Each line here comes from the project's own page or repository, and [open-source Perplexity Computer alternatives](https://opensourceperplexitycomputer.com/alternatives) ranks the field on the two facts a buyer can check.

- [OpenClaw](https://github.com/openclaw/openclaw) is an open-source AI assistant that runs on your own computer and meets you in the channels you already use, including Discord, Slack, Teams and WhatsApp, with one Gateway serving a personal assistant or a shared deployment.
- [Eigent](https://github.com/eigent-ai/eigent) is the open-source Cowork desktop application, a local, model-agnostic workforce for desktop workflows with MCP and skill integration.
- [Open WebUI](https://github.com/open-webui/open-webui) is a self-hosted AI platform over Ollama and OpenAI-compatible APIs, with role-based access control and companion apps for terminal and coding work.
- [AnythingLLM](https://github.com/Mintplex-Labs/anything-llm) is an on-device assistant that runs with no accounts and no API keys, builds a local document knowledge base, and self-hosts as a multi-user deployment.
- [Vellum](https://www.vellum.ai/) is a personal assistant that runs on your Mac or in Vellum's cloud, switches between OpenAI, Anthropic, Gemini and Ollama models, and asks for permission on high-stakes actions.
- [Vane](https://github.com/ItzCrazyKns/Vane) is a privacy-focused answering engine that runs on your own hardware, with SearxNG search behind it and cited sources.

Perplexity Computer stays closed and runs only in Perplexity's cloud, and every project above is instead compared on whether you can read and run the source and who owns the configuration. The migration runbook walks the ordered move onto Kortix.
