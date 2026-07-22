# My First Agentic Software Process

*A compact guide to building reliable software with agents*

*By Jon Chester | Last updated July 21st, 2026*

This is a guide to working with language models and coding agents, but it is not really a guide to writing code. The important shift is learning to give a capable agent context, judgment, and a definition of done; to preserve the useful state outside any one conversation; and to review the result at the level where your own expertise matters.

That applies whether you are an engineer, a product manager, a designer, a consultant, or simply a smart person with an annoying problem and a computer. The technical ceiling is much higher than it used to be, but the useful on-ramp is surprisingly ordinary: pick a real problem, explain it fully, let the agent work, and keep the result somewhere durable.

The guide is deliberately layered. The first four sections are the minimum viable mental model. The later sections build toward a serious software workflow. You do not need to absorb all of it before starting. In fact, please don't. The point is to get moving, then add machinery when you feel the problem that machinery solves.

## 1. What a language model is actually doing

A language model generates text one token at a time. A token is roughly a word fragment: sometimes a whole short word, sometimes part of a longer one, sometimes punctuation. At each step, the model predicts a useful next token from the enormous set of statistical patterns it learned during training, appends that token, and repeats.

I think it is really worth having a basic understanding of that generative loop. I doubt you need much technical detail beyond it. Plenty of engineers using these systems will not know much more. You do not need this information to use language models, but keeping it in mind often helps you use them better.

The absurd part is that this works as well as it does. It sounds like a card trick: learn patterns from the co-occurrence of words across trillions of data points, predict one fragment after another, and hey look - a passable replica of human intelligence. The model also represents language in a many-dimensional mathematical space, where related ideas occupy related regions. I tried explaining that once and concluded that it sounds like science fiction, especially while high.

The useful consequence is simpler. The model does not retrieve a complete answer from a database. It constructs an answer in response to the material currently in front of it. Better material produces better construction.

If you want a friendly technical introduction, Andrej Karpathy's [Intro to Large Language Models](https://www.youtube.com/watch?v=zjkBMFhNj_g) is still an excellent place to start. It predates some recent agentic developments, which is an eternity in AI years, but the foundations remain useful.

## 2. The context window is the agent's working memory

The context window is everything the model can currently consider: your latest request, the conversation so far, its instructions, relevant files, tool results, and sometimes summaries of earlier material. Think of it as a very large desk. The agent can reason across anything laid out on the desk, but the size is finite, and filling it with irrelevant paper makes the useful paper harder to see.

My interactions with language models have tended to get longer over time, both in the amount of text in each prompt and in the number of round trips. Less often am I asking a contextless question. More often I am starting a conversation where we go back and forth, inspect possibilities, and refine the answer.

That is the first important habit: treat it as a conversation, not a command line. I often do not get the best answer on the first interaction. I get instructions or a product to investigate, follow up, make the situation more specific, and get a much better answer on the second or third pass. This happened often enough to change how I work. For real problems, the conversation is the unit of work.

More context is usually better, but only when it is relevant. A giant context window does not excuse dumping in everything you own. The goal is to increase the average relevance of the tokens the model sees. A short, accurate project summary can be more valuable than hundreds of pages of undifferentiated history.

This is why good agentic systems eventually develop context artifacts: a project overview, a glossary, a record of decisions, a set of executable issues, and reference documents describing how the finished system actually works. Those files let a fresh agent reconstruct the right mental model without rereading the history of civilization.

## 3. Models, tools, harnesses, and agents

People collapse several different things into the word "AI," which makes the products more mysterious than they are.

A **model** is the reasoning and language engine. Models differ in intelligence, speed, cost, taste, instruction-following, and how efficiently they use their context window.

A **tool** is an external capability the model can call. Search gives it current information. A calculator or code runtime gives it precise arithmetic. A Gmail connection lets it search mail. A browser lets it inspect and operate a website. Model Context Protocol, usually called MCP, is one standard way to describe tools so an agent can discover what they do and how to call them.

