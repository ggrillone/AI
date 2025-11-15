# Context Engineering Guide - Outline

## Introduction

### What is Context Engineering

### What Problems Does Context Engineering Solve

### Context Engineering vs. Prompt Engineering

## Foundational Concepts

### Understanding Context Windows

### Understanding Tokens

#### What is a Token

#### Token Cost and Economics

#### Input vs. Output Tokens

### Context Failure Modes

#### Context Poisoning

#### Context Distraction

#### Context Confusion

#### Context Clash

#### Context Rot

## Core Context Management Strategies

### Task Decomposition (Breaking Tasks into Smaller Pieces)

### Structured Note-Taking and Planning

#### AI Log Files

#### Planning Files

#### Memory Systems

### Context Editing

#### Branching Conversations

#### Reverting and Backtracking

#### Clearing Wrong Tool Calls

### Just-in-Time Context Strategies

### Compaction Techniques

#### When to Compact

#### Summarization

#### Context Pruning

### Context Offloading (Scratchpads and External Storage)

## Best Practices for Context Management

### Context Usage Guidelines

### Co-location of Mandatory Context

### Keeping Context Small

## Retrieval Augmented Generation (RAG)

### What is RAG

### When to Use RAG vs. Long Context

### Basic RAG Architecture

### Advanced RAG Techniques

#### Contextual Retrieval

#### Contextual Embeddings

#### Hybrid Search (BM25 + Embeddings)

#### Reranking

#### Query Enhancement

#### Chunking Strategies

### RAG in Production

## Tool Design and Tool Use

### Principles of Effective Tool Design

### Tool Selection and Tool Loadout

### Tool Response Design

#### Levels of Tool Response Quality

#### Faceted Search and Agent Peripheral Vision

#### Tool Response as Prompt Engineering

### Progressive Disclosure

## Multi-Agent Architecture

### Single-Agent vs. Multi-Agent Considerations

### Sub-Agents for Context Isolation

#### When to Use Sub-Agents

#### Sub-Agent Design Patterns

### Context Quarantine

### Slash Commands vs. Sub-Agents

## Agent Workflows and Form Factors

### The Three Agent Approaches

#### Conversation Interface (Chatbots)

#### Side-Effect Engine (Workflows)

#### Research Artifact (Reports & Tables)

### The Autonomy Spectrum

#### Deterministic Systems

#### AI Functions

#### Prompt Chains

#### Graph State Machines

#### Tool-Calling Loops

## Context Engineering for Coding Agents

### Onboarding for Coding Agents

### Quality Gates and Constraints

### The OODA Loop for Agents

### Frequent Intentional Compaction

#### Research Phase

#### Planning Phase

#### Implementation Phase

### Mental Alignment and Code Review

## Advanced Topics

### Model Context Protocol (MCP)

#### What is MCP

#### When to Use MCP

#### Code Execution with MCP

### Memory and Long-Term Context

#### Memory Tool

#### Cross-Conversation Learning

### Context Observability

### Agent Prototyping and Testing

#### Rapid Prototyping Methodology

#### Test-Driven Agent Development

## Production Considerations

### Cost Optimization

#### Prompt Caching

#### Input-Output Ratio Management

### Latency Considerations

### Security and Privacy

#### Privacy-Preserving Operations

#### Governance and Trust

### Evaluation and Monitoring

## Resources and Further Learning

---

# Content Sections

---

## Introduction

### What is Context Engineering

Context engineering is the natural progression from prompt engineering, focusing on curating and maintaining the optimal set of tokens during LLM inference rather than just writing effective prompts. Context refers to all information available to the model at inference time (system prompts, tools, Model Context Protocol, external data, message history, etc.). As agents operate over multiple turns and longer time horizons, managing this entire context state becomes critical.

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Context engineering is the process of designing and optimizing instructions and relevant context for LLMs and advanced AI models to perform tasks effectively. This encompasses multimodal models and includes: designing and managing prompt chains, tuning instructions/system prompts, managing dynamic elements (user inputs, date/time), searching and preparing relevant knowledge (RAG), query augmentation, tool definitions and instructions for agentic systems, preparing and optimizing few-shot demonstrations, structuring inputs and outputs (delimiters, JSON schema), short-term memory (state/historical context management) and long-term memory (retrieval from vector stores), and filtering out noisy information.

