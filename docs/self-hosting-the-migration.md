# Self-hosting the migration: run the open-source Kortix on hardware you control

Kortix is open source, and self-hosting is the part of the migration that moves the whole system onto machines you own. Perplexity Computer runs only in Perplexity's cloud, and its local variant runs a closed runtime on your hardware, so neither path gives you a server you can inspect. A self-hosted Kortix instance is the full platform on a server you control: one Docker Compose stack that the kortix self-host CLI installs, configures and updates.

## What self-hosting changes after the move

Self-hosting moves four things to your side of the line. The repo lives on your infrastructure, so the agents, the skills, the memory files and the triggers are yours to back up and restore. The connectors use project secrets on your instance, and connector credentials are brokered server-side and never enter the machine. The model keys are yours, so the model bill is a provider invoice you can read. And the session work still lands through a change request on the same instance, so the review gate follows you.

The operational trade is real and worth naming before you commit: you own uptime, upgrades and isolation. That means patching the host, watching the stack, and backing up the data yourself.

## Requirements

A self-hosted instance needs a few things in place before the first start. The CLI runs on Linux and macOS, on x86_64 and arm64. The instance must be reachable from the internet, because agent sessions run on a separate sandbox provider that calls back to the instance, and the first start pulls images from a public registry.

- A Linux server with a public IP. The bootstrap installs Docker Engine and the Compose plugin when they are missing.
- DNS records for your domain and for api.<domain>, both pointing at the server, plus a wildcard record for previews. Caddy needs them to issue the certificate.
- Ports 80 and 443 open inbound.
- A sandbox provider key: Daytona, Platinum or E2B. Without one, sessions do not start.
- A model provider key, added in the web app after the first sign-in.

## Install in three commands

The manual path takes a server that already has Docker and the Compose plugin from a bare box to a running system. Install the CLI, initialize the instance, then start the stack.

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com --admin-email you@example.com
kortix self-host start
```

To try it on your own machine with no domain, use the evaluation mode, which publishes the API through a Cloudflare tunnel instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use that mode for evaluation rather than production. On a domain install, run `kortix self-host configure` to answer the setup questions again, then `kortix self-host start` to apply them, and run `kortix self-host doctor` to check the instance and fix every failing check. Do the first sign-in and connect GitHub as soon as the stack starts, because until you restrict account creation, anyone who reaches the instance can create an account for any address.

## Where the parts run

The stack holds the frontend, the API, the LLM gateway and a bundled Postgres distribution behind a proxy. Agent sessions run off the box on your sandbox provider, not on the server, and the server's network is reachable so those sandboxes can call back. That split is why a self-hosted instance does not need a GPU: the agents reach models through an API, and the heavy model work happens at the provider you configured.

## Choose the host by what you can maintain

| Host | Good for | You provide | You manage |
|---|---|---|---|
| A laptop | A first trial on your own files | Docker and the install | Backups |
| A VPS | A shared instance for a team | A small Linux server | Uptime, upgrades, backups |
| Your VPC | Work inside your cloud account | Your cloud account | Network rules and keys |
| On-prem | Regulated environments | Your own hardware | Patching, capacity, recovery |
| Kortix Cloud | Starting with nothing to run | Nothing | Nothing |

## What you own when it is running

When the instance is up, the whole system is one repo on your hardware and one command surface. The agents, the skills, the memory, the connector configuration and the triggers are text you can read, diff and roll back, and the finished work arrives as a change request a person reads. Run it on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free.

If you want the wider background before you run it, what Perplexity Computer is explains the hosted model, the [self-hosting guide](https://opensourceperplexitycomputer.com/self-hosting) on the campaign site walks the four decisions, and the [FAQ](https://opensourceperplexitycomputer.com/faq) answers the short questions. Read the docs at [Kortix](https://kortix.com).