A **harness** is the environment around the model: the application that manages conversations, files, permissions, tools, context, and execution. Codex, Claude Code, Cowork, and similar products are harnesses. The same model can feel dramatically more or less useful in different harnesses.

An **agent** is a model operating in a loop with tools and a goal. It plans, acts, observes the result, and adjusts. A coding agent can inspect a repository, change files, run the tests, notice a failure, fix it, and present the completed work. The model still generates tokens, but the harness turns those tokens into actions and feeds the results back into the next turn.

The cleanest definition I found in my own notes was this:

> Claude Code is "just" good agentic task management that is allowed to modify files and run code.

That sounds reductive until you notice how big the consequence is. We went from searching the web for an answer, to describing the issue to an AI and having it explain the solution, to telling an agent that we have a problem and asking it to go fix it.

## 4. Stop trying to write the perfect prompt

The old prompting advice emphasized clever phrasing and precision. Modern models are much better at recovering meaning from ordinary language. For most serious work, more signal beats a tiny jewel of a prompt.

A couple of AI-assisted coding guides suggested dictating specifications because it is easier to be verbose. When we speak, we tend to be less precise but say much more. The extra examples, constraints, motivations, and half-formed concerns give the model useful evidence. You can always ask it to organize the mess before acting.

Voice input became my primary text-input method for exactly that reason. I started because I wanted to type less. I kept doing it because it is cognitively easier to describe something in detail than to compose written sentences at the same level of detail. A rambling explanation full of fragments can still contain more useful information than a pristine three-line prompt.

Voice also lets you steer while doing something else. I can test a new interface and dictate a stream-of-consciousness account of every little thing that feels wrong. When I finish, the agent can organize the feedback, file tasks, or make the changes. This is much more natural than stopping after every observation to write a ticket.

If raw dictation gets too chaotic, add post-processing. The useful trade is not maximum fidelity versus laziness. It is the fastest input method that still gives the agent dense, accurate context.

The practical rule is: explain the situation as you would to a smart new colleague. Include what you are trying to accomplish, why it matters, what constraints are real, what you have already tried, and what a good result would feel like. Then let the agent ask questions.

## 5. Let the agent interview you

One of the best uses of a strong model is not answering your questions. It is asking you better ones.

Having the model run the interview is an excellent way to flesh out an idea. A good interview workflow walks down each branch of the decision tree, resolves dependencies between decisions, recommends an answer when useful, and asks one question at a time. Facts that can be discovered from the environment should be discovered; actual decisions belong to you.

The first time I used this process seriously, I spent about an hour answering roughly 40 questions about a product. The discussion moved from the broad purpose into successively finer decisions until we had a shared model. The durable output was not merely a transcript. It was a domain definition, a specification, and a set of decisions with their reasoning preserved.

There is nothing inherently software-specific about this. The same process can define a consultancy offering, a research plan, a house brief, a pitch, or a difficult personal decision. The agent supplies patience, breadth, and pressure-testing. You supply values, judgment, and authority.

You are always in charge of the depth. A methodical interview can examine every branch, but sometimes you have enough. Ask what topics remain, fast-forward through the obvious ones, cut the list down, or go deeper where the risk is real. The process is a tool, not a small bureaucrat you accidentally hired.

## 6. Start with a real project, not an AI exercise

The best first project is useful, forgiving, and rich enough to require judgment. A fresh computer setup is nearly perfect. It has real files, real preferences, lots of tedious choices, and almost no deadline pressure. Treat it as a flight simulator.

Delegate like a chief executive, not like a search engine. You already know how to hand work to a smart employee: give context and intent, not keystrokes. Do not ask, "How do I install Homebrew?" Say, "Here is the Applications folder and Documents tree from my old Mac. Interview me about how I work, propose what to keep, what to replace with something better, and what to let die."

The agent asking questions is a feature. A good first session should feel more like an intake meeting than a command line.

The habit trick is to narrate the groan. Every time you catch yourself sighing, "Ugh, I have to..." - rename 40 files, chase down a vendor document, turn meeting notes into an RFP section - say the annoyance to the agent before doing anything. Half the time it just gets done. The failure mode is not asking too much. It is the thousand small things that feel too trivial to delegate and quietly eat the week.

