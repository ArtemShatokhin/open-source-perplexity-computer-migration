# The Perplexity Computer to Kortix migration runbook, on the open-source system you own

Kortix is open source, and this runbook is the ordered move from a closed cloud agent you rent to an AI Operating System you own, one team and one repo at a time. There is no export button in Perplexity Computer, because its configuration, routing and connector set live inside Perplexity's product, so the migration is a rebuild in plain files. Work through the steps in order; each one produces a file or a setting you keep.

## Before you start

Two accounts and one host are the whole prerequisite list. On Kortix you can start on Kortix Cloud with nothing installed, or self-host the same system on a Linux box you control. Self-host is free. Keep the Perplexity subscription running until the last step, so you can compare outputs while you rebuild.

Collect three things from your Perplexity Computer use before you stop: the list of connectors you actually used, the recurring tasks and monitors you set up, and notes on the outcomes you got from each. Perplexity Computer keeps its memory and skills inside the product, so these notes are what you rebuild from rather than a file you copy out. It helps to know the failure modes you are leaving: the [review of Perplexity Computer](https://opensourceperplexitycomputer.com/perplexity-computer-review) collects them from the hands-on reviews.

## Step 1: Create the Kortix project repo

A Kortix project is a git repo with kortix.yaml at its root, and you own the repo. Create a project from the web app, or clone one through the authenticated git proxy with `kortix projects clone`. The repo is where every later step lands, so give it a real name and a short description that a teammate would understand.

What you get: one place that holds the agents, the skills, the company memory, the connector configuration and the triggers, all as text you can read, diff and roll back.

## Step 2: Recreate grounded answers as memory files

Perplexity Computer remembers context across sessions inside its product ([Builder.io's hands-on review](https://www.builder.io/blog/perplexity-computer)). Kortix keeps company memory as files in the repo under memory/. This is the step where a repeated answer becomes a durable fact instead of a re-ask.

For each note you collected, decide whether it is a stable fact (a client name, a preference, a definition), a procedure (how a task should be run), or a one-off. Stable facts and procedures become memory files; one-offs stay out. Prune anything that was true last quarter and is not true now, because a memory file is read as current.

## Step 3: Recreate skills and playbooks

Perplexity Computer loads 50+ domain skill playbooks on demand, and the review counts the generalist flexibility as the product's real value. A Kortix skill is a folder with SKILL.md inside it, under skills/<name>/SKILL.md. For each playbook you relied on, write a skill file that states the logic it applies and when to use it, then allow that skill to the agents that should have it.

## Step 4: Write each agent as a file

On Perplexity Computer, subagents and the routing between them are managed by Perplexity, and you do not write config files. On Kortix, an agent is agents/<name>.md, which holds the behavior, plus an agents.<name> block in kortix.yaml, which holds the governance. Start with the small set of roles you actually ran, and name them by job rather than by model.

One decision moves here. Perplexity Computer routes each subtask across about 19 hosted models it selects, and the review notes that the routing stays invisible to you. On Kortix you name the model per agent, per session or per message, using any model provider with your own keys. Set the model where the agent is defined, so the choice is versioned with everything else.

## Step 5: Reconnect your tools as connectors

Perplexity Computer reaches services such as Slack, Gmail, GitHub and Notion through more than 400 managed OAuth connectors, and the review found the working ones uneven in practice. On Kortix, each service is a connector account, and credentials are project secrets. Reconnect the services on your list, and set the reach for each one.

For each connector, set the action policy to Allow, Ask or Block. Approval holds the call, and the agent's turn pauses and resumes after the decision. This is the control Perplexity Computer does not expose: on a managed connector you take what the vendor ships.

## Step 6: Map the credit meter to agent runs and gates

Perplexity Computer meters credits per task on top of the subscription, which is where a bad run gets expensive: in the Builder.io test a silent npm install failure burned 10,000 credits before a person read the logs. Kortix changes the shape of that cost. Self-host is free, and on Kortix Cloud free is $0 with 200 credits per month and 1 project; paid plans start at $50 a month for 5,000 credits, and members are free, sharing one credit pool (from the [Kortix pricing page](https://kortix.com/pricing), quoted as written).

The bigger change is the gate. Approval gates you set. Off until you set them. Put an Ask on the step that spends real money or sends something outside the team, so a repeated failure stops at the gate instead of running the meter. You can also hold reach at the connector, down to the arguments of a single call. Model spend follows your own provider keys, so it is a bill you can read rather than a credit total you have to infer.

## Step 7: Recreate scheduled work as triggers

Perplexity Computer runs background tasks and continuous monitoring on a schedule inside the product ([Perplexity's product page](https://www.perplexity.ai/products/computer)). On Kortix, a trigger is a file in kortix.yaml, and there are exactly two types: cron and webhook. Recreate each recurring task and monitor as a cron trigger, choose the session mode it needs from fresh, reuse, pinned or keyed, and treat the default (fresh) as a new session each run unless a task genuinely needs to reuse or pin a session.

## Step 8: Change how the work lands

This is the one behavioral change a team has to agree on before the first real task. On Perplexity Computer, work lands where it is done, and the Builder.io review describes an agent editing a repository directly through its API rather than cloning, branching and opening a review. On Kortix, a session clones the repo, works on its own branch, and opens a change request against the project's default branch. Session work reaches main through a change request. Merge is default-deny for agents. A person reads the diff and merges it.

Tell the team what changes in their day: they review a diff instead of trusting an outcome, and a bad run shows up as an unmerged change request rather than as a silent edit.

## Step 9: Run the first session and the first review

Pick one low-risk job you already ran on Perplexity Computer, and run it as the first Kortix session. Watch for three things: the agent reads the memory files you wrote, it reaches only the connectors you allowed, and the finished work arrives as a change request. Read the diff, leave a comment, and merge it. From then on, every finished task lands the same way.

## What you have when you are done

When the last step lands, the configuration, the memory, the connector set, the model choice and the triggers are all in one git repo you own, and the work the agents finish lands through a review you set. If you want the whole system on hardware you control, the [self-hosting guide](https://opensourceperplexitycomputer.com/self-hosting) walks a bare host to a running instance, and the [FAQ](https://opensourceperplexitycomputer.com/faq) answers the short questions. Read the docs at [Kortix](https://kortix.com).
