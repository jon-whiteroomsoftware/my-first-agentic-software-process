# My First Agentic Software Process

*You can build software now. You still need a process.*

I've spent the last few months helping a handful of smart friends get up and running with agentic tools — some of them lifelong engineers, some of them people who have never written a line of code. This document is the distillation of all those emails, plus some things I've posted publicly, arranged in the order I wish someone had given them to me.

My thesis, up front: a lot of people can suddenly create software, and most of them don't know that what they're missing isn't better prompts or coding guardrails — it's a **software process**. Without one, you build impressive things fast and watch them quietly rot into a buggy mess. With one, the ceiling keeps rising. Front-loaded, iterative planning pays off more than any other single thing I can teach you.

This document is in two tracks. **Track 1** assumes you've never written software and know nothing about LLMs — it's a quick catch-up primer, not a course. **Track 2** picks up from people who know what git is, know what JavaScript is, maybe have written a little code, but have never worked on a real software project and don't really know what a software process is. If you're technical, skim Track 1 anyway; a couple of the mental models there are load-bearing later.

*Written July 2026. The model names in here will rot within months. The principles shouldn't.*

---

## Track 1: Starting from zero

### 1. Chatbots and agents

Here's the fundamental difference: you generally get value from a **chatbot** by it answering your questions, but you get value from an **agent** by it doing tasks for you (although it will answer questions too).

A chatbot talks. An agent has hands — it can read and write files, run programs, browse the web, drive applications on your computer. When you use ChatGPT or Claude in a browser window, you're mostly using a chatbot. When you point one of the agentic tools (Claude Code, Codex) at a folder on your machine and say "build me this," you're using an agent. The same brain is behind both. The difference is what it's allowed to touch.

### 2. Context: the model's working memory

The single most useful technical concept to understand is the **context window**. It's the model's working memory: everything it can "see" right now — your conversation, the files it has read, the output of the commands it has run. It's measured in **tokens** (word-fragments; a token is roughly three-quarters of a word).

Four things follow from this, and they explain most of the odd behavior you'll ever see:

1. **The context window fills up.** Every message, every file read, every result accumulates. When it gets full, the harness performs **compaction** — summarizing the history to make room — and the agent has to get back up to speed from the summary. The good news is that compaction now works quickly and reliably on both major platforms, so you can mostly forget about how full your context window is when you're just getting started.

2. **That said, prefer the emptier window when the choice is cheap.** A fresh agent costs less, responds faster, and thinks better. What you want is a high-quality context window, not a high-quantity one — so where it doesn't matter, start fresh.

3. **Models think better with less in the window.** A cluttered context isn't just expensive, it makes the model dumber — it starts hallucinating connections to irrelevant stuff it read three turns ago. Denser, more relevant context gets the best outcomes and uses fewer resources.

4. **You'd be surprised how little the model remembers about you between conversations.** The context window is the conversation. When it ends, that working memory is gone. There are memory features bolted on, and they help, but go look at what they actually retain — it's terse, and the quality is variable. This is why Track 1 spends two whole sections on files.

There's a more advanced version of this topic — token economics, why some models cost triple what others do for the same work, tools that keep your context clean — in Track 2. For now: working memory, it fills up, less is more.

### 3. Just Ask

Mantra for the agentic era: **Just Ask.** Fire up Claude or ChatGPT and say "hey, I want to research this. Can you help me figure out a good plan?" You can also go meta: "I want you to do a lot of research for me, but it needs to be high quality and not spend too much money. I don't really know what my options are — help me understand."

These agentic models can do so much with so little information. Folks should not be scared to try, even if they feel like they don't know how to describe things well or how exactly to use the tools best. Even if you barely know what you want, and don't know anything about where to find it or how to organize it, the agent will take whatever meager scraps of information you give it and likely make extremely good decisions about all the rest.

This extends to the tools themselves. Before posting basic "which model should I use?" or "what does this setting do?" questions on a forum — ask your agent. These models are surprisingly good at explaining themselves, comparing options, and recommending settings for your use case. You'll usually get a great answer in seconds.

The habit that took me longest to build: **stop doing it yourself.** Agents will happily tell you how to fix things — and within coding they'll just start doing it — but if the fix involves a browser or an application, they seldom volunteer. So whenever my agent tells me to do anything, I've made it a mental habit to just say "no, *you* can do that." Ninety percent of the time they can, faster and better than you.

The canonical version of this is fixing your computer, and I mention it because it's the one that surprises people most. Agents can *use* your computer — click, type, take screenshots, change settings. That's counterintuitive if your mental model is chatbot. "Make this problem go away" is a great upgrade over doing the clicking yourself. You check back at the end to see the outcome; you don't do the clicking.

### 4. Agents come and go, files are forever

This is the core mental shift for working with agents, so I'm going to belabor it.

The first step everyone goes through is treating these things as consultants and focusing on one chat at a time. You quickly run into the key issue: how do I go from chat to chat and preserve all the important state, so the next chat just picks up from there? The second step is having things oriented around a durable set of artifacts — literally files. **Agents come and go (the technical word is "transient"); the files are what stays.**