[See: Context Engineering Guide](https://www.promptingguide.ai/guides/context-engineering-guide)

Context engineering is the discipline of building dynamic systems that supply an LLM with everything it needs to accomplish a task. Unlike prompt engineering, which focuses on crafting individual instructions, context engineering takes a systems-level approach encompassing the entire information ecosystem—memory, retrieval systems, tool integrations, and dynamic information flow across multiple interactions.

[See: Context Engineering - The Evolution Beyond Prompt Engineering](https://www.vincirufus.com/posts/context-engineering/)

### What Problems Does Context Engineering Solve

Context must be treated as a finite resource due to "context rot"—as token count increases in the context window, the model's ability to accurately recall information decreases. This stems from the transformer architecture where every token attends to every other token (n² pairwise relationships), creating attention scarcity. LLMs have an "attention budget" that depletes with each new token, similar to human working memory limitations.

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Context engineering addresses key limitations: conversations should be append-only to maximize cacheability, models are more responsive to "fresh" context near the end of the window, and models perform worse when overwhelmed with large amounts of context. The key tension: models need access to all valuable context, BUT ONLY when that context is relevant to the task at hand.

[See: Context engineering is sleeping on the humble hyperlink](https://mbleigh.dev/posts/context-engineering-with-links/)

Most agent failures are not model failures—they are context failures. The core argument is that most agent failures have less to do with model limitations and everything to do with context quality. Building agents is less about the code/framework you use—the difference between a cheap demo and a "magical" agent is the quality of context provided.

[See: The New Skill in AI is Not Prompting, It's Context Engineering](https://www.philschmid.de/context-engineering)

### Context Engineering vs. Prompt Engineering

Many confuse prompt engineering with "blind prompting" (short task descriptions in ChatGPT). In actual prompt engineering, you think carefully about context and structure. Context engineering is the next phase—architecting the full context through rigorous methods to obtain, enhance, and optimize knowledge for the system.

[See: Context Engineering Guide](https://www.promptingguide.ai/guides/context-engineering-guide)

**Prompt engineering:** Learning to ask really good questions. Focuses on crafting the perfect set of instructions in a single text string.

**Context engineering:** Being a librarian who decides what books someone has access to before they even start reading. Far broader than prompt engineering.

[See: Context Engineering: Going Beyond Prompts To Push AI](https://simple.ai/p/the-skill-thats-replacing-prompt-engineering)

Context engineering differs fundamentally from prompt engineering by focusing on "context" as the better abstraction—grounding the model in accurate and exhaustive information rather than nailing specific wording. Context engineering refers to the discipline of designing systems and workflows that reliably ensure AI receives the right information. Two key qualities make this an engineering discipline: 1) Multi-player—designed with the team in mind, featuring shared workflows and practices; 2) Dynamic—enabling AI to fetch the right content by itself rather than requiring humans to pass it every time.

[See: How to Manage Context in AI Coding](https://refactoring.fm/p/managing-context-for-ai-coding)

Prompt engineering is a subset of context engineering. Even with all the context, how you assemble it in the prompt still matters. The difference: you're architecting prompts to work with dynamic data sets rather than a single static input. Prompting tells the model how to think, but context engineering gives the model the training and tools to get the job done.

[See: The rise of "context engineering"](https://blog.langchain.com/the-rise-of-context-engineering/)

---

## Foundational Concepts

### Understanding Context Windows

A context window is the "working memory" for language models—the entirety of text a model can look back on and reference when generating new text, distinct from the training data corpus. There's a practical limit to how much information a model can consider at once = context window. Your prompts + AI response + other information you provide → context window.

[See: Context windows](https://docs.anthropic.com/en/docs/build-with-claude/context-windows)

The context window operates with progressive token accumulation where each user message and assistant response accumulates within the window. Previous turns are preserved completely, creating linear growth with each turn. Claude models have a 200K token capacity (200,000 tokens) representing the maximum capacity for conversation history and generating new output. Each turn consists of an input phase (all previous conversation history plus current message) and output phase (generates response that becomes part of future input).

[See: Context windows](https://docs.anthropic.com/en/docs/build-with-claude/context-windows)

Claude Sonnet 4 and 4.5 support 1-million token context windows, currently in beta for organizations in usage tier 4 and those with custom rate limits. This allows processing much larger documents, maintaining longer conversations, and working with extensive codebases.

[See: Context windows](https://docs.anthropic.com/en/docs/build-with-claude/context-windows)

A context window is like a big sheet of paper passed to the LLM with a token limit. Key limitation: LLMs only know what they were trained on and what's provided in the context window. As context windows have exploded in token size, we've gotten increasingly clever about what we put in the window.

[See: Context Engineering: Going Beyond Prompts To Push AI](https://simple.ai/p/the-skill-thats-replacing-prompt-engineering)

---

### Understanding Tokens

#### What is a Token

Tokens are roughly ¾ of an English word or about four characters (e.g., "ChatGPT" = two tokens: "Chat" and "GPT"). Token count matters because billing, latency, and memory all scale with it.

[See: Context Engineering: Going Beyond Prompts To Push AI](https://simple.ai/p/the-skill-thats-replacing-prompt-engineering)

---

#### Token Cost and Economics

With API calls priced per token, understanding the input-to-output ratio is critical. Experiments reveal the actual ratio is dramatically higher than initially assumed: **300× on average and up to 4000×**. This means that for every token the model generates in its response, it processes 300 tokens of input context on average, with some queries requiring as much as 4000 tokens of input per output token.

[See: The Hungry, Hungry AI Model](https://tomtunguz.com/input-output-ratio/)

With a 300:1 ratio, costs are dictated by the context, not the answer. Even though output tokens are more expensive per token, the sheer volume difference overwhelms this. On OpenAI's pricing page, output tokens for GPT-4.1 are 4× as expensive as input tokens. However, when the input is 300× more voluminous, **the input costs are still 98% of the total bill**.

[See: The Hungry, Hungry AI Model](https://tomtunguz.com/input-output-ratio/)

This completely reframes the cost optimization challenge—reducing input token count has 50× more impact on total costs than optimizing output length. The critical task is building efficient data retrieval and context: crafting pipelines that can find the best information and distilling it into the smallest possible token footprint.

[See: The Hungry, Hungry AI Model](https://tomtunguz.com/input-output-ratio/)

If 99% of tokens are in the input, building a robust caching layer for frequently retrieved documents or common query contexts moves from a "nice-to-have" to a **core architectural requirement** for building a cost-effective and scalable product.

[See: The Hungry, Hungry AI Model](https://tomtunguz.com/input-output-ratio/)

---

#### Input vs. Output Tokens

Output tokens cost more than input tokens across all providers. For example:
- GPT-4.1: Input $2/1M tokens, Output $8/1M tokens (4x more expensive)
- Claude Opus 4: Input $15/1M tokens, Output $75/1M tokens (5x more expensive)
- Claude Sonnet 4: Input $3/1M tokens, Output $15/1M tokens (5x more expensive)
- Gemini 2.5 Pro: Input $1.25/1M tokens, Output $10/1M tokens (8x more expensive)

[See: Token Calculator for LLMs](https://token-calculator.net/)

Output tokens = Chat output + code generated. Think about what you want it to output - might want the chat to output concise bullet points to reduce token usage.

Content from Braindumpnotes.md

Not a reliable way to estimate input tokens (and definitely can't estimate output tokens) because the agent can look at code files you didn't specify and you can't predict caching it will use.

Content from Braindumpnotes.md

Some models like OpenAI's GPT-4.1 and GPT-4.1 mini show cached input pricing at significantly reduced rates ($0.5/1M and $0.1/1M respectively), demonstrating the cost benefits of prompt caching.

[See: Token Calculator for LLMs](https://token-calculator.net/)

---

### Context Failure Modes

#### Context Poisoning

When hallucinations or errors enter the context and are repeatedly referenced, corrupting subsequent reasoning. The Gemini 2.5 technical report documented this issue in their Pokémon-playing agent, where the agent would hallucinate game state information that poisoned the "goals" section of context. The agent would then develop nonsensical strategies pursuing impossible or irrelevant goals. Once the context is poisoned with misinformation, it can take a very long time to undo.

[See: How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

Hallucinations enter the context.

Content from Braindumpnotes.md

---

#### Context Distraction

When context grows so long that the model over-focuses on context history, neglecting what it learned during training. The Gemini Pokémon agent demonstrated this clearly—as context grew significantly beyond 100K tokens, the agent favored repeating actions from its vast history rather than synthesizing novel plans. This highlights an important distinction: long-context works well for retrieval and summarization, but struggles with multi-step generative reasoning.

[See: How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

A Databricks study found model correctness began falling around 32K tokens for Llama 3.1 405B, even earlier for smaller models. If models misbehave long before context windows are filled, what's the point of super large windows? Answer: summarization and fact retrieval. For other tasks, be wary of your model's "distraction ceiling."

[See: How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

Context overwhelms training.

Content from Braindumpnotes.md

---

#### Context Confusion

When superfluous content in the context causes the model to generate low-quality responses. The Berkeley Function-Calling Leaderboard shows every model performs worse when provided with more than one tool. The problem worsens with smaller models—a recent paper showed a quantized Llama 3.1 8B failed on GeoEngine benchmark when given all 46 tools (well within its 16K context window), but succeeded when given only 19 tools.

[See: How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

The fundamental issue: if you put something in context, the model must pay attention to it. Even irrelevant information or needless tool definitions will be taken into account. This has major implications for MCP adoption—connecting to every tool and stuffing all tool descriptions into prompts will cause context confusion.

[See: How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

Superfluous context influences responses.

Content from Braindumpnotes.md

---

#### Context Clash

When information and tools accumulated in context directly conflict with other context information. A Microsoft and Salesforce paper documented this by "sharding" benchmark prompts across multiple conversation turns rather than providing all information at once. The sharded prompts yielded dramatically worse results, with an average 39% performance drop. Even OpenAI's o3 dropped from 98.1 to 64.1 accuracy.

[See: How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

The problem: LLMs often make premature assumptions in early turns and attempt to generate final solutions before having complete information. These incorrect early answers remain in context and influence final responses. "When LLMs take a wrong turn in a conversation, they get lost and do not recover." This is particularly problematic for agents that assemble context from documents, tool calls, and other models—all with potential to disagree.

[See: How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

Context parts disagree.

Content from Braindumpnotes.md

---

#### Context Rot

A larger context window does not necessarily equate to "I can use this single chat longer."

Content from Braindumpnotes.md

[See: Context Rot: How Increasing Input Tokens Impacts LLM Performance](https://research.trychroma.com/context-rot)

The phenomenon where model performance becomes increasingly unreliable as input length grows. This comprehensive Chroma technical report evaluates 18 LLMs (including GPT-4.1, Claude 4, Gemini 2.5, Qwen3) to investigate "context rot." The research challenges the common assumption that models process context uniformly, showing that the 10,000th token is not handled as reliably as the 100th token.

[See: Context Rot: How Increasing Input Tokens Impacts LLM Performance](https://research.trychroma.com/context-rot)

**Key Finding:** Models do not use their context uniformly; performance degrades significantly as input length increases, even on intentionally simple tasks. While models achieve near-perfect scores on standard benchmarks like Needle in a Haystack (NIAH), these tests primarily assess direct lexical matching and may not represent flexible, semantically-oriented real-world tasks.

[See: Context Rot: How Increasing Input Tokens Impacts LLM Performance](https://research.trychroma.com/context-rot)

**Extended NIAH Experiments:**

1. **Needle-Question Similarity:** Performance degrades more quickly with lower similarity needle-question pairs. At short input lengths, models perform well even on low-similarity pairs, but longer inputs cause significant degradation. This isn't due to intrinsic difficulty—holding the needle-question pair constant while varying irrelevant content isolates input size as the primary factor.

2. **Impact of Distractors:** Distractors (topically related content that doesn't answer the question) have non-uniform impact that amplifies as input length grows. Even a single distractor reduces performance relative to baseline, and four distractors compound degradation further. Model families show distinct behaviors: Claude models are conservative and abstain when uncertain; GPT models show highest hallucination rates, generating confident but incorrect responses.

3. **Needle-Haystack Similarity:** When needles blend semantically with haystack content, model performance is affected non-uniformly. Testing PG essays vs. arXiv papers revealed that models perform better when needles don't blend with haystacks, though results vary by topic combination.

4. **Haystack Structure:** Surprisingly, structural coherence consistently hurts performance. Models perform better on shuffled haystacks (randomly reordered sentences) than on logically structured ones. This counterintuitive finding suggests structural patterns influence attention mechanisms, particularly as input length increases.

[See: Context Rot: How Increasing Input Tokens Impacts LLM Performance](https://research.trychroma.com/context-rot)

**Implications:** Real-world applications involve far greater complexity than these simple controlled tasks, implying that input length impact may be even more pronounced in practice. This highlights the critical importance of context engineering—the careful construction and management of a model's context window. Where and how information is presented strongly influences task performance, not just whether information is present.

[See: Context Rot: How Increasing Input Tokens Impacts LLM Performance](https://research.trychroma.com/context-rot)

---

## Core Context Management Strategies

### Task Decomposition (Breaking Tasks into Smaller Pieces)

Breaking tasks into smaller pieces (Decomposition).

Content from Braindumpnotes.md

Task decomposition is a foundational strategy for managing context effectively. By breaking complex tasks into smaller, focused subtasks, you can keep each agent's context window clean and focused. This prevents context pollution and enables more reliable execution.

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Several other concepts are needed to leverage sub-agents:
* Decomposition
* Research / planning
* Structured note taking (planning file & AI log file)

You break your task into stages and store relevant context/memory for sub-agents to use. For example:
* An initial agent that does the research
* 2nd agent does the planning
* All of the context goes into a md file (or multiple files)
* Now sub-agents can follow instructions and execute
* The md file(s) from the initial agent(s) should contain all context that the sub-agents need
  * Each sub-agent now does not need to go make the same tool calls to gather context
  * The context is complete and the sub-agents can reference the information they need to complete their individual tasks
  * Each sub-agent has its own context window
* Achieves a clear separation of concerns

Content from Braindumpnotes.md

---

### Structured Note-Taking and Planning

Having the agent write to planning / AI log files (structured note-taking). Agents can summarize for you, but this gives you more control. Can more easily switch to a new chat and continue from where you left off.

Content from Braindumpnotes.md

Agents regularly write notes persisted outside the context window, pulled back in at later times. Provides persistent memory with minimal overhead. This is also known as "Agentic Memory" or "Scratchpads."

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

#### AI Log Files

_No content available for this topic._

#### Planning Files

_No content available for this topic._

#### Memory Systems

Enables Claude to store and consult information outside the context window through a file-based system. Claude can create, read, update, and delete files in a dedicated memory directory stored in your infrastructure that persists across conversations. This allows agents to build up knowledge bases over time, maintain project state across sessions, and reference previous learnings without keeping everything in context.

[See: Managing context on the Claude Developer Platform](https://www.anthropic.com/news/context-management)

The memory tool operates entirely client-side through tool calls. Developers manage the storage backend, giving them complete control over where the data is stored and how it's persisted.

Content from Braindumpnotes.md

[See: Managing context on the Claude Developer Platform](https://www.anthropic.com/news/context-management)

---

### Context Editing

**Context Editing:** Automatically clears stale tool calls and results from within the context window when approaching token limits. As agents execute tasks and accumulate tool results, context editing removes stale content while preserving conversation flow, effectively extending how long agents can run without manual intervention. This also increases effective model performance as Claude focuses only on relevant context.

[See: Managing context on the Claude Developer Platform](https://www.anthropic.com/news/context-management)

"Enable longer conversations by automatically removing stale tool results from context"

"Context editing clears old file reads and test results while memory preserves debugging insights and architectural decisions, enabling agents to work on large codebases without losing progress."

"Memory stores key findings while context editing removes old search results, building knowledge bases that improve performance over time."

"Agents store intermediate results in memory while context editing clears raw data, handling workflows that would otherwise exceed token limits."

Content from Braindumpnotes.md

[See: Managing context on the Claude Developer Platform](https://www.anthropic.com/news/context-management)

#### Branching Conversations

If you find your chat going in the wrong direction or want to branch off at multiple points:
* In Cursor you can branch off from a past point find the user prompt you want as the "last left off point"
  * Click the "…"
  * Click "Duplicate Chat"

Content from Braindumpnotes.md

#### Reverting and Backtracking

The chat goes in the wrong direction and you want to backtrack:
* Find your user prompt where the agent started to diverge and click into it
* Change the prompt and hit enter
* You will get a pop-up from Cursor - Submit from previous message?
  * Select "Continue and revert"
  * Observe how the context % used goes down, that "bad context" is cleared and you can continue in the same chat

Content from Braindumpnotes.md

#### Clearing Wrong Tool Calls

The agent makes a tool call, but it's the wrong tool call:
* Revert back to the point before it made that tool call
* This wrong tool call only pollutes your context window with irrelevant information

Content from Braindumpnotes.md

---

### Just-in-Time Context Strategies

"Rather than pre-processing all relevant data up front, agents built with the "just in time" approach maintain lightweight identifiers (file paths, stored queries, web links, etc.) and use these references to dynamically load data into context at runtime using tools."

Content from Braindumpnotes.md

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

**Context Retrieval and Agentic Search:** Rather than pre-processing all relevant data upfront, the "just in time" approach maintains lightweight identifiers (file paths, stored queries, web links) and uses tools to dynamically load data at runtime. This mirrors human cognition—we use indexing systems rather than memorizing entire corpuses. Metadata (folder hierarchies, naming conventions, timestamps) provides important signals for understanding when to utilize information.

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

---

### Compaction Techniques

**Compaction:** Summarizing conversation contents nearing context limits and reinitiating with the summary. Tool result clearing is a lightweight form—once a tool is called deep in message history, the raw result is cleared.

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Compaction is automatic summarization of conversation history when context windows approach limits, preserving essential information while freeing memory space. This is a critical technique for long-running tasks that would otherwise exceed context capacity.

[See: Two Experiments We Need to Run on AI Agent Compaction](https://jxnl.co/writing/2025/08/30/context-engineering-compaction/)

If in-context learning is gradient descent, then compaction is momentum. Compaction isn't just storing facts—it's preserving the learned optimization path. When you compact "I tried X, it failed, then Y worked because Z," you're maintaining the gradient direction that led to success.

[See: Two Experiments We Need to Run on AI Agent Compaction](https://jxnl.co/writing/2025/08/30/context-engineering-compaction/)

#### When to Compact

Don't wait until your context window to reach 100%, stay closer to 70%. When you get to 60% context usage, start thinking about wrapping up the current chat.

Content from Braindumpnotes.md

Frequent intentional compaction—deliberately structuring how you feed context to the AI throughout the development process. Designing your ENTIRE WORKFLOW around context management, keeping utilization in the 40%-60% range.

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

#### Summarization

Context summarization involves boiling down an accrued context into a condensed summary. This first appeared as a tool for dealing with smaller context windows—as chat sessions approached maximum context length, a summary would be generated and a new thread would begin. Users did this manually in ChatGPT or Claude, asking the bot to generate a short recap for pasting into a new session.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

As context windows increased, agent builders discovered benefits beyond staying within total context limits. As context grows, it becomes distracting, causing the model to rely less on training data (Context Distraction). The Pokémon-playing Gemini agent discovered anything beyond 100,000 tokens triggered this behavior—the agent favored repeating actions from vast history rather than synthesizing novel plans.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

Summarizing context is easy to do but hard to perfect for any given agent. Knowing what information should be preserved and detailing that to an LLM-powered compression step is critical. Worth breaking out this function as its own LLM-powered stage or app to collect evaluation data that can inform and optimize this task directly.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

#### Context Pruning

Context pruning involves removing irrelevant or otherwise unneeded information from the context. Agents accrue context as they fire off tools and assemble documents. Periodically assessing what's been assembled and removing cruft improves performance. This could be tasked to your main LLM, a separate LLM-powered tool, or something more tailored to pruning.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

A current method is Provence, "an efficient and robust context pruner for Question Answering." Provence is fast, accurate, simple to use, and relatively small (only 1.75 GB). This tool can edit down content by 95%, leaving only relevant content for specific queries.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

This pattern argues strongly for maintaining a structured version of your context in a dictionary or other form, from which you assemble a compiled string prior to every LLM call. This structure helps when pruning, ensuring main instructions and goals are preserved while document or history sections can be pruned or summarized.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

---

### Context Offloading (Scratchpads and External Storage)

Context offloading involves storing information outside the LLM's context, usually via a tool that stores and manages data. Anthropic's "think" tool is essentially a scratchpad—a place for the model to write down notes that don't cloud its context but remain available for later reference.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

Having a space to log notes and progress works. Anthropic shows pairing the "think" tool with domain-specific prompts yields significant gains—up to 54% improvement against benchmarks for specialized agents. Anthropic identified three scenarios where context offloading is useful:

1. **Tool output analysis—**when Claude needs to carefully process previous tool calls before acting and might need to backtrack
2. **Policy-heavy environments—**when Claude needs to follow detailed guidelines and verify compliance
3. **Sequential decision making—**when each action builds on previous ones and mistakes are costly (often found in multi-step domains)

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

Write all necessary information to a md file so you can continue in a new chat (Compaction). If you prefer ask the agent to summarize (e.g. in Cursor the "/Summarize" slash command). But this hands over the reigns to the agent, I prefer explicitly writing to a file and taking the extra time to include what I want specifically in my prompt to the agent when telling it to create this file.

Content from Braindumpnotes.md

---

## Best Practices for Context Management

### Context Usage Guidelines

Don't wait until your context window to reach 100%, stay closer to 70%. When you get to 60% context usage, start thinking about wrapping up the current chat. Write all necessary information to a md file so you can continue in a new chat (Compaction).

Content from Braindumpnotes.md

Context management is usually the hardest part of building an agent. Programming the LLM to "pack the context windows just right", smartly deploying tools, information, and regular context maintenance is the job of the agent designer. As you build or optimize agents, ask yourself: Is everything in this context earning its keep?

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

### Co-location of Mandatory Context

The #1 rule for mandatory context is co-location—store it alongside where the task happens. For coding, this means keeping critical information in the repo:
* CLAUDE.md or AGENTS.md file for how AI should write code
* README file for instructions on building/testing/executing code
* SYSTEM-DESIGN.md file capturing main design features

Avoid relying too heavily on conversation threads/memories—consolidate useful information into files. For meaningful tasks, have agents create and maintain a ROADMAP.md file (git-ignored) for tracking progress, making it easier to recover from context rot and parallelize work with multiple agents.

[See: How to Manage Context in AI Coding](https://refactoring.fm/p/managing-context-for-ai-coding)

Context should be categorized by importance for the task at hand:
* **Mandatory context—**must be fetched correctly 100% of the time
* **Best effort context—**nice to have as additional info, but okay if retrieval sometimes fails or isn't 100% accurate

Getting this distinction right is crucial because if AI fails to account for mandatory context even a small percentage of times, engineers get frustrated and stop using it for complex work.

[See: How to Manage Context in AI Coding](https://refactoring.fm/p/managing-context-for-ai-coding)

### Keeping Context Small

The easiest way to improve context management for both humans and AI is keeping it simple and small through:
* **Low coupling—**componentized, isolated code reduces what needs to be fetched, considered, or updated
* **Convention over configuration—**great defaults reduce cognitive load and context size, with less code written meaning less to remember
* **Simple tech stack—**using the same language everywhere, favoring buy over build, using well-understood technology that doesn't require extensive documentation

[See: How to Manage Context in AI Coding](https://refactoring.fm/p/managing-context-for-ai-coding)

---

## Retrieval Augmented Generation (RAG)

### What is RAG

Retrieval-Augmented Generation (RAG) is a method for addressing knowledge-intensive tasks by combining information retrieval with text generation. Meta AI researchers introduced RAG as a method that combines two core components:
1. **Information retrieval component:** Finds relevant documents from external sources
2. **Text generator model:** Produces final output using retrieved information

[See: Retrieval Augmented Generation (RAG)](https://www.promptingguide.ai/techniques/rag)

The RAG process follows these steps:
1. RAG takes an input query
2. Retrieves a set of relevant/supporting documents from a source (e.g., Wikipedia)
3. Documents are concatenated as context with the original input prompt
4. The combined context is fed to the text generator
5. The generator produces the final output using both the query and retrieved knowledge

[See: Retrieval Augmented Generation (RAG)](https://www.promptingguide.ai/techniques/rag)

General-purpose language models can be fine-tuned for common tasks like sentiment analysis and named entity recognition, which generally don't require additional background knowledge. However, more complex and knowledge-intensive tasks require language model-based systems that access external knowledge sources to complete tasks effectively. This need arises because: static parametric knowledge is frozen at training time, models may hallucinate (generate plausible-sounding but incorrect information), and without external knowledge, generated responses may lack factual consistency.

[See: Retrieval Augmented Generation (RAG)](https://www.promptingguide.ai/techniques/rag)

RAG selectively adds relevant information to help the LLM generate better responses. Despite recurring "RAG is Dead" debates whenever models increase context windows, RAG remains very much alive. The temptation to "throw it all in" is strong, but treating your context like a junk drawer means the junk will influence your response. RAG prevents context confusion by ensuring only relevant information enters the context.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

---

### When to Use RAG vs. Long Context

For knowledge bases smaller than 200,000 tokens (about 500 pages), developers can include the entire knowledge base directly in the prompt, especially with prompt caching which reduces latency by >2x and costs by up to 90%. For larger knowledge bases, RAG becomes necessary.

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

This comprehensive research paper evaluates two fundamental strategies for enabling LLMs to work with extremely long external contexts:

1. **Long Context (LC):** Extending the context window to accommodate more information directly within the model's attention mechanism. Modern models support 200K-1M token windows, allowing vast amounts of information to be processed in a single pass.

2. **Retrieval-Augmented Generation (RAG):** Using retrieval systems to selectively access only the relevant information from large knowledge bases, injecting retrieved content into shorter context windows as needed.

[See: Long Context vs. RAG for LLMs: An Evaluation and Revisits](https://arxiv.org/abs/2501.01880)

**Key Findings:**

**LC Generally Outperforms RAG in QA Benchmarks:** Long Context shows superior performance on question-answering tasks, particularly strong advantage for Wikipedia-based questions. The ability to process all relevant information simultaneously within the context window provides performance benefits when the entire knowledge base can fit.

**RAG Has Specific Advantages:** RAG shows advantages in dialogue-based queries where maintaining long conversation history may be impractical, and for general question queries where selective retrieval can provide more focused context.

[See: Long Context vs. RAG for LLMs: An Evaluation and Revisits](https://arxiv.org/abs/2501.01880)

**Trade-offs:**

**Long Context Advantages:**
- No retrieval errors (no risk of missing relevant information)
- Full information available for reasoning
- Simpler system architecture without retrieval complexity
- Better for encyclopedic, fact-based questions where all context can fit

**RAG Advantages:**
- Computational efficiency when knowledge bases exceed practical context limits
- Lower token costs (only process retrieved relevant portions)
- Better for extremely large knowledge bases that exceed any practical context window
- More flexible for dynamic, evolving knowledge bases
- Better for dialogue and conversational contexts

[See: Long Context vs. RAG for LLMs: An Evaluation and Revisits](https://arxiv.org/abs/2501.01880)

---

### Basic RAG Architecture

The standard RAG preprocessing flow:
1. Break knowledge base into smaller chunks (usually a few hundred tokens)
2. Convert chunks into vector embeddings using embedding models
3. Store embeddings in a vector database for semantic similarity searching
4. At runtime, find most relevant chunks based on semantic similarity to query
5. Add most relevant chunks to the prompt sent to the generative model

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

Traditional RAG systems combine embeddings and BM25:
1. Break knowledge base into chunks
2. Create TF-IDF encodings and semantic embeddings
3. Use BM25 for exact matches
4. Use embeddings for semantic similarity
5. Combine and deduplicate results using rank fusion techniques
6. Add top-K chunks to prompt

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

**The Role of BM25:**

While embedding models excel at capturing semantic relationships, they can miss crucial exact matches. BM25 (Best Matching 25) is a ranking function using lexical matching to find precise word or phrase matches, particularly effective for unique identifiers or technical terms. BM25 builds on TF-IDF (Term Frequency-Inverse Document Frequency) by considering document length and applying a saturation function to term frequency.

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

**The Context Conundrum:**

Traditional RAG destroys context when splitting documents into chunks. For example, a chunk stating "The company's revenue grew by 3% over the previous quarter" lacks crucial context about which company and what time period, making it difficult to retrieve or use effectively.

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

---

### Advanced RAG Techniques

#### Contextual Retrieval

Anthropic introduces Contextual Retrieval, a method that dramatically improves the retrieval step in RAG systems by reducing failed retrievals by 49%, and by 67% when combined with reranking. The technique solves a fundamental problem in traditional RAG: context destruction during document chunking.

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

Contextual Retrieval prepends chunk-specific explanatory context to each chunk before embedding (Contextual Embeddings) and creating the BM25 index (Contextual BM25). Using Claude 3 Haiku, the system generates concise, chunk-specific context (50-100 tokens) that situates each chunk within the overall document.

Example transformation:
- **Original:** "The company's revenue grew by 3% over the previous quarter."
- **Contextualized:** "This chunk is from an SEC filing on ACME corp's performance in Q2 2023; the previous quarter's revenue was $314 million. The company's revenue grew by 3% over the previous quarter."

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

Contextual Retrieval is uniquely cost-effective with Claude's prompt caching. Rather than passing the reference document for every chunk, developers load the document into cache once and reference previously cached content. Assuming 800 token chunks, 8k token documents, 50 token context instructions, and 100 tokens of context per chunk, the one-time cost to generate contextualized chunks is $1.02 per million document tokens.

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

**Performance Results:**
- Contextual Embeddings alone reduced top-20-chunk retrieval failure rate by 35% (5.7% → 3.7%)
- Contextual Embeddings + Contextual BM25 reduced failure rate by 49% (5.7% → 2.9%)
- Adding reranking further reduced failure rate by 67% (5.7% → 1.9%)

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

---

#### Contextual Embeddings

Individual chunks in basic RAG often lack sufficient context when embedded in isolation. Contextual Embeddings use Claude to generate a brief description that "situates" each chunk within its source document. For each chunk, both the chunk and full source file are passed to Claude, which generates a concise explanation of what the chunk contains and where it fits in the overall file. This context gets prepended to the chunk before embedding.

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

Contextualization happens once at ingestion time, not during queries. Unlike HyDE (hypothetical document embeddings) that adds latency to each search, contextual embeddings are a one-time cost. Prompt caching makes this practical:
1. First chunk: Write full document to cache (small premium)
2. Subsequent chunks: Read from cache (90% discount)
3. Cache lasts 5 minutes (plenty of time to process all chunks in a document)

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

**Real Dataset Results (737 chunks across 9 files):**
- 61.83% of input tokens read from cache (2.27M tokens at 90% discount)
- Without caching: ~$9.20 in input tokens
- With caching: ~$2.85 (69% savings)
- Cache hit rate depends on chunks per document (more chunks = better caching benefit)

**Performance Improvement:** Contextual embeddings reduced retrieval failures by 30-40% across all k values. Pass@10 improved from 87% to 92%, with most pronounced improvement at Pass@5 where precision matters most.

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

#### Hybrid Search (BM25 + Embeddings)

Combining semantic search with keyword-based search further improves performance. BM25 (probabilistic keyword ranking algorithm) excels at finding specific terms but lacks semantic understanding. By combining both:
- **Semantic search:** Captures conceptual similarity and paraphrases
- **BM25:** Catches exact terminology, function names, specific phrases
- **Reciprocal Rank Fusion:** Intelligently merges results from both sources

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

Instead of only searching raw chunk content, the hybrid approach searches both the chunk AND the contextual description. This enables better matching for both semantic queries and exact terminology searches.

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

#### Reranking

Reranking is a filtering technique ensuring only the most relevant chunks are passed to the model. The process:
1. Perform initial retrieval to get top potentially relevant chunks (top 150)
2. Pass top-N chunks with user query through reranking model
3. Score each chunk based on relevance and importance
4. Select top-K chunks (top 20)
5. Pass top-K chunks to model as context for final generation

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

The highest value 5 lines of code you'll add. Chunk ranking shifted significantly—more than expected. Reranking can often compensate for a bad setup if you pass in enough chunks. The ideal reranker setup found: 50 chunk input → 15 output.

[See: Production RAG: what I learned from processing 5M+ documents](https://blog.abdellatif.io/production-rag-processing-5m-documents)

Two-stage retrieval approach:
1. **Stage 1 - Broad Retrieval:** Retrieve more candidates than needed (e.g., 100 chunks)
2. **Stage 2 - Precise Selection:** Use specialized reranking model (Cohere rerank-english-v3.0) to score candidates and select top-k

Trade-off: adds ~100-200ms query latency but reduces failures significantly.

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

#### Query Enhancement

Not all context can be captured by the user's last query. An LLM reviews the thread and generates a number of semantic + keyword queries. Processing all queries in parallel and passing them to a reranker covers a larger surface area and avoids dependence on a computed score for hybrid search.

[See: Production RAG: what I learned from processing 5M+ documents](https://blog.abdellatif.io/production-rag-processing-5m-documents)

Query enhancement techniques include query rewriting, step-back prompting for broader queries, and sub-query decomposition for complex queries.

[See: Advanced RAG Techniques: Elevating Your Retrieval-Augmented Generation Systems](https://github.com/NirDiamant/RAG_Techniques)

#### Chunking Strategies

Takes the most effort; you'll probably spend most of your time on it. Custom flows were built for both enterprises. Critical steps: understand the data, review the chunks, and verify (a) chunks aren't cut mid-word or mid-sentence, and (b) each chunk is a logical unit capturing information on its own.

[See: Production RAG: what I learned from processing 5M+ documents](https://blog.abdellatif.io/production-rag-processing-5m-documents)

Choice of chunk size, boundary, and overlap affects retrieval performance. Semantic chunking divides documents based on semantic coherence using NLP to identify topic boundaries rather than fixed sizes.

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

[See: Advanced RAG Techniques: Elevating Your Retrieval-Augmented Generation Systems](https://github.com/NirDiamant/RAG_Techniques)

---

### RAG in Production

What moved the needle for production RAG systems, ranked by ROI:

1. **Query Generation** 2. **Reranking** 3. **Chunking Strategy** 4. **Metadata to LLM** - Initially, only chunk text was passed to the LLM. Running an experiment found that injecting relevant metadata (title, author, etc.) improves context and answers significantly. 5. **Query Routing** - Many users asked questions that can't be answered by RAG (e.g., "summarize the article," "who wrote this"). A small router was created to detect these questions and answer them using an API call + LLM instead of the full-blown RAG setup.

[See: Production RAG: what I learned from processing 5M+ documents](https://blog.abdellatif.io/production-rag-processing-5m-documents)

**The Stack:**
- **Vector Database:** Azure → Pinecone → Turbopuffer (cheap, supports keyword search natively)
- **Document Extraction:** Custom
- **Chunking:** Unstructured.io by default, custom for enterprises
- **Embedding:** text-embedding-3-large
- **Reranker:** None → Cohere 3.5 → Zerank
- **LLM:** GPT-4.1 → GPT-5 → GPT-4.1

[See: Production RAG: what I learned from processing 5M+ documents](https://blog.abdellatif.io/production-rag-processing-5m-documents)

**Comprehensive Performance Results:**

| Approach | Pass@5 | Pass@10 | Pass@20 |
|----------|--------|---------|---------|
| **Baseline RAG** | 80.92% | 87.15% | 90.06% |
| **+ Contextual Embeddings** | 88.12% | 92.34% | 94.29% |
| **+ Hybrid Search (BM25)** | 86.43% | 93.21% | 94.99% |
| **+ Reranking** | 92.15% | 95.26% | 97.45% |

**Key Findings:**
1. **Contextual embeddings provided largest single improvement** (+5-7 percentage points)
2. **Reranking achieves highest absolute performance** (95.26% Pass@10), representing a 47% reduction in retrieval failures compared to baseline
3. **Trade-offs exist:** Contextual embeddings have one-time ingestion cost, hybrid search requires infrastructure, reranking adds query latency

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

**Recommendations by Use Case:**
- **High-volume, cost-sensitive:** Contextual embeddings alone (92% Pass@10, no per-query costs)
- **Maximum accuracy, latency-tolerant:** Full reranking pipeline (95% Pass@10, best precision)
- **Balanced production system:** Hybrid search (93% Pass@10, no per-query costs)

[See: Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

---

## Tool Design and Tool Use

### Principles of Effective Tool Design

**System Prompts:** Should be clear, direct, and at the right "altitude"—specific enough to guide behavior but flexible enough to avoid brittle, hardcoded logic. Organize into distinct sections using XML tags or Markdown headers. Start minimal and add based on failure modes.

**Tools:** Should be token-efficient, well-understood, self-contained, and have minimal functionality overlap. Avoid bloated tool sets that create ambiguous decision points. If humans can't definitively determine which tool to use, agents can't either.

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Tools represent a new software contract between deterministic systems and non-deterministic agents. Traditional functions like getWeather("NYC") work predictably every time, but when an agent asks "Should I bring an umbrella today?" it might call the weather tool, answer from memory, ask for location clarification, or hallucinate. This fundamental non-determinism means designing tools that increase the surface area over which agents can be effective, not just return the "right" answer.

[See: Beyond Chunks: Why Context Engineering is the Future of RAG](https://jxnl.co/writing/2025/08/27/facets-context-engineering/)

CLI tools should be deliberately simple—CLI commands that wrap your actual APIs. The simplicity enables rapid iteration without debugging complex tool call parsing. Error messages that guide next actions: instead of generic failures, tools should suggest specific next steps (e.g., "NEXT_STEP: Call lookup_user --email first").

[See: Context Engineering: Rapid Agent Prototyping](https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/)

---

### Tool Selection and Tool Loadout

Selecting only relevant tool definitions to add to your context. The simplest approach is applying RAG to tool descriptions. When prompting DeepSeek-v3, tool selection becomes critical above 30 tools—descriptions begin to overlap, creating confusion. Beyond 100 tools, the model virtually guaranteed failure. Using RAG techniques to select fewer than 30 tools yielded dramatically shorter prompts and up to 3× better tool selection accuracy.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

For smaller models, problems begin earlier. The "Less is More" paper showed Llama 3.1 8B fails a benchmark with 46 tools but succeeds with only 19 tools—the issue is context confusion, not context window limitations. Testing with Berkeley Function Calling Leaderboard found Llama 3.1 8B performance improved 44% with dynamic tool selection. Even when dynamic tool selection didn't improve results, power savings and speed gains (18% and 77% respectively) justified the effort.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

Too many tools overload agents, especially with overlapping tool descriptions causing confusion. Applying RAG to tool descriptions to fetch semantically similar tools improves selection accuracy by 3-fold according to recent papers.

[See: Context Engineering for Agents](https://rlancemartin.github.io/2025/06/23/context_engineering/)

---

### Tool Response Design

Structured tool responses that control output format for easier parsing, providing status, output files, metrics, warnings, and facets (metadata that helps agents make better decisions). This is a practical application of context engineering principles around faceted tool responses—Level 4 faceted responses give agents peripheral vision about task completion, enabling better follow-up decisions.

[See: Context Engineering: Rapid Agent Prototyping](https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/)

Context Engineering is specifically about designing tool responses and interaction patterns that give agents situational awareness to navigate complex information spaces effectively. Agents are persistent, make multiple tool calls, and build understanding across conversations. They don't just need the right chunk—they need to understand the landscape of available information.

[See: Context Engineering Series for Agentic RAG Systems](https://jxnl.co/writing/2025/08/28/context-engineering-index)

#### Levels of Tool Response Quality

**Level 1 - Minimal Chunks (No Metadata):** Basic tool responses returning only raw text content without source information or metadata. The limitation: without metadata, agents can't make strategic decisions about where to search next—they're flying blind.

**Level 2 - Chunks with Basic Source Metadata:** Returns chunks with source files, page numbers, and chunk content. Enables citations and reveals document clustering patterns. The breakthrough: agents now see when multiple chunks come from the same source and can strategically load full pages instead of piecing together fragments. Includes system instructions teaching agents that "multiple chunks from same source = use load_pages() instead of fragments."

**Level 3 - Multi-Modal Content Representation:** Modern documents contain tables, charts, diagrams, code blocks, and structured content. This level provides appropriate representations for different content modalities. Simple tables return as Markdown for easy data work; complex tables with merged cells return as HTML to preserve relationships; images include both visual content and searchable OCR text. Agents can filter by content_types like ["text", "table", "image", "code"].

**Level 4 - Facets and Query Refinement:** Introduces aggregated metadata helping agents understand the data landscape and refine queries iteratively, like users do on e-commerce sites. Think e-commerce: search "running shoes" → get results + facets (Nike: 45, Adidas: 32, 4-star: 28, 5-star: 12). Agents already understand this pattern from coding—when grep shows file distribution counts, agents recognize that files with highest occurrence counts deserve full attention rather than reading disconnected snippets.

[See: Beyond Chunks: Why Context Engineering is the Future of RAG](https://jxnl.co/writing/2025/08/27/facets-context-engineering/)

#### Faceted Search and Agent Peripheral Vision

Faceted Search exposes metadata aggregations (counts, categories, filters) alongside search results to reveal the data landscape. Agent Peripheral Vision provides agents with structured metadata about the broader information space beyond just the top-k results.

[See: Context Engineering Series for Agentic RAG Systems](https://jxnl.co/writing/2025/08/28/context-engineering-index)

Faceted search is exactly this: aggregate counts reveal which documents deserve complete context rather than fragmented chunks. When searching "API timeout issues," facets reveal the complete landscape—all 3 returned tickets are "Done" but facets show 5 "Open" tickets exist. Resolved tickets have better documentation and rank higher in similarity search, while active issues get filtered out (similarity bias alert).

[See: Beyond Chunks: Why Context Engineering is the Future of RAG](https://jxnl.co/writing/2025/08/27/facets-context-engineering/)

**Agent Persistence as Paradigm Shift:** Agentic systems are incredibly persistent. Given enough budget and time, they'll keep searching until they find what they need. Traditional RAG optimized for humans who make one query and expect comprehensive results, creating "stuff everything relevant into the first response" mentality that led to context window bloat and degraded performance. Agents operate differently—they're methodical, systematic, and don't get frustrated. Show them a facet indicating 47 relevant documents in a category they haven't explored? They'll investigate. The strategic implication: you don't need perfect recall on query #1. You need to give agents enough context about the information landscape that they can systematically traverse it.

[See: Beyond Chunks: Why Context Engineering is the Future of RAG](https://jxnl.co/writing/2025/08/27/facets-context-engineering/)

#### Tool Response as Prompt Engineering

Tool Response as Prompt Engineering uses XML structure, metadata, and system instructions in tool outputs to guide future agent behavior. The metadata became prompt engineering itself. Structured tool responses weren't just returning data—they were teaching agents how to think about the data.

[See: Context Engineering Series for Agentic RAG Systems](https://jxnl.co/writing/2025/08/28/context-engineering-index)

Think of tool descriptions as prompt engineering for your agents (from Anthropic's tool development guide). How you name functions, structure parameters, and format responses directly influences agent reasoning patterns. Clear tool boundaries and meaningful parameter names reduce confusion and hallucinations.

[See: Beyond Chunks: Why Context Engineering is the Future of RAG](https://jxnl.co/writing/2025/08/27/facets-context-engineering/)

Token efficiency insight from Anthropic: tool responses should prioritize contextual relevance over flexibility. Return high-signal information that directly informs downstream actions, not low-level technical identifiers.

[See: Beyond Chunks: Why Context Engineering is the Future of RAG](https://jxnl.co/writing/2025/08/27/facets-context-engineering/)

---

### Progressive Disclosure

Models excel at navigating filesystems. Presenting tools as code on a filesystem allows models to read tool definitions on-demand rather than loading everything upfront. Alternatively, a `search_tools` tool can be added to find relevant definitions (searching for "salesforce" loads only those tools). Including a detail level parameter (name only, name and description, or full definition with schemas) helps agents conserve context and find tools efficiently.

[See: Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)

Hyperlinks are woefully underutilized as a context engineering technique. When humans need to learn something (e.g., about an open source library), they Google search the topic, click a relevant link to a docs page, read a high-level guide, Cmd+Click a few more pages to open in new tabs to review, and refer between open tabs while completing the task. Once finding an entrypoint through search, they incrementally explore the topic through discovered links, filling mental context with relevant information. We can do the same thing with LLMs.

[See: Context engineering is sleeping on the humble hyperlink](https://mbleigh.dev/posts/context-engineering-with-links/)

Links are powerful in the context engineering toolbelt because of their simplicity, flexibility, and efficiency:
- **Trivial to implement:** Current models are "intuitively" good at understanding how to follow links
- **Surface anywhere:** Can be specified in system prompts, provided by users, or returned by tools
- **Token-efficient:** Use a small number of tokens to provide on-demand access to specific information
- **Tool-efficient:** Consolidate many types of reads into a single tool
- **Just-in-time context:** Mitigates issues of context rot and recency bias

[See: Context engineering is sleeping on the humble hyperlink](https://mbleigh.dev/posts/context-engineering-with-links/)

---

## Multi-Agent Architecture

### Single-Agent vs. Multi-Agent Considerations

This influential article by Walden Yan from Cognition (creators of Devin) argues against multi-agent architectures in favor of simpler, more reliable approaches. The core argument centers on context engineering—the dynamic, automatic management of context in AI agent systems.

**Two Fundamental Principles:**

1. **Share context, and share full agent traces, not just individual messages:** In multi-agent systems, subagents often work with incomplete context, leading to miscommunication. Full agent traces must be shared to prevent misunderstandings.

2. **Actions carry implicit decisions, and conflicting decisions carry bad results:** When parallel subagents cannot see each other's work, they make decisions based on conflicting assumptions.

[See: Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents)

**Recommended Architectures:**

1. **Single-threaded linear agent:** The simplest and most reliable approach where context is continuous. This gets you "very far" and should be the default choice.

2. **Context compression architecture (for advanced use cases):** For truly long-duration tasks, introduce a specialized LLM model whose purpose is compressing action history and conversation into key details, events, and decisions.

[See: Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents)

While optimistic about long-term possibilities, in 2025, multiple agents in collaboration only create fragile systems due to dispersed decision-making and insufficient context sharing. No one is currently solving the difficult cross-agent context-passing problem. This will "come for free" as single-threaded agents improve at communicating with humans, eventually unlocking parallelism and efficiency.

[See: Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents)

---

### Sub-Agents for Context Isolation

**Sub-Agent Architectures:** Specialized sub-agents handle focused tasks with clean context windows while the main agent coordinates with high-level plans. Subagents explore extensively but return condensed summaries (1,000-2,000 tokens), achieving clear separation of concerns.

[See: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Subagents are not about playing house and anthropomorphizing roles—**subagents are about context control**. The most common use case: let you use a fresh context window to do finding/searching/summarizing that enables the parent agent to get straight to work without clouding its context window with `Glob`/`Grep`/`Read` calls.

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

Subagents are separate AI helpers with their own instructions, tools, and memory. They're like having a team of workers where each worker does a messy job, then comes back with just the important results. This approach addresses a core challenge in multi-agent systems: maintaining context coherence while enabling specialization.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

#### When to Use Sub-Agents

Anthropic's multi-agent research system demonstrates this strategy excellently. They write: "The essence of search is compression: distilling insights from a vast corpus. Subagents facilitate compression by operating in parallel with their own context windows, exploring different aspects of the question simultaneously before condensing the most important tokens for the lead research agent. Each subagent also provides separation of concerns—distinct tools, prompts, and exploration trajectories—which reduces path dependency and enables thorough, independent investigations."

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

Research naturally lends itself to this pattern. When given a question, several subquestions can be separately prompted using multiple agents, speeding up information gathering and distillation while keeping each context from accruing too much or irrelevant information. Anthropic's internal evaluations showed multi-agent systems excel especially for breadth-first queries involving multiple independent directions simultaneously.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

This approach also helps with tool loadouts—designers can create several agent archetypes with dedicated loadouts and instructions. The challenge: finding opportunities for isolated tasks to spin out onto separate threads. Problems requiring context-sharing among multiple agents aren't particularly suited to this tactic.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

#### Sub-Agent Design Patterns

**What Subagents Can Do:** Your test runner subagent can: run all tests in ultra-verbose mode with full stack traces; use awk, grep, and python to parse gigabytes of application logs, database logs, and system logs; use Git to check when failing files last changed, including full commit diffs; correlate failures with PRs and read entire code review threads; read all the files at fault, their imports, and related modules to hypothesize root causes; analyze performance metrics and memory dumps. It might use 180,000 tokens in the process, but what comes back to your main AI is a short, clear summary.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

**Subagent Token Economics:** Main thread total is 21,000 tokens (16k clean + 2k summary + 3k continuing) while subagent burned 150,000 tokens off-thread, resulting in 76% signal context quality—8x cleaner main thread with same diagnostic capability. The mess stayed with the sidecar; only the useful stuff came back. Your main context remains tight and focused.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

**Read-Write Coordination Pattern:** Read operations can be massively parallel—multiple subagents can read files, run git operations, parse logs all simultaneously because they don't step on each other (they're just consuming information). Write operations need to be single-threaded—if multiple agents try to edit the same files, you get merge conflicts and broken state. The research happens in parallel, the implementation happens coordinated. The noise stays in the sidecars, the signal comes to main.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

---

### Context Quarantine

Isolating contexts in their own dedicated threads, each used separately by one or more LLMs. Breaking tasks into smaller, isolated jobs—each with their own context—yields better results.

[See: How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)

### Slash Commands vs. Sub-Agents

**The Core Problem:** Bad context is cheap but toxic. Loading 100,000 lines of test logs costs almost nothing computationally, but easily pollutes valuable context. A well-crafted 3,000-token feature spec gets destroyed when you dump Python outputs and error traces on top of it.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

**The Dramatic Difference:** Using Claude Code as an example with identical capability to find problems and identical results, slash commands use 169,000 tokens with 91% junk while subagents use only 21,000 tokens with 76% useful information—8x cleaner. This massive difference in context quality fundamentally changes what agents can accomplish reliably.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

**The Slash Command Path:** When you need to run tests, the slash command triggers a prompt that puts test results directly into the same conversation. Your clean 5,000-word plan gets flooded with 150,000 words of test logs—your AI's memory is suddenly 95% junk. This is the well-documented phenomenon of context rot where AI performance degrades as input length increases.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

**The Subagent Path:** Instead of using a slash command, you create a Test Runner helper. The test runner subagent might use 180,000 tokens in the process, reading huge log files, parsing long error traces, and checking hundreds of code files. But what comes back to your main AI is a short, clear summary. The mess stayed with the sidecar; only the useful stuff came back.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

**Claude Code Implementation Details:** Slash commands are just prompt injection—when you type /run-tests, Claude Code literally injects that long prompt into your main thread. Subagents are separate workers—Claude Code spawns them with their own context windows and tool access. They go off, do the work, burn 150k tokens parsing logs, and come back with just the insights. The brilliance is in what gets isolated vs. what gets shared.

[See: Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)

---

## Agent Workflows and Form Factors

### The Three Agent Approaches

When companies say they want to build agents, the focus should be on practical outcomes: What specific functionality do you need? What business value are you trying to create? Choose one of these three approaches first, as all other technical decisions—tool design, prompts, data processing, orchestration—depend on this choice.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Conversation Interface (Chatbots)

A chat interface that can access tools and APIs where a human oversees the conversation while the system suggests actions. Success means users get connected to the right functionality and can complete their tasks. Focus on tool integration, fast response times, and helping users find what they need quickly.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Side-Effect Engine (Workflows)

Automated workflow execution triggered by events with no user interface needed—contracts get sent, invoices get processed, tickets get updated. Success is measured by completion rate, accuracy, and processing time. The user experience is the audit trail showing what happened.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Research Artifact (Reports & Tables)

Produces structured outputs like reports, summaries, or data tables. The system generates documents that follow a consistent format and meet quality standards. Success means the output is accurate, well-formatted, and ready to use in business contexts.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

**Critical Guidance:** Don't try to build a chatbot that should be a workflow, or force a report generator to be conversational. Once you know what you're building, focus on two key areas: 1) Clear tool design—your system is limited by the tools you provide; 2) Testing setup—test your concept quickly before building complex systems.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

---

### The Autonomy Spectrum

When leadership hears "agent," they imagine fully autonomous systems. That's not what works in practice. Successful systems follow a spectrum of increasing autonomy. This progression gives you a clear upgrade path—you don't need to start with the most complex option. Begin with deterministic code, add AI functions where you need flexibility, use chains when tasks have multiple steps, upgrade to graphs when workflows branch, and save the tool-calling loop for cases that truly need improvisation.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Deterministic Systems

Use traditional programming with if/else logic and clear rules. When inputs are predictable and tasks have one correct solution, code is cheaper, faster, and more reliable than AI. Use this approach when requirements are stable and inputs vary little.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### AI Functions

You control the workflow completely. Call the LLM like any other function: pass in data, get structured output back. Extract action items from transcripts, normalize addresses, classify documents. Test it like any dependency. No loops or complex logic—just a single AI call per task. Why it works: Real-world data is messy, and these functions clean it up so your code can handle it reliably.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Prompt Chains

Chain multiple AI calls together when tasks need several steps: draft, then critique, then revise; or extract, then verify, then summarize. You still control the order completely. The AI handles each step, but you decide what comes next and when to stop. Common mistake: Using chains for simple tasks that need only one AI call, or for complex tasks that need branching logic.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Graph State Machines

Here the workflow has multiple paths. You define specific states and transitions between them. The AI helps choose which path to take when the data isn't clear. For example: intake leads to triage, which leads to one of three different workflows, each with its own ending conditions. Key difference: You recognize that requests are different and need different handling. You track the current state clearly instead of hiding it in prompts.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Tool-Calling Loops

This is the classic "agent": a loop where the AI suggests an action, you execute it with a tool, add the result back to the conversation, and repeat until the task is complete. It's powerful but expensive and easy to get wrong. Use this for unusual cases that can't be handled with fixed workflows. How to control it: Put the steps in your system prompt, tool descriptions, and error messages. Set clear end conditions. Limit the number of tool calls. Track the cost.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

**Composability:** Every level is a tool for higher levels. A deterministic script becomes a tool for an AI function. An AI function becomes a tool for a prompt chain. A complete prompt chain becomes a tool for a graph state machine. Even an entire tool-calling agent can be a single tool in a larger orchestration system. This creates an architecture where simple, reliable components compose into more complex systems.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

---

## Context Engineering for Coding Agents

### Onboarding for Coding Agents

Think of context as onboarding for both human teammates and AI tools. Ask yourself: if a new software engineer or designer joined this project tomorrow, what would you want them to read before they start on their first task? That's the type of context you should put in READMEs. The crucial realization: every new Cursor or Claude Code session is like a new teammate joining the project with zero context. If you don't first get them up to speed, how will they do a good job on the tasks you give them?

[See: Onboarding for coding agents](https://www.fuzzycomputer.com/posts/onboarding)

The author reduced their CLAUDE.md file from hundreds of lines to just 13 by following two principles: (1) Put context in READMEs (universal and tool-agnostic), and (2) Put constraints in the environment via tools (type checkers, linters, formatters, tests).

[See: Onboarding for coding agents](https://www.fuzzycomputer.com/posts/onboarding)

**Put Context in READMEs:** READMEs have worked well for 50 years as a universal, tool-agnostic format for project context. Instead of cramming everything into one long README, use a simple naming convention to create composable context for different domains:
- `README.md` - High-level overview
- `README.architecture.md` - App structure, key architectural decisions
- `README.commands.md` - Key development commands and scripts
- `README.design.md` - Design system, components, visual guidelines
- `README.testing.md` - Testing patterns and strategies

[See: Onboarding for coding agents](https://www.fuzzycomputer.com/posts/onboarding)

---

### Quality Gates and Constraints

**Quality Gates (Constraints in the Environment):** The goal is to encode as many constraints as possible in the environment, via tools rather than prompts. These "Quality Gates" are whatever checks you'd want to run before a new engineer pushes to production. Example: When writing code, Claude must not finish until all of these succeed: type-check, format, lint, all unit tests pass. If any check fails, fix the issues and run checks again.

[See: Onboarding for coding agents](https://www.fuzzycomputer.com/posts/onboarding)

This works well because LLMs are terrible at formatting whitespace, sorting imports, or ensuring dependency arrays are correct. But they're good at running tools and fixing errors until all checks pass. The specific gates depend on your stack—ESLint/Prettier in TypeScript, ruff/pytest in Python, or go fmt/vet/test in Go.

[See: Onboarding for coding agents](https://www.fuzzycomputer.com/posts/onboarding)

### The OODA Loop for Agents

Why does the Quality Gates pattern suddenly work so well? Newer models (like Sonnet 4) and tools (like Claude Code) mean coding agents can now iterate for minutes or even hours until all specified constraints pass. This represents a deeper shift: coding agents can now run their own OODA loop (Observe, Orient, Decide, Act). Instead of just executing instructions or predicting tokens, they can observe outcomes and adapt to feedback from their environment.

[See: Onboarding for coding agents](https://www.fuzzycomputer.com/posts/onboarding)

### Frequent Intentional Compaction

The team has gotten Claude Code to handle 300K LOC Rust codebases, ship a week's worth of work in a day, and maintain code quality that passes expert review. They use a family of techniques called "frequent intentional compaction"—deliberately structuring how you feed context to the AI throughout the development process, keeping utilization in the 40%-60% range (depends on problem complexity).

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

Split into three (ish) steps (sometimes skip research and go straight to planning; sometimes do multiple passes of compacted research before implementing):

#### Research Phase

Understand the codebase, files relevant to the issue, how information flows, and perhaps potential causes of a problem. This is the only step that needs context from the codebase itself. Research phase results get compacted into structured artifacts that subsequent phases can reference.

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

#### Planning Phase

Outline the exact steps to fix the issue, and the files you'll need to edit and how, being super precise about testing/verification steps in each phase. The plan becomes the source of truth for what's being built and why. Plans differed significantly when built with vs without research—both "would have worked" but the one built with research fixed the problem in the *best* place and prescribed testing in line with codebase conventions.

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

#### Implementation Phase

Step through the plan, phase by phase. For complex work, often compact the current status back into the original plan file after each implementation phase is verified. This is the only step that needs to be done in a worktree; everything else happens on main.

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

### Mental Alignment and Code Review

A bad line of code is just a bad line of code. But a bad line of a **plan** could lead to hundreds of bad lines of code. And a bad line of **research**, a misunderstanding of how the codebase works or where certain functionality is located, could land you with thousands of bad lines of code. So you want to **focus human effort and attention** on the HIGHEST LEVERAGE parts of the pipeline. When you review research and plans, you get more leverage than when you review code.

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

The most important part of code review is mental alignment—keeping team members on the same page as to how the code is changing and why. A guaranteed side effect of everyone shipping way more code is that a much larger proportion of your codebase will be unfamiliar to any given engineer at any point in time. For most teams, this is pull requests and internal docs. For this team, it's now specs, plans, and research. The author can't read 2000 lines of golang daily, but *can* read 200 lines of a well-written implementation plan.

[See: Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

---

## Advanced Topics

### Model Context Protocol (MCP)

#### What is MCP

Since launching in November 2024, the community has built thousands of MCP servers, SDKs are available for all major programming languages, and the industry has adopted MCP as the de-facto standard for connecting agents to tools and data.

[See: Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)

MCP (Model Context Protocol) is a protocol for reusable tools across clients; best when reuse and client diversity justify the overhead.

[See: Context Engineering Series for Agentic RAG Systems](https://jxnl.co/writing/2025/08/28/context-engineering-index)

#### When to Use MCP

**MCP Decision Factors:** The decision is straightforward: If your team already uses Claude Enterprise (which includes Google Drive, Atlassian, and calendar integrations), then adding four more APIs via MCP makes sense—you're extending an existing system, not building from scratch. But if your team is using Ruby, or you're in an environment where MCP client libraries don't exist or are immature, you might spend more time on protocol plumbing than on the actual business logic.

Four concrete factors: 1) **Client diversity**—are you serving multiple agent platforms, or just one application? 2) **Team standardization**—does your organization already have MCP infrastructure, or are you starting from scratch? 3) **Tool complexity**—are your tools simple CRUD operations, or do they involve complex authentication and state management? 4) **Headcount allocation**—do you want to spend engineering time on protocol compliance, or on business logic?

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

MCP servers make sense when you need the same tools across multiple applications. If your team uses Claude Desktop, ChatGPT, and other AI platforms that all need Google Drive integration, an MCP server lets you build once and reuse everywhere. However, MCP adds complexity—you're building protocol adapters, managing authentication across clients, and debugging connection issues. If you have tools that only one application will use, MCP is probably overkill. Direct API calls with the OpenAI SDK will be faster to implement.

[See: Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)

#### Code Execution with MCP

Present MCP servers as code APIs rather than direct tool calls. The agent writes code to interact with MCP servers. This addresses both challenges: agents load only the tools they need and process data in the execution environment before passing results back to the model.

[See: Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)

The Google Drive to Salesforce example reduces token usage from 150,000 tokens to 2,000 tokens—a time and cost saving of 98.7%. The core insight: LLMs are adept at writing code, and developers should take advantage of this strength to build agents that interact with MCP servers more efficiently.

[See: Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)

**Benefits:**
1. **Progressive Disclosure:** Models read tool definitions on-demand rather than loading everything upfront
2. **Context Efficient Tool Results:** Agents filter and transform results in code before returning them
3. **More Powerful Control Flow:** Loops, conditionals, and error handling use familiar code patterns
4. **Privacy-Preserving Operations:** Intermediate results stay in the execution environment by default
5. **State Persistence and Skills:** Agents can write intermediate results to files and persist code as reusable functions

[See: Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)

---

### Memory and Long-Term Context

#### Memory Tool

The memory tool (`memory_20250818`) enables cross-conversation learning where Claude can write down what it learns for future reference. The file-based system operates under a `/memories` directory with full client-side control. Commands include view, create, str_replace, insert, delete, and rename operations on memory files.

[See: Memory & Context Management with Claude Sonnet 4.5](https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb)

Agents get better at specific tasks over time: In Session 1, Claude solves a problem and writes down the pattern. In Session 2, Claude applies the learned pattern immediately (faster response). For long sessions, context editing keeps conversations manageable without losing critical learnings.

[See: Memory & Context Management with Claude Sonnet 4.5](https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb)

#### Cross-Conversation Learning

Claude stores architectural insights including symptoms, causes, solutions, and red flags. This knowledge applies cross-language and improves with each review. The key pattern demonstrates semantic pattern recognition, not just syntax. For example, after learning about race conditions in thread-based code (Session 1), Claude immediately recognizes similar patterns in async code (Session 2) without re-learning—applying stored knowledge about shared mutable state across different contexts.

[See: Memory & Context Management with Claude Sonnet 4.5](https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb)

During long review sessions, context fills with tool results from previous reviews, but memory must persist. Context editing triggers automatically when input tokens exceed thresholds, removing old tool results while keeping memory files intact. This demonstrates the critical distinction:
- **Short-term memory** (conversation context with tool results) → Cleared to save space
- **Long-term memory** (stored patterns in `/memories`) → Persists across sessions

[See: Memory & Context Management with Claude Sonnet 4.5](https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb)

### Context Observability

Context observability is about measuring which inputs consistently improve output and which context leads to hallucination. Most teams fly blind without systematic ways to measure which context helps vs hurts model performance. Critical missing infrastructure: What inputs improved/worsened output quality? How do you test context like you test model prompts?

[See: What Makes 5% of AI Agents Actually Work in Production?](https://www.motivenotes.ai/p/what-makes-5-of-ai-agents-actually)

Context can become diluted or inefficient (filled with stale and irrelevant information), requiring special evaluation workflows. The guide emphasizes that context engineering is an evolving skill set for AI developers/engineers with opportunities to build automation tools for effective context engineering.

[See: Context Engineering Guide](https://www.promptingguide.ai/guides/context-engineering-guide)

---

### Agent Prototyping and Testing

#### Rapid Prototyping Methodology

Most teams waste months building agent frameworks before knowing if their idea actually works. There's a faster way: use Claude Code (or similar coding agents) as your testing harness to validate agent concepts without writing orchestration code. If Claude Code can't achieve your task with perfect tool access and no UI constraints, your production version likely won't either. But if you can get one passing test, you've proven the concept and can invest in hardening with confidence.

[See: Context Engineering: Rapid Agent Prototyping](https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/)

The rapid prototyping methodology uses Claude Code's project runner mode (`claude -p`) that turns any directory into an agent execution environment. It reads a CLAUDE.md file as system instructions and executes workflows using CLI tools you provide. This creates a perfect testing harness—you write instructions in English, expose tools as simple commands, and let Claude Code handle the execution loop.

[See: Context Engineering: Rapid Agent Prototyping](https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/)

#### Test-Driven Agent Development

Before writing orchestration code, implement:
1. **Define success criteria**—what concrete output proves the agent works?
2. **Identify 3-6 core tools** that would make the task possible
3. **Create 5-10 test scenarios** with real-world inputs
4. **Write CLAUDE.md** with clear execution flow
5. **Build simple CLI tool wrappers** for your APIs
6. **Execute test scenarios** and iterate on instructions/tools
7. **Achieve at least one passing test** before considering production architecture

[See: Context Engineering: Rapid Agent Prototyping](https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/)

Each test folder represents a real scenario with concrete pass/fail criteria. Validation scripts (e.g., `check.py`) verify output file existence and validate structure using assertions. This provides binary success metrics—either output meets specification or it doesn't, with no subjective evaluation.

[See: Context Engineering: Rapid Agent Prototyping](https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/)

---

## Production Considerations

### Cost Optimization

#### Prompt Caching

With Claude's prompt caching, cached tokens cost $0.30/MTok versus $3/MTok uncached—a 10x difference. Keep prompt prefixes stable, make context append-only, use deterministic serialization, and mark cache breakpoints explicitly.

[See: Context Engineering - The Evolution Beyond Prompt Engineering](https://www.vincirufus.com/posts/context-engineering/)

For knowledge bases smaller than 200,000 tokens (about 500 pages), developers can include the entire knowledge base directly in the prompt, especially with prompt caching which reduces latency by >2x and costs by up to 90%.

[See: Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)

#### Input-Output Ratio Management

For developers, focusing on input optimization is a critical lever for: **Controlling costs** (since input represents 98%+ of token costs, input optimization has 50× more impact than output optimization), **Reducing latency** (processing time is dominated by input token count), and **Building successful AI-powered products** (efficient context engineering is the core engineering challenge).

[See: The Hungry, Hungry AI Model](https://tomtunguz.com/input-output-ratio/)

### Latency Considerations

An important factor determining how long a user waits for an answer is the time it takes the model to process the input. Since input tokens dominate the token count, reducing input size directly improves response time. Context engineering for latency optimization means minimizing the input token footprint while maintaining answer quality.

[See: The Hungry, Hungry AI Model](https://tomtunguz.com/input-output-ratio/)

### Security and Privacy

#### Privacy-Preserving Operations

When agents use code execution with MCP, intermediate results stay in the execution environment by default. The agent only sees what's explicitly logged or returned, meaning data you don't wish to share with the model can flow through workflows without entering the model's context. For even more sensitive workloads, the agent harness can tokenize sensitive data automatically. Real data flows from source to destination but never through the model. This prevents the agent from accidentally logging or processing sensitive data and enables deterministic security rules about where data can flow.

[See: Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)

#### Governance and Trust

Security, lineage, and permissioning are deployment blockers. Key requirements: trace which inputs led to which outputs (lineage), respect row-level, role-based access (policy gating), and allow user-specific output even if prompts are identical. "If two employees ask the same question, the model output should differ because they have different permissions." Without these controls, agents may be functionally right but organizationally wrong, leaking access or violating compliance.

[See: What Makes 5% of AI Agents Actually Work in Production?](https://www.motivenotes.ai/p/what-makes-5-of-ai-agents-actually)

The trust problem is human, not technical. The successful 5% of AI agents all have human-in-the-loop design, positioning AI as assistant, not autonomous decision maker, with feedback loops where systems learn from corrections and easy verification/override mechanisms.

[See: What Makes 5% of AI Agents Actually Work in Production?](https://www.motivenotes.ai/p/what-makes-5-of-ai-agents-actually)

### Evaluation and Monitoring

The goal is optimizing information provided in the context window while systematically measuring LLM performance. From a developer's perspective, context engineering involves an iterative process with formal evaluation pipelines to measure whether tactics are working.

[See: Context Engineering Guide](https://www.promptingguide.ai/guides/context-engineering-guide)

**Performance Improvements with Context Management:** On an internal evaluation set for agentic search, testing showed how context management improves agent performance on complex, multi-step tasks. Combining the memory tool with context editing improved performance by 39% over baseline. Context editing alone delivered a 29% improvement. In a 100-turn web search evaluation, context editing enabled agents to complete workflows that would otherwise fail due to context exhaustion—while reducing token consumption by 84%.

[See: Managing context on the Claude Developer Platform](https://www.anthropic.com/news/context-management)

---

## Resources and Further Learning

**Anthropic Resources:**
- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Introducing Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval)
- [Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)
- [Managing context on the Claude Developer Platform](https://www.anthropic.com/news/context-management)
- [Context windows documentation](https://docs.anthropic.com/en/docs/build-with-claude/context-windows)
- [Anthropic Academy - Build with Claude](https://www.anthropic.com/learn/build-with-claude)
- [Memory & Context Management Cookbook](https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb)
- [Retrieval Augmented Generation with Contextual Embeddings](https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings)

**Foundational Guides:**
- [Context Engineering Guide (DAIR.AI)](https://www.promptingguide.ai/guides/context-engineering-guide)
- [The New Skill in AI is Not Prompting, It's Context Engineering](https://www.philschmid.de/context-engineering)
- [Context Engineering: Going Beyond Prompts To Push AI](https://simple.ai/p/the-skill-thats-replacing-prompt-engineering)
- [Context Engineering - The Evolution Beyond Prompt Engineering](https://www.vincirufus.com/posts/context-engineering/)
- [How to Manage Context in AI Coding](https://refactoring.fm/p/managing-context-for-ai-coding)

**Context Engineering Series by Jason Liu:**
- [Context Engineering Series for Agentic RAG Systems (Index)](https://jxnl.co/writing/2025/08/28/context-engineering-index)
- [Beyond Chunks: Why Context Engineering is the Future of RAG](https://jxnl.co/writing/2025/08/27/facets-context-engineering/)
- [Slash Commands vs Subagents: How to Keep AI Tools Focused](https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/)
- [Two Experiments We Need to Run on AI Agent Compaction](https://jxnl.co/writing/2025/08/30/context-engineering-compaction/)
- [Context Engineering: Agent Frameworks and Form Factors](https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/)
- [Context Engineering: Rapid Agent Prototyping](https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/)

**Context Failure Modes & Solutions:**
- [How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)
- [How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html)
- [Context Rot: How Increasing Input Tokens Impacts LLM Performance](https://research.trychroma.com/context-rot)

**Agent Architecture:**
- [Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents)
- [Context Engineering for Agents](https://rlancemartin.github.io/2025/06/23/context_engineering/)
- [12-Factor Agents - Principles for building reliable LLM applications](https://github.com/humanlayer/12-factor-agents)
- [The rise of "context engineering"](https://blog.langchain.com/the-rise-of-context-engineering/)
- [What Makes 5% of AI Agents Actually Work in Production?](https://www.motivenotes.ai/p/what-makes-5-of-ai-agents-actually)

**RAG & Retrieval:**
- [Retrieval Augmented Generation (RAG)](https://www.promptingguide.ai/techniques/rag)
- [Long Context vs. RAG for LLMs: An Evaluation and Revisits](https://arxiv.org/abs/2501.01880)
- [Advanced RAG Techniques Repository](https://github.com/NirDiamant/RAG_Techniques)
- [Production RAG: what I learned from processing 5M+ documents](https://blog.abdellatif.io/production-rag-processing-5m-documents)
- [Context engineering is sleeping on the humble hyperlink](https://mbleigh.dev/posts/context-engineering-with-links/)

**Coding Agents:**
- [Getting AI to Work in Complex Codebases](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)
- [Onboarding for coding agents](https://www.fuzzycomputer.com/posts/onboarding)

**Economics & Metrics:**
- [The Hungry, Hungry AI Model](https://tomtunguz.com/input-output-ratio/)
- [Token Calculator for LLMs](https://token-calculator.net/)

---

# End of Guide Outline

This comprehensive outline covers all major aspects of Context Engineering, from foundational concepts through advanced techniques and production considerations. Each section includes content from both the Braindumpnotes.md file and relevant summaries from ResourceSummaries.md, with proper citations to source materials.

The outline is structured to support a beginner-to-advanced learning path, starting with "What is Context Engineering" and progressing through increasingly sophisticated techniques including RAG, tool design, multi-agent architectures, and production deployment strategies.