Let the agent touch the machine, but grow trust deliberately. Begin with the agent proposing actions and you approving them. Loosen permissions after you have seen how it behaves. Watching it narrate the steps is also one of the fastest ways to learn what it can do.

Then graduate to a small, real tool that somebody will use. Ask for two or three prototypes in an afternoon, pick one, and ship it. Once you have experienced "I described a tool at lunch and somebody used it by Friday," the boundary of what seems possible moves very quickly.

One warning: during the first week, people tend to over-verify everything. By the third week, they start under-verifying. The steady state is in between. Trust the agent, but read the diff before the work goes to a client.

## 7. The agents are transient; the state is preserved

Most people begin by treating an AI as a consultant and focusing on one chat at a time. The limitation appears quickly: how does the next conversation pick up the important state without re-explaining everything?

The answer is to orient the work around durable artifacts - literally files. The agents are transient; the state is preserved.

Coding environments arrived at this model early because software already lives in project folders. Every agent works within a defined set of files, with explicit permission required to reach beyond it. But the pattern is not limited to code. A project can contain research notes, presentations, interview transcripts, plans, decisions, and financial models.

The core mental shift is this:

> Stop treating chat as the workspace. The folder is the workspace; chats are steering.

A minimal project folder might contain:

```text
project-name/
  README.md        # What this is and how to begin
  AGENTS.md        # How agents should work in this project
  docs/
    context.md     # Domain language and shared mental model
    plans/         # Future work and decisions still being made
    reference/     # How the current, finished system works
```

Do not create this entire structure because a guide told you to. Start with the folder. Add documents as the project becomes large enough to feel the problem each one solves.

## 8. Global and project agent instructions

Agent instruction files are durable context that the harness loads automatically. They save you from repeating how you want the agent to work, but they come in two different scopes that should not be muddled together.

**Global instructions follow you from project to project.** My Codex defaults live at `~/.codex/AGENTS.md`, outside any Git repository. That file contains the stable preferences I want applied nearly everywhere: where repositories live, how files are named, when agents need permission, how subagents and token budgets should be handled, how Git operations should be approached, and practical details such as where to look when I mention a screenshot.

Global instructions are also a good home for broad product and engineering process defaults. Mine describes preferences such as test-driven development, small vertical slices, keeping framework code separate from business logic, and maintaining current reference documentation. Those are not facts about one product; they are the way I generally want to work.

Keep the global file reasonably terse. It enters a huge number of conversations, so every paragraph should earn its place. A preference that applies to only one repository belongs in that repository. A correction or working rule that keeps recurring across unrelated projects may deserve promotion to the global file.

**Project instructions live inside the repository.** A project's `AGENTS.md` describes what is special about that project: its purpose, domain language, architecture, technology choices, setup commands, issue tracker, documentation layout, local development URL, testing expectations, and any strange hardware or deployment constraints. Because the file is committed, every human and agent working in that repository receives the same guidance.