The first tools that really connected the models to the idea of ongoing storage were the coding IDEs. They orient everything around a project folder, so every agent works within that set of files unless it asks for exceptions (safety!). But this pattern isn't for coders — anyone who wants to do agentic work needs agents plus durable state, even normies. The folder is the workspace; the chats are just steering.

All the durable state for your project is really just context, in the sense from section 2. You make agents work better by setting up little systems — summary documents for feature areas, a status file per project — that let them dip into your storage and pluck out what they need using as few tokens as possible.

Two practical habits to start immediately:

- **Teach the agent who you are, early and in writing.** The agentic tools all support a standing-instructions file — called `AGENTS.md` or `CLAUDE.md` — that the agent reads at the start of every single session. There's a global one for facts about you (your business, your preferences, how you like your prose) and a per-project one for how that project works. Every fact you write down once is a fact you never re-explain, and every time you catch the agent repeatedly doing something wrong, the correction goes in the file. Agents compound like employees do — but only if you onboard them.
- **If you want to keep it, externalize it.** Don't rely on the model's built-in memory. If a conversation produced something valuable, have the agent write it to a file before you close the tab.

In five years I reckon an enormous amount of work will be done by people using their voice to talk to agents that are organized around a set of common shared state. The frontier labs clearly see this coming — they've spent the last few months converging their chat products and their coding products into the same app.

### 5. Git without tears

Every software project on earth keeps its files in **git**, and I need you to not skip this section just because you've heard git is miserable. It is miserable — even someone like me finds it tedious and byzantine. But in the new world, you set up a GitHub account once and the agent does all the git work: setting up repositories, saving changes, all of it. You don't need to learn the commands. You need about four concepts, and learning them is maybe an afternoon:

- a **commit** is a checkpoint of your whole project, with a note saying why
- a **branch** is a cheap parallel draft
- a **diff** is exactly what changed between two points
- a **revert** undoes a checkpoint

Why bother? I had Fable make the case to a friend who's never been an engineer, and its framing was better than mine, so I'll borrow it: git isn't backup. Backup keeps the latest copy; git keeps *every state the project has ever been in, with the reasons attached*. The commit log becomes a decision journal that writes itself as a side effect of working — six months later, "why does this say 30 days instead of 14?" is answerable. Branches replace `PRD_v3_FINAL_revised_ACTUAL.docx`. And the modern clincher: **git is the safety rail for AI agents.** Every agent change lands as a reviewable diff, and any mistake is a one-command revert instead of a corrupted project. It's also how multiple agents work on the same project without trampling each other.

The agents deeply understand git, by the way. If you ask a question that's best answered by looking back through the project's history, they'll just do that without being told.

Working with agents runs on plain text files — generally **Markdown**, not Word or Google Docs. Plain text is what makes diffs readable, and it's the format agents handle best. (When visual presentation matters, have the agent produce HTML, or generate SVG diagrams to embed in your Markdown — a massive boost to the format.)

You don't have to start here. A folder with a bunch of files in it that all the agents look at is just fine, and you can take that folder and make it a git repository at any point later. But it's become such a lingua franca that a whole ecosystem of products syncs through it, so the earlier you start, the more doors are open.

### 6. Tools and money

What to actually buy and install, as of July 2026:

- **A $20/month subscription to Anthropic (Claude) or OpenAI (ChatGPT) is the entry point**, and it's enough to learn on. Anything above the $20 plan is enough to use an agent full-time for most work. The subscriptions are a genuinely absurd deal — you get access to what would cost thousands of dollars of pay-per-token inference.
- **You need the desktop app, not just the browser.** That's where the agentic tools live — Claude Code is just a part of the Claude desktop app now (don't let the "Code" name scare you; it's the best match for non-coders too). OpenAI folded Codex into the ChatGPT app the same way.
- **Which company? It matters less than you'd think.** Both are running at a relentless pace and leapfrogging each other every few months. At this point you could be quite happy on either ecosystem. And here's the important part: as long as you build a good context-storage system and some good processes, you can jump between platforms without noticing much. Intelligence is commodifying; your state and your process are what you need to care about. Ask your agent to help you pick — see section 3.
- **Two models are better than one.** I've had a subscription to both for months, because getting two points of view on the same topic — or having one model critique the other's work — turns out to be one of the most useful moves in the whole playbook. Start with one; know that the second is worth it later.
- **MCP, briefly.** You'll hear this acronym. MCP servers are plug-ins that teach your agent to drive other tools — create 3D models, build things in Canva, control your smart lights, whatever. There are a ton of them out there, and the point is that you don't need to teach the model anything; the MCP is what teaches it. I haven't done much here yet myself. Just know the term and that the door exists.

### 7. Your first week

Don't overthink the first project — the skill you're building is *working with an agent*, and that transfers to everything. A few starters that have worked for my friends: have the agent interview you and organize a messy real thing (a folder, a trip, your finances); export your old chat logs (Google Takeout works for Gemini) and have a new model distill 18 months of conversations into a profile of you; or take a real internal tool you've always wanted and get a first version running. Real beats tutorial, small beats grand.

And one warning to pass along, kindly, from a Fable conversation I forwarded to a friend in exactly this position: the first week you'll over-verify everything the agent does, and the third week you'll under-verify. The steady state is in between — trust, but read the output before it goes to a client.

