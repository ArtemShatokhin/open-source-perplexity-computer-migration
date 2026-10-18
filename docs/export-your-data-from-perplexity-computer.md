# Export your data from Perplexity Computer before you cancel

Kortix is open source, and leaving Perplexity Computer for it has an order: the data comes out first, the subscription ends second. Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. Perplexity Computer, Perplexity's hosted digital worker, runs only inside Perplexity's cloud. Months of use leave threads behind: research sessions in its Library, task output in Computer tasks. As of 18 October 2026, Perplexity offers a per-thread export menu and an official account data request. It offers no bulk export of conversation history. The exit runs thread by thread, while the account stays open.

## What you can export today

Perplexity keeps your work as threads in its Library, the signed-in store of past sessions. Any single thread downloads as a formatted document. The [Texas A&M University IT knowledge base](https://service.tamu.edu/TDClient/36/Portal/KB/Article/2019/Perplexity-Exporting-Work-from-Perplexity) documents the route (checked 18 October 2026):

1. Open the thread you want to keep.
2. In the top right of the thread, click the three-dot menu left of the Share button.
3. Choose Export as PDF, Export as Markdown, or Export as DOCX to download the thread.
4. For plain text, use the copy button at the end of each chat interaction, or select and copy the text.

The third route is a shareable link from a thread's share icon. It opens the thread only while the thread exists in Perplexity: [LLMnesia's export guide](https://www.llmnesia.com/blog/how-to-export-perplexity-conversation-history) notes that closing the account takes the link with it.

For long threads, export as Markdown; a PDF can cut off a very long conversation ([Univik's export guide](https://univik.com/help/export-perplexity-chats.html), updated March 2026). Copy the citation URLs too: the pages behind them can change or disappear, so the URLs are the fragile part ([LLMnesia](https://www.llmnesia.com/blog/how-to-export-perplexity-conversation-history)).

## What you cannot export yet

Perplexity ships no bulk export of its own as of 18 October 2026. There is no one-click archive of the Library or conversation history, and no zip in settings ([LLMnesia](https://www.llmnesia.com/blog/how-to-export-perplexity-conversation-history)). Export guides updated in March 2026 describe the same gap ([Univik](https://univik.com/help/export-perplexity-chats.html)).

The official route for everything at once is the account data request. The [Texas A&M guide](https://service.tamu.edu/TDClient/36/Portal/KB/Article/2019/Perplexity-Exporting-Work-from-Perplexity) says to sign in, open Help from your name in the lower left, and ask support for an export of your content. A download link for the account data zip arrives by email. Guides that track the request form report a wait of up to 30 days, which they attribute to GDPR and CCPA timelines ([Univik](https://univik.com/help/export-perplexity-chats.html)). The result is JSON that needs parsing. Order matters: request the export, verify the archive, and close the account only after that ([Texas A&M](https://service.tamu.edu/TDClient/36/Portal/KB/Article/2019/Perplexity-Exporting-Work-from-Perplexity)).

The gap shows in Perplexity's own community. A [feature request for a bulk export of all threaded conversations](https://community.perplexity.ai/t/feature-request-bulk-export-of-all-threaded-conversations/371) sits on the company's forum; a moderator reply steers it to Discord, and no feature has shipped (read 18 October 2026). Until one ships, the per-thread menu and the data request are the whole official surface.

## The Computer wrinkle

Computer's work product lives in threads too. A third-party Chrome extension, [Perplexity to Notion (Batch Export)](https://chromewebstore.google.com/detail/perplexity-to-notion-batc/gfmjaemghnjokjhafjiiijhllkkfcjpk), advertises saving "Perplexity chats, Spaces and Computer Tasks" with sources (its Chrome Web Store listing, read 18 October 2026). That is evidence the task output sits in the same thread store the export menu reads. No official export for the Computer setup itself, its configuration, model routing or connector grants, appears on Perplexity's own pages. That part is rebuilt on the other side.

Decide which task threads matter before the account closes. Start with the official menu; an extension is for when the thread count is too large for one-by-one work. An extension is third-party code running against your logged-in account; check what it does with your data before installing one ([Univik](https://univik.com/help/export-perplexity-chats.html)).

## Why an owned system has no export problem

A hosted system holds your work behind its own API, so leaving means negotiating with its limits. On Kortix the same material starts on your side of the wall. The starter `kortix.yaml` registers the project configuration as files in the repo. The starter agent file describes a session as an ephemeral branch of the repo where only committed work survives. Company memory lives as files under `memory/` in the same repo (starter templates, 18 October 2026). Nothing needs exporting: the history is a folder you can clone, grep and back up with the tools you already use. The source is public at [Kortix on GitHub](https://github.com/kortix-ai/suna): read it, fork it, audit it.

The [migration runbook in this repository](migrate-from-perplexity-computer-to-kortix.md) picks up from exactly here. Its before-you-start checklist asks for notes on the outcomes of each Computer job; exported threads are the better version of those notes.

## Export first, cancel second

Work through the threads that carry real work, save the citation URLs with them, and run the data request for the full archive. Verify what arrived before you close anything. When the files are on your side, the [migration guide](https://opensourceperplexitycomputer.com/migrate-from-perplexity-computer) takes the move from there, one job at a time, on [Kortix](https://kortix.com).