For a concrete example, here is the [`AGENTS.md` from my PXLBLZ-IDE project](https://github.com/jon-whiteroomsoftware/PXLBLZ-IDE/blob/main/AGENTS.md). It shows how process, architecture, testing, documentation, and tool guidance can accumulate in a substantial repository. Do not copy it wholesale. Use it as an example of what can belong there, then keep only the parts your project actually needs.

Project instructions should explain how to work in the repository, not try to become the entire repository. Current work belongs in issues. Domain concepts belong in a context document. Future decisions belong in plans. Finished behavior belongs in reference documentation. `AGENTS.md` points agents toward those sources and states the rules for using them.

Teach the agent who you are early and in writing, but put each fact at the right level. A stable personal preference belongs globally. The audience, tone, constraints, and working conventions of one business or product belong in its project instructions. Every durable fact written down once is a fact that does not have to be reconstructed from hazy memory later. Agents compound like employees do, but only if you onboard them.

### AGENTS.md versus CLAUDE.md

Use `AGENTS.md` as the canonical shared instruction file for a repository. When creating a new project, create `AGENTS.md` first. If Codex and Claude should receive the same project guidance, make `CLAUDE.md` a symbolic link to `AGENTS.md`:

```text
project-name/
  AGENTS.md
  CLAUDE.md -> AGENTS.md
```

That gives both tools the same source of truth without maintaining two copies that will quietly drift apart. If Claude genuinely needs different instructions, keep a separate `CLAUDE.md`, but make it small and clearly limited to Claude-specific behavior. The same idea applies globally: a global Claude instruction file should contain only the defaults Claude needs, not a stale duplicate of the entire Codex file.

This arrangement is not sacred ceremony. It is just the least lossy setup: one shared file for shared guidance, small tool-specific files for real differences, and project knowledge in the documents that actually own it.

## 9. Git is durable state with time travel

Git has a reputation for being tedious and Byzantine. Fair. Fortunately, you no longer need to become a command-line Git enthusiast to benefit from it. The agent can operate Git; you need the conceptual vocabulary.

Git is not merely backup. Backup keeps the latest copy. Git keeps every meaningful state the project has occupied, with the reason for each change attached.

- A **commit** is a coherent checkpoint with a reason.
- A **diff** is the exact set of changes between checkpoints.
- A **branch** is a parallel version used to explore an alternative safely.
- A **revert** undoes a checkpoint without erasing the history.
- A **pull request** presents a proposed branch for review and discussion.

The consequences are surprisingly useful outside engineering.

**Project-wide time travel.** Git captures the whole project at a coherent moment, not one file at a time. "Show me the project as it stood when we committed to the second-quarter scope" is answerable.

**A decision journal.** Every change can carry a message explaining why. Six months later, you can find the change from 14 days to 30 days and see what else changed with it.

**Cheap parallel drafts.** Two competing approaches can live on separate branches. Compare them, choose one, and discard the other without contaminating the main version. Goodbye, `FINAL_v3_revised_ACTUAL.docx`.

**Precise review.** A diff shows the 14 lines that changed instead of asking a reviewer to reread the entire document.

**A safety rail for agents.** Every agent change is reviewable and reversible. Multiple agents, or an agent and a human, can work without silently trampling the same state.

GitHub adds a shared remote home for the repository. That makes Git the common substrate across local agents, cloud agents, multiple computers, and automated workflows. The repository is the hub; agents and devices are spokes.

## 10. Define the thing before implementing the thing

Implementation is becoming dramatically cheaper. That makes judgment, taste, and communication more valuable, not less.

An amateur with strong tools can now get surprisingly close to an expert in many bounded domains, but usually cannot reach beyond the limit of current expert practice. Experts receive the same force multiplier. This is an unusually good moment for product people, designers, and flexible generalists who can explain what they want and recognize quality when they see it.

The big trap is using the increased implementation speed to build the wrong thing faster.

Shake out the load-bearing decisions early. Have long conversations. Ask the agent to interview you. Build a prototype. Request several approaches and compare them. The core data model, vocabulary, and boundaries should become clear before a large amount of code hardens around them.

I use the house-hunting analogy. The first couple of houses are difficult to judge because you do not yet know what good value looks like. The solution is to look at more houses. By house 30, you know which features are essential, which are cosmetic, and where the trade-offs live. Turning over more rocks brings you closer to the thing you actually want to build.

The other useful maxim is: creation is hard; editing is easy. It is far easier to choose among concrete alternatives than to conjure the correct answer from nothing. Ask the agent for three architectures, three UI directions, or three versions of the paragraph. Have it explain the trade-offs. Pick what you like, reject what you do not, or use what you learned to make a fourth option that is much better.

For strategic conversations full of unknowns, preserve optionality. Do not prematurely force confidence into one path. Generate credible alternatives, learn from each, and converge when the decision becomes real.

## 11. A durable software workflow

If you don't already have a basic process, my standard recommendation is [Matt Pocock's skills](https://github.com/mattpocock/skills):

- **Product definition:** `/grill_me`, `/to_prd`, and `/to_issues` get a lot of use. They still do.
- **Development:** `/tdd` and `/improve-codebase-architecture`.

For substantial software, the workflow I have converged on is:

1. **Establish the domain model.** Define the important concepts, boundaries, and shared vocabulary in a context document.
2. **Interrogate the idea.** Use an interview or grilling process to expose missing decisions and weak assumptions.
3. **Write the plan.** Capture the intended outcome and major decisions in a product requirement document or technical design.
4. **Slice the work vertically.** Create issues that each produce a small, working, testable increment rather than building disconnected layers.
5. **Implement test-first.** Write a failing test, implement the behavior, then refactor with the test as a safety rail.
6. **Keep the docs synchronized.** Move finished behavior out of future plans and into current reference documentation. Reconcile issues, decisions, and the actual system.

The context document matters more than it may initially appear. A crisp glossary keeps your vocabulary precise and ensures the agent implements the concept you intended rather than a plausible neighbor. Decision records preserve why a thorny choice was made. Issues preserve executable state. Reference documents tell both humans and future agents how the system currently works.

Maintaining completely accurate user-facing and developer-facing reference documentation used to be prohibitively tedious. Now it is close enough to free that it becomes a powerful engineering tool. If agents cannot find the documentation, or if the documentation and tasks contradict reality, you are much less likely to get good software at the end.

This is why a documentation sweep is part of completing a feature rather than a cleanup chore for later. Flush finished work out of plans, update the reference, check the issues, and reconcile everything against the current state of the world.

## 12. Tests are rails for the agent

The `/tdd` skill alone is worth adding to your process. It takes almost no time to set up, but brings a lot of value: the agent writes tests as it develops, and those tests become a growing safety net around the codebase. Even if you rarely read or write them yourself, they will catch a surprising number of regressions before those regressions spread.

Tests are not magic or entirely self-validating. An agent can write a weak test or engage in test gaming - changing the test to make the code pass instead of fixing the code - so important behavior still deserves some human validation and a few controls against weakening the suite. Start with the easy win. The sophistication can come as the project earns it.

Good bones start with the important domain decisions. Prototype enough to settle the core objects and processes, then put tests around them early. When a later change breaks one of those assumptions, the failure is immediate and local. The agent can inspect the failing test, correct course, and try again.

Most coverage should live around pure logic: state transformations, parsers, validators, business rules, and other behavior that can run without a user interface. Framework components should remain thin and receive lighter smoke coverage. Integration tests accumulate as layers begin working together.

A practical commit gate runs fast tests, targeted new tests, type checking, and linting before a change is accepted. Smoke tests run before a push, review, merge, or handoff. The point is not ceremony. The point is that an agent can move extremely quickly, and fast feedback keeps that speed from compounding the wrong result.

## 13. Keep context clean as the project grows

Searching and reading a large codebase consumes a lot of the context window. A blunt search can flood the main thread with irrelevant files, and the model may later invent relationships among things it happened to read three turns ago.

The general optimization is to move discovery outside the main reasoning thread. A specialized code-search agent can receive a high-level architectural question, inspect the repository, and return only the relevant code and relationships. The main agent reasons over the result instead of inheriting all the search noise.

Subagents are useful for the same reason. Parallelism is only one application. The other is context isolation: send token-intensive research, code discovery, or mechanical extraction to a bounded worker and bring back a compact answer.

Do not jump into elaborate multi-agent orchestration because it sounds advanced. I usually get transformative output from one active implementation agent, sometimes paired with one planning or domain agent. More agents introduce coordination cost, collision risk, subscription usage, and more places for judgment to go missing.

I learned this the expensive way when a model proposed a research workflow for a task that should have taken one agent ten minutes. I approved it, got coffee, and returned to find that it had spawned 100 agents, burned two million tokens, exhausted the subscription, and failed to finish. Advanced is not the same as intelligent.

Start with one agent. Use a second when the tasks are genuinely independent or when isolating context clearly improves the main thread. State the number, purpose, model, and budget before launching a crowd.

## 14. Model choice matters less than workflow - until it matters

Models have different strengths. Some are better at aesthetics, prose, strategy, or high-level architecture. Others are faster, more token-efficient, or particularly strong at implementation. The rankings change constantly, so do not build your entire working method around this month's leaderboard.

A durable pattern is to use the strongest available reasoning for definition, architecture, user experience, planning, and task sequencing. Much of that intelligence survives when a faster or cheaper model performs the implementation from a good plan. Use the expensive judgment where it shapes everything downstream.

Do not optimize prematurely. Focus first on the practices that improve output quality. Subscription efficiency, specialized search, model routing, and overnight batch work become relevant after you hit a real boundary. Modern models can do astonishingly useful work even with an unsophisticated setup and mediocre prompting.

Benchmarks are evidence, not scripture. Prefer benchmarks that resemble real work and separate model quality from harness quality. Then run your own repeatable evaluations on tasks you actually care about. I use a visual-programming pattern library as a casual model test because it requires code comprehension, originality, performance judgment, and aesthetic taste. That tells me more about my work than a generic score alone.

## 15. Verification and failure modes

Agents are capable and still do dumb things. They may repeat a failing tool call, wander into the weeds, confidently choose the wrong interpretation, or produce something beautiful and structurally false.

When an agent starts behaving strangely, interrupt it and ask what it is doing. That simple prompt often triggers enough reflection for it to notice the mistake. Steering is normal collaboration, not evidence that the system failed.

Match verification to the stakes.

- For a disposable prototype, run it and see whether the idea works.
- For production code, inspect the diff and require tests.
- For client-facing prose, read every word and check the claims.
- For legal, medical, tax, or financial advice, use the model to research, organize, and prepare questions; use the qualified professional as the final authority.
- For precise geometry, measurements, or physical-world claims, verify with the appropriate instrument or expert. A model's language fluency is not a ruler.

One useful high-stakes pattern is to let the model produce the first analysis, including sources and statutes, then ask the expert to correct and confirm it. That can reduce expensive discovery time without pretending the model is the authority.

AI slop is not an unavoidable property of AI output. It is usually the visible result of insufficient judgment and editing. Writing from scratch is difficult; editing is much easier. Generate alternatives, select the good material, remove the generic filler, and verify the facts. The good outcomes are often invisible because they simply look like competent work.

## 16. July 2026 setup notes

These recommendations are a dated snapshot, not eternal truth. Product interfaces and model rankings are moving too quickly for anything else.

- Start in a desktop agent environment, not a terminal-only interface, unless you already prefer terminals. A good desktop harness exposes projects, threads, files, diffs, a browser, and tools without forcing you to operate all of them manually.
- Non-coders should still work from durable project folders. A general agent workspace such as Cowork may be the gentlest on-ramp; an agentic coding environment may be the better long-term choice if building software is even half the ambition.
- Keep important projects in GitHub. Local remote-control sessions are convenient but depend on the home machine. Cloud agents depend on committed repository state. Git is the bridge.
- Use the strongest model available for important planning and design. Use a fast, capable implementation model where the plan is already crisp. Do not manage model routing until the cost or speed difference is real for you.
- Prefer steering over silently queueing new guidance when you notice the agent moving in the wrong direction. Interrupt immediately when necessary.
- Add specialized search, multiple agents, cloud execution, scheduled work, and remote development only as actual needs appear.

The systems will keep changing. The durable skill is not remembering which button exists this month. It is learning to provide context, externalize state, specify outcomes, preserve decisions, and apply judgment to what comes back.

## Further resources

- [Intro to Large Language Models - Andrej Karpathy](https://www.youtube.com/watch?v=zjkBMFhNj_g)
- [Codex changelog](https://developers.openai.com/codex/changelog)
- [Matt Pocock's agent skills](https://github.com/mattpocock/skills)
- [Anthropic's frontend design skill](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md)
- [DeepSWE coding-agent benchmark](https://deepswe.datacurve.ai/)
- [Morph WarpGrep](https://www.morphllm.com/products/warpgrep)
- [Thursd.ai](https://podcasts.apple.com/us/podcast/thursdai-the-top-ai-news-from-the-past-week/id1698613329)