---

## Track 2: The software process

### 8. Why you need a process

We're at a point where an amateur with these tools can be close to as good as an expert in a lot of domains. But the tools are a **multiplier on judgment, not a substitute for it** — and nowhere is that more visible than in what happens to a project after week two.

You'll start out working full-time interactively with one agent, cycling between product definition, UX, and implementation in a single context window — and that's not a bad thing. It lets you catch mistakes as they start, and watching the agent's train of thought is a genuinely useful way to learn. (My first vibe-coded app felt amazing right up until it devolved into a buggy mess.) The lesson is this: **the scale, complexity, and code quality of what you can build has a ceiling proportional to your software process quality.** Adding tools and customized process — task management, docs, workflows, validation and fault-detection mechanisms — is how you raise that ceiling.

And here's the good news that makes this document worth reading rather than depressing: **you can basically copy/paste a good software process now.** It won't work as well as one you fully understand and have fit to your needs, but it will let you get much, much further than no process. The rest of Track 2 is the process I'd copy.

One framing to carry through everything that follows: the foundation you're building toward is *basic software process plus validation tooling plus a technical architecture*. Once that foundation exists, the agent barely needs you for technical decisions. Where it always needs you is the subject of section 11.

### 9. Plan first, plan iteratively

**Up-front planning is the master skill of agentic coding.**

In almost every aspect of building software products, more up-front planning is better than less. The problem with waterfall — the old style of software planning where you tried to write the complete blueprint before building anything — was that it expected you could specify 100% of things up front, and that just doesn't work. What works better is establishing the boundaries and frameworks for the largest pieces of each domain, and then the agents work within those lines. If the framework is sound, you should be able to keep adding detail and making new decisions within each piece without violating or needing to revise the framework. You might tweak the framework as you establish it, but it should rapidly settle to a steady state. If agents keep being unable to work within the framework without changing it, you probably need to rethink the framework at a lower level.

I've kept that abstract because it's broadly applicable: software architecture (database schema, object model, technology choices), software quality (lint, code review), product features (PRDs, issue descriptions), UX. Same shape everywhere: lay out a consistent system for the highest-level pieces, let detail accumulate inside it.

Concretely, for a new project, you want two artifacts before anyone writes code:

1. **A PRD** — a product requirements document. This can literally be a Markdown file called `PRD.md`. What is this thing, who is it for, what are the features, what's out of scope.
2. **A technical design.** Have a technical design conversation with the agent and make it produce an artifact — a spec, even a short one. You don't need to bring deep technical knowledge to this; the agent knows all of it and can do most of it for you. But the decisions have to get *taken*: are we using a database? What kind of app is this — web page, desktop, phone? What are the non-functional requirements (how fast, how many users, what happens to the data)? You need a skeleton to hang the code on. If you care about it, put it in the spec rather than leave it to chance.

The best tool I know for producing both is having the LLM run the interview. The first skill I ever used a lot and still use today is Matt Pocock's `/grill_me` (more on skills in section 14). It interviews you relentlessly, one question at a time, walking down each branch of the decision tree — looking up whatever it can on its own, but putting every real decision to you, with a recommendation attached. The first time I did this for a real product, I ended up in an hour-long conversation with probably forty questions, and the durable outcomes were a domain-definition file (`CONTEXT.md` — the shared vocabulary between you and your agents) and a set of decision records. There's nothing inherently software-ish about this; it works on definition problems from any domain. And you're always in charge of the depth — I regularly fast-forward through topics once I've got enough, or ask what topics the agent has planned and cut the list down.

Why does deep planning work so well now? Because thinking broadly, cross-domain, while obeying all sorts of constraints and best practices, is one of the newest models' superpowers. They can do it at a scale far beyond our fragile meat computers. We talk a lot about keeping each unit of *execution* small and well-defined with a small, relevant context — but planning is where you want the opposite, and the models deliver.

Two habits that make the planning phase dramatically better:

**Creation is hard; editing is easy.** It's far easier to pick from a bunch of options than to magic stuff up out of thin air. I first noticed this with writing — have the AI generate options, pick the fragments I like — and now I apply the same pattern to code architecture and UI design. I'll say to the model, "make me three of those, then let's talk through the pros and cons, and I'll tell you what I like and don't." You usually end up either picking one with minor refinements, or you learn so much during the process that you make a fourth one which is way better.

**Every rock you turn over brings you closer to what you're going to build.** I think about this like shopping for a used car. The first couple you look at, you have no idea what's a fair price or what you should even be checking. The solution is to look at more cars. By the time you've walked around thirty of them, you know what you want, you know what a good deal looks like, which features are essential and which are not. Iterating on plans isn't wasted time; it's how you develop taste in the domain.

### 10. Slice the work into issues

Once the PRD and the design exist, have the agent break the work into **issues** — discrete, well-specified tasks. The slicing matters: each issue should be a vertical slice that can be implemented, tested, reviewed, and documented independently.

You'll want some form of task tracking. A list in a `.md` file is fine if that works for you, but it gets tedious pretty fast. GitHub Issues is a good, simple, usable choice. I end up reading most of the tasks and doing some light management in Issues, and it becomes a nice command center for understanding what work is being done, its state, what's left. Agents are pretty meticulous to start with, and if you want them excruciatingly so, that's easy to arrange. It's genuinely great to open an issue and see sixteen acceptance criteria, fourteen checked off, with a little note explaining what's left and why.

Two adjustments to start making now:

- As soon as you have more than one agent, you need shared artifacts. Some documents are dual-use (for people too), but the large majority are BAFA: *by agents, for agents*. **You will write 0% of the docs, and you will only ever open 10%.**
- The issues are the primary shared state between agents. If your PRD and an issue disagree, or what's described in a task can't be matched to the current state of the code, your agent is much more likely to go off the rails. Keeping these reconciled is a real job — and in section 12 you'll see it's a job you can delegate too.

### 11. Validation is the constant thread

Here's the theme that ties the whole process together, and the single most important idea in Track 2.

Every stage of the process — product definition, feature specs, UX, architecture, code — produces work that can be *wrong*. The question that should organize your entire setup is: **how does wrong work get caught?** You need to automate validation as much as possible, and as you get more sophisticated, you make validation more rigorous and more *independent*.

The independence ladder looks like this:

1. **Same agent, prompted to check.** "Go back and have a longer think about that." Cheap, catches some things — but an agent reviewing its own work in its own context has real failure modes. It tends to either double down or capitulate to your skepticism regardless of the truth.
2. **A fresh instance.** A new session with clean context can't be anchored by the conversation that produced the answer.
3. **A different model entirely.** This also controls for the biases of the model family itself. Don't grade your own homework — use a separate agent with fresh context to eliminate one kind of bias, and a completely different model to control for that dimension as well.

The mechanics of that last rung are almost embarrassingly easy, so let me demystify it: the models can call each other. You can literally just ask GPT to have Fable do a code review, or vice versa. That's about all there is to it. I've since automated my version into a little skill that runs a multi-round design bake-off between the two models, but the ad-hoc version is one sentence long.

Now, the principle that tells you where to spend *your own* attention — this one came out of Fable pushing back on an earlier writeup of mine, and it was right: **human involvement should scale inversely with how well the work can be machine-verified.** Code has tests, typecheckers, linters, CI — drift gets caught mechanically, so technical work can run with a lot of autonomy. But product definition and user interface design have no oracle except you. That's exactly why you involve yourself deeply in those: not because they're the most fun (they are), but because they're the hardest things to assess programmatically. I'll happily let agents make architecture decisions all day, and I will still spend forty-five minutes talking through a UX design across three rounds of iteration.

### 12. Let the agent write the tests

The workhorse of automated validation for code is testing, and the agentic version of it is a spectacular deal.

Adding a TDD (test-driven development) skill to your process causes the agent to write a ton of tests as it builds. Solid tests harden your codebase, and their value grows over time as more accumulate. The agent is very good at writing them, tests run automatically on every commit, and from then on, any time an agent writes code that would break another part of the system, a failing test usually catches it immediately. That's the part that's basically free: two minutes to add the skill, easy wins forever after.

I used to tell people "you never even read the tests." I want to soften that, because when Fable reviewed that claim it made a pushback I can't refute: when the same agent writes the code and repairs the tests, a failing test sometimes gets *weakened to pass* rather than treated as a caught bug — the agent grading its own homework again. So the more nuanced read is: **you get a lot of value even if all you ever do is turn TDD on.** And when you want better, you apply section 11: a rule that agents never modify a failing test without flagging it explicitly, an occasional spot-audit of what the tests assert, review by the other model.

One more planning-shaped testing tip: the best thing you can do for your project's bones is to shake out the big data-model decisions early — by prototyping and having long conversations with the model — so that implementation starts at the core of your domain. If those fundamental objects and processes get a lot of tests around them at the start, the rest of development goes smoothly, and when an agent breaks a test it course-corrects easily.

### 13. Good artifact hygiene is good cognition

I see a lot of conversation online about context hygiene, but almost none about **artifact hygiene**. Artifacts (files, if you're nasty) are all that remains once an agent is finished. Side-effects like Memory exist and prove useful, but you can't, and shouldn't, rely on them. If you want to keep it, externalize it.

During my time at Reddit I talked to a lot of people about this problem in its human form: it's hard to get all the information out of people's heads, communication is imperfect, data rots if not regularly maintained. It's an important issue for human projects *despite* the creation and carrying costs of documentation. With agentic coding, the value of good artifact hygiene is even higher — agents can make dumber mistakes than people when their ground truth is wrong — and the cost is *basically free*, and automating it is trivial.

One of the hardest things in software development has always been making sure everybody has a complete and accurate picture of what they're doing, why, how it works, and what needs to happen next. Maintaining those documents by hand was always tedious, so nobody did it. Now the economics have flipped. Keeping completely accurate, current reference documentation — user-facing and developer-facing — was impossible until about a year ago. Since it's now effectively free, it's a powerful tool: agents don't get confused by contradictory docs, the documents become the entry point to the project for both humans and agents, and the domain glossary keeps your vocabulary crisp so that what you intend is what the agent carries out.

My structure, if you want to copy it: `CONTEXT.md` for domain language and concepts; `docs/plans/` for forward-looking PRDs and designs; `docs/reference/` for how the product actually works as built; issues for executable work. The wall between *plans* and *as-built reference* is the important part. And if you want to see what a real project's agent instruction file looks like, the [`AGENTS.md` at the root of my Pixelblaze IDE repo](https://github.com/jon-whiteroomsoftware/PXLBLZ-IDE/blob/main/AGENTS.md) is publicly available.

The maintenance loop is delegated, of course. The first skill I ever built is called `doc-sweep`: once a feature is mostly built, an agent sweeps through everything — moves what's now built out of the PRD and into reference docs, audits closed issues to make sure everything actually got done and captured, checks that remaining open issues are still relevant given everything that's changed. Keeping accurate and up-to-date documentation is a context hygiene practice — possibly the most important one — **because every agent bases its worldview and ground truth on what's in those documents.**

### 14. Skills are FREE BRAINS

A **skill** is a little bundle of instructions — literally Markdown files — that you install so your agent knows how to do something, or knows *when* to do something. Since skills are just text, they're portable between platforms, and you can read them to see exactly what they do — which is also a great way to learn.

There are skill extremists at both ends: use way too many, or use none. I've seen advice to avoid third-party skills entirely until you know what skills you want to write yourself, and I think that's terrible advice. When you're starting out, you have no idea what skills you need or how to make one. What I'm trying to say is that this is **FREE BRAINS**: the opportunity to copy/paste real distilled knowledge and best practices into your agent. You no longer need to know how to do TDD to use TDD; you just need to know it's a benefit and who has the best skill. It's not much of an exaggeration to say you can now copy/paste most of a good software process.

Skills have a carrying cost, though — every installed skill competes for the agent's attention, and dozens of overlapping ones cause misfires. The synthesis: install liberally to learn, curate periodically, and read the skills you keep.

My standard recommendation for a basic product process is Matt Pocock's skill set — product definition: `/grill_me`, `/to_prd`, `/to_issues`; development: `/tdd`, `/improve-codebase-architecture`. You'll notice those map exactly onto sections 9 through 12. That's not a coincidence; that's the copy/paste-able process. Also grab Anthropic's frontend design plugin — it's one of the reasons the Claude models are excellent at web design, and it installs into Codex too (just ask Codex to install it).

When you eventually need a skill of your own, here's my complete process for creating one: there is no process; I just ask the agent. My favorite example — I wanted my agents to write in my voice, so I had one mine my own chat logs (there's a folder containing every agent conversation you've ever had) and synthesize a personal-voice skill from how I actually talk. It's really impressive how much it extracted. And skills compose: horizontally as steps in a workflow, or vertically stacked in one task — style skill plus voice skill plus document-format skill, all applying at once.

The part nobody tells you: if a skill encodes a reasonably generic *mental strategy*, the agent will start using it in places you never anticipated, with good judgment. I built a `/blind-spot-check` skill for auditing plans, and the agent now reaches for it in summaries and documents — basically anywhere it would add depth.

### 15. The day-to-day craft

A grab bag of things that each took me weeks to figure out and take a paragraph to transfer:

**Choose interruption over non-interruption.** There's no point in your agent working on anything but the most current, most important thing with the most current information. Interrupting is a normal, healthy part of the workflow, not an insult to the robot — you can occasionally catch it at an inopportune moment, but in general, when in doubt, interrupt. The tools support this: Codex's input box has a "steer" mode (which I recommend over the queue default) that delivers your message at the next natural opening, and escape-escape interrupts immediately. And when an agent is visibly off in the weeds, interrupting with just "what are you doing?" is usually enough to make it introspect and catch its own mistake.

**"Walk me through this."** When an agent has worked for hours, so much has changed that it's hard to pick apart what's new. So I just say "walk me through this" and get a guided tour, one step at a time, with rationale, drilling in as deep as I want. A good follow-up question, courtesy of a Fable review: *"what did you decide that wasn't in the spec?"* — it makes the agent enumerate its own improvisations, which is exactly where surprises hide.

**Stay skeptical, but cheaply.** Most of the time these models are so good that you necessarily extend enormous trust. But when a first answer disagrees with your own knowledge, or doesn't sound plausible, or your subconscious just doesn't like it — it costs you almost nothing to say "go back and have a longer think," "give me some more options," or "I don't think that's true; research it and prove it to me." (And per section 11, the strong version is a fresh context or the other model.)

**Add an analysis step to your asks.** "Show me the open tasks" becomes "find the open tasks, evaluate each for customer value and implementation complexity, and show them to me sorted." You have an analyst on staff; use it. (Ask it to show its rubric first — ranked-with-reasons beats numeric scores, which can be confidently made up.)

**Optimize for your time, not the agent's.** I used to have agents pause before committing so I could review — this was dumb. The overwhelming majority of the time the work is fine, and I'd made myself the bottleneck. Undoing a commit is faster than making one, and any agent can do it equally well. So now: agent finishes, commits, marks the task ready for human review, moves on; I batch-review later and close several at once.

**Time-box the root-causing.** Agents want to keep making progress, to a fault. When a tool fails transiently, they'll sometimes make a snap judgment and lurch to a worse workaround — and an unattended agent can stay stuck with an inferior approach for hours. The fix was to have the agent write itself a rule: don't abandon the preferred tool on first failure; spend a small diagnostic budget (2–3 focused probes) checking the boring causes first; treat the first plausible explanation as a hypothesis, not a verdict. That last clause is the load-bearing one.

**When an agent fails in a characteristic way, have the *agent that failed* write the rule.** The failure is fresh in its context, so it writes a sharper rule than you would. This is a repeatable pipeline — incident, post-mortem, rule — that works on any recurring failure mode.

**Soft guardrails versus hard gates.** Everything you put in `AGENTS.md`/`CLAUDE.md` is advice — probabilistic, and it loses force as context fills. When a violation is expensive, graduate the rule to a deterministic gate that *can't* be ignored. Claude Code has a built-in hook system for this (run checks before tool calls, before commits, etc.); Codex currently doesn't — but git itself does: pre-commit hooks via Husky or equivalent run your tests and lint on every commit no matter which agent, or which vendor, made it. Prose rules bend behavior; gates guarantee it.

**Subagent discipline.** Both platforms let your agent spawn helper agents. Understand the defaults before you say yes to a "workflow," because the default can be the most expensive model at full reasoning strength for every helper — and an eager orchestrator (the Anthropic models are notably more enthusiastic here) can burn through an entire subscription on a task that needed one agent. General good practice: have explicit rules in your config for *when* subagents are warranted, *which* (cheaper) models they run on, and what the cap is.

**Small wins.** An end-of-turn chime so you know when the agent needs you without watching it. Dev agents rename their thread to the issue number they're working, so the sidebar becomes a status board. Tell the agent to set up Karabiner with a hyper key — a one-sentence ask that used to be an evening of config. Point it at your screenshots folder once, in your global config, so "look at the screenshot" just works.

### 16. Talk, don't type

This might not seem like it's part of the process. It's part of the process, and here's why.

The quality of everything in sections 9–13 depends on how much high-quality input you actually give the model — and it turns out the bottleneck was never your thinking, it was your typing. You can talk far faster than you can type, and it's cognitively easier to describe something in detail than to compose written sentences at the same level of detail. Studies back this up now, and voice input has become a genuine best practice among agentic engineers: people simply provide more useful information by talking. My poorly-organized rant, full of sentence fragments and abrupt topic changes, beats my carefully-typed summary — because the agent is superhuman at untangling a garbled stream of consciousness, and it remembers every single thing I mention.

The workflow this unlocks is the real payoff: voice is a completely separable input channel from your mouse and keyboard. I turn on dictation, switch over to my app, and click through testing the features that were just built while narrating a continuous stream of feedback — every little thing that needs fixing or tweaking. When I'm done, the agent digests the whole slab, makes a holistic plan, and cranks through it.

Tooling: I use Superwhisper on macOS — hotkey to dictate into any text field, ~20 models to choose from including on-device ones (which also solves the "can't send work data to the cloud" problem). I've recently added a post-processing step that runs the transcript through a small language model to clean up transcription errors, and it does a phenomenal job. This whole document was substantially dictated, which is also why my friends' inboxes fill up so fast.

### 17. More agents: IRL and AFK

As you scale up, agent use falls into two broad families, and they want different things:

- **IRL (interactive):** long-lived, very smart, fast. Uses its accumulated context *and* the artifacts to reason. This is your planning partner.
- **AFK (independent):** disposable, smart, cheap. Works unsupervised for an hour or more, and reasons *only* from artifacts. This is your implementation workforce.

It's only very recently become feasible to treat one agent as a single long-lived consciousness, and it's transformative. My planning agent is effectively a product manager: they've been thinking about nothing but my product — strategy, features, UX — for days, so I flip over and get instant, fully-loaded judgment. My implementation agent's context is full of terminal output and code; it isn't going to do the best product thinking, and I don't ask it to. The specialization keeps both context windows dense with exactly the right things — which, remember, is what makes models smart.

The PM generates the *entire* plan: PRD, visual artifacts, implementation order, task dependencies, and all the GitHub issues. It sounds like a lot, and that's the point. Developer agents then just get handed the orientation docs, the PRD, and the issue — very little additional planning needed. The greater the percentage of directly relevant information in the developer's context window, the smoother development goes. If the framework and skeleton are good, agents make solid decisions at the lower levels. If you care about it, put it in the spec.

What AFK agents need to succeed scales with how long you want them working alone: extremely detailed issues (user-facing and technical subtasks, acceptance criteria, references to docs and commits); solid tooling (tests, lint, review); accurate documents; and context they can't discover on their own — both environmental ("you'll see another agent working in this repo; they're only editing documents, your work won't collide") and operational ("I'm going to bed. Keep working through this entire stack. If anything needs my input, mark the issue and keep moving"). The newest models will run for hours on this and do good work — my largest overnight run so far was an entire epic, five thousand lines, near-perfect. My daily rhythm has reorganized around it: interactive definition work in the afternoon tees up the stack of well-specified tasks the agents chew through while I sleep.

The honest caveat about working in massive chunks: anything you *didn't* specify may get done in a sensible way, or the agent may make decisions you didn't want — the same quality you get when you allow substitutions in your grocery delivery, often in small ways you don't initially notice. That's not a reason to avoid AFK work; it's a reason to keep the specs tight and to use section 11's validation on what comes back.

Two logistics notes: when multiple agents started colliding in one checkout, I moved each to its own git worktree (an agent can set this up for you — just describe the collision problem). And when you want to work away from your desk, the durable answer is the repo-as-hub pattern: GitHub is the canonical state, and cloud agents — both vendors now run agent sessions on their own infrastructure against your repo, drivable from a phone — are windows into it. Chat histories don't transfer between tools; committed documents and issues do.

### 18. Context, part two: the token economy

You know from Track 1 that the context window is working memory and less is more. Here's the economic layer, which starts mattering the day you're running agents for hours.

**A wasted token isn't a one-time cost.** Models are autoregressive: the model re-reads the whole context to produce the next token, and the next, thousands of times over. You pay rent on the same token again and again — savings compound. Token efficiency buys you four things at once: speed, a context window that lasts longer (less compaction, less getting-back-up-to-speed), the option to trade the savings for a higher reasoning level, and a subscription that stretches further.

**The expensive unit is the turn, not the command.** Every message roundtrip is a full model inference over the entire conversation — tens of seconds on a frontier model with a long session — while the shell command it decided to run took milliseconds. A naive git commit ritual (status, diff, log, stage, commit, verify) is five or six turns: several minutes of inference wrapping 100ms of actual git. People watch that spinner and conclude "the agent is slow at git," when they're really watching a large model re-read a long conversation five times. The fix is to tell your agent to batch: one call to inspect, one call to act. Same information, half the wall clock. And batching applies to any tool workflow — test loops, file exploration, CI checks — not just git. (One caveat: keep commands with hook or permission significance standalone, so your gates still see them.)

**Get the searching out of the main thread.** Searching and reading code burns a lot of tokens, and the built-in approach — grep — is a blunt hammer. Two better options. Subagents aren't just for parallelism; their other main application is moving token-intensive work like research and code search out of the main context so the main thread only sees the result. And specialized search services (I use MorphLLM's WarpGrep, ~$20/month) run a local model that answers high-level questions about your codebase in one shot, returning just the relevant blocks. The vendor's own benchmark numbers — treat them as vendor numbers — claim about 39% input-token reduction and about a 10% *accuracy* bump, and that second number is the interesting one: a cleaner context window makes the model smarter, not just cheaper. I'd expect the harnesses to build this in natively before long — because why wouldn't you?

**Match the model to the phase, not the task list.** There's growing evidence — mine and others' — that if you use a very smart model to design, plan, and schedule the project, you retain almost all the benefit even when a somewhat cheaper model does the implementation. It's a best practice for humans, after all. My current tiering is in the "current process" section below. Related: reasoning-level curves flatten at the top — on [DeepSWE](https://deepswe.datacurve.ai), the benchmark I trust, the difference between High and the maximum settings is small enough that the top levels are rarely worth the tokens. Medium and High are the sweet spots. But don't optimize prematurely: focus first on things that improve output *quality*, and ignore efficiency until you actually start hitting subscription limits. There's no penalty for using 100% of a plan, and they're generous.

**On benchmarks, briefly:** the reason I keep citing [DeepSWE](https://deepswe.datacurve.ai) is that the older agentic-coding benchmarks turned out to have non-representative questions and internet-leaked answers, and — critically — DeepSWE runs every model in the *same* harness, so you're comparing models rather than model-harness bundles. And on vendors: I try hard not to be a fanboy of any AI company. I've switched primary models twice this year on the merits. Intelligence is commodifying — the frontier models are more similar than different now, next-gen models keep landing from multiple labs — and to me that's great news. It says my state and my process are what I need to care about, and I can shop around for whoever is selling intelligence at the best price.

### 19. Where this goes

I don't have many super-profound conclusions about this sea change — I'll just say, without exaggeration, it's a more radical change than has ever happened in software engineering, so it's worth having a think.

Implementation doesn't actually go to zero, but ever-more-sophisticated slices of it are commoditizing very quickly. We're in an interesting place where an amateur with these tools can be close to as good as an expert in a lot of domains, but can't generally reach past what the best experts can do — while for experts, the tools are force multipliers. There's been talk of 10x engineers for twenty years; there are now many 10x and a few 20x engineers, and you can see it in the job market at both ends.

There's a debate raging among engineers right now about whether you should still read the code. It's fascinating because everyone in it knows that, given the direction things are heading, there's no way to read it all and keep up. The frame I find useful: software engineering has always been the continual invention of new layers of abstraction, followed by increasingly rigorous ways to *verify* those layers until they're trusted enough that most engineers stop thinking about what lies beneath. We didn't stop thinking about CPU registers because registers stopped mattering; we stopped because compilers, debuggers, and tests got good enough that looking was usually a waste of time. Code won't disappear. It's becoming a specialist's representation rather than the everyday medium of software construction — and the verification layer for it is what most of this document builds. Every abstraction starts life as heresy, becomes craftsmanship, matures into infrastructure, and eventually becomes invisible. In the meantime, calibrate: how much of the code you read, and how much attention you pay, should scale in proportion to how important the software is and how critical its stability is.

What appreciates while implementation depreciates: taste and communication. I've worked with many engineers who write great code but can't express their ideas verbally, and those people are going to really suffer. Product managers and designers are going to have ever more ability to realize their own ideas without engineers — most of them will never realize just how close they are to this possibility. There's less and less technical skill required every six months. It's an ascendant time for polymaths and flexible thinkers.

I think of this as the third wave of technology supercharging the velocity of human knowledge. The text web massively democratized access to expert documents. The video web was the second wave — for so many topics it's vastly more powerful to watch someone do a thing than read about it. An interactive expert you can converse with on literally any topic has to be a bigger multiplier than either. And when I asked one of those experts to challenge the fantasy that we'll all just delegate everything to agent fleets, it gave me the counterpoint I now believe: the bottleneck doesn't disappear, it moves upstream to deciding what to build and what good looks like. You are not a bottleneck that hasn't been automated away yet — you're the quality function. The human in the loop is where the product comes from. The agents are the scaffolding.

---

## My current tooling and process (July 2026)

This section will go stale first.

- **Subscriptions:** OpenAI $200/month, Anthropic $100–200/month, MorphLLM WarpGrep pay-as-you-go (~$20 cap). The pair costs less than a gym membership and does the work of a small team.
- **Models:** This is as much about principles now as about specific models: use a fast model for the work you sit with, the smartest model for definition and planning, and a cheaper-but-clever model for implementation. My current instantiation: Sol High Fast for feature definition, UX design, project planning, and task scheduling (Fast because it's interactive work — I'm worth it); Terra Extra High for most implementation, including having the implementation agent update the plans and reference docs for its own work. Fable and GPT 5.6 are more similar than they are different, and I've become much less choosy about who does what — I'll use either happily for coding, design, and technical tasks. The one exception is written prose: GPT writes well, but Fable writes exceptionally well. To me there's a noticeable gap, and it's one of the few places I can still see clear daylight between them.
- **Cross-model validation:** The bigger shift in my process is using both models on the same task, one as creator and one as reviewer — I get unique, valuable insights from each. Ad hoc, it's one sentence: "Ask a new Fable High agent to review this document and then summarize the results." For the most important decisions, my `/dual_model_design` skill has both agents iteratively generate outputs and review each other's work. And Fable is set up to review every commit GPT creates.
- **Harnesses:** Codex as the daily driver (Steer input mode, end-of-turn bell); Claude Code IDE alongside. One-time config so both see the same instructions and skills.
- **Input:** Superwhisper for essentially all text, with a post-processing model cleaning the transcript.
- **Process skills:** Matt Pocock's set (`/grill_me`, `/to_prd`, `/to_issues`, `/tdd`, `/improve-codebase-architecture`) plus my own four: `doc-sweep`, `blind-spot-check`, `dual-model-design` (the Claude-vs-GPT bake-off), and `personal-voice`.
- **Structure:** global `AGENTS.md` as canonical instructions with `CLAUDE.md` symlinked to it; per-project `CONTEXT.md`, `docs/plans/`, `docs/reference/`, GitHub Issues; agents commit automatically and mark work ready for review; dev agents rename their thread to the issue number.
- **Working shape:** usually two concurrent agents — a long-lived planner and an implementation agent — plus AFK stacks overnight; worktrees when agents would collide; afternoons for definition work that tees up the overnight stack; phone check-ins on the go.

*(To be extended — this is the section I'll keep re-dating.)*

---

## Glossary

- **Agent** — an LLM with hands: it can read/write files, run commands, browse, and act, not just answer.
- **Harness** — the application wrapped around the model (Claude Code, Codex). Same brain, different body; a lot of your experience is the harness.
- **Context window** — the model's working memory, measured in tokens. Finite, fills up, and quality drops as it fills.
- **Token** — the unit models read and write; roughly three-quarters of a word. Also the unit you're billed in.
- **Compaction** — summarizing a long conversation to free up context; the agent then works from the summary.
- **AGENTS.md / CLAUDE.md** — the standing-instructions file an agent reads at the start of every session. Your process lives here.
- **Skill** — an installable bundle of instructions (plain Markdown) that teaches an agent a capability or workflow.
- **MCP** — a plug-in standard that teaches agents to drive external tools (design apps, 3D software, services) without you teaching them anything.
- **Subagent** — a helper agent spawned by your agent; useful for parallelism and for keeping heavy searches out of the main context.
- **PRD** — product requirements document: what you're building and why. Can be one Markdown file.
- **CONTEXT.md** — the shared domain vocabulary between you and your agents.
- **Issue** — one well-specified unit of work; the shared to-do state between you and all your agents.
- **TDD** — test-driven development: tests written alongside (or before) the code, so breakage is caught automatically.
- **Hook / gate** — a deterministic check that runs automatically (before a commit, before a tool call). Unlike instructions, it can't be ignored.
- **Worktree** — a separate checkout of the same repository so multiple agents can work without colliding.
- **Cloud agent** — an agent session running on the vendor's servers against your repo, steerable from any device.
