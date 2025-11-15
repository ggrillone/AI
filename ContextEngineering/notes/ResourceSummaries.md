# Context Engineering Resource Summaries

## Resources to Process:

All resources have been processed!

---

## Resources that have already been processed:

1. https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
2. https://research.trychroma.com/context-rot
3. https://token-calculator.net/
4. https://docs.anthropic.com/en/docs/build-with-claude/context-windows
5. https://www.promptingguide.ai/guides/context-engineering-guide
6. https://cognition.ai/blog/dont-build-multi-agents
7. https://rlancemartin.github.io/2025/06/23/context_engineering/
8. https://www.philschmid.de/context-engineering
9. https://simple.ai/p/the-skill-thats-replacing-prompt-engineering
10. https://github.com/humanlayer/12-factor-agents
11. https://blog.langchain.com/the-rise-of-context-engineering/
12. https://www.promptingguide.ai/techniques/rag
13. https://arxiv.org/abs/2501.01880
14. https://www.anthropic.com/learn/build-with-claude
15. https://github.com/NirDiamant/RAG_Techniques
16. https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html
17. https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html
18. https://www.fuzzycomputer.com/posts/onboarding
19. https://tomtunguz.com/input-output-ratio/
20. https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
21. https://www.vincirufus.com/posts/context-engineering/
22. https://www.motivenotes.ai/p/what-makes-5-of-ai-agents-actually
23. https://mbleigh.dev/posts/context-engineering-with-links/
24. https://blog.abdellatif.io/production-rag-processing-5m-documents
25. https://www.anthropic.com/news/context-management
26. https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb
27. https://jxnl.co/writing/2025/08/28/context-engineering-index
28. https://www.anthropic.com/engineering/contextual-retrieval
29. https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings
30. https://www.anthropic.com/engineering/code-execution-with-mcp
31. https://refactoring.fm/p/managing-context-for-ai-coding
32. https://jxnl.co/writing/2025/08/27/facets-context-engineering/
33. https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/
34. https://jxnl.co/writing/2025/08/30/context-engineering-compaction/
35. https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/
36. https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/
37. https://blog.langchain.com/context-engineering-for-agents/
38. https://mariozechner.at/posts/2025-06-02-prompts-are-code/

---

## Processed Articles and Summaries:

Title: Effective context engineering for AI agents
Tags: agents, attention budget, compaction, context engineering, context retrieval, just-in-time, memory, multi-agent, prompt engineering, sub-agents, tools
URL: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
<br/>
Summary:<br/>
See notes: This article addresses what context engineering is, the problems it solves, how it differs from prompt engineering, and discusses "just in time" context strategies.

Context engineering is the natural progression from prompt engineering, focusing on curating and maintaining the optimal set of tokens during LLM inference rather than just writing effective prompts. Context refers to all information available to the model at inference time (system prompts, tools, Model Context Protocol, external data, message history, etc.). As agents operate over multiple turns and longer time horizons, managing this entire context state becomes critical.

The article explains that context must be treated as a finite resource due to "context rot"—as token count increases in the context window, the model's ability to accurately recall information decreases. This stems from the transformer architecture where every token attends to every other token (n² pairwise relationships), creating attention scarcity. LLMs have an "attention budget" that depletes with each new token, similar to human working memory limitations.

Effective context engineering means finding the smallest possible set of high-signal tokens that maximize the likelihood of desired outcomes. Key principles include:

**System Prompts:** Should be clear, direct, and at the right "altitude"—specific enough to guide behavior but flexible enough to avoid brittle, hardcoded logic. Organize into distinct sections using XML tags or Markdown headers. Start minimal and add based on failure modes.

**Tools:** Should be token-efficient, well-understood, self-contained, and have minimal functionality overlap. Avoid bloated tool sets that create ambiguous decision points. If humans can't definitively determine which tool to use, agents can't either.

**Context Retrieval and Agentic Search:** Rather than pre-processing all relevant data upfront, the "just in time" approach maintains lightweight identifiers (file paths, stored queries, web links) and uses tools to dynamically load data at runtime. This mirrors human cognition—we use indexing systems rather than memorizing entire corpuses. Metadata (folder hierarchies, naming conventions, timestamps) provides important signals for understanding when to utilize information.

**Long-Horizon Tasks:** For tasks exceeding context window limits, three specialized techniques address context pollution:
1. **Compaction:** Summarizing conversation contents nearing context limits and reinitiating with the summary. Tool result clearing is a lightweight form—once a tool is called deep in message history, the raw result is cleared.
2. **Structured Note-Taking (Agentic Memory):** Agents regularly write notes persisted outside the context window, pulled back in at later times. Provides persistent memory with minimal overhead.
3. **Sub-Agent Architectures:** Specialized sub-agents handle focused tasks with clean context windows while the main agent coordinates with high-level plans. Subagents explore extensively but return condensed summaries (1,000-2,000 tokens), achieving clear separation of concerns.

The hybrid strategy combines retrieval of some data upfront for speed with autonomous exploration at the agent's discretion. The optimal level of autonomy depends on the task. As models improve, the trend moves toward letting intelligent models act intelligently with progressively less human curation.

---

Title: Context Rot: How Increasing Input Tokens Impacts LLM Performance
Tags: attention budget, context rot, context windows, distractors, embeddings, haystack structure, LLM performance, long-context, needle-in-a-haystack, retrieval
URL: https://research.trychroma.com/context-rot
<br/>
Summary:<br/>
See notes: Important awareness that a larger context window does not necessarily mean you can use a single chat longer.

This comprehensive Chroma technical report evaluates 18 LLMs (including GPT-4.1, Claude 4, Gemini 2.5, Qwen3) to investigate "context rot"—the phenomenon where model performance becomes increasingly unreliable as input length grows. The research challenges the common assumption that models process context uniformly, showing that the 10,000th token is not handled as reliably as the 100th token.

**Key Finding:** Models do not use their context uniformly; performance degrades significantly as input length increases, even on intentionally simple tasks. While models achieve near-perfect scores on standard benchmarks like Needle in a Haystack (NIAH), these tests primarily assess direct lexical matching and may not represent flexible, semantically-oriented real-world tasks.

**Extended NIAH Experiments:**

1. **Needle-Question Similarity:** Performance degrades more quickly with lower similarity needle-question pairs. At short input lengths, models perform well even on low-similarity pairs, but longer inputs cause significant degradation. This isn't due to intrinsic difficulty—holding the needle-question pair constant while varying irrelevant content isolates input size as the primary factor.

2. **Impact of Distractors:** Distractors (topically related content that doesn't answer the question) have non-uniform impact that amplifies as input length grows. Even a single distractor reduces performance relative to baseline, and four distractors compound degradation further. Model families show distinct behaviors: Claude models are conservative and abstain when uncertain; GPT models show highest hallucination rates, generating confident but incorrect responses.

3. **Needle-Haystack Similarity:** When needles blend semantically with haystack content, model performance is affected non-uniformly. Testing PG essays vs. arXiv papers revealed that models perform better when needles don't blend with haystacks, though results vary by topic combination.

4. **Haystack Structure:** Surprisingly, structural coherence consistently hurts performance. Models perform better on shuffled haystacks (randomly reordered sentences) than on logically structured ones. This counterintuitive finding suggests structural patterns influence attention mechanisms, particularly as input length increases.

**LongMemEval Results:** Using conversational question-answering tasks (~113k tokens), researchers compared "focused" inputs (only relevant parts, ~300 tokens) versus "full" inputs (includes irrelevant context). All models showed significantly higher performance on focused prompts. Adding irrelevant context forces models to perform two tasks simultaneously—retrieval plus reasoning—rather than just reasoning, causing substantial performance degradation.

**Repeated Words Task:** Testing models' ability to replicate sequences of repeated words with a single unique word inserted revealed:
- Performance consistently degrades as context length (both input and output) increases
- Position accuracy is highest when unique words appear near the beginning
- Models often generate random words not present in input, typically starting around 500-750 words
- Different model families show distinct failure patterns (refusals, over-generation, under-generation)

**Implications:** Real-world applications involve far greater complexity than these simple controlled tasks, implying that input length impact may be even more pronounced in practice. This highlights the critical importance of context engineering—the careful construction and management of a model's context window. Where and how information is presented strongly influences task performance, not just whether information is present.

---

Title: Token Calculator for LLMs
Tags: cost estimation, input tokens, LLM pricing, output tokens, token calculator, tokens
URL: https://token-calculator.net/
<br/>
Summary:<br/>
See notes: Used to show cost differences between input and output tokens. Not a reliable way to estimate input tokens (and definitely can't estimate output tokens) because the agent can look at code files you didn't specify and you can't predict caching it will use.

This is an online utility tool that calculates the number of tokens in text for various Large Language Models (LLMs) including OpenAI GPT, Anthropic Claude, and Google Gemini models. The calculator provides real-time token counting along with word count, character count (with and without spaces), and most importantly, cost estimation across different model providers.

**Key Features:**
- Real-time token calculation as you type or paste text
- Comprehensive pricing comparison showing costs per 1M tokens for input, cached input (where applicable), and output tokens
- Context window information for each model
- Multiple LLM providers: OpenAI/Azure, Anthropic, and Google

**Pricing Structure Insights:**
The tool clearly demonstrates that output tokens cost significantly more than input tokens across all providers. For example:
- GPT-4.1: Input $2/1M tokens, Output $8/1M tokens (4x more expensive)
- Claude Opus 4: Input $15/1M tokens, Output $75/1M tokens (5x more expensive)
- Claude Sonnet 4: Input $3/1M tokens, Output $15/1M tokens (5x more expensive)
- Gemini 2.5 Pro: Input $1.25/1M tokens, Output $10/1M tokens (8x more expensive)

Some models like OpenAI's GPT-4.1 and GPT-4.1 mini also show cached input pricing at significantly reduced rates ($0.5/1M and $0.1/1M respectively), demonstrating the cost benefits of prompt caching.

**Calculated Metrics:**
- Token count (model-specific tokenization)
- Word count
- Character count (excluding spaces)
- Total character count
- Cost breakdown by input/cached input/output for each model

**Limitations for Context Engineering:**
As noted, this calculator has practical limitations for real agent workflows. It cannot predict:
1. Which additional files the agent might access beyond those explicitly specified
2. Cache hit rates and which portions of context will benefit from caching
3. Actual output token counts, which vary based on agent behavior and task complexity
4. Tool call overhead and multiple inference rounds in agentic workflows

The tool is useful for understanding the cost structure and relative pricing differences between input and output tokens, which informs decisions about what to include in prompts (chat output + code generated = output tokens). Being concise in output requirements (e.g., bullet points vs. verbose explanations) can meaningfully reduce costs.

---

Title: Context windows
Tags: context awareness, context windows, extended thinking, LLM capacity, tool use, token budget, token counting, working memory
URL: https://docs.anthropic.com/en/docs/build-with-claude/context-windows
<br/>
Summary:<br/>
See notes: Understanding context windows, the practical limit to how much information a model can consider at once, working memory, and how prompts + AI response + other information fit into the context window.

This Anthropic documentation provides comprehensive technical guidance on understanding and managing context windows in Claude models. The context window represents the "working memory" for language models—the entirety of text a model can look back on and reference when generating new text, distinct from the training data corpus.

**Understanding Standard Context Window Behavior:**
The context window operates with progressive token accumulation where each user message and assistant response accumulates within the window. Previous turns are preserved completely, creating linear growth with each turn. Claude models have a 200K token capacity (200,000 tokens) representing the maximum capacity for conversation history and generating new output. Each turn consists of an input phase (all previous conversation history plus current message) and output phase (generates response that becomes part of future input).

**Extended Thinking and Context Windows:**
When using extended thinking, all input and output tokens (including thinking tokens) count toward the context window limit with important nuances:
- Thinking budget tokens are a subset of max_tokens parameter, billed as output tokens
- Previous thinking blocks are automatically stripped from context window calculation by the Claude API and not part of conversation history for subsequent turns
- This preserves token capacity for actual conversation content
- Effective context window becomes: context_window = (input_tokens - previous_thinking_tokens) + current_turn_tokens
- Architecture is token-efficient, allowing extensive reasoning without token waste

**Extended Thinking with Tool Use:**
Combining extended thinking with tool use requires careful token management:
- First turn includes tools configuration, user message, extended thinking, text response, and tool use request
- Tool result handling requires returning the extended thinking block with tool results (only case where thinking blocks must be returned)
- After tool results, Claude responds with text only (no additional thinking until next user message)
- System uses cryptographic signatures to verify thinking block authenticity—modifying thinking blocks returns an error
- Claude 4 models support interleaved thinking (thinking between tool calls), enabling sophisticated reasoning after receiving tool results
- Claude Sonnet 3.7 does not support interleaved thinking

**1M Token Context Window (Beta):**
Claude Sonnet 4 and 4.5 support 1-million token context windows, currently in beta for organizations in usage tier 4 and those with custom rate limits. This allows processing much larger documents, maintaining longer conversations, and working with extensive codebases. Key considerations:
- Requires context-1m-2025-08-07 beta header in API requests
- Available on Claude API, Amazon Bedrock, and Google Cloud's Vertex AI
- Premium pricing: requests exceeding 200K tokens charged at 2x input, 1.5x output rates
- Dedicated rate limits for long context requests
- Multimodal considerations: large prompts with many images may hit request size limits due to variable token usage

**Context Awareness in Claude 4.5:**
Claude Sonnet 4.5 and Haiku 4.5 feature native context awareness, enabling models to track their remaining "token budget" throughout conversations. At conversation start, Claude receives total context window information (200K, 500K for Claude.ai Enterprise, or 1M for beta). After each tool call, Claude receives updates on remaining capacity (e.g., "Token usage: 35000/200000; 165000 remaining"). This awareness helps Claude:
- Determine how much capacity remains for work
- Enable more effective execution on long-running tasks
- Execute tasks to completion rather than guessing remaining tokens
- Particularly valuable for long-running agent sessions, multi-context-window workflows, and complex tasks requiring careful token management

**Context Window Management:**
Starting with Claude Sonnet 3.7, if prompt tokens plus output tokens exceed the context window, the system returns a validation error rather than silently truncating. This requires careful token management using the token counting API to estimate message token usage before sending to Claude.

---

Title: Context Engineering Guide
Tags: agent workflows, context engineering, dynamic context, instructions, memory, prompt engineering, RAG, structured outputs, system prompts, tools
URL: https://www.promptingguide.ai/guides/context-engineering-guide
<br/>
Summary:<br/>
See notes: This is the first article in a series that links to several other resources about context engineering, including articles on multi-agents, RAG, and more.

This comprehensive guide by DAIR.AI explains context engineering as the natural evolution and rebranding of prompt engineering. The author argues that many who claimed prompt engineering would die were wrong—it's now more important than ever, but requires a broader perspective than simple prompting.

**Defining Context Engineering:**
Context engineering is the process of designing and optimizing instructions and relevant context for LLMs and advanced AI models to perform tasks effectively. This encompasses multimodal models and includes:
- Designing and managing prompt chains
- Tuning instructions/system prompts
- Managing dynamic elements (user inputs, date/time)
- Searching and preparing relevant knowledge (RAG)
- Query augmentation
- Tool definitions and instructions for agentic systems
- Preparing and optimizing few-shot demonstrations
- Structuring inputs and outputs (delimiters, JSON schema)
- Short-term memory (state/historical context management) and long-term memory (retrieval from vector stores)
- Filtering out noisy information

The goal is optimizing information provided in the context window while systematically measuring LLM performance. From a developer's perspective, context engineering involves an iterative process with formal evaluation pipelines to measure whether tactics are working.

**Context Engineering vs. Prompt Engineering:**
Many confuse prompt engineering with "blind prompting" (short task descriptions in ChatGPT). In actual prompt engineering, you think carefully about context and structure. Context engineering is the next phase—architecting the full context through rigorous methods to obtain, enhance, and optimize knowledge for the system.

**Practical Implementation (Multi-Agent Deep Research Application):**

The guide walks through a concrete example of a Search Planner agent built in n8n that breaks down complex research queries into specific search subtasks. Key components:

1. **System Prompt:** High-level instructions defining the agent as an "expert research planner" with detailed specifications about breaking down queries into subtasks with specific fields (ID, query, source_type, time_period, domain_focus, priority).

2. **Instructions:** Clear, high-level guidance on what the system should do. Many developers stop here, but context engineering requires much more detailed context for optimal performance.

3. **User Input:** Structured using delimiters (e.g., `<user_query>` tags) to avoid confusion and add clarity about what constitutes user input versus system-generated content. Important when input types relate to output types.

4. **Structured Inputs and Outputs:** Detailed instructions on required subtask information with hints/examples to steer data generation. Includes field types and JSON examples for output parsing. Many AI developers ignore this, but it's powerful for ensuring consistent outputs that integrate properly with workflow components. Tools like n8n provide structured output functionality out of the box.

5. **Tools:** Dynamic context like current date/time using simple functions (`{{ $now.toISO() }}`). Forces concrete decisions about what context to pass and when, eliminating assumptions and inaccuracies. Crucial for queries requiring temporal knowledge—without correct date/time, systems guess and generate suboptimal queries.

6. **RAG & Memory:** Caching subqueries for similar user queries in vector stores to achieve speed-ups and cost optimization. Every LLM API call increases latency and costs. Creative context engineering about maintaining vector stores and pulling existing subtasks into context provides competitive advantages.

7. **States & Historical Context:** For revision phases, agents need access to previous states and historical context—past subtasks, revisions, results from each workflow agent. Requires many iterations and careful decision-making. Emphasizes importance of evaluation: measuring whether context engineering efforts are working.

**Advanced Context Engineering (Future Topics):**
- Context compression
- Context management techniques
- Context safety
- Evaluating context effectiveness over time
- Automated context engineering methods

Context can become diluted or inefficient (filled with stale and irrelevant information), requiring special evaluation workflows. The guide emphasizes that context engineering is an evolving skill set for AI developers/engineers with opportunities to build automation tools for effective context engineering.

**Linked Resources:** The article references several important resources on context engineering from various practitioners and researchers in the field.

---

Title: Don't Build Multi-Agents
Tags: agent architecture, compaction, context compression, context engineering, context windows, decision-making, multi-agent, reliability, single-threaded, sub-agents
URL: https://cognition.ai/blog/dont-build-multi-agents
<br/>
Summary:<br/>
See notes: This article is referenced in the promptingguide.ai context engineering guide and addresses multi-agent architecture considerations.

This influential article by Walden Yan from Cognition (creators of Devin) argues against multi-agent architectures in favor of simpler, more reliable approaches. The core argument centers on context engineering—the dynamic, automatic management of context in AI agent systems, which the author identifies as the #1 job of engineers building production AI agents.

**Two Fundamental Principles:**

1. **Share context, and share full agent traces, not just individual messages:** In multi-agent systems, subagents often work with incomplete context, leading to miscommunication. Even copying the original task isn't sufficient—in real production systems with multi-turn conversations and tool calls, numerous details can affect task interpretation. Full agent traces must be shared to prevent misunderstandings.

2. **Actions carry implicit decisions, and conflicting decisions carry bad results:** When parallel subagents cannot see each other's work, they make decisions based on conflicting assumptions. For example, if building a Flappy Bird clone is split between two subagents (one for background, one for bird), they might create components with incompatible visual styles because neither saw the other's implicit design decisions.

**The Fragility of Multi-Agent Systems:**

The author demonstrates how typical multi-agent workflows (break work into parts → start subagents → combine results) fail due to compounding errors. The failure point occurs when subagents misinterpret subtasks without full context and make conflicting implicit decisions that are impossible to reconcile at the combination stage. Libraries like OpenAI's Swarm and Microsoft's AutoGen are specifically criticized for actively pushing multi-agent concepts that violate these principles.

**Recommended Architectures:**

1. **Single-threaded linear agent:** The simplest and most reliable approach where context is continuous. This gets you "very far" and should be the default choice. May encounter issues with very large tasks that overflow context windows.

2. **Context compression architecture (for advanced use cases):** For truly long-duration tasks, introduce a specialized LLM model whose purpose is compressing action history and conversation into key details, events, and decisions. This is difficult to get right and may require fine-tuning smaller models for specific domains (which Cognition has done). Enables effectiveness at longer contexts but still eventually hits limits.

**Real-World Examples:**

- **Claude Code Subagents:** As of June 2025, Claude Code spawns subtasks but never does work in parallel with the subtask agent. Subtask agents only answer well-defined questions, not write code, because they lack the main agent's context. This purposefully simple approach prevents conflicting decisions while allowing investigative work to stay out of main agent history, extending context capacity.

- **Edit Apply Models:** In 2024, many coding agents used separate "edit apply models"—large models output markdown explanations of code changes, then small models rewrote files. This two-model approach was fragile due to ambiguous instructions causing misinterpretations. By 2025, edit decision-making and applying are typically done by a single model in one action, following the principle of avoiding split decision-making.

**The Future of Multi-Agent Systems:**

While optimistic about long-term possibilities, the author asserts that in 2025, multiple agents in collaboration only create fragile systems due to dispersed decision-making and insufficient context sharing. No one is currently solving the difficult cross-agent context-passing problem. The author believes this will "come for free" as single-threaded agents improve at communicating with humans, eventually unlocking parallelism and efficiency.

**Philosophy:** The article frames context engineering as analogous to React's philosophy for web development—not just scaffolding for code but a fundamental approach to building systems. The field is still in its "raw HTML & CSS" phase, and these principles represent early attempts to establish standards for production-grade agent systems.

---

Title: Context Engineering for Agents
Tags: agent workflows, code agents, compaction, compression, context engineering, context isolation, context retrieval, context selection, embeddings, knowledge graphs, memory, multi-agent, RAG, runtime state, scratchpads, summarization, tools, trimming
URL: https://rlancemartin.github.io/2025/06/23/context_engineering/
<br/>
Summary:<br/>
See notes: This article is referenced in the promptingguide.ai context engineering guide and provides a taxonomy of context engineering approaches.

This comprehensive post by Lance Martin (LangChain) provides a clear framework for understanding context engineering by organizing common strategies into four primary buckets: write, select, compress, and isolate. The article uses Andrej Karpathy's metaphor: LLMs are like a new operating system where the LLM is the CPU and the context window is the RAM (working memory). Context engineering is the "delicate art and science of filling the context window with just the right information for the next step."

**Context Types to Manage:**
- **Instructions:** Prompts, memories, few-shot examples, tool descriptions
- **Knowledge:** Facts, memories
- **Tools:** Feedback from tool calls

**Why Context Engineering Matters for Agents:**

Long-running agent tasks with accumulating tool call feedback consume large numbers of tokens, causing problems including context window overflow, ballooning costs/latency, and degraded performance. Drew Breunig identified specific failure modes:
- **Context Poisoning:** Hallucinations enter the context
- **Context Distraction:** Context overwhelms training
- **Context Confusion:** Superfluous context influences responses
- **Context Clash:** Context parts disagree

Both Cognition and Anthropic emphasize context engineering as the #1 job when building production AI agents.

**The Four Context Engineering Strategies:**

**1. Write Context (Saving context outside the context window):**

- **Scratchpads:** Agents take notes and persist information during task execution. Can be implemented as tool calls writing to files or fields in runtime state objects. Anthropic's multi-agent researcher saves plans to memory when approaching the 200K token limit to avoid truncation.

- **Memories:** Long-term memory across sessions. Reflexion introduced reflection after each agent turn to create reusable self-generated memories. Generative Agents periodically synthesized memories from collections of past agent feedback. Popular products like ChatGPT, Cursor, and Windsurf now auto-generate long-term memories from user-agent interactions. Memory types include:
  - Episodic memories (few-shot examples)
  - Procedural memories (instructions)
  - Semantic memories (facts)

**2. Select Context (Pulling context into the context window):**

- **Scratchpad Selection:** If scratchpads are tools, agents read via tool calls. If part of runtime state, developers control what state gets exposed each step, providing fine-grained control.

- **Memory Selection:** Agents need to select relevant memories for tasks. Many code agents use specific files pulled into context (Claude Code uses CLAUDE.md; Cursor and Windsurf use rules files). For larger memory collections, embeddings and/or knowledge graphs assist with indexing and selection. Challenge: Memory selection can go wrong (example: ChatGPT unexpectedly injecting location into requested images), making users feel the context window "no longer belongs to them."

- **Tool Selection:** Too many tools overload agents, especially with overlapping tool descriptions causing confusion. Applying RAG to tool descriptions to fetch semantically similar tools improves selection accuracy by 3-fold according to recent papers.

- **Knowledge Selection (RAG):** Code agents exemplify large-scale production RAG. Windsurf's Varun explains: "Indexing code != context retrieval." They use AST parsing with semantic chunking, but embedding search becomes unreliable as codebases grow, requiring combinations of grep/file search, knowledge graph retrieval, and re-ranking steps.

**3. Compress Context (Retaining only required tokens):**

- **Context Summarization:** Agent interactions spanning hundreds of turns with token-heavy tool calls benefit from summarization. Claude Code's "auto-compact" activates at 95% context window capacity, summarizing full user-agent interaction trajectories using recursive or hierarchical strategies. Summarization can also post-process specific tool calls (e.g., token-heavy search tools). At agent-agent boundaries, Cognition uses summarization to reduce tokens during knowledge hand-off, employing a fine-tuned model to capture specific events and decisions.

- **Context Trimming:** Unlike LLM-based summarization, trimming filters or "prunes" context using hard-coded heuristics like removing older messages. Drew Breunig mentions Provence, a trained context pruner for Question-Answering.

**4. Isolate Context (Splitting context to help task performance):**

- **Multi-agent:** OpenAI's Swarm library emphasizes "separation of concerns" where agent teams handle sub-tasks, each with specific tools, instructions, and isolated context windows. Anthropic's multi-agent researcher found many agents with isolated contexts outperformed single-agent because each subagent's context window focuses on narrower sub-tasks, with subagents operating in parallel. Challenges include high token use (up to 15× more tokens than chat), careful prompt engineering for planning, and coordination overhead.

- **Context Isolation with Environments:** HuggingFace's deep researcher uses a CodeAgent that outputs code containing tool calls, which runs in a sandbox. Selected context (e.g., return values) passes back to the LLM, isolating token-heavy objects like images and audio in the environment rather than the context window.

- **State Objects:** Agent runtime state objects provide isolation similar to sandboxing. Designed with schemas (e.g., Pydantic models), they have fields for writing context. One field (e.g., messages) exposes to the LLM each turn while other fields isolate information for selective use.

**Conclusion:** These four patterns—write, select, compress, and isolate—represent the current best practices for agent context engineering, though patterns continue evolving as the field advances.

---

Title: The New Skill in AI is Not Prompting, It's Context Engineering
Tags: agent failures, context components, context engineering, context failures, dynamic context, instructions, long-term memory, prompt engineering, RAG, short-term memory, state management, structured outputs, system prompts, tools
URL: https://www.philschmid.de/context-engineering
<br/>
Summary:<br/>
See notes: This article is referenced in the promptingguide.ai context engineering guide and provides a practical definition of context engineering with real-world examples.

This accessible article by Philipp Schmid (HuggingFace) reframes the AI development conversation from prompt engineering to context engineering, with Tobi Lutke's definition: "the art of providing all the context for the task to be plausibly solvable by the LLM." The core argument is that most agent failures are not model failures—they are context failures.

**Defining Context:**

Context encompasses everything the model sees before generating a response, far beyond a single prompt:

1. **Instructions/System Prompt:** Initial instructions defining model behavior during conversation, including examples and rules
2. **User Prompt:** Immediate task or question from the user
3. **State/History (short-term Memory):** Current conversation including user and model responses leading to this moment
4. **Long-Term Memory:** Persistent knowledge base from prior conversations containing learned user preferences, project summaries, or facts to remember for future use
5. **Retrieved Information (RAG):** External, up-to-date knowledge from documents, databases, or APIs for specific questions
6. **Available Tools:** Definitions of functions or built-in tools it can call (e.g., check_inventory, send_email)
7. **Structured Output:** Definitions for response format (e.g., JSON object)

**Why Context Engineering Matters: Cheap Demo vs. Magical Product**

The secret to building truly effective AI agents has less to do with code complexity and everything to do with context quality. Building agents is less about the code/framework you use—the difference between a cheap demo and a "magical" agent is the quality of context provided.

**Illustrative Example:**

User email: "Hey, just checking if you're around for a quick sync tomorrow."

**Cheap Demo Agent (Poor Context):**
- Sees only the user's request and nothing else
- Code might be perfectly functional but output is unhelpful and robotic
- Response: "Thank you for your message. Tomorrow works for me. May I ask what time you had in mind?"

**Magical Agent (Rich Context):**
- Code's primary job is gathering information the LLM needs to fulfill its goal
- Before calling LLM, extends context to include:
  - Calendar information (showing fully booked tomorrow)
  - Past emails with this person (determining appropriate informal tone)
  - Contact list (identifying them as a key partner)
  - Tools for send_invite or send_email
- Response: "Hey Jim! Tomorrow's packed on my end, back-to-back all day. Thursday AM free if that works for you? Sent an invite, lmk if it works."

The magic isn't in a smarter model or clever algorithm—it's about providing the right context for the right task. Agent failures aren't model failures; they are context failures.

**From Prompt to Context Engineering:**

While prompt engineering focuses on crafting the perfect set of instructions in a single text string, context engineering is far broader:

**Context Engineering Definition:**
"The discipline of designing and building dynamic systems that provides the right information and tools, in the right format, at the right time, to give a LLM everything it needs to accomplish a task."

**Context Engineering Is:**

1. **A System, Not a String:** Context isn't just a static prompt template—it's the output of a system that runs before the main LLM call

2. **Dynamic:** Created on-the-fly, tailored to the immediate task. For one request this could be calendar data; for another, emails or web search results

3. **About the right information, tools at the right time:** The core job is ensuring the model isn't missing crucial details ("Garbage In, Garbage Out"). This means providing both knowledge (information) and capabilities (tools) only when required and helpful

4. **Where the format matters:** How you present information matters. A concise summary is better than a raw data dump. A clear tool schema is better than a vague instruction

**Conclusion:**

Building powerful and reliable AI agents is becoming less about finding a magic prompt or model updates. It's about the engineering of context—a cross-functional challenge involving understanding your business use case, defining outputs, and structuring all necessary information so an LLM can accomplish the task.

---

Title: Context Engineering: Going Beyond Prompts To Push AI
Tags: context curation, context dilution, context engineering, context evaluation, context windows, cost optimization, information architecture, latency, prompt engineering, RAG, short-term memory, structuring context, token count, tool calling
URL: https://simple.ai/p/the-skill-thats-replacing-prompt-engineering
<br/>
Summary:<br/>
See notes: This article is referenced in the promptingguide.ai context engineering guide and provides an accessible introduction to context engineering.

This accessible article by Dharmesh Shah (co-founder & CTO of HubSpot) provides a beginner-friendly introduction to context engineering, framing it as the evolution from prompt engineering. The core insight: as context windows exploded from 4K to over 1M tokens in two years, something more powerful than prompt engineering emerged—instead of optimizing how you ask, you now optimize what the AI has access to when it thinks. (Shah credits Tobi Lutke from Shopify for coining the term "context engineering.")

**Understanding Context Windows:**

A context window is like a big sheet of paper passed to the LLM with a token limit. Tokens are roughly ¾ of an English word or about four characters (e.g., "ChatGPT" = two tokens: "Chat" and "GPT"). Token count matters because billing, latency, and memory all scale with it.

Key limitation: LLMs only know what they were trained on and what's provided in the context window. As context windows have exploded in token size, we've gotten increasingly clever about what we put in the window.

**What Goes in the Context Window:**

1. **Short-term Memory (Conversation History):** ChatGPT and Claude have good short-term memory because behind the scenes they pass prior prompts and outputs into the context window. Analogous to the movie Memento where the main character writes notes on his body to remember who he is and what's happening.

2. **RAG (Retrieval-Augmented Generation):** Find documents related to the user prompt and pass them into the context window, "teaching" the LLM precisely the things that help it answer a question.

3. **Tool Calling:** Tell the LLM it has access to tools (web search, stock price lookups, weather forecasts). The LLM doesn't actually call tools itself—it only takes context in and produces output. The application (like ChatGPT) invokes tools on the LLM's behalf and puts results back in the context window. A clever workaround for the fact that LLMs just work with context windows.

With a million-token context window, you can feed an AI an entire codebase, complete business plan, or months of customer support conversations, and it can reason across all that information simultaneously.

**The Evolution from Prompt Engineering:**

The 2023 prompt engineering craze featured headlines about $300k+ salaries for "Prompt Engineers" at places like Anthropic, requiring no formal CS degree—just the ability to speak fluent "LLM." While some were hired, it didn't become the massive job category predicted because everyone became a prompt engineer.

Now context engineering is emerging as more important—a higher-level version of prompt engineering.

**Simple Explanation:**
- **Prompt engineering:** Learning to ask really good questions
- **Context engineering:** Being a librarian who decides what books someone has access to before they even start reading

**What Context Engineers Actually Do:**

1. **Curate:** Decide which documents, memories, or APIs matter for each specific task
2. **Structure:** Layer system messages → tools → retrieved data → user prompt in optimal order
3. **Compress:** Summarize or chunk information to stay under token limits while preserving what matters
4. **Evaluate:** Measure accuracy and watch for "context dilution" where irrelevant info distracts the model

**Challenges and Opportunities:**

More context means richer documents and longer conversations, but cost and latency rise roughly linearly with window length. This leaves room for context engineers to discover best practices (many still emerging).

Context engineering requires thinking about information architecture, data strategy, and user experience in ways prompt engineering never did. Companies who master this will have massive competitive advantage.

**Key Insight:**
"Prompting tells the model how to think, but context engineering gives the model the training and tools to get the job done."

**The Context-First Future:**

The prompt engineering hype taught an important lesson: the most valuable AI skills aren't about learning secret phrases or clever tricks. They're about understanding how to architect intelligent systems with access to the right information at the right time.

It's a fundamental shift from optimizing sentences to optimizing knowledge. The prompt engineering era taught us to talk to AI. The context engineering era is teaching us to think with AI.

---

Title: 12-Factor Agents - Principles for building reliable LLM applications
Tags: agent architecture, agent frameworks, agent loops, compaction, context engineering, context windows, control flow, error handling, human-in-the-loop, modular design, production agents, prompt engineering, state management, stateless reducers, structured outputs, tool calling
URL: https://github.com/humanlayer/12-factor-agents
<br/>
Summary:<br/>
See notes: This comprehensive guide is referenced in the promptingguide.ai context engineering guide and provides 12 principles for building production-grade AI agents.

This influential guide by Dex from HumanLayer addresses a critical question: "What are the principles we can use to build LLM-powered software that is actually good enough to put in the hands of production customers?" Inspired by the 12 Factor Apps methodology, it synthesizes lessons from building production agents and talking to 100+ SaaS founders.

**Core Observation:**

After trying every agent framework (crew/langchains, smolagents, langraph, griptape), Dex found that most production customer-facing products aren't very agentic. They're mostly deterministic code with LLM steps sprinkled in at just the right points. Good agents don't follow the "here's your prompt, here's a bag of tools, loop until you hit the goal" pattern—they are comprised mostly of just software.

**The Typical Framework Journey:**
1. Decide to build an agent
2. Product design and UX mapping
3. Grab a framework and start building
4. Get to 70-80% quality bar
5. Realize 80% isn't good enough for customer-facing features
6. Realize getting past 80% requires reverse-engineering the framework
7. Start over from scratch

**Core Philosophy:**

The fastest way to get good AI software in the hands of customers is to take small, modular concepts from agent building and incorporate them into existing products. These modular concepts can be defined and applied by most skilled software engineers, even without AI backgrounds.

**Brief History - From Code to Agents:**

**Software as Directed Graphs:** All software is fundamentally a directed graph (why we used flow charts).

**DAG Orchestrators (20 years ago):** Tools like Airflow, Prefect, Dagster, Inngest, and Windmill followed the graph pattern with added benefits: observability, modularity, retries, administration.

**The Promise of Agents:** You get to throw the DAG away. Instead of coding each step and edge case, give the agent a goal and set of transitions, letting the LLM make real-time decisions to figure out the path. Promise: write less software, recover from errors, LLMs find novel solutions.

**Agents as Loops:** The basic agent loop consists of:
1. LLM determines next step, outputting structured JSON ("tool calling")
2. Deterministic code executes the tool call
3. Result appended to context window
4. Repeat until "done"

However, as the guide demonstrates, this approach doesn't work as well as we want for production systems.

**The 12 Factors:**

**1. Natural Language to Tool Calls:** Converting user intent into structured tool calls that deterministic code can execute.

**2. Own Your Prompts:** Take direct control of prompts rather than relying on framework abstractions. Prompts are code and should be treated as such.

**3. Own Your Context Window:** (Highlighted as the Context Engineering factor) Take direct control of what goes into the context window at each step. The context window is your agent's working memory—curate it carefully. Pre-fetch context you might need, structure it optimally, and understand exactly what the LLM sees.

**4. Tools are Just Structured Outputs:** Tool calling is just a specialized form of structured output. Understanding this allows for more flexible agent design.

**5. Unify Execution State and Business State:** Don't separate agent execution state from your application's business state. They should be unified for reliability and easier debugging.

**6. Launch/Pause/Resume with Simple APIs:** Design agents to be pausable and resumable. This is critical for long-running tasks, human-in-the-loop patterns, and error recovery.

**7. Contact Humans with Tool Calls:** Human-in-the-loop should be implemented as tool calls, not special cases. This treats human input as another tool the agent can use.

**8. Own Your Control Flow:** Don't let frameworks dictate your control flow. You should explicitly control the flow of execution, not rely on opaque framework loops.

**9. Compact Errors into Context Window:** When errors occur, compact them into concise, useful information for the context window. Don't let error messages pollute context with unhelpful stack traces.

**10. Small, Focused Agents:** Build small, focused agents rather than one large "do everything" agent. This improves reliability, debuggability, and performance. Even as LLMs get smarter, specialized agents will outperform generalists.

**11. Trigger from Anywhere, Meet Users Where They Are:** Agents should be triggerable from multiple surfaces—web, mobile, Slack, email, webhooks, cron jobs. The agent logic should be decoupled from the interface.

**12. Make Your Agent a Stateless Reducer:** Design agents as pure functions that take state as input and return new state as output. This makes them easier to test, debug, and reason about.

**Honorable Mention - Factor 13: Pre-fetch All the Context You Might Need:** Anticipate what context the agent might need and pre-fetch it rather than relying on the agent to figure out what to retrieve. This reduces token waste and improves reliability.

**Key Design Insights:**

1. **Core things make agents great:** There are fundamental principles that matter regardless of framework choice.

2. **Greenfield rewrites may be counter-productive:** Going all-in on a framework and building from scratch often leads to dead ends.

3. **Modular concepts are key:** Take small, modular concepts from agent building and incorporate them into existing products rather than wholesale framework adoption.

4. **Framework abstractions vs. control:** While frameworks enable rapid prototyping and getting to 70-80%, getting to production quality often requires reverse-engineering the framework and taking direct control.

**Target Audience:**

The guide is aimed at SaaS builders and technical founders looking to make existing products more agentic, emphasizing that these principles apply whether you're using TypeScript, Python, or any other language. It advocates for treating prompts as code and emphasizing that skilled software engineers can apply these concepts even without deep AI backgrounds.

---

Title: The rise of "context engineering"
Tags: agent workflows, context engineering, dynamic context, LangGraph, LangSmith, long-term memory, observability, prompt engineering, short-term memory, tools
URL: https://blog.langchain.com/the-rise-of-context-engineering/
<br/>
Summary:<br/>
See notes: This article is referenced in the promptingguide.ai context engineering guide and provides LangChain's perspective on context engineering.

This LangChain blog post by Harrison Chase defines context engineering as "building dynamic systems to provide the right information and tools in the right format such that the LLM can plausibly accomplish the task." The article synthesizes recent perspectives from Tobi Lutke, Ankur Goyal, and Walden Yan to establish context engineering as the most important skill AI engineers can develop.

**Core Definition Breakdown:**

**Context Engineering is a System:** Complex agents pull context from many sources—the developer, the user, previous interactions, tool calls, or external data. Assembling these requires a complex system, not a single prompt.

**The System is Dynamic:** Many context pieces come in dynamically, so the logic for constructing the final prompt must be dynamic rather than static. The system adapts to varying inputs and situations.

**You Need the Right Information:** A common reason agentic systems fail is missing the right context. LLMs cannot read minds—you must provide the right information. "Garbage in, garbage out" applies directly.

**You Need the Right Tools:** The LLM may not solve tasks solely based on inputs. Empowering the LLM requires the right tools to look up information, take actions, or perform intermediate steps. Tool access is as important as information access.

**Format Matters:** How you communicate with LLMs matters as much as with humans. A short, descriptive error message is far more effective than a large JSON blob. This applies equally to tool input parameters—clear, well-structured parameters ensure LLMs can use them effectively.

**"Can It Plausibly Accomplish the Task?"** This question should guide context engineering. It reinforces that LLMs need to be set up for success and helps separate failure modes: Is it failing due to missing information/tools, or does it have everything but still messed up? These failure modes require very different fixes.

**Why Context Engineering Matters:**

LLMs mess up for two fundamental reasons:
1. The underlying model isn't good enough (intrinsic failure)
2. The model wasn't passed appropriate context (context failure)

More often than not (especially as models improve), mistakes are caused by the second reason. Bad context arises from:
- **Missing context:** Models aren't mind readers. Without the right context, they won't know it exists.
- **Poorly formatted context:** Communication is critical. How you format data when passing to a model absolutely affects responses.

**Context Engineering vs. Prompt Engineering:**

Early on, developers focused on phrasing prompts cleverly to coax better answers. As applications grow more complex, providing complete and structured context is far more important than any magic wording.

Prompt engineering is a subset of context engineering. Even with all the context, how you assemble it in the prompt still matters. The difference: you're architecting prompts to work with dynamic data sets rather than a single static input.

A key part of context often involves core instructions for how the LLM should behave (traditionally considered prompt engineering). Providing clear, detailed instructions for agent behavior is both context engineering and prompt engineering.

**Examples of Context Engineering:**

1. **Tool Use:** Ensuring agents have tools to access external information when needed, with tool returns formatted to be maximally digestible for LLMs
2. **Short-Term Memory:** For lengthy conversations, creating summaries and using them in future turns
3. **Long-Term Memory:** Fetching user preferences expressed in previous conversations
4. **Prompt Engineering:** Clear enumeration of agent behavior instructions in the prompt
5. **Retrieval:** Dynamically fetching information and inserting it into the prompt before calling the LLM

**How LangGraph Enables Context Engineering:**

LangGraph was built with the goal of being the most controllable agent framework, perfectly enabling context engineering. You control everything:
- What steps are run
- Exactly what goes into your LLM
- Where outputs are stored

This total control allows all desired context engineering. Many agent frameworks emphasize abstractions that restrict context engineering—places where you cannot change exactly what goes into the LLM or what steps run beforehand.

The article references Dex Horthy's "12 Factor Agents" as an excellent read with many points relating to context engineering ("own your prompts," "own your context building," etc.).

**How LangSmith Helps with Context Engineering:**

LangSmith is LangChain's LLM application observability and evaluation solution. Key features for context engineering:

1. **Trace Agent Calls:** See all steps that happen in your agent and what steps were run to gather data sent into the LLM
2. **Inspect Exact Inputs/Outputs:** See exactly what went into the LLM—the data it had and how it was formatted. Debug whether it contains all relevant information for the task, including what tools the LLM has access to

**"Communication is All You Need":**

The author references a previous blog emphasizing that communicating to the LLM is hard, underappreciated, and often the root cause of agent errors. Many of these points relate to context engineering.

Context engineering isn't a new idea—agent builders have been doing it for years. It's a new term that aptly describes an increasingly important skill. LangChain's tools (LangGraph, LangSmith) are built to enable context engineering.

---

Title: Retrieval Augmented Generation (RAG)
Tags: context engineering, external knowledge, factual consistency, hallucination, knowledge-intensive tasks, LLM performance, parametric memory, RAG, retrieval
URL: https://www.promptingguide.ai/techniques/rag
<br/>
Summary:<br/>
This comprehensive guide on the Prompt Engineering Guide website explains Retrieval Augmented Generation (RAG), a foundational technique for context engineering that addresses knowledge-intensive tasks by combining information retrieval with text generation.

**The Problem RAG Solves:**

General-purpose language models can be fine-tuned for common tasks like sentiment analysis and named entity recognition, which generally don't require additional background knowledge. However, more complex and knowledge-intensive tasks require language model-based systems that access external knowledge sources to complete tasks effectively. This need arises because:

1. **Static parametric knowledge:** LLMs' built-in knowledge is frozen at training time
2. **Hallucination:** Models generate plausible-sounding but incorrect information
3. **Reliability:** Without external knowledge, generated responses may lack factual consistency

**What is RAG:**

Meta AI researchers introduced RAG as a method to address knowledge-intensive tasks. RAG combines two core components:
1. **Information retrieval component:** Finds relevant documents from external sources
2. **Text generator model:** Produces final output using retrieved information

**How RAG Works:**

The RAG process follows these steps:
1. RAG takes an input query
2. Retrieves a set of relevant/supporting documents from a source (e.g., Wikipedia)
3. Documents are concatenated as context with the original input prompt
4. The combined context is fed to the text generator
5. The generator produces the final output using both the query and retrieved knowledge

**Key Advantages:**

1. **Adaptive to evolving facts:** Since retrieval happens at query time, RAG can access up-to-date information as facts change, unlike static parametric knowledge
2. **Efficient knowledge updates:** RAG's internal knowledge can be modified efficiently without needing to retrain the entire model
3. **Bypass retraining:** Language models can access the latest information for generating reliable outputs via retrieval-based generation
4. **Improved factual consistency:** External knowledge sources ground responses in verifiable information
5. **Hallucination mitigation:** Retrieval-based approach reduces model tendency to generate incorrect information

**Technical Implementation (Lewis et al., 2021):**

The paper proposed a general-purpose fine-tuning recipe for RAG:
- **Parametric memory:** Pre-trained seq2seq model stores learned patterns
- **Non-parametric memory:** Dense vector index of Wikipedia accessed using a neural pre-trained retriever
- The retriever finds relevant documents that the generator conditions on to produce outputs

**Performance:**

RAG demonstrates strong performance on multiple benchmarks:
- **Natural Questions:** Question answering over Wikipedia
- **WebQuestions:** Web-based question answering
- **CuratedTrec:** Curated question-answer pairs
- **MS-MARCO:** Microsoft MAchine Reading COmprehension dataset
- **Jeopardy questions:** Generates more factual, specific, and diverse responses
- **FEVER:** Fact Extraction and VERification - improves fact verification results

These results show RAG as a viable option for enhancing language model outputs in knowledge-intensive tasks.

**Modern Applications:**

More recently, retriever-based approaches have become increasingly popular and are combined with modern LLMs like ChatGPT to improve capabilities and factual consistency. RAG has become a foundational technique in production AI systems requiring up-to-date, verifiable information.

**Relation to Context Engineering:**

RAG is a core context engineering technique—it dynamically constructs context windows by retrieving relevant information at query time rather than relying solely on static training data. This represents a fundamental approach to "context selection" and "knowledge selection," two key aspects of effective context engineering for AI agents.

**Additional Resources:**

The guide references:
1. "Retrieval-Augmented Generation for Large Language Models: A Survey" (Dec 2023)
2. "Retrieval Augmented Generation: Streamlining the creation of intelligent natural language processing models" (Sep 2020)

The article also includes a hands-on notebook tutorial demonstrating how to build a RAG system using open-source LLMs for generating short and concise machine learning paper titles.

---

Title: Long Context vs. RAG for LLMs: An Evaluation and Revisits
Tags: context engineering, context relevance, context windows, dialogue systems, evaluation, LC vs RAG, LLM performance, long-context, question-answering, RAG, retrieval, summarization, Wikipedia
URL: https://arxiv.org/abs/2501.01880
<br/>
Summary:<br/>
See notes: This paper examines the tradeoffs between RAG and Long Context approaches, referenced in the brain dump notes as an important consideration for context engineering.

This comprehensive research paper by Xinze Li, Yixin Cao, Yubo Ma, and Aixin Sun (submitted December 27, 2024) provides a rigorous evaluation comparing two fundamental strategies for enabling LLMs to work with extremely long external contexts, addressing a critical question in context engineering: when to use RAG versus when to rely on long context windows.

**Two Main Strategies for Long External Context:**

1. **Long Context (LC):** Extending the context window to accommodate more information directly within the model's attention mechanism. Modern models support 200K-1M token windows, allowing vast amounts of information to be processed in a single pass.

2. **Retrieval-Augmented Generation (RAG):** Using retrieval systems to selectively access only the relevant information from large knowledge bases, injecting retrieved content into shorter context windows as needed.

**Research Approach:**

The paper revisits recent studies on this topic, identifying key insights and discrepancies in existing research. To provide a more comprehensive evaluation, the researchers:

1. **Filter out questions answerable without external context:** Ensures the evaluation truly tests the models' ability to work with external knowledge rather than parametric knowledge
2. **Identify the most effective retrieval methods:** Compares different retrieval approaches to isolate the best-performing strategies
3. **Expand the datasets:** Broadens evaluation beyond single benchmark limitations to provide more generalizable insights

**Key Findings:**

**LC Generally Outperforms RAG in QA Benchmarks:**
- Long Context shows superior performance on question-answering tasks
- Particularly strong advantage for Wikipedia-based questions
- The ability to process all relevant information simultaneously within the context window provides performance benefits when the entire knowledge base can fit

**Retrieval Method Performance Varies Significantly:**
- **Summarization-based retrieval:** Performs comparably to Long Context, approaching LC performance levels
- **Chunk-based retrieval:** Lags behind both LC and summarization-based retrieval
- This suggests that how you retrieve and prepare context significantly impacts downstream performance

**RAG Has Specific Advantages:**
- **Dialogue-based queries:** RAG shows advantages in conversational contexts where maintaining long conversation history may be impractical
- **General question queries:** For open-ended questions, RAG's selective retrieval can provide more focused context

**Trade-offs Between RAG and LC:**

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

**Critical Insight: Context Relevance:**

The paper highlights an overlooked aspect in existing studies—the importance of **context relevance**. Not just whether information is present, but whether the right information is present and whether irrelevant information is absent. This relates directly to the "context rot" phenomenon where adding more tokens can degrade performance even when those tokens contain the needed information somewhere within them.

**Implications for Context Engineering:**

This research provides crucial guidance for practitioners designing systems with external knowledge:

1. **Task-dependent strategy selection:** Choose LC vs. RAG based on task type (QA vs. dialogue), knowledge base size, and cost constraints
2. **Hybrid approaches may be optimal:** Combining LC with selective retrieval (summarization-based) can provide best-of-both-worlds performance
3. **Context relevance matters:** Simply having long context windows isn't sufficient—you must ensure high signal-to-noise ratio in what you include
4. **Retrieval method matters:** If using RAG, summarization-based retrieval significantly outperforms naive chunk-based approaches

**Research Significance:**

This 14-page paper (excluding references and appendix) contributes to the evolving understanding of how to optimally architect LLM systems for knowledge-intensive tasks. As context windows continue to expand, understanding when to use direct context inclusion versus selective retrieval becomes increasingly important for cost-effective, high-performance system design.

The findings underscore that context engineering isn't just about maximizing what you can fit into a context window—it's about strategically deciding what information to provide, in what format, and through what mechanism (direct inclusion vs. retrieval).

---

Title: Anthropic Academy - Build with Claude
Tags: agent workflows, API, Claude, code execution, computer use, context engineering, documentation, embeddings, evaluations, extended thinking, learning resources, MCP, prompt caching, prompt engineering, RAG, SDK, Skills, tool use, tutorials, vision
URL: https://www.anthropic.com/learn/build-with-claude
<br/>
Summary:<br/>
See notes: This is Anthropic's comprehensive learning hub referenced in the brain dump notes for RAG tutorials and building with Claude.

This is Anthropic's central learning hub—"Anthropic Academy: Build with Claude"—providing comprehensive resources for developing Claude-powered applications. The page serves as a comprehensive gateway to API guides, best practices, tutorials, and documentation covering the full spectrum of Claude development from foundational prompting to advanced agentic systems.

**Structure and Organization:**

The learning hub is organized into 14 major topic areas, each with "Get Started," "Documentation," "Insights," and sometimes "Courses" sections. This structure provides progressive learning paths from beginner quickstarts to advanced implementations.

**Major Topic Areas:**

**1. Claude 4 Models:**
- Latest features in Claude Sonnet 4.5 and Opus 4.1
- Model migration checklist for upgrading
- Model selection guidance
- Claude 4 prompting best practices
- Model comparison charts and pricing

**2. APIs & SDKs:**
- SDKs for Python, TypeScript, Java, Go, and Ruby
- Messages API fundamentals
- Message Batches API for multiple requests
- Prompt caching for optimization
- Amazon Bedrock API integration
- Google Vertex AI integration
- Admin API for permissions and workspace management
- Files API for file uploads
- PDF support for text extraction and visual understanding
- Experimental prompt generation and improvement APIs
- Comprehensive courses covering Anthropic API, Amazon Bedrock, and Google Vertex AI

**3. Agents:**
- Building autonomous agents that understand, plan, and execute complex tasks
- Agent patterns in the Anthropic Cookbook
- JSON outputs for reliable agent control
- Model Context Protocol for improved agentic workflows
- Best practices for building effective agents

**4. Skills:**
- Performing specific tasks with detailed instructions
- Skills implementation best practices
- Using Skills in API and Claude Code

**5. Model Context Protocol (MCP):**
- Setting up MCP in Claude Desktop
- Ready-made MCP servers from Anthropic
- MCP with Claude Code
- Remote MCP server setup and connection
- MCP with Messages API
- GitHub contribution opportunities
- Courses on getting started and advanced MCP concepts

**6. Claude Code:**
- IDE integration for speeding up development
- Google Vertex and Amazon Bedrock connections
- Common workflows documentation
- Troubleshooting guides
- Launch video and comprehensive courses

**7. Tool Use:**
- Extending Claude's capabilities with external tools and APIs
- Tool use courses and demo videos
- Tool use cookbooks
- Code execution tool, text editor tool, web search tool
- Comprehensive documentation

**8. Extended Thinking:**
- Improving Claude's ability to solve complex tasks through reasoning
- Extended thinking models overview
- Cookbook guides
- Best practices implementation
- Launch video

**9. Retrieval Augmented Generation (RAG):**

This section is specifically referenced in the brain dump notes. RAG resources include:

**Get Started:**
- **Build a toy customer support agent with RAG:** Hands-on tutorial demonstrating RAG implementation in a practical customer service context
- **Use Voyage AI for embeddings:** Integration guide for Voyage AI's embedding models
- **Integrate RAG with LlamaIndex:** Connecting Claude with LlamaIndex's RAG framework
- **Build a RAG system with MongoDB:** Database-backed RAG implementation

**Documentation:**
- Embeddings documentation for understanding vector representations

**Insights:**
- **Learn how contextual retrieval works:** Advanced RAG technique that enhances retrieval accuracy by adding context to chunks before embedding

The RAG section emphasizes building effective RAG systems to enhance Claude's responses with external data sources, addressing knowledge-intensive tasks and reducing hallucination through grounded information retrieval.

**10. Prompt Engineering:**
- Interactive prompt engineering tutorial
- Real-world scenario practice
- Prompt generator tool
- Comprehensive prompt engineering documentation
- Prompt engineering roundtable video

**11. Evaluations:**
- Building strong evaluations
- Automated evaluation systems
- Eval Tool on Claude Console
- Comprehensive evaluations documentation

**12. Prompt Caching:**
- Optimizing performance and reducing costs by reusing context
- Explainer video
- Anthropic Cookbook implementation guide
- Launch post insights

**13. Vision:**
- Understanding and analyzing visual information
- Vision best practices
- Text extraction from images
- Chart and graph analysis
- Comprehensive vision documentation

**14. Computer Use:**
- Using Claude models to interact with desktop environments
- Computer Use quickstart
- API implementation
- Data handling documentation
- Development insights and launch post

**15. Hackathon Hacker Guide:**
- Developer account setup and API key generation
- Quickstart guide for first API call
- Claude Code installation (`npm install -g @anthropic-ai/claude-code`)
- Anthropic Cookbook code snippets
- Anthropic Quickstarts repository
- Full API documentation
- Workshop slides

**Value for Context Engineering:**

This learning hub is essential for context engineering because it provides:

1. **Comprehensive RAG Resources:** Direct tutorials for implementing retrieval systems, a core context engineering technique
2. **Agent Building:** Guides for autonomous systems that must manage context across multiple turns
3. **MCP Integration:** Tools for expanding context capabilities through external data sources
4. **Prompt Caching:** Techniques for efficiently managing repeated context
5. **Skills Implementation:** Structured approaches to providing detailed task-specific context
6. **Extended Thinking:** Enabling deeper reasoning by managing thinking tokens within context windows
7. **Tool Use:** Expanding context through dynamic tool calls

**Target Audience:**

The comprehensive structure serves multiple experience levels:
- **Beginners:** "Get Started" sections with quickstarts and interactive tutorials
- **Intermediate:** "Documentation" sections with detailed implementation guides
- **Advanced:** "Insights" sections with deep dives, best practices, and architectural considerations
- **Hands-on Learners:** "Courses" providing structured, in-depth learning paths

This resource hub represents Anthropic's commitment to developer education, providing everything needed to build production-grade Claude applications from foundational concepts through advanced context engineering techniques.

---

Title: Advanced RAG Techniques: Elevating Your Retrieval-Augmented Generation Systems
Tags: adaptive retrieval, advanced techniques, agentic RAG, chunking, context enrichment, embeddings, evaluation, explainability, fusion retrieval, GitHub, graph RAG, hierarchical indices, HyDE, iterative retrieval, knowledge graphs, LangChain, LlamaIndex, multi-modal, query enhancement, RAG, RAPTOR, reranking, retrieval, semantic chunking, Self-RAG, tutorials
URL: https://github.com/NirDiamant/RAG_Techniques
<br/>
Summary:<br/>
This is one of the most comprehensive and dynamic collections of Retrieval-Augmented Generation (RAG) tutorials available today, created by Nir Diamant. With 22.9k stars and 2.6k forks on GitHub, this repository serves as a premier hub for cutting-edge techniques aimed at enhancing the accuracy, efficiency, and contextual richness of RAG systems.

**Repository Mission:**

The repository's goal is to provide a valuable resource for researchers and practitioners looking to push the boundaries of what's possible with RAG by fostering a collaborative environment to accelerate innovation in this field. It grows stronger through community contributions and includes both educational content and practical implementations.

**Key Features:**

- **State-of-the-art RAG enhancements:** 35+ advanced techniques covering the full spectrum of RAG capabilities
- **Comprehensive documentation:** Each technique includes detailed explanations and implementation guides
- **Practical implementations:** Both LangChain and LlamaIndex versions for most techniques
- **Interactive learning:** Google Colab notebooks for hands-on experimentation
- **Runnable scripts:** Ready-to-use code for immediate implementation
- **Regular updates:** Continuously maintained with latest advancements
- **Community-driven:** Active Discord community and subreddit for collaboration

**Related Projects:**

The repository author also maintains complementary projects:
- **Agents Towards Production:** Code-first tutorials for building production-grade GenAI agents
- **GenAI Agents Repository:** Various AI agent implementations and tutorials
- **Prompt Engineering Techniques:** Comprehensive collection of prompting strategies

**Advanced Techniques Organized by Category:**

**1. Foundational RAG Techniques (6 techniques):**

- **Simple RAG:** Basic retrieval with incremental learning mechanisms for newcomers
- **RAG with CSV Files:** Basic retrieval using structured CSV data with OpenAI integration
- **Reliable RAG:** Enhanced Simple RAG with validation, relevancy checking, and document segment highlighting
- **Optimizing Chunk Sizes:** Experimenting with fixed chunk sizes to balance context preservation and retrieval efficiency
- **Proposition Chunking:** Breaking text into concise, complete, meaningful sentences using LLM-generated factual statements with quality checking for accuracy, clarity, completeness, and conciseness

**2. Query Enhancement (3 techniques):**

- **Query Transformations:** Query rewriting, step-back prompting for broader queries, and sub-query decomposition for complex queries
- **HyDE (Hypothetical Document Embedding):** Generating hypothetical questions that point to relevant data locations, improving query-data matching
- **HyPE (Hypothetical Prompt Embeddings):** Precomputing hypothetical prompts at indexing stage, transforming retrieval into question-question matching with no runtime overhead, improving precision by up to 42 percentage points and recall by up to 45 percentage points

**3. Context and Content Enrichment (6 techniques):**

- **Contextual Chunk Headers (CCH):** Creating document-level and section-level context headers prepended to chunks before embedding
- **Relevant Segment Extraction (RSE):** Dynamically constructing multi-chunk segments relevant to queries through retrieval post-processing
- **Context Window Enhancement:** Embedding individual sentences while extending context to neighboring sentences
- **Semantic Chunking:** Dividing documents based on semantic coherence using NLP to identify topic boundaries rather than fixed sizes
- **Contextual Compression:** Compressing retrieved information while preserving query-relevant content using LLM summarization
- **Document Augmentation:** Augmenting text datasets with all possible questions that can be asked to each document

**4. Advanced Retrieval Methods (7 techniques):**

- **Fusion Retrieval:** Combining keyword-based search with vector-based search for comprehensive and accurate retrieval
- **Intelligent Reranking:** LLM-based scoring, cross-encoder models for joint query-document encoding, and metadata-enhanced ranking
- **Multi-faceted Filtering:** Metadata filtering, similarity thresholds, content filtering, and diversity filtering
- **Hierarchical Indices:** Two-tiered system with document summaries and detailed chunks, both with metadata pointing to the same data location
- **Ensemble Retrieval:** Combining multiple retrieval models using voting or weighting mechanisms
- **Dartboard Retrieval:** Optimizing for Relevant Information Gain by combining relevance and diversity into a single scoring function
- **Multi-modal RAG:** Handling diverse data types through captioning (storing multimedia with text in vector store) or Colpali approach (converting data to images for vision LLM processing)

**5. Iterative and Adaptive Techniques (3 techniques):**

- **Retrieval with Feedback Loops:** Collecting and utilizing user feedback to fine-tune retrieval and ranking models
- **Adaptive Retrieval:** Classifying queries into categories with tailored retrieval strategies considering user context and preferences
- **Iterative Retrieval:** Performing multiple rounds using LLM to analyze initial results and generate follow-up queries

**6. Evaluation (2 techniques):**

- **DeepEval:** Comprehensive RAG evaluation covering correctness, faithfulness, and contextual relevancy metrics with test case creation
- **GroUSE Evaluation:** Contextually-grounded LLM evaluation using 6 metrics of the GroUSE framework with meta-evaluation capabilities

**7. Explainability and Transparency (1 technique):**

- **Explainable Retrieval:** Explaining why certain information was retrieved and how it relates to the query to enhance user trust

**8. Advanced Architectures (7 techniques):**

- **Agentic RAG with Contextual AI:** Production-ready pipelines with document parser, instruction-following reranker, grounded language models (GLM), and LMUnit natural language testing
- **Graph RAG with Milvus:** Combining relationship-based retrieval with vector search and reranking using stored text passages and relationship triplets
- **Knowledge Graph Integration (Graph RAG):** Retrieving entities and relationships from knowledge graphs combined with unstructured text
- **Microsoft GraphRAG:** Extracting entities and relationships, generating community summaries from bottom-up
- **RAPTOR (Recursive Abstractive Processing for Tree-Organized Retrieval):** Using abstractive summarization recursively to organize information in tree structures for hierarchical context
- **Self-RAG:** Implementing retrieval decision, document retrieval, relevance evaluation, response generation, support assessment, and utility evaluation
- **Corrective RAG (CRAG):** Integrating retrieval evaluator, knowledge refinement, web search query rewriter, and response generator adapting information sourcing strategy based on relevance scores

**9. Special Advanced Technique (1 technique):**

- **Sophisticated Controllable Agent:** Using deterministic graph as the "brain" of autonomous agent for complex questions through anonymization, high-level planning, task breakdown, adaptive retrieval, continuous re-planning, and answer verification

**Implementation Approach:**

Each technique includes:
- Detailed overview explaining the concept
- Implementation guidance with specific steps
- Code examples in both LangChain and LlamaIndex (where applicable)
- Google Colab notebooks for interactive learning
- Runnable scripts for immediate use
- Links to additional resources and research papers

**Getting Started:**

The repository provides clear instructions for cloning and navigating to specific techniques, with each technique having its own directory containing comprehensive implementation guides.

**Community and Contribution:**

The repository encourages contributions through:
- Active Discord community (RAG Techniques Discord)
- Educational AI Subreddit
- Clear contribution guidelines in CONTRIBUTING.md
- Fork-and-pull-request workflow
- 31 contributors already collaborating

**Sponsorship:**

The project accepts sponsorship from companies and individuals, with current sponsors including Contextual AI, CodeRabbit, and iGPT. Over 20,000 AI enthusiasts subscribe to the DiamantAI newsletter for cutting-edge insights and exclusive early access to related content.

**Technical Stack:**

- Languages: Jupyter Notebook (94.9%), Python (5.1%)
- Frameworks: LangChain, LlamaIndex
- Topics: Python, AI, tutorials, RAG, LLM, embeddings, semantic search

**Value for Context Engineering:**

This repository is essential for context engineering because it provides:

1. **Comprehensive Coverage:** From foundational techniques to advanced architectures, covering every aspect of context retrieval and management
2. **Practical Implementation:** Working code examples demonstrating how to implement each technique
3. **Quality vs. Quantity Trade-offs:** Techniques like chunking, compression, and filtering address the core context engineering challenge of maximizing signal-to-noise ratio
4. **Dynamic Context Management:** Adaptive and iterative techniques show how to manage context over multiple turns
5. **Evaluation Frameworks:** Tools for measuring whether context engineering efforts are working
6. **Advanced Architectures:** Graph RAG, RAPTOR, Self-RAG, and Corrective RAG demonstrate sophisticated approaches to context management

**Target Audience:**

This resource serves multiple levels:
- **Beginners:** Foundational techniques with clear explanations
- **Intermediate Practitioners:** Advanced retrieval methods and context enrichment
- **Advanced Researchers:** Cutting-edge architectures and evaluation frameworks
- **Production Engineers:** Practical, deployable implementations with real-world applicability

This repository represents the state-of-the-art in RAG techniques and is an indispensable resource for anyone serious about building effective context engineering systems for LLM applications.

---

Title: How Long Contexts Fail
Tags: agent failures, context clash, context confusion, context distraction, context engineering, context failures, context poisoning, context windows, LLM performance, long-context, MCP, tool calling
URL: https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html
<br/>
Summary:<br/>
This influential article by Drew Breunig challenges the common assumption that longer context windows automatically enable better AI agents. While frontier models now support up to 1 million tokens, simply throwing everything into the prompt often causes agents to fail in surprising ways. The article identifies and explains four distinct context failure modes that become especially problematic for agentic workflows.

**Context Poisoning:** When hallucinations or errors enter the context and are repeatedly referenced, corrupting subsequent reasoning. The Gemini 2.5 technical report documented this issue in their Pokémon-playing agent, where the agent would hallucinate game state information that poisoned the "goals" section of context. The agent would then develop nonsensical strategies pursuing impossible or irrelevant goals. Once the context is poisoned with misinformation, it can take a very long time to undo.

**Context Distraction:** When context grows so long that the model over-focuses on context history, neglecting what it learned during training. The Gemini Pokémon agent demonstrated this clearly—as context grew significantly beyond 100K tokens, the agent favored repeating actions from its vast history rather than synthesizing novel plans. This highlights an important distinction: long-context works well for retrieval and summarization, but struggles with multi-step generative reasoning. A Databricks study found model correctness began falling around 32K tokens for Llama 3.1 405B, even earlier for smaller models. If models misbehave long before context windows are filled, what's the point of super large windows? Answer: summarization and fact retrieval. For other tasks, be wary of your model's "distraction ceiling."

**Context Confusion:** When superfluous content in the context causes the model to generate low-quality responses. The Berkeley Function-Calling Leaderboard shows every model performs worse when provided with more than one tool. The problem worsens with smaller models—a recent paper showed a quantized Llama 3.1 8B failed on GeoEngine benchmark when given all 46 tools (well within its 16K context window), but succeeded when given only 19 tools. The fundamental issue: if you put something in context, the model must pay attention to it. Even irrelevant information or needless tool definitions will be taken into account. This has major implications for MCP adoption—connecting to every tool and stuffing all tool descriptions into prompts will cause context confusion.

**Context Clash:** When information and tools accumulated in context directly conflict with other context information. A Microsoft and Salesforce paper documented this by "sharding" benchmark prompts across multiple conversation turns rather than providing all information at once. The sharded prompts yielded dramatically worse results, with an average 39% performance drop. Even OpenAI's o3 dropped from 98.1 to 64.1 accuracy. The problem: LLMs often make premature assumptions in early turns and attempt to generate final solutions before having complete information. These incorrect early answers remain in context and influence final responses. "When LLMs take a wrong turn in a conversation, they get lost and do not recover." This is particularly problematic for agents that assemble context from documents, tool calls, and other models—all with potential to disagree. Connecting to MCP tools you didn't create increases the chance their descriptions clash with your prompt.

**Key Insights:**

The arrival of million-token context windows felt transformative, inspiring visions of superintelligent assistants with access to any document, every tool, and perfect memory. But bigger contexts create new failure modes. These failures hit agents hardest because agents operate in exactly the scenarios where contexts balloon: gathering information from multiple sources, making sequential tool calls, engaging in multi-turn reasoning, and accumulating extensive histories.

Long contexts kneecapped RAG enthusiasm (no need to find the best doc when you can fit it all!), enabled MCP hype (connect to every tool!), and fueled agent enthusiasm. But in reality, longer contexts do not automatically generate better responses. Overloading context causes surprising failures.

The article emphasizes that managing context is the key to successful agents, not simply maximizing context window utilization. It promises a follow-up article covering techniques for mitigating or avoiding these issues, from methods for dynamically loading tools to "context quarantines."

This article is essential reading for understanding why context engineering matters and why simply stuffing everything into ever-larger context windows is not a viable strategy for building reliable agents.

---

Title: How to Fix Your Context
Tags: compaction, context engineering, context offloading, context pruning, context quarantine, multi-agent, RAG, sub-agents, summarization, tool calling, tool selection
URL: https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html
<br/>
Summary:<br/>
This follow-up article by Drew Breunig provides practical solutions for the context failure modes identified in "How Long Contexts Fail." The core insight across all tactics: context is not free—every token influences the model's behavior, for better or worse. Massive context windows are powerful capabilities but not an excuse to be sloppy with information management. The article presents six tactical approaches for context management.

**RAG (Retrieval-Augmented Generation):** Selectively adding relevant information to help the LLM generate better responses. Despite recurring "RAG is Dead" debates whenever models increase context windows (most recently with Llama 4 Scout's 10 million token window), RAG remains very much alive. The temptation to "throw it all in" is strong, but treating your context like a junk drawer means the junk will influence your response. RAG prevents context confusion by ensuring only relevant information enters the context.

**Tool Loadout:** Selecting only relevant tool definitions to add to your context, borrowing the gaming term "loadout" (the specific combination of abilities, weapons, and equipment selected before a level). The simplest approach is applying RAG to tool descriptions. The "RAG MCP" paper by Tiantian Gan and Qiyao Sun demonstrated that when prompting DeepSeek-v3, tool selection becomes critical above 30 tools—descriptions begin to overlap, creating confusion. Beyond 100 tools, the model virtually guaranteed failure. Using RAG techniques to select fewer than 30 tools yielded dramatically shorter prompts and up to 3× better tool selection accuracy.

For smaller models, problems begin earlier. The "Less is More" paper showed Llama 3.1 8B fails a benchmark with 46 tools but succeeds with only 19 tools—the issue is context confusion, not context window limitations. The team developed an LLM-powered tool recommender that reasons about the "number and type of tools it 'believes' it requires." This output is then semantically searched to determine the final loadout. Testing with Berkeley Function Calling Leaderboard found Llama 3.1 8B performance improved 44%. Even when dynamic tool selection didn't improve results, power savings and speed gains (18% and 77% respectively) justified the effort—crucial metrics when operating at the edge (running LLMs on phones or PCs rather than specialized servers).

**Context Quarantine:** Isolating contexts in their own dedicated threads, each used separately by one or more LLMs. Breaking tasks into smaller, isolated jobs—each with their own context—yields better results. Anthropic's multi-agent research system demonstrates this strategy excellently. They write: "The essence of search is compression: distilling insights from a vast corpus. Subagents facilitate compression by operating in parallel with their own context windows, exploring different aspects of the question simultaneously before condensing the most important tokens for the lead research agent. Each subagent also provides separation of concerns—distinct tools, prompts, and exploration trajectories—which reduces path dependency and enables thorough, independent investigations."

Research naturally lends itself to this pattern. When given a question, several subquestions can be separately prompted using multiple agents, speeding up information gathering and distillation while keeping each context from accruing too much or irrelevant information. Anthropic's internal evaluations showed multi-agent systems excel especially for breadth-first queries involving multiple independent directions simultaneously. A multi-agent system with Claude Opus 4 as lead agent and Claude Sonnet 4 subagents outperformed single-agent Claude Opus 4 by 90.2% on their internal research eval. For example, identifying all board members of Information Technology S&P 500 companies succeeded with multi-agent decomposition while single-agent failed with slow, sequential searches.

This approach also helps with tool loadouts—designers can create several agent archetypes with dedicated loadouts and instructions. The challenge: finding opportunities for isolated tasks to spin out onto separate threads. Problems requiring context-sharing among multiple agents aren't particularly suited to this tactic.

**Context Pruning:** Removing irrelevant or otherwise unneeded information from the context. Agents accrue context as they fire off tools and assemble documents. Periodically assessing what's been assembled and removing cruft improves performance. This could be tasked to your main LLM, a separate LLM-powered tool, or something more tailored to pruning.

Context pruning has a relatively long history from pre-ChatGPT NLP field when context lengths were more problematic bottlenecks. A current method is Provence, "an efficient and robust context pruner for Question Answering." Provence is fast, accurate, simple to use, and relatively small (only 1.75 GB). The article demonstrates Provence editing down a Wikipedia article by 95%, leaving only relevant content for the query "What are my options for leaving Alameda?"

This pattern argues strongly for maintaining a structured version of your context in a dictionary or other form, from which you assemble a compiled string prior to every LLM call. This structure helps when pruning, ensuring main instructions and goals are preserved while document or history sections can be pruned or summarized.

**Context Summarization:** Boiling down an accrued context into a condensed summary. This first appeared as a tool for dealing with smaller context windows—as chat sessions approached maximum context length, a summary would be generated and a new thread would begin. Users did this manually in ChatGPT or Claude, asking the bot to generate a short recap for pasting into a new session.

As context windows increased, agent builders discovered benefits beyond staying within total context limits. As context grows, it becomes distracting, causing the model to rely less on training data (Context Distraction). The Pokémon-playing Gemini agent discovered anything beyond 100,000 tokens triggered this behavior—the agent favored repeating actions from vast history rather than synthesizing novel plans. This highlights an important distinction: long-context works well for retrieval, but struggles with multi-step generative reasoning.

Summarizing context is easy to do but hard to perfect for any given agent. Knowing what information should be preserved and detailing that to an LLM-powered compression step is critical. Worth breaking out this function as its own LLM-powered stage or app to collect evaluation data that can inform and optimize this task directly.

**Context Offloading:** Storing information outside the LLM's context, usually via a tool that stores and manages data. The author notes this might be his favorite tactic because it's so simple you don't believe it will work.

Anthropic's write-up details their "think" tool, essentially a scratchpad (though the author wishes it were called "scratchpad" for clarity—the name "think" clashes with "extended thinking" and needlessly anthropomorphizes the model). It's a place for the model to write down notes that don't cloud its context but remain available for later reference.

Having a space to log notes and progress works. Anthropic shows pairing the "think" tool with domain-specific prompts yields significant gains—up to 54% improvement against benchmarks for specialized agents. Anthropic identified three scenarios where context offloading is useful: (1) Tool output analysis—when Claude needs to carefully process previous tool calls before acting and might need to backtrack; (2) Policy-heavy environments—when Claude needs to follow detailed guidelines and verify compliance; and (3) Sequential decision making—when each action builds on previous ones and mistakes are costly (often found in multi-step domains).

**Key Takeaway:**

Context management is usually the hardest part of building an agent. Programming the LLM to "pack the context windows just right" (Karpathy), smartly deploying tools, information, and regular context maintenance is the job of the agent designer. As you build or optimize agents, ask yourself: Is everything in this context earning its keep? If not, you now have six ways to fix it.

---

Title: Onboarding for coding agents
Tags: code agents, constraints, context engineering, documentation, OODA loop, onboarding, quality gates, testing, type checking
URL: https://www.fuzzycomputer.com/posts/onboarding
<br/>
Summary:<br/>
This practical article by Holden Matt shares a remarkably simple yet effective approach to context engineering for coding agents (Claude Code, Cursor, Codex, Jules, etc.). The author reduced their CLAUDE.md file from hundreds of lines to just 13 by following two principles: (1) Put context in READMEs (universal and tool-agnostic), and (2) Put constraints in the environment via tools (type checkers, linters, formatters, tests).

**The Problem with Tool-Specific Context Files:**

Each coding agent wants context in different places—Cursor uses `.cursor/rules`, Claude Code looks for `CLAUDE.md`, Codex and Jules want `AGENTS.md` (plus `.windsurfrules`, `.clinerules`, `.github/copilot-instructions.md`, etc.). The author used to put hundreds of lines of context in these tool-specific formats, leading to duplication and maintenance burden.

**Solution 1: Put Context in READMEs**

READMEs have worked well for 50 years as a universal, tool-agnostic format for project context, already familiar to every developer. Instead of cramming everything into one long README, the author uses a simple naming convention to create composable context for different domains:

- `README.md` - High-level overview (for the project or a package/module)
- `README.<domain>.md` - Focused context for a specific domain or purpose

Examples of domain-specific READMEs:
- `README.architecture.md` - App structure, key architectural decisions, data flow, patterns to follow when adding new features
- `README.commands.md` - Key development commands and scripts
- `README.design.md` - Design system, components, visual guidelines
- `README.testing.md` - Testing patterns and strategies

This convention keeps context more modular and DRY (Don't Repeat Yourself).

**The Onboarding Mental Model:**

The key insight: think of context as onboarding for both human teammates and AI tools. Ask yourself: if a new software engineer or designer joined this project tomorrow, what would you want them to read before they start on their first task? That's the type of context you should put in READMEs.

The crucial realization: every new Cursor or Claude Code session is like a new teammate joining the project with zero context. If you don't first get them up to speed, how will they do a good job on the tasks you give them?

The author's entire CLAUDE.md onboarding section now reads:

```
## Onboarding

At the start of each session, read:
1. Any `**/README.md` docs across the project
2. Any `**/README.*.md` docs across the project
```

The `**` wildcard matches files in any subdirectories, not just the root folder. Now that context is in READMEs, it's easy to reuse it across multiple tools. However AI coding tools evolve in the future, clear written communication will always be valuable.

**Solution 2: Quality Gates (Constraints in the Environment)**

The author used to list various rules and coding preferences in `.cursorrules` or `CLAUDE.md` files. Now the goal is to encode as many constraints as possible in the environment, via tools rather than prompts. These "Quality Gates" are whatever checks you'd want to run before a new engineer pushes to production.

Example from a NextJS/TypeScript project:

```
## Quality Gates

When writing code, Claude must not finish until all of these succeed:

1. `pnpm type-check`
2. `pnpm format`
3. `pnpm lint`
4. All unit tests (`pnpm test:run`) pass

If any check fails, fix the issues and run checks again.
```

This works well because LLMs are terrible at formatting whitespace, sorting imports and Tailwind classes consistently, or ensuring every React hook's dependency array is correct. But they're good at running tools and fixing errors until all checks pass.

The specific gates depend on your stack—ESLint/Prettier in TypeScript, ruff/pytest in Python, or go fmt/vet/test in Go. The key is to load up constraints and make them strict.

With these two sections (Onboarding and Quality Gates), the entire CLAUDE.md file is now 13 lines.

**Software Gets an OODA Loop:**

Why does this Quality Gates pattern suddenly work so well? It didn't work a year ago, but newer models (like Sonnet 4) and tools (like Claude Code) mean coding agents can now iterate for minutes or even hours until all specified constraints pass.

This represents a deeper shift: coding agents can now run their own OODA loop (Observe, Orient, Decide, Act). Instead of just executing instructions or predicting tokens, they can observe outcomes and adapt to feedback from their environment. When Claude writes code, it sees type errors and fixes them. It runs linters and adjusts. It works in a loop until all constraints pass—similar to how a junior engineer would use IDE or compiler feedback to fix mistakes.

Humans have been tool builders for thousands of years, but we've always operated the OODA loop ourselves. Now we're building tools with their own primitive OODA loops.

**Define the Laws of Physics:**

"Vibe coding" (where AI handles implementation while you focus on outcomes) is very fun and fast, but without good constraints, it's easy to make a mess.

The author's rule: never let AI vibe code your environment. Define the laws of physics yourself—the tech stack, components, libraries, database, deployment setup, design system, etc. These can be expensive to change later, and they define many of a project's constraints. Then let AI work within those constraints.

When needing a new library, the author asks Claude for options and trade-offs, but always makes the choice personally after reviewing docs. A bad dependency choice can derail a project, while solid abstractions are a joy to build on.

Strict laws of physics give more confidence in what AI tools are doing and make code review much easier. They also help with speed—no time wasted reviewing or testing half-baked AI code before every constraint passes.

**Key Insights:**

This article demonstrates a practical, production-tested approach to context engineering for coding agents. By separating concerns—context in universal, composable READMEs and constraints in the environment via tools—the author achieves a maintainable system that works across different AI coding tools. The onboarding metaphor provides an intuitive framework for deciding what context to provide, while quality gates ensure reliable output without verbose prompt engineering.

The emergence of OODA loops in coding agents represents a significant capability shift, enabling iterative improvement rather than one-shot generation. This makes constraint-based approaches more effective than verbose instructions.

---

Title: The Hungry, Hungry AI Model
Tags: caching, context engineering, cost optimization, input tokens, input-output ratio, latency, LLM performance, output tokens, token budget
URL: https://tomtunguz.com/input-output-ratio/
<br/>
Summary:<br/>
This data-driven article by Tomasz Tunguz (GP at Theory Ventures, former Google PM) challenges common assumptions about LLM token economics by revealing the actual input-to-output ratio in AI model interactions. The findings have profound implications for context engineering, cost management, and system architecture.

**The Core Finding: Input-to-Output Ratio**

When AI models query for information to answer questions, practitioners initially assumed the input was approximately 20× larger than the output. However, experiments with Gemini tool command line interface, which outputs detailed token statistics, revealed the actual ratio is dramatically higher: **300× on average and up to 4000×**.

This means that for every token the model generates in its response, it processes 300 tokens of input context on average, with some queries requiring as much as 4000 tokens of input per output token.

**Why This High Input-to-Output Ratio Matters:**

**1. Cost Management is All About the Input**

With API calls priced per token, a 300:1 ratio means costs are dictated by the context, not the answer. This pricing dynamic holds true across all major models.

Even though output tokens are more expensive per token, the sheer volume difference overwhelms this. On OpenAI's pricing page, output tokens for GPT-4.1 are 4× as expensive as input tokens. However, when the input is 300× more voluminous, **the input costs are still 98% of the total bill**.

This completely reframes the cost optimization challenge—reducing input token count has 50× more impact on total costs than optimizing output length.

**2. Latency is a Function of Context Size**

An important factor determining how long a user waits for an answer is the time it takes the model to process the input. Since input tokens dominate the token count, reducing input size directly improves response time. Context engineering for latency optimization means minimizing the input token footprint while maintaining answer quality.

**3. It Redefines the Engineering Challenge**

This observation proves that the core challenge of building with LLMs isn't just prompting—**it's context engineering**.

The critical task is building efficient data retrieval and context: crafting pipelines that can find the best information and distilling it into the smallest possible token footprint. Rather than focusing on how to phrase outputs or craft clever prompts, the engineering effort should focus on:
- Retrieval efficiency (finding the right information)
- Context distillation (reducing token count while preserving signal)
- Context relevance (ensuring every input token contributes to answer quality)

**4. Caching Becomes Mission-Critical**

If 99% of tokens are in the input, building a robust caching layer for frequently retrieved documents or common query contexts moves from a "nice-to-have" to a **core architectural requirement** for building a cost-effective and scalable product.

Caching strategies that seemed marginally valuable when focused on output tokens become essential when input tokens dominate. For applications with repeated queries or common context patterns, implementing prompt caching or context caching can reduce costs by orders of magnitude.

**Strategic Implications:**

For developers, this means **focusing on input optimization is a critical lever** for:
- **Controlling costs:** Since input represents 98%+ of token costs, input optimization has 50× more impact than output optimization
- **Reducing latency:** Processing time is dominated by input token count
- **Building successful AI-powered products:** Efficient context engineering is the core engineering challenge, not just prompt engineering

**The Context Engineering Imperative:**

This article provides quantitative evidence for what context engineering practitioners have been advocating: the value of AI applications is determined by the quality and efficiency of context management. With input-to-output ratios of 300:1 or higher, every engineering decision about what context to include, how to structure it, and how to cache it has direct impact on product economics and user experience.

The "hungry, hungry AI model" metaphor captures the reality that models consume vast amounts of input context relative to their output. Building successful AI products requires treating context engineering as a first-class discipline, not an afterthought to prompt engineering.

---

Title: Getting AI to Work in Complex Codebases
Tags: agent workflows, brownfield codebases, code agents, code review, compaction, context engineering, context windows, human-in-the-loop, mental alignment, spec-driven development, sub-agents
URL: https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
<br/>
Summary:<br/>
This comprehensive guide by Dex from HumanLayer (author of the 12-Factor Agents) addresses the widely-acknowledged problem that AI coding tools struggle with real production codebases. The Stanford study on AI's impact on developer productivity found: (1) A lot of "extra code" shipped by AI tools ends up just reworking the slop shipped last week, and (2) Coding agents are great for new projects or small changes, but in large established codebases often make developers *less* productive.

The common response falls between "this will never work" and "maybe someday when there are smarter models." After several months of tinkering, the author demonstrates that **you can get really far with today's models if you embrace core context engineering principles**. The team has gotten Claude Code to handle 300K LOC Rust codebases, ship a week's worth of work in a day, and maintain code quality that passes expert review. They use a family of techniques called "frequent intentional compaction"—deliberately structuring how you feed context to the AI throughout the development process.

**Key Insight:** AI for coding is not just for toys and prototypes but rather a deeply technical engineering craft.

**Grounding Context:**

Two talks from AI Engineer 2025 shaped the author's thinking:

1. **Sean Grove's "Specs are the new code":** We're all vibe coding wrong. Chatting with an AI agent for two hours, specifying what you want, then throwing away all prompts while committing only the final code is like a Java developer checking in compiled binaries while throwing away source code. Sean proposes that in the AI future, specs will become the real code. In two years, you'll open Python files with about the same frequency you open hex editors to read assembly today (which for most is never).

2. **Stanford study on developer productivity:** Analyzed commits from 100K developers and found AI tools often lead to lots of rework, diminishing perceived productivity gains. AI tools work well for greenfield projects but are often counter-productive for brownfield codebases and complex tasks. Founders reported: "Too much slop," "Tech debt factory," "Doesn't work in big repos," "Doesn't work for complex systems."

The general vibe: "Maybe someday, when models are smarter..." But context engineering is all about getting the most out of *today's* models.

**What's Actually Possible Today:**

The author tested their techniques on BAML, a 300K LOC Rust codebase for a programming language working with LLMs. As at-best an amateur Rust dev who had never touched BAML before, within an hour he had a PR fixing a bug approved by the maintainer the next morning. A few weeks later, he and Vaibhav paired on shipping 35K LOC to BAML, adding cancellation support and WASM compilation—features the team estimated would take a senior engineer 3-5 days each. They got both draft PRs ready in about 7 hours.

This is built around "frequent intentional compaction"—designing your entire development process around context management, keeping utilization in the 40-60% range, and building in high-leverage human review at exactly the right points.

**The Naive Way to Manage Agent Context:**

Most start by using coding agents like chatbots—talking back and forth, vibing through a problem until running out of context, giving up, or the agent starts apologizing. A slightly smarter way is restarting when off track, discarding the session and starting fresh with more steering.

**Slightly Smarter: Intentional Compaction**

As context fills up, pause work and start over with a fresh context window. Example prompt: "Write everything we did so far to progress.md, ensure to note the end goal, the approach we're taking, the steps we've done so far, and the current failure we're working on." You can also use commit messages for intentional compaction.

**What Exactly Are We Compacting?**

What eats up context:
- Searching for files
- Understanding code flow
- Applying edits
- Test/build logs
- Huge JSON blobs from tools

All of these can flood the context window. **Compaction** is simply distilling them into structured artifacts.

**Why Obsess Over Context?**

As covered in 12-Factor Agents, LLMs are stateless functions. The only thing affecting output quality (without training/tuning models) is input quality. At any given point, a turn in an agent like Claude Code is a stateless function call: context window in, next step out.

The contents of your context window are the ONLY lever you have to affect output quality. So yeah, it's worth obsessing over.

Optimize your context window for:
1. **Correctness** (worst: incorrect information)
2. **Completeness** (second worst: missing information)
3. **Size** (third worst: too much noise)
4. **Trajectory**

As Geoff Huntley puts it: "The name of the game is that you only have approximately 170K of context window to work with. So it's essential to use as little of it as possible. The more you use the context window, the worse the outcomes you'll get."

**Using Sub-Agents:**

Subagents are another way to manage context. Generic subagents have been a feature of Claude Code and many coding CLIs since early days. Subagents are not about playing house and anthropomorphizing roles—**subagents are about context control**.

The most common use case: let you use a fresh context window to do finding/searching/summarizing that enables the parent agent to get straight to work without clouding its context window with `Glob`/`Grep`/`Read` calls.

**What Works Even Better: Frequent Intentional Compaction**

The techniques fall under "frequent intentional compaction"—designing your ENTIRE WORKFLOW around context management, keeping utilization in the 40%-60% range (depends on problem complexity). Split into three (ish) steps (sometimes skip research and go straight to planning; sometimes do multiple passes of compacted research before implementing):

**1. Research:** Understand the codebase, files relevant to the issue, how information flows, and perhaps potential causes of a problem. The team has a research prompt that currently uses custom subagents, but a generic version using Claude Code Task() tool with `general-agent` works almost as well.

**2. Plan:** Outline the exact steps to fix the issue, and the files you'll need to edit and how, being super precise about testing/verification steps in each phase. The plan becomes the source of truth for what's being built and why.

**3. Implement:** Step through the plan, phase by phase. For complex work, often compact the current status back into the original plan file after each implementation phase is verified. This is the only step that needs to be done in a worktree; everything else happens on main.

**Putting This Into Practice (BAML Example):**

The author picked a bug from the BAML repo and got to work. Worth noting: amateur Rust dev at best, never touched BAML codebase before.

- **Research Phase:** Created research, read it. Claude decided bug was invalid and codebase was correct. Threw out research and kicked off new one with more steering.
- **Planning Phase:** While research was running, kicked off a plan with no research to see if Claude could go straight to implementation. Also kicked off another plan using research results. Plans differed significantly—fixed issue in different ways with different testing approaches. Both "would have worked" but the one built with research fixed the problem in the *best* place and prescribed testing in line with codebase conventions.
- **Implementation:** Ran both plans in parallel and submitted both as PRs before signing off. By 10am PT next day, the PR from the plan with research was already approved by the maintainer, who didn't even know this was for a podcast.

Out of original 4 goals:
- ✅ Works in brownfield codebases (300K LOC Rust project)
- ✅ Solves complex problems (more examples followed)
- ✅ No slop (PR merged)
- ✅ Keeps mental alignment

**This is Not Magic:**

Remember the part where the author read research and threw it out because it was wrong? Or spending DEEPLY ENGAGED FOR 7 HOURS? You have to engage with your task when doing this or IT WILL NOT WORK.

There's a certain type of person always looking for the one magic prompt that will solve all their problems. It doesn't exist. Frequent Intentional Compaction via research/plan/implement flow makes performance **better**, but what makes it **good enough for hard problems** is building high-leverage human review into your pipeline.

**On Human Leverage:**

A bad line of code is just a bad line of code. But a bad line of a **plan** could lead to hundreds of bad lines of code. And a bad line of **research**, a misunderstanding of how the codebase works or where certain functionality is located, could land you with thousands of bad lines of code.

So you want to **focus human effort and attention** on the HIGHEST LEVERAGE parts of the pipeline. When you review research and plans, you get more leverage than when you review code.

**What is Code Review For?**

The author prefers Blake Smith's framing in "Code Review Essentials for Software Teams": the most important part of code review is mental alignment—keeping team members on the same page as to how the code is changing and why.

Those 2K line golang PRs were the biggest source of internal unrest and frustration—the author was starting to lose touch with what their product was and how it worked. Anyone who's worked with a very productive AI coder has had this experience.

A guaranteed side effect of everyone shipping way more code is that a much larger proportion of your codebase will be unfamiliar to any given engineer at any point in time. You ABSOLUTELY need an engineering process that:
1. Keeps team members on the same page
2. Enables team members to quickly learn about unfamiliar parts of the codebase

For most teams, this is pull requests and internal docs. For this team, it's now specs, plans, and research. The author can't read 2000 lines of golang daily, but *can* read 200 lines of a well-written implementation plan.

**Recap:**

Basically they got everything needed:
- ✅ Works in brownfield codebases
- ✅ Solves complex problems
- ✅ No slop
- ✅ Maintains mental alignment

(And their team of three is averaging about $12K on Opus per month)

This does not work perfectly for every problem. The team spent 2 weeks spinning on a really tricky race condition that spiraled into rabbit holes. But that's the exception now. In general, this works well. Their intern shipped 2 PRs on his first day, and 10 on his 8th day. The author was genuinely skeptical it would work for anyone else, but he and Vaibhav shipped 35K LOC of working BAML code in 7 hours (and Vaibhav is one of the most meticulous engineers when it comes to code design and quality).

**Key Philosophical Insight:**

The author is reasonably confident that coding agents will be commoditized. The hard part will be the team and workflow transformation. Everything about collaboration will change in a world where AI writes 99% of our code. If you don't figure this out, you're going to get lapped by someone who did.

This article provides one of the most comprehensive, battle-tested guides to context engineering for coding agents available today, demonstrating that with proper context management, today's models can handle complex production codebases effectively.

---

Title: Context Engineering - The Evolution Beyond Prompt Engineering
Tags: agents, attention management, caching, context engineering, error recovery, KV-cache, memory, prompt engineering, systems design, tools, workflow orchestration
URL: https://www.vincirufus.com/posts/context-engineering/
<br/>
Summary:<br/>
See notes: This article discusses context engineering as a discipline and how it differs from prompt engineering.

Context engineering is the discipline of building dynamic systems that supply an LLM with everything it needs to accomplish a task. Unlike prompt engineering, which focuses on crafting individual instructions, context engineering takes a systems-level approach encompassing the entire information ecosystem—memory, retrieval systems, tool integrations, and dynamic information flow across multiple interactions. Prompt engineering is a subset of context engineering; prompting tells the model how to think, while context engineering gives the model the training and tools to complete the job.

**Core Principles from Production Experience:**

1. **Design Around the KV-Cache:** The KV-cache hit rate is the most critical metric for production AI agents, directly affecting latency and cost. Keep prompt prefixes stable, make context append-only, use deterministic serialization, and mark cache breakpoints explicitly. With Claude Sonnet, cached tokens cost $0.30/MTok versus $3/MTok uncached—a 10x difference.

2. **Mask, Don't Remove:** Rather than removing tools from context, mask token logits during decoding to prevent/enforce action selection based on current context. This maintains KV-cache validity and prevents model confusion when previous actions reference now-absent tools.

3. **Use the File System as Context:** Modern LLMs offer large context windows, but in real-world agentic scenarios, that's often insufficient. The file system serves as ultimate context—unlimited in size, persistent, directly operable by agents, enables compression strategies that are restorable, and allows models to externalize long-term state.

4. **Manipulate Attention Through Recitation:** Constantly rewriting the todo list recites objectives into the end of context, pushing the global plan into the model's recent attention span. This avoids "lost-in-the-middle" issues and reduces goal misalignment by using natural language to bias the model's focus.

5. **Keep the Wrong Stuff In:** Counter-intuitively, preserving failure traces is highly effective. When models see failed actions and resulting observations/stack traces, they implicitly update internal beliefs, shifting priors away from similar actions and reducing repeated mistakes. Error recovery is a clear indicator of true agentic behavior.

6. **Don't Get Few-Shotted:** While few-shot prompting is valuable for prompt engineering, it can backfire in agent systems. Models are excellent mimics; contexts full of similar past action-observation pairs cause the model to follow that pattern even when no longer optimal. Introduce structured variation—different serialization templates, alternate phrasing, and controlled randomness to break patterns.

**Practical Implementation Strategies:**

- **Memory Management:** Requires hierarchical memory (system prompt, session memory, working memory), selective compression (preserve essential context while compressing verbose observations), and memory indexing (enable efficient retrieval of past interactions).

- **Tool Integration:** Dynamic tool loading (runtime discovery and integration), tool state management (tracking availability and constraints), and result contextualization (meaningfully integrating tool outputs into ongoing context).

- **Workflow Orchestration:** State machines (managing agent behavior across contexts), context transitions (seamless handoffs between operational modes), and error recovery (graceful failure handling while preserving context).

Context engineering represents the maturation of AI systems from experimental tools to production infrastructure. While prompt engineering remains valuable for specific applications, context engineering provides the systematic framework necessary for building reliable, scalable AI agents. Prompt engineering gets the first good output; context engineering ensures the 1,000th output is still good.

---

Title: What Makes 5% of AI Agents Actually Work in Production?
Tags: agents, context engineering, context observability, governance, memory, multi-model orchestration, production, RAG, security, semantic layers, trust, UX design
URL: https://www.motivenotes.ai/p/what-makes-5-of-ai-agents-actually
<br/>
Summary:<br/>
This article reports on a San Francisco panel discussion featuring engineers from Uber, WisdomAI, EvenUp, and Datastrato about context engineering and production AI agents. Key finding: 95% of AI agent deployments fail in production, not due to model limitations but because the scaffolding—context engineering, security, memory design—isn't properly implemented. The metaphor: "The base models are the soil; context is the seed."

**Context Engineering != Prompt Hacking:**

Most RAG systems today are too naive, with three failure modes: (1) index everything → retrieve too much → confuse the model; (2) index too little → starve the model of signal; (3) mix structured + unstructured data → break embeddings or flatten key schema.

Advanced context engineering approaches:

- **Feature Selection for LLMs:** Reframe context engineering as LLM-native feature engineering—selective context pruning equals feature selection, context validation equals schema/type/recency checks, context observability traces which inputs improved/worsened output quality, and embedding augmentation with metadata equals typed features + conditions. This means treating context like a versioned, auditable, testable artifact, not a string blob.

- **Semantic + Metadata Layering:** Dual-layer architectures with (1) semantic layer for classic vector search and (2) metadata layer enforcing filters based on document type, timestamp, access permissions, or vertical ontology. This hybrid normalizes messy input formats (PDFs, audio, logs, metrics) ensuring retrieval of relevant structured knowledge, not just "similar content." Includes taxonomies, entity linking, and domain-specific schemas on top of embeddings.

- **Text-to-SQL Reality Check:** When asked how many audience members built text-to-SQL in production, not a single hand went up. Query understanding is brutally hard—natural language is ambiguous, business terminology is domain-specific, and LLMs don't know company-specific definitions without extensive context engineering. Successful teams build business glossaries with term mappings, query templates with constraints, validation layers catching semantic errors before execution, and feedback loops improving understanding over time.

**Governance & Trust Are Not "Enterprise Only" Problems:**

Security, lineage, and permissioning are deployment blockers. Key requirements: trace which inputs led to which outputs (lineage), respect row-level, role-based access (policy gating), and allow user-specific output even if prompts are identical. "If two employees ask the same question, the model output should differ because they have different permissions." Without these controls, agents may be functionally right but organizationally wrong, leaking access or violating compliance. Leading pattern: unified metadata catalogs for structured + unstructured data with embedded access policies at index + query time.

The trust problem is human, not technical. A panelist's wife refuses Tesla autopilot not because it doesn't work, but because she doesn't trust it. "When AI touches very sensitive parts about your safety, your money, did you trust AI?" This barrier exists for enterprise AI agents making decisions about revenue recognition, medical records, or compliance. The successful 5% of AI agents all have human-in-the-loop design, positioning AI as assistant, not autonomous decision maker, with feedback loops where systems learn from corrections and easy verification/override mechanisms.

**Memory Isn't Just Storage, It's Architectural:**

Memory isn't a feature—it's a design decision with UX, privacy, and system implications. Three levels: (1) User level: preferences (chart types, style, writing tone); (2) Team level: recurring queries, dashboards, runbooks; (3) Org level: institutional knowledge, policies, prior decisions. Best teams abstract it as a versioned, composable context layer + behavior layer. "Semantic memory + taxonomy + runbooks = context. Individual preferences = memory."

Memory serves two purposes at the application level: (1) customizing behavior to individual users (writing style, preferred formats, domain expertise); (2) proactive assistance based on events and metadata, not just reactive chat responses. One team built conversational BI at Uber solving the cold-start problem (users don't know what to ask) by building memory from past query logs to suggest relevant questions as conversation starters.

Design tension: Memory improves UX and agent fluency, but over-personalization crosses into privacy territory fast. One panelist described ChatGPT responding with movie recommendations tailored to his children by name: "I don't like this answer. Why do you know my son and my girl so much? Don't touch my privacy." Shared memory can break access controls unless carefully scoped. Missing primitive: a secure, portable memory layer working across apps, usable by the user, not locked inside the provider.

**Multi-Model Inference & Orchestration Patterns:**

In production, teams run model routing logic based on task complexity, latency constraints, cost sensitivity, data locality/regulatory concerns, and query type (summarization vs semantic search vs structured QA). Example pattern: trivial queries → local model (no network call); structured queries → DSL → SQL translator; complex analysis → OpenAI/Anthropic/Gemini; fallback/verification → dual-model redundancy (judge + responder). This is closer to compiler design than webapp routing—running a DAG of decisions across heterogeneous models, tools, and validations. The model selection itself can be learned over time by tracking which queries succeed with which models.

**When Is Chat Actually the Right Interface?**

Not every task needs a chatbot. Conversation works when it removes a learning curve. For complex tools like BI dashboards requiring expertise, natural language lowers the barrier to entry, but once you have an answer, users want GUI controls (switching chart types shouldn't require more typing). Hybrid pattern: start with chat for zero-learning-curve entry, provide GUI controls for refinement and iteration, let users choose mode based on task and preference. Perfect NLP use cases: (1) sporadic, emotional tasks like customer service where people want help without navigating menus; (2) exploratory, open-ended queries with complex, contextual requirements.

**What's Still Missing (Where Builders Can Win):**

- **Context Observability:** What inputs consistently improve output? What context leads to hallucination? How do you test context like you test model prompts? Most teams fly blind without systematic ways to measure which context helps vs hurts model performance.

- **Composable Memory:** Could memory live with the user (not the app), portable and secure, with opt-in layers for org vs team vs personal state? Solves two problems: users don't rebuild context in every new tool, and privacy/security are user-controlled, not vendor-locked. This is the biggest missing primitive in the stack.

- **Domain-Aware DSLs:** Most business user needs are structured and repetitive. Instead of parsing natural language into brittle SQL, define higher-level, constraint-safe DSLs. "Show me Q4 revenue" should map to a verified calculation, not raw SQL generation (semantic business logic layers).

- **Latency-Aware UX:** Different tasks have different latency requirements. A joke should be instant; deep analysis can take 10 seconds if it shows progress and feels intelligent. UX unlock for async, proactive AI: agents preparing briefings before meetings, surfacing relevant context when opening documents, alerting to data anomalies before being asked.

The next real moats in GenAI won't come from model access but from context quality, memory design, orchestration reliability, and trust UX.

---

Title: Context engineering is sleeping on the humble hyperlink
Tags: agents, context engineering, HATEOAS, hyperlinks, just-in-time, links, MCP, RAG, tools
URL: https://mbleigh.dev/posts/context-engineering-with-links/
<br/>
Summary:<br/>
This article advocates for using hyperlinks as an underutilized context engineering technique for LLMs. Context engineering addresses key limitations: conversations should be append-only to maximize cacheability, models are more responsive to "fresh" context near the end of the window, and models perform worse when overwhelmed with large amounts of context. The key tension: models need access to all valuable context, BUT ONLY when that context is relevant to the task at hand.

**Popular Context Engineering Solutions:**
- **Retrieval Augmented Generation (RAG):** Dynamically discovers and loads specific relevant context for the current query proactively.
- **Subagents:** Encapsulate specialized instructions and tools to avoid polluting the main thread.
- **get_* Tools:** Allow models to proactively request information deemed relevant using tool calls.

However, hyperlinks are woefully underutilized. When humans need to learn something (e.g., about an open source library), they Google search the topic, click a relevant link to a docs page, read a high-level guide, Cmd+Click a few more pages to open in new tabs to review, and refer between open tabs while completing the task. Once finding an entrypoint through search, they incrementally explore the topic through discovered links, filling mental context with relevant information. We can do the same thing with LLMs.

**HATEOAS in the Era of Agents:**

The power of linked data is nothing new. HATEOAS (Hypertext as the Engine of Application State) is the concept that a "truly" RESTful API should be fully self-describing, such that a client can explore and interact knowing nothing but an entrypoint in advance, with hyperlinks providing all necessary context to discover and consume additional endpoints. This never worked in practice—building hypertext APIs was too cumbersome, and humans needed to understand API structure anyway. "REST-ish" APIs with good documentation pages were more useful.

LLMs change this dramatically. When machines can not only parse but also navigate the context and relevance of hyperlinks, you have an actually useful paradigm: **Hypertext as the Engine of Agent State**. This applies to the web and HTTP APIs (expect a resurgence of hypermedia concepts to make APIs more self-documenting in coming years), but also to local data, agent-specific data, and any data we want agents to discover and read.

**One Tool to Read Them All:**

The scaffolding for implementing powerful link-based context systems is trivial, requiring only: (1) a tool accepting a list of URIs as arguments, and (2) an entrypoint bringing at least one URI into context. The article demonstrates this with ~30 lines of code using Genkit in JavaScript with system instructions as entrypoint. Testing shows exactly the hoped-for results: when no link reading is required, no links are read; when one link is sufficient, only one is read; when the model understands it needs to recursively fetch context linked from the first loaded document, it does so correctly. This creates a system that can dynamically load and correctly apply relevant context on-demand using very little prompting and a cost-effective model.

**Benefits of Links:**

Links are powerful in the context engineering toolbelt because of their simplicity, flexibility, and efficiency:

- **Trivial to implement:** Current models are "intuitively" good at understanding how to follow links.
- **Surface anywhere:** Can be specified in system prompts, provided by users, or returned by tools.
- **Token-efficient:** Use a small number of tokens to provide on-demand access to specific information. The model can load a link if needed; if not, few tokens are wasted.
- **Tool-efficient:** Consolidate many types of reads into a single tool. You can have a `data://me` link dynamically loading current user information, a `file://foo.md` link loading a local file, and a `prompt://pet-help` link returning static instructions—without needing a separate tool for each type of data.
- **Just-in-time context:** Mitigates issues of context rot and recency bias. Because linked context is loaded when needed by the model, the context is "fresher" instead of overloading a system prompt.

**MCP Resources: The Future is Now(ish):**

To make link-based context engineering universal, we need a way to provide linked content to the model. Many agents have built-in "fetch URL" or "search the web" tools automatically fetching data from public sources, but the content to link might not always be on the public internet. The exact primitive we need already exists: **MCP Resources**. Resources allow servers to register URIs (or patterns of URIs) that can then be read on-demand by clients to provide static or dynamic content.

The bad news: no MCP client currently makes MCP resources consumable by the model. Today, they only allow resources to be inserted by users via @-mentions and similar devices, which doesn't enable linking. Critical need: **Every MCP-enabled agent should expose a read_resources tool that accepts one or more URIs and aggregates reading across all connected MCP servers (and probably web URLs as well).**

Other helpful changes: a mechanism for indexing/listing available MCP resources and exposing that in system instructions, maybe even indexing MCP resources so they can be searched using RAG techniques. But just enabling agents to access linked content opens up a world of new context engineering techniques.

**Working with What You Have:**

If building your own agent, you don't need new technology to start making linked context—you can do it in a few dozen lines of code. But even when integrating with existing agents like Gemini CLI, Claude Code, or Cursor, you can still build with linked data patterns. The Firebase MCP Server recently launched new capabilities including a `/firebase:init` slash command. They built linked context into the MCP server itself: (1) added support for MCP Resources, (2) created a read_resources MCP tool capable of reading resources (from the Firebase MCP Server only), and (3) created an MCP prompt that creates a guided workflow walking the model step-by-step through configuring Firebase, including linked branching paths. Testing against several popular coding agents supporting MCP Prompts shows each is able to understand and follow hyperlinks using the MCP server's read_resources tool, making Firebase onboarding easier.

Effective context engineering is constantly evolving as models and agent harnesses improve; however, hyperlinks are such a powerfully efficient mechanism for information traversal that a future of agents without linked context is unimaginable. The next time you're thinking of building half a dozen get_* or list_* tools for your agent, consider: could the humble hyperlink get the job done instead?

---

Title: Production RAG: what I learned from processing 5M+ documents
Tags: chunking, embeddings, LLM, metadata, production, query generation, query routing, RAG, reranking, vector database
URL: https://blog.abdellatif.io/production-rag-processing-5m-documents
<br/>
Summary:<br/>
This article shares practical lessons from 8 months building production RAG systems for Usul AI (9M pages) and an unnamed legal AI enterprise (4M pages). The author started with YouTube tutorials, first Langchain then Llamaindex, achieving a working prototype in a couple of days. Testing on a subset (100 documents) produced great results, and the full production pipeline was working within a week—seemingly incredible progress.

**The Reality:**

The results were actually subpar, and only end users could tell. The following months were spent rewriting pieces of the system one at a time until performance reached desired levels.

**What Moved the Needle (Ranked by ROI):**

1. **Query Generation:** Not all context can be captured by the user's last query. An LLM reviews the thread and generates a number of semantic + keyword queries. Processing all queries in parallel and passing them to a reranker covers a larger surface area and avoids dependence on a computed score for hybrid search.

2. **Reranking:** The highest value 5 lines of code you'll add. Chunk ranking shifted significantly—more than expected. Reranking can often compensate for a bad setup if you pass in enough chunks. The ideal reranker setup found: 50 chunk input → 15 output.

3. **Chunking Strategy:** Takes the most effort; you'll probably spend most of your time on it. Custom flows were built for both enterprises. Critical steps: understand the data, review the chunks, and verify (a) chunks aren't cut mid-word or mid-sentence, and (b) each chunk is a logical unit capturing information on its own.

4. **Metadata to LLM:** Initially, only chunk text was passed to the LLM. Running an experiment found that injecting relevant metadata (title, author, etc.) improves context and answers significantly.

5. **Query Routing:** Many users asked questions that can't be answered by RAG (e.g., "summarize the article," "who wrote this"). A small router was created to detect these questions and answer them using an API call + LLM instead of the full-blown RAG setup.

**The Stack:**

- **Vector Database:** Azure → Pinecone → Turbopuffer (cheap, supports keyword search natively)
- **Document Extraction:** Custom
- **Chunking:** Unstructured.io by default, custom for enterprises (heard that Chonkie is good)
- **Embedding:** text-embedding-3-large (haven't tested others)
- **Reranker:** None → Cohere 3.5 → Zerank (less known but actually good)
- **LLM:** GPT-4.1 → GPT-5 → GPT-4.1 (covered by Azure credits)

**Going Open-source:**

All learning has been put into an open-source project: agentset-ai/agentset under an MIT license.

---

Title: Managing context on the Claude Developer Platform
Tags: agents, context editing, context management, context windows, long-running tasks, memory, performance, tools
URL: https://www.anthropic.com/news/context-management
<br/>
Summary:<br/>
See notes: The memory tool operates entirely client-side through tool calls. Developers manage the storage backend, giving them complete control over where the data is stored and how it's persisted. Context editing enables longer conversations by automatically removing stale tool results from context. Context editing clears old file reads and test results while memory preserves debugging insights and architectural decisions, enabling agents to work on large codebases without losing progress. Memory stores key findings while context editing removes old search results, building knowledge bases that improve performance over time. Agents store intermediate results in memory while context editing clears raw data, handling workflows that would otherwise exceed token limits.

Anthropic introduces new capabilities for managing agents' context on the Claude Developer Platform: context editing and the memory tool. With Claude Sonnet 4.5, these capabilities enable developers to build AI agents capable of handling long-running tasks at higher performance without hitting context limits or losing critical information.

**Context Windows Have Limits, But Real Work Doesn't:**

As production agents handle complex tasks and generate more tool results, they often exhaust their effective context windows—leaving developers stuck choosing between cutting agent transcripts or degrading performance. Context management solves this in two ways, ensuring only relevant data stays in context and valuable insights get preserved across sessions.

**Context Editing:** Automatically clears stale tool calls and results from within the context window when approaching token limits. As agents execute tasks and accumulate tool results, context editing removes stale content while preserving conversation flow, effectively extending how long agents can run without manual intervention. This also increases effective model performance as Claude focuses only on relevant context.

**Memory Tool:** Enables Claude to store and consult information outside the context window through a file-based system. Claude can create, read, update, and delete files in a dedicated memory directory stored in your infrastructure that persists across conversations. This allows agents to build up knowledge bases over time, maintain project state across sessions, and reference previous learnings without keeping everything in context. The memory tool operates entirely client-side through tool calls, with developers managing the storage backend for complete control over data storage and persistence.

Claude Sonnet 4.5 enhances both capabilities with built-in context awareness—tracking available tokens throughout conversations to manage context more effectively. Together, these updates create a system that improves agent performance by enabling longer conversations through automatic removal of stale tool results and boosting accuracy by saving critical information to memory and bringing that learning across successive agentic sessions.

**Building Long-Running Agents:**

Claude Sonnet 4.5 is the best model in the world for building agents. These features unlock new possibilities for long-running agents—processing entire codebases, analyzing hundreds of documents, or maintaining extensive tool interaction histories. Context management ensures agents can leverage this expanded capacity efficiently while handling workflows that extend beyond any fixed limit. Use cases include:

- **Coding:** Context editing clears old file reads and test results while memory preserves debugging insights and architectural decisions, enabling agents to work on large codebases without losing progress.

- **Research:** Memory stores key findings while context editing removes old search results, building knowledge bases that improve performance over time.

- **Data Processing:** Agents store intermediate results in memory while context editing clears raw data, handling workflows that would otherwise exceed token limits.

**Performance Improvements with Context Management:**

On an internal evaluation set for agentic search, testing showed how context management improves agent performance on complex, multi-step tasks. The results demonstrate significant gains: combining the memory tool with context editing improved performance by 39% over baseline. Context editing alone delivered a 29% improvement. In a 100-turn web search evaluation, context editing enabled agents to complete workflows that would otherwise fail due to context exhaustion—while reducing token consumption by 84%.

**Getting Started:**

These capabilities are available in public beta on the Claude Developer Platform, natively and in Amazon Bedrock and Google Cloud's Vertex AI.

---

Title: Memory & Context Management with Claude Sonnet 4.5
Tags: agents, client-side implementation, code review, compaction, context editing, context engineering, context management, context windows, cross-conversation learning, learning patterns, memory, structured note-taking, tools, tutorial
URL: https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb
<br/>
Summary:<br/>
This practical Jupyter notebook cookbook demonstrates implementations of context engineering patterns using Claude Sonnet 4.5's memory tool and context editing capabilities. The cookbook provides hands-on examples of building AI agents that learn and improve across conversations, focusing on a code review assistant use case.

**The Problem Addressed:**

Large language models have finite context windows (200k tokens for Claude 4), creating several challenges:
- Context limits: Long conversations or complex tasks can exceed available context
- Computational cost: Processing large contexts is expensive as attention mechanisms scale quadratically
- Repeated patterns: Similar tasks across conversations require re-explaining context every time
- Information loss: When context fills up, earlier important information gets lost

**Two Key Solutions:**

1. **Memory Tool (`memory_20250818`):** Enables cross-conversation learning where Claude can write down what it learns for future reference. The file-based system operates under a `/memories` directory with full client-side control. Commands include view, create, str_replace, insert, delete, and rename operations on memory files.

2. **Context Editing (`clear_tool_uses_20250919`):** Automatically manages context by clearing old tool results when context grows large while preserving recent context and memory. Features configurable triggers and retention policies.

**Benefits:**

Agents get better at specific tasks over time: In Session 1, Claude solves a problem and writes down the pattern. In Session 2, Claude applies the learned pattern immediately (faster response). For long sessions, context editing keeps conversations manageable without losing critical learnings.

**Use Cases Demonstrated:**

- **Code Review Assistant:** Learns debugging patterns from past reviews, recognizes similar bugs instantly in future sessions, builds team-specific code quality knowledge. Production-ready integration available with claude-code-action for GitHub PR reviews.
- **Research Assistant:** Accumulates knowledge across multiple sessions, connects insights across research threads, maintains bibliography tracking.
- **Customer Support Bot:** Learns user preferences and communication style, remembers common issues and solutions, builds product knowledge base.
- **Data Analysis Helper:** Remembers dataset patterns and anomalies, stores successful analysis techniques, builds domain-specific insights.

**How It Works:**

The memory tool architecture is entirely client-side—developers control storage while Claude makes tool calls that the application executes. The conversation loop continuously calls the API while tool uses exist, executing them and feeding results back. The key pattern demonstrates semantic pattern recognition, not just syntax. For example, after learning about race conditions in thread-based code (Session 1), Claude immediately recognizes similar patterns in async code (Session 2) without re-learning—applying stored knowledge about shared mutable state across different contexts.

**What Claude Learns:**

Claude stores architectural insights including symptoms (inconsistent results in concurrent operations), causes (shared mutable state modified from multiple threads), solutions (use locks, thread-safe data structures, or return results), and red flags (instance variables in thread callbacks). This knowledge applies cross-language (Go, Java, Rust concurrency) and improves with each review.

**Context Clearing While Preserving Memory:**

During long review sessions, context fills with tool results from previous reviews, but memory must persist. Context editing triggers automatically when input tokens exceed thresholds, removing old tool results while keeping memory files intact. This demonstrates the critical distinction:
- Short-term memory (conversation context with tool results) → Cleared to save space
- Long-term memory (stored patterns in `/memories`) → Persists across sessions

**Implementation Details:**

The cookbook includes helper functions (`run_conversation_loop()`, `run_conversation_turn()`, `print_context_management_info()`) and sample code files with intentional concurrency bugs for demonstration. The memory handler implements path validation and security measures. Context management configuration is available through beta features with adjustable token thresholds for when to trigger clearing.

**Supported Models:** Claude Opus 4.1 (`claude-opus-4-1`) and Claude Sonnet 4.5 (`claude-sonnet-4-5`)

The cookbook provides a complete, reproducible environment for learning these patterns, including setup instructions, code examples, and best practices for production deployment. It demonstrates how giving Claude a "notebook" to take notes and refer back to—just like humans do—creates agents that genuinely improve over time.

---

Title: Context Engineering Series for Agentic RAG Systems
Tags: agent architecture, agent trajectory, agent workflows, agents, agentic RAG, coding agents, compaction, context engineering, context pollution, context rot, faceted search, form factors, MCP, peripheral vision, prompt engineering, RAG, slash commands, structured outputs, subagents, tool calling, tools
URL: https://jxnl.co/writing/2025/08/28/context-engineering-index
<br/>
Summary:<br/>
This index article introduces a comprehensive series on context engineering based on insights from helping companies build agentic RAG systems and studying coding agents from Cognition, Claude Code, Cursor, and others. The series explores what makes coding agents successful and applies those learnings to other industries.

**What is Context Engineering:**

Context engineering represents the evolution beyond prompt engineering. Modern systems now involve designing portfolios of tools (directory listing, file editing, web search), slash commands like `/pr-create` that inject prompts, specialized subagents such as `@pr-creation-agent`, and instruction files like `AGENT.md` that work across IDEs, command lines, GitHub, and Slack. Context engineering is specifically about designing tool responses and interaction patterns that give agents situational awareness to navigate complex information spaces effectively.

**Evolution from RAG to Agents:**

**Before:** Systems precomputed what chunks needed to be put into context, injected them, and asked the system to reason about the chunks. Search was a one-shot operation returning top-k results with no metadata—just raw text chunks for single-turn reasoning.

**Now:** Agents are persistent, make multiple tool calls, and build understanding across conversations. They don't just need the right chunk—they need to understand the landscape of available information. The fundamental shift is that agents don't just consume information, they explore information spaces.

**Key Terms Defined:**

- **Context Engineering:** Designing tool responses and interaction patterns that teach agents how to navigate data landscapes, not just consume chunks
- **Faceted Search:** Returning metadata aggregations (counts, categories) alongside results so agents can refine queries strategically
- **Agent Peripheral Vision:** Structured hints about the broader information space beyond top-k results
- **Tool Response as Prompt Engineering:** Using structure (XML/JSON), metadata, and inline system instructions in tool outputs to shape future behavior
- **Context Pollution:** Noisy, low-signal outputs (logs, traces) that crowd out useful reasoning context
- **Context Rot:** Reliability degrading as conversations get longer and messier
- **Subagents:** Specialized sidecar agents that do token-heavy, messy reads in isolation and return distilled summaries
- **Compaction:** Summarizing conversation history to preserve essential trajectory while freeing context; treated as "momentum" in the series
- **Agent Trajectory:** The full sequence of tool calls, steps, and messages that accomplish a task
- **Form Factors:** Chatbots (conversational), workflows (side-effect engines), and research artifacts (reports/tables)
- **MCP (Model Context Protocol):** A protocol for reusable tools across clients; best when reuse and client diversity justify the overhead

**Series Articles Covered:**

1. **Beyond Chunks: Context Engineering Tool Response** - Core thesis that agent success depends on tool response structure, not just content. Shows how faceted search and metadata give agents "peripheral vision" of data landscapes. Tool responses become prompt engineering—XML structure and system instructions in tool outputs directly influence how agents think about subsequent searches.

2. **Slash Commands vs Subagents: How to Keep AI Tools Focused** - Core thesis that context pollution kills agent performance, but subagent architecture solves it. Bad context is cheap but toxic. Slash commands flood main threads with 91% noise; subagents burn tokens off-thread and return 8x cleaner context with 76% signal.

3. **Two Experiments We Need to Run on AI Agent Compaction** - Core thesis that if in-context learning is gradient descent, then compaction is momentum. Compaction can be used as both an optimization technique and a lens for understanding agent behavior at scale. Compaction timing affects learning trajectory preservation.

4. **Context Engineering: Agent Frameworks and Form Factors** - Core thesis that agent success starts with choosing the right form factor (chatbot, workflow, or research artifact) and navigating the autonomy spectrum from deterministic systems to tool-calling loops. Teams fail because they don't commit to outcomes. Provides MCP decision matrix and autonomy spectrum for making architectural choices based on economic realities.

5. **Context Engineering: Rapid Agent Prototyping** - Core thesis that most teams waste months building agent infrastructure before knowing if their idea works. Claude Code's project runner provides a faster path to evidence through folder-based testing and executable specifications. If Claude Code can't achieve your task with perfect tool access, your production version probably won't either.

**Implementation Guidance:**

The series provides recommended paths by role:
- **Engineering:** Tool Response → Rapid Prototyping → Slash vs Subagents → Compaction → Frameworks
- **Product/Leads:** Frameworks → Rapid Prototyping → Tool Response → Slash vs Subagents
- **Researchers:** Compaction → Tool Response → Slash vs Subagents → Rapid Prototyping

**Quick Start Recommendations:**
- Audit tool responses for sources and structure; add Level 2 (source metadata) immediately
- Use CLAUDE.md + CLI tools + scenario checks to validate one task end-to-end before building orchestration
- Keep test logs and heavy reads in subagents; return summaries to main thread
- Track clarification rate, expert escalations, 504s, and resolution time before/after changes
- Plan compaction strategy: choose when and how to compact; test timing and prompts on long trajectories

**Target Audience:**

Engineering teams building agentic RAG systems, product leaders evaluating ROI of agent implementations, AI researchers interested in tool design and agent cognition, and anyone curious about how agents work with structured data. Each post includes practical code examples, implementation strategies, and real business metrics from companies making this transition.

**Related Series:** The article references a Coding Agents Speaker Series (insights from teams behind Cognition/Devin, Sourcegraph/Amp, Cline, and Augment) and a RAG Master Series (comprehensive guide to building and scaling retrieval-augmented generation systems).

The central insight: The future of RAG isn't about better embeddings or larger context windows—it's about teaching agents to navigate information spaces systematically through carefully designed tool responses and interaction patterns.

---

Title: Introducing Contextual Retrieval
Tags: BM25, chunking, context engineering, contextual embeddings, contextual retrieval, cost optimization, embeddings, knowledge bases, prompt caching, RAG, reranking, retrieval, semantic search, TF-IDF, vector database
URL: https://www.anthropic.com/engineering/contextual-retrieval
<br/>
Summary:<br/>
See notes: This article addresses contextual retrieval, which is referenced in Braindumpnotes.md as a key technique for improving RAG systems.

Anthropic introduces Contextual Retrieval, a method that dramatically improves the retrieval step in RAG systems by reducing failed retrievals by 49%, and by 67% when combined with reranking. The technique solves a fundamental problem in traditional RAG: context destruction during document chunking.

**The Problem with Traditional RAG:**

For AI models to be useful in specific contexts, they need access to background knowledge (customer support needs business-specific knowledge, legal analysts need case law). Retrieval-Augmented Generation (RAG) is the standard method for enhancing AI models with this knowledge. However, traditional RAG solutions remove context when encoding information, often causing the system to fail to retrieve relevant information.

**When to Use Simple Prompting vs. RAG:**

For knowledge bases smaller than 200,000 tokens (about 500 pages), developers can include the entire knowledge base directly in the prompt, especially with prompt caching which reduces latency by >2x and costs by up to 90%. For larger knowledge bases, RAG becomes necessary.

**Traditional RAG Architecture:**

The standard RAG preprocessing flow:
1. Break knowledge base into smaller chunks (usually a few hundred tokens)
2. Convert chunks into vector embeddings using embedding models
3. Store embeddings in a vector database for semantic similarity searching
4. At runtime, find most relevant chunks based on semantic similarity to query
5. Add most relevant chunks to the prompt sent to the generative model

**The Role of BM25:**

While embedding models excel at capturing semantic relationships, they can miss crucial exact matches. BM25 (Best Matching 25) is a ranking function using lexical matching to find precise word or phrase matches, particularly effective for unique identifiers or technical terms. BM25 builds on TF-IDF (Term Frequency-Inverse Document Frequency) by considering document length and applying a saturation function to term frequency.

Traditional RAG systems combine embeddings and BM25:
1. Break knowledge base into chunks
2. Create TF-IDF encodings and semantic embeddings
3. Use BM25 for exact matches
4. Use embeddings for semantic similarity
5. Combine and deduplicate results using rank fusion techniques
6. Add top-K chunks to prompt

**The Context Conundrum:**

Traditional RAG destroys context when splitting documents into chunks. For example, a chunk stating "The company's revenue grew by 3% over the previous quarter" lacks crucial context about which company and what time period, making it difficult to retrieve or use effectively.

**Contextual Retrieval Solution:**

Contextual Retrieval prepends chunk-specific explanatory context to each chunk before embedding (Contextual Embeddings) and creating the BM25 index (Contextual BM25). Using Claude 3 Haiku, the system generates concise, chunk-specific context (50-100 tokens) that situates each chunk within the overall document.

Example transformation:
- Original: "The company's revenue grew by 3% over the previous quarter."
- Contextualized: "This chunk is from an SEC filing on ACME corp's performance in Q2 2023; the previous quarter's revenue was $314 million. The company's revenue grew by 3% over the previous quarter."

**Prompt Caching Cost Optimization:**

Contextual Retrieval is uniquely cost-effective with Claude's prompt caching. Rather than passing the reference document for every chunk, developers load the document into cache once and reference previously cached content. Assuming 800 token chunks, 8k token documents, 50 token context instructions, and 100 tokens of context per chunk, the one-time cost to generate contextualized chunks is $1.02 per million document tokens.

**Performance Results:**

Experiments across various knowledge domains (codebases, fiction, ArXiv papers, science papers), embedding models, retrieval strategies, and evaluation metrics showed:
- Contextual Embeddings alone reduced top-20-chunk retrieval failure rate by 35% (5.7% → 3.7%)
- Contextual Embeddings + Contextual BM25 reduced failure rate by 49% (5.7% → 2.9%)
- Adding reranking further reduced failure rate by 67% (5.7% → 1.9%)

**Reranking Enhancement:**

Reranking is a filtering technique ensuring only the most relevant chunks are passed to the model. The process:
1. Perform initial retrieval to get top potentially relevant chunks (top 150)
2. Pass top-N chunks with user query through reranking model
3. Score each chunk based on relevance and importance
4. Select top-K chunks (top 20)
5. Pass top-K chunks to model as context for final generation

Testing used Cohere reranker. Reranking adds small latency but provides better responses and reduces cost by processing less information.

**Implementation Considerations:**

1. **Chunk boundaries:** Choice of chunk size, boundary, and overlap affects retrieval performance
2. **Embedding model:** Contextual Retrieval improves performance across all models tested, but Gemini and Voyage embeddings were particularly effective
3. **Custom contextualizer prompts:** Domain-specific prompts (including glossaries of key terms) can achieve better results
4. **Number of chunks:** More chunks increase chances of including relevant information, but can be distracting. Testing with 5, 10, and 20 chunks found 20 to be most performant

**Key Findings Summary:**

1. Embeddings + BM25 is better than embeddings alone
2. Voyage and Gemini have the best embeddings tested
3. Top-20 chunks more effective than top-10 or top-5
4. Adding context to chunks significantly improves retrieval accuracy
5. Reranking is better than no reranking
6. All benefits stack: maximum performance comes from combining contextual embeddings (Voyage or Gemini) with contextual BM25, reranking, and 20 chunks in the prompt

Developers working with knowledge bases are encouraged to use Anthropic's cookbook to experiment with these approaches for unlocking new performance levels.

---

Title: Retrieval Augmented Generation with Contextual Embeddings
Tags: BM25, chunking, code examples, context engineering, contextual embeddings, cost optimization, embeddings, evaluation, hybrid search, implementation guide, performance metrics, prompt caching, RAG, reranking, retrieval, tutorial, vector database, Voyage AI
URL: https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings
<br/>
Summary:<br/>
See notes: This cookbook provides practical implementation guidance for contextual embeddings referenced in Braindumpnotes.md. It complements the contextual retrieval article with detailed code examples and evaluation metrics.

This comprehensive Jupyter notebook tutorial demonstrates how to build and optimize a Contextual Retrieval system, providing practical implementation guidance for the techniques introduced in Anthropic's contextual retrieval blog post. The guide uses a dataset of 9 codebases (737 chunks, 248 evaluation queries) to demonstrate progressive improvements in RAG performance.

**What This Guide Covers:**

1. Setting up a basic retrieval pipeline to establish baseline performance
2. Contextual Embeddings: what it is, why it works, and how prompt caching makes it practical
3. Implementing Contextual Embeddings with performance demonstrations
4. Contextual BM25: improving performance with contextual hybrid search
5. Reranking for maximum retrieval accuracy

**Prerequisites:**

- **Technical Skills:** Intermediate Python, basic RAG understanding, familiarity with vector databases and embeddings, basic command-line proficiency
- **System Requirements:** Python 3.8+, Docker (optional, for BM25), 4GB+ RAM, ~5-10 GB disk space
- **API Access:** Anthropic API key, Voyage AI API key, Cohere API key
- **Time & Cost:** 30-45 minutes completion time, ~$5-10 API costs for full dataset

**Evaluation Methodology:**

Uses Pass@k metric to evaluate whether the 'golden chunk' (correct answer) appears in the first k documents retrieved. The dataset contains 248 queries across 9 pre-chunked codebases. Baseline performance: 81% Pass@5, 87% Pass@10, 90% Pass@20.

**Baseline RAG Pipeline:**

The "naive RAG" approach includes three steps:
1. Chunk documents by heading (containing only content from each subheading)
2. Embed each document using Voyage AI
3. Use cosine similarity to retrieve documents for answering queries

**VectorDB Implementation:**

The tutorial provides a simple in-memory vector database class with pickle serialization for easy understanding and no external dependencies. Key features:
- Batch processing (128 chunks at a time)
- Progress tracking with tqdm
- Query caching for repeated searches
- Automatic disk persistence to avoid re-computing embeddings
- Same interface patterns as production solutions for easy migration

**Contextual Embeddings Deep Dive:**

Individual chunks in basic RAG often lack sufficient context when embedded in isolation. Contextual Embeddings use Claude to generate a brief description that "situates" each chunk within its source document. For each chunk, both the chunk and full source file are passed to Claude, which generates a concise explanation of what the chunk contains and where it fits in the overall file. This context gets prepended to the chunk before embedding.

**Cost and Latency Optimization:**

Contextualization happens once at ingestion time, not during queries. Unlike HyDE (hypothetical document embeddings) that adds latency to each search, contextual embeddings are a one-time cost. Prompt caching makes this practical:
1. First chunk: Write full document to cache (small premium)
2. Subsequent chunks: Read from cache (90% discount)
3. Cache lasts 5 minutes (plenty of time to process all chunks in a document)

**Cost Example:** For 800-token chunks in 8k-token documents with 100 tokens of generated context, total cost is $1.02 per million document tokens.

**Real Dataset Results (737 chunks across 9 files):**
- 61.83% of input tokens read from cache (2.27M tokens at 90% discount)
- Without caching: ~$9.20 in input tokens
- With caching: ~$2.85 (69% savings)
- Cache hit rate depends on chunks per document (more chunks = better caching benefit)

**Performance Improvement:** Contextual embeddings reduced retrieval failures by 30-40% across all k values. Pass@10 improved from 87% to 92%, with most pronounced improvement at Pass@5 where precision matters most.

**ContextualVectorDB Implementation:**

Extends basic VectorDB with automatic contextualization during ingestion. Key features:
- Parallel processing with ThreadPoolExecutor (configurable thread count)
- Automatic prompt caching
- Token tracking for cache performance monitoring
- Persistent storage for embeddings and contextualized metadata

**Contextual BM25 - Hybrid Search:**

Combining semantic search with keyword-based search further improves performance. BM25 (probabilistic keyword ranking algorithm) excels at finding specific terms but lacks semantic understanding. By combining both:
- **Semantic search:** Captures conceptual similarity and paraphrases
- **BM25:** Catches exact terminology, function names, specific phrases
- **Reciprocal Rank Fusion:** Intelligently merges results from both sources

Instead of only searching raw chunk content, the hybrid approach searches both the chunk AND the contextual description. The retrieve_advanced function implements:
1. Retrieve top 150 results from both semantic search and BM25
2. Score fusion using weighted Reciprocal Rank Fusion (default: 80% semantic, 20% BM25)
3. Return top-k highest-scoring results

**Setup Requirements:** Elasticsearch running locally via Docker for BM25 functionality.

**Reranking Enhancement:**

Two-stage retrieval approach:
1. **Stage 1 - Broad Retrieval:** Retrieve more candidates than needed (e.g., 100 chunks)
2. **Stage 2 - Precise Selection:** Use specialized reranking model (Cohere rerank-english-v3.0) to score candidates and select top-k

The pipeline over-retrieves (10x more results than needed), rerranks with Cohere using both original chunk content and contextual descriptions, then selects top-k. Trade-off: adds ~100-200ms query latency but reduces failures from 7.66% to ~5%.

**Comprehensive Performance Results:**

| Approach | Pass@5 | Pass@10 | Pass@20 |
|----------|--------|---------|---------|
| **Baseline RAG** | 80.92% | 87.15% | 90.06% |
| **+ Contextual Embeddings** | 88.12% | 92.34% | 94.29% |
| **+ Hybrid Search (BM25)** | 86.43% | 93.21% | 94.99% |
| **+ Reranking** | 92.15% | 95.26% | 97.45% |

**Key Findings:**

1. **Contextual embeddings provided largest single improvement** (+5-7 percentage points), validating that adding document-level context to chunks significantly improves retrieval quality. Gets you 90% of the way to optimal performance.

2. **Reranking achieves highest absolute performance** (95.26% Pass@10), representing a 47% reduction in retrieval failures compared to baseline (from 12.85% failure rate to 4.74%).

3. **Trade-offs exist:**
   - Contextual embeddings: One-time ingestion cost (~$3 for this dataset with prompt caching)
   - Hybrid search: Requires Elasticsearch infrastructure and maintenance
   - Reranking: Adds 100-200ms query latency and per-query API costs (~$0.002 per query)

**Recommendations by Use Case:**

- **High-volume, cost-sensitive:** Contextual embeddings alone (92% Pass@10, no per-query costs)
- **Maximum accuracy, latency-tolerant:** Full reranking pipeline (95% Pass@10, best precision)
- **Balanced production system:** Hybrid search (93% Pass@10, no per-query costs)

**Deployment Considerations:**

- **AWS users:** Lambda function provided in `contextual-rag-lambda-function` directory for use with Bedrock Knowledge Bases as custom chunking option
- **GCP users:** Can spin up Cloud Run instance following similar pattern
- **Production environments:** Consider hosted vector database solutions instead of in-memory pickle-based approach

The tutorial applies to various data types beyond codebases: internal company knowledge bases, financial and legal content, educational content, and more. Contextual embeddings provide the best performance-to-cost ratio for most production RAG systems, delivering 92% Pass@10 with only one-time ingestion costs.

---

Title: Code execution with MCP: Building more efficient agents
Tags: agent architecture, agents, code execution, context engineering, context management, control flow, cost optimization, data filtering, latency, MCP, privacy, progressive disclosure, sandboxing, security, Skills, state management, token budget, tool calling, tools
URL: https://www.anthropic.com/engineering/code-execution-with-mcp
<br/>
Summary:<br/>
See notes: This article addresses code execution with MCP as referenced in Braindumpnotes.md, showing how agents can scale more efficiently when using code to interact with MCP servers.

Anthropic introduces a paradigm shift in how agents interact with MCP (Model Context Protocol) servers. As MCP adoption has grown rapidly since its November 2024 launch (thousands of community-built servers, SDKs for all major programming languages, industry adoption as de-facto standard), developers now routinely build agents with access to hundreds or thousands of tools across dozens of MCP servers. However, this scale creates efficiency problems: loading all tool definitions upfront and passing intermediate results through the context window slows down agents and increases costs.

**The Problem: Excessive Token Consumption:**

Two common patterns increase agent cost and latency as MCP usage scales:

1. **Tool definitions overload the context window:** Most MCP clients load all tool definitions upfront directly into context using direct tool-calling syntax. Tool descriptions consume significant context window space, increasing response time and costs. For agents connected to thousands of tools, they process hundreds of thousands of tokens before reading a request.

2. **Intermediate tool results consume additional tokens:** Most MCP clients allow models to directly call MCP tools. Every intermediate result must pass through the model. Example: "Download my meeting transcript from Google Drive and attach it to the Salesforce lead" requires the full transcript to flow through the model twice—once when retrieved, once when written to Salesforce. For a 2-hour sales meeting, this could mean processing an additional 50,000 tokens. Even larger documents may exceed context window limits, breaking workflows. Large documents or complex data structures increase likelihood of mistakes when models copy data between tool calls.

**The Solution: Code Execution with MCP:**

Present MCP servers as code APIs rather than direct tool calls. The agent writes code to interact with MCP servers. This addresses both challenges: agents load only the tools they need and process data in the execution environment before passing results back to the model.

**Implementation Approach:**

Generate a file tree of all available tools from connected MCP servers. Example using TypeScript:

```
servers
+-- google-drive
|   +-- getDocument.ts
|   +-- ... (other tools)
|   +-- index.ts
+-- salesforce
|   +-- updateRecord.ts
|   +-- ... (other tools)
|   +-- index.ts
```

Each tool corresponds to a file with a clear interface. The agent discovers tools by exploring the filesystem: listing the `./servers/` directory to find available servers, then reading specific tool files it needs to understand each tool's interface. This lets the agent load only the definitions it needs for the current task.

**Performance Impact:**

The Google Drive to Salesforce example reduces token usage from 150,000 tokens to 2,000 tokens—a time and cost saving of 98.7%. Cloudflare published similar findings, referring to code execution with MCP as "Code Mode." The core insight: LLMs are adept at writing code, and developers should take advantage of this strength to build agents that interact with MCP servers more efficiently.

**Benefits of Code Execution with MCP:**

1. **Progressive Disclosure:** Models excel at navigating filesystems. Presenting tools as code on a filesystem allows models to read tool definitions on-demand rather than loading everything upfront. Alternatively, a `search_tools` tool can be added to find relevant definitions (searching for "salesforce" loads only those tools). Including a detail level parameter (name only, name and description, or full definition with schemas) helps agents conserve context and find tools efficiently.

2. **Context Efficient Tool Results:** When working with large datasets, agents filter and transform results in code before returning them. Example: fetching a 10,000-row spreadsheet without code execution flows all rows through context for manual filtering. With code execution, filtering happens in the execution environment—the agent sees five rows instead of 10,000. Similar patterns work for aggregations, joins across multiple data sources, or extracting specific fields without bloating the context window.

3. **More Powerful and Context-Efficient Control Flow:** Loops, conditionals, and error handling use familiar code patterns rather than chaining individual tool calls. Example: polling for deployment notifications in Slack can be written as a while loop with sleep, rather than alternating between MCP tool calls and sleep commands through the agent loop. Writing out conditional trees that get executed also saves on "time to first token" latency—rather than waiting for a model to evaluate an if-statement, the agent lets the code execution environment handle this.

4. **Privacy-Preserving Operations:** When agents use code execution with MCP, intermediate results stay in the execution environment by default. The agent only sees what's explicitly logged or returned, meaning data you don't wish to share with the model can flow through workflows without entering the model's context. For even more sensitive workloads, the agent harness can tokenize sensitive data automatically. Example: importing customer contact details from a spreadsheet into Salesforce can have the MCP client intercept and tokenize PII before it reaches the model (replacing with [EMAIL_1], [PHONE_1], [NAME_1]). When data is shared in another MCP tool call, it's untokenized via a lookup in the MCP client. Real data flows from Google Sheets to Salesforce but never through the model. This prevents the agent from accidentally logging or processing sensitive data and enables deterministic security rules about where data can flow to and from.

5. **State Persistence and Skills:** Code execution with filesystem access allows agents to maintain state across operations. Agents can write intermediate results to files, enabling them to resume work and track progress. Example: querying 1,000 Salesforce leads and saving to CSV, then later picking up from saved file. Agents can also persist their own code as reusable functions. Once an agent develops working code for a task, it can save that implementation for future use. This ties closely to the concept of Skills—folders of reusable instructions, scripts, and resources for models to improve performance on specialized tasks. Adding a SKILL.md file to saved functions creates a structured skill that models can reference and use. Over time, the agent builds a toolbox of higher-level capabilities, evolving the scaffolding needed to work most effectively.

**Trade-offs and Considerations:**

Code execution introduces its own complexity. Running agent-generated code requires a secure execution environment with appropriate sandboxing, resource limits, and monitoring. These infrastructure requirements add operational overhead and security considerations that direct tool calls avoid. The benefits of code execution—reduced token costs, lower latency, and improved tool composition—should be weighed against these implementation costs.

**Summary:**

MCP provides a foundational protocol for agents to connect to many tools and systems. However, once too many servers are connected, tool definitions and results can consume excessive tokens, reducing agent efficiency. Although many problems here feel novel—context management, tool composition, state persistence—they have known solutions from software engineering. Code execution applies these established patterns to agents, letting them use familiar programming constructs to interact with MCP servers more efficiently.

**Industry Adoption:** Since launching in November 2024, the community has built thousands of MCP servers, SDKs are available for all major programming languages, and the industry has adopted MCP as the de-facto standard for connecting agents to tools and data.

---

Title: How to Manage Context in AI Coding
Tags: best practices, co-location, coding workflows, context engineering, dynamic retrieval, mandatory context, multi-player, prompt engineering, simplicity, task-relevant maturity, team workflows
URL: https://refactoring.fm/p/managing-context-for-ai-coding
<br/>
Summary:<br/>
See notes: This article discusses managing context for AI coding as part of the Context Engineering guide.

This comprehensive essay explores context engineering as the evolution beyond prompt engineering, emphasizing building multiplayer, dynamic systems that reliably provide AI with the right information. Written by Luca Rossi based on research from keynoting the CTO Craft Conference in Berlin, including survey data, podcast interviews, and conversations with tech leaders using AI successfully.

**Context Engineering vs. Prompt Engineering:** Context engineering differs fundamentally from prompt engineering by focusing on "context" as the better abstraction—grounding the model in accurate and exhaustive information rather than nailing specific wording. Context engineering refers to the discipline of designing systems and workflows that reliably ensure AI receives the right information. Two key qualities make this an engineering discipline: 1) Multi-player—designed with the team in mind, featuring shared workflows and practices; 2) Dynamic—enabling AI to fetch the right content by itself rather than requiring humans to pass it every time.

**Tasks vs. Procedures:** Good context separates into two categories: 1) Task-specific instructions (the what needs to be done), and 2) Procedures/principles (the how it needs to be done). Teams should trend toward shrinking explicit instructions while growing shared standard practices. You don't want to say "write tests" in every prompt or ticket—it should be standard practice everyone knows. The best context system enables developers and AI to succeed with as little explicit instruction as possible. Focus on improving inputs rather than just fixing outputs—when something fails, improve the context that created it to nurture a feedback loop for continuous system improvement.

**Sharing the Why:** Beyond the "what" and "how," there's a third context category: the "why." For tasks like finding architecture improvements, refactoring opportunities, or making product strategy, the what is up in the air and the how is not yet relevant. Instead, you need context on why something would be valuable. This includes evergreen content (principles, values, business domain), future-looking content (quarterly goals), and historical content (past goals, ADRs). Questions to ask: How much is written down? Does everyone have access? Do they know where it is? Do people think it's important?

**Task-Relevant Context:** Borrowed from Andy Grove's "task-relevant maturity" concept from High Output Management, context should be categorized by importance for the task at hand: 1) Mandatory context—must be fetched correctly 100% of the time; 2) Best effort context—nice to have as additional info, but okay if retrieval sometimes fails or isn't 100% accurate. Getting this distinction right is crucial because if AI fails to account for mandatory context even a small percentage of times, engineers get frustrated and stop using it for complex work. The more AI can be trusted, the looser the feedback loop and the bigger the problems it can tackle.

**Mandatory Context Implementation:** The #1 rule for mandatory context is co-location—store it alongside where the task happens. For coding, this means keeping critical information in the repo: 1) CLAUDE.md or AGENTS.md file for how AI should write code; 2) README file for instructions on building/testing/executing code; 3) SYSTEM-DESIGN.md file capturing main design features. Avoid relying too heavily on conversation threads/memories—consolidate useful information into files. For meaningful tasks, have agents create and maintain a ROADMAP.md file (git-ignored) for tracking progress, making it easier to recover from context rot and parallelize work with multiple agents.

**Best Effort Context Implementation:** Much best-effort context isn't appropriate to co-locate—it's Slack chats, ADRs, and information from Notion, Linear, GitHub history, etc. While individual MCPs exist for many tools, centralizing access through a single tool (like Unblocked) proves more reliable. Individual MCPs face challenges: too many MCPs confuse agents about when/how to use them; many MCPs are too simplistic and require extra agent work that may fail; they waste reasoning and context window space. Centralizing through a tool enables delivering the experience across multiple platforms (Slack, Teams, etc.), vital for understanding old code, onboarding new team members, and figuring things out.

**Keep Context Small:** The easiest way to improve context management for both humans and AI is keeping it simple and small through: 1) Low coupling—componentized, isolated code reduces what needs to be fetched, considered, or updated; 2) Convention over configuration—great defaults reduce cognitive load and context size, with less code written meaning less to remember; 3) Simple tech stack—using the same language everywhere, favoring buy over build, using well-understood technology that doesn't require extensive documentation.

**Key Takeaways:** Focus on inputs rather than outputs—nurture the feedback loop that improves the system over time. Gradually shift from explicit instructions to embedded standards. Co-locate mandatory context for 100% reliable retrieval while centralizing access to distributed best-effort context. Simplicity through low coupling, convention over configuration, and simple tech stacks keeps context manageable, producing better results for both humans and AI.

---

Title: Beyond Chunks: Why Context Engineering is the Future of RAG
Tags: agents, agentic systems, context engineering, database design, faceted search, metadata, multi-modal content, peripheral vision, prompt engineering, RAG, retrieval, search quality, tool responses, XML structure
URL: https://jxnl.co/writing/2025/08/27/facets-context-engineering/
<br/>
Summary:<br/>
This comprehensive essay by Jason Liu explores context engineering as the critical evolution of RAG for agentic systems, demonstrating how structuring tool responses is as important as the information they contain. Based on consulting work and teaching at improvingrag.com, including office hours with teams facing real production challenges, the article reveals a consistent pattern: teams with functional search systems struggle when users ask contextual questions like "Who modified this document?" and "How recent is this policy?"

**Core Insight:** Agentic systems are persistent, make multiple tool calls, and build understanding across conversations. They don't just need the right chunk—they need to understand the landscape of available information to decide what to explore, make plans, and execute. This fundamental shift is exemplified by successful coding agents where simple tools with agentic loops consistently outperform complex retrieval systems.

**Key Terms:** Context Engineering structures tool responses and information flow to give agents the right data in the right format for effective reasoning. Faceted Search exposes metadata aggregations (counts, categories, filters) alongside search results to reveal the data landscape. Agent Peripheral Vision provides agents with structured metadata about the broader information space beyond just the top-k results. Tool Response as Prompt Engineering uses XML structure, metadata, and system instructions in tool outputs to guide future agent behavior.

**The Chunk Limitation:** The breakthrough came when realizing chunks themselves were the limitation. When search results showed multiple fragments from the same document, agents had to piece together puzzles instead of loading complete pages. A simple load_pages() function improved agent reasoning dramatically. Then a profound insight emerged: structured tool responses weren't just returning data—they were teaching agents how to think about the data. The metadata became prompt engineering itself.

**The Paradigm Shift:** As Anthropic explains, tools represent a new software contract between deterministic systems and non-deterministic agents. Traditional functions like getWeather("NYC") work predictably every time, but when an agent asks "Should I bring an umbrella today?" it might call the weather tool, answer from memory, ask for location clarification, or hallucinate. This fundamental non-determinism means designing tools that increase the surface area over which agents can be effective, not just return the "right" answer.

**Four Levels of Context Engineering:**

**Level 1 - Minimal Chunks (No Metadata):** Basic tool responses returning only raw text content without source information or metadata. The limitation: without metadata, agents can't make strategic decisions about where to search next—they're flying blind.

**Level 2 - Chunks with Basic Source Metadata:** Returns chunks with source files, page numbers, and chunk content. Enables citations and reveals document clustering patterns. The breakthrough: agents now see when multiple chunks come from the same source and can strategically load full pages instead of piecing together fragments. Includes system instructions teaching agents that "multiple chunks from same source = use load_pages() instead of fragments."

**Level 3 - Multi-Modal Content Representation:** Modern documents contain tables, charts, diagrams, code blocks, and structured content. This level provides appropriate representations for different content modalities. Simple tables return as Markdown for easy data work; complex tables with merged cells return as HTML to preserve relationships; images include both visual content and searchable OCR text. Agents can filter by content_types like ["text", "table", "image", "code"].

**Level 4 - Facets and Query Refinement:** Introduces aggregated metadata helping agents understand the data landscape and refine queries iteratively, like users do on e-commerce sites. Think e-commerce: search "running shoes" → get results + facets (Nike: 45, Adidas: 32, 4-star: 28, 5-star: 12). Agents already understand this pattern from coding—when grep shows file distribution counts, agents recognize that files with highest occurrence counts deserve full attention rather than reading disconnected snippets. Faceted search is exactly this: aggregate counts reveal which documents deserve complete context rather than fragmented chunks.

**Types of Facet Data Sources:**

**Structured Systems:** CRMs, ERPs, HR systems, and business databases already contain rich structured data for faceted search. Example: Linear ticket search with facets for team, status, priority, and assignee. When searching "API timeout issues," facets reveal the complete landscape—all 3 returned tickets are "Done" but facets show 5 "Open" tickets exist. Resolved tickets have better documentation and rank higher in similarity search, while active issues get filtered out (similarity bias alert).

**Extracted Facets:** Companies like Extend and Reducto perform structured data extraction over documents to create facets that don't naturally exist in raw text. Example: contract analysis with AI-extracted facets for signature_status, project classification, and document_type. When searching "liability provisions," all 3 returned contracts are signed, but facets reveal 12 unsigned contracts exist. Signed contracts have better-developed liability language (higher similarity scores), while unsigned contracts with liability provisions didn't make the top-k cut—they need attention before signing.

**Agent Persistence as Paradigm Shift:** This is what most teams miss—agentic systems are incredibly persistent. Given enough budget and time, they'll keep searching until they find what they need. Traditional RAG optimized for humans who make one query and expect comprehensive results, creating "stuff everything relevant into the first response" mentality that led to context window bloat and degraded performance. Agents operate differently—they're methodical, systematic, and don't get frustrated. Show them a facet indicating 47 relevant documents in a category they haven't explored? They'll investigate. The strategic implication: you don't need perfect recall on query #1. You need to give agents enough context about the information landscape that they can systematically traverse it. Each faceted search reveals new dimensions to explore, creating an implicit knowledge graph agents can navigate without explicitly defined node relationships.

**Design Principles:** Hard truth—good search is the ceiling on RAG quality. If recall is poor, no prompt engineering or model upgrade will save you. Before building new infrastructure, audit what your tools actually return. Most improvements are just better string formatting—wrapping results in XML, adding source metadata, including system instructions. No major architectural changes required. Think of tool descriptions as prompt engineering for your agents (from Anthropic's tool development guide). How you name functions, structure parameters, and format responses directly influences agent reasoning patterns. Clear tool boundaries and meaningful parameter names reduce confusion and hallucinations.

**Balancing Complexity:** There's no single right answer for how much metadata to include. Every system has different needs, and more complex tools increase likelihood of hallucinations and tool misuse. This reality demands: 1) Better prompts—complex tools require sophisticated instructions; 2) Better creativity in system design—same outcome can often be achieved through simpler tool compositions rather than one mega-tool. Recognize when complexity pays for itself. Metadata that doesn't change agent behavior is just expensive noise. Token efficiency insight from Anthropic: tool responses should prioritize contextual relevance over flexibility. Return high-signal information that directly informs downstream actions, not low-level technical identifiers.

**Evolution Summary:** Each level adds peripheral vision about the information space. Agents don't just get better answers—they get better context about what questions to ask next. Tool responses become teaching moments, showing agents how to think about data systematically. The business impacts are measurable: 90% reduction in clarification questions, 75% reduction in expert escalations, 95% reduction in 504 errors, 4x improvement in resolution times. The deeper transformation is architectural—databases evolve from passive storage to active reasoning partners that surface patterns human users would never think to request.

**Lowest Hanging Fruit:** Context engineering doesn't require rebuilding infrastructure or redesigning tools. It's primarily better string formatting—wrapping responses in XML, adding source metadata, including strategic system instructions. Low technical lift, potentially massive business impact. Most teams can implement Level 2 (source metadata) in an afternoon. The beauty: you don't need to redesign tools or rebuild infrastructure. Most improvements are XML structuring, source tracking, and system instructions—essentially better string formatting with potentially massive upside.

**What's Next:** Adoption will follow the usual pattern: teams building agents today will implement context engineering first, then tooling will catch up. Vector databases are already adding facet support (TurboPuffer ships facets and aggregations), but you don't need to wait for perfect tooling to start. Tool responses become teaching moments—the XML structures and system instructions in your tool responses directly influence how agents think about subsequent searches. Design them intentionally.

---

Title: Slash Commands vs Subagents: How to Keep AI Tools Focused
Tags: agents, Claude Code, context engineering, context pollution, context rot, isolation, parallel processing, read-write coordination, slash commands, sub-agents, token efficiency, workflow orchestration
URL: https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/
<br/>
Summary:<br/>
This practical essay from Jason Liu's Context Engineering Series explores the critical architectural choice between slash commands and subagents for keeping AI tools focused when handling messy, token-intensive tasks. Based on consulting work helping companies build AI systems, the article demonstrates how AI tools often waste enormous processing power on messy information, with main thinking getting clouded by test results, error logs, and long outputs.

**Core Problem:** Bad context is cheap but toxic. Loading 100,000 lines of test logs costs almost nothing computationally, but easily pollutes valuable context. A well-crafted 3,000-token feature spec gets destroyed when you dump Python outputs and error traces on top of it. The choice isn't about what the AI can do—it's about what it can do given the information it has and how focused it can stay on one task.

**Key Terms:** Context Pollution is when valuable reasoning context gets flooded with irrelevant but computationally cheap information (logs, error traces, diagnostic output). Context Rot is the degradation of AI performance as input length increases, where models process context less reliably in longer conversations. Subagents are specialized AI workers that handle messy, token-intensive tasks in isolation and return only distilled insights to the main reasoning thread.

**The Dramatic Difference:** Using Claude Code as an example with identical capability to find problems and identical results, slash commands use 169,000 tokens with 91% junk while subagents use only 21,000 tokens with 76% useful information—8x cleaner. This massive difference in context quality fundamentally changes what agents can accomplish reliably.

**The Slash Command Path:** When you need to run tests, the slash command triggers a prompt like "Run the tests in verbose mode and read the outputs carefully. Then inspect any of the files that have changed that might be causing issues." The AI tool puts test results directly into the same conversation. Your clean 5,000-word plan gets flooded with 150,000 words of test logs—your AI's memory is suddenly 95% junk: error messages, long outputs, thousands of "expected this but got that" failures, timestamps, and system dumps. The diagram shows how tokens accumulate: you start with clean, focused work (16,000 tokens), then /run-tests dumps 150,000 tokens of diagnostic noise into your main thread. By the time you want to continue your original feature work, your AI is drowning in random bits of raw logs, error traces, and debug info—exactly the kind of mess that makes traditional search systems fail.

**Context Rot in Action:** This is the well-documented phenomenon where AI performance degrades as input length increases, as demonstrated by Chroma's research on context rot. As the conversation grows, it's hard to figure out what the main goal is. The more irrelevant stuff you add, the worse the AI performs. Your first 5,000 words were focused on adding a new feature to the refunds system. Now 95% of your AI's memory looks like diagnostic junk. It's like the reverse of finding a needle in a haystack—you had the needle and then buried it under a pile of hay. This problem happens in more than just coding tools; keeping clean information is key to system performance whether you're fixing code or answering customer questions.

**The Subagent Path:** Instead of using a slash command, you create a Test Runner helper. Claude Code makes this easy—subagents are separate AI helpers with their own instructions, tools, and memory. They're like having a team of workers where each worker does a messy job, then comes back with just the important results. This approach addresses a core challenge in multi-agent systems: maintaining context coherence while enabling specialization. The key insight is that subagents should operate in isolation on well-defined tasks, then return distilled results rather than trying to collaborate continuously. This aligns with Cognition's insights on why multi-agent systems are problematic for coding tasks—the "telephone game" effect between agents creates more problems than benefits.

**What Subagents Can Do:** Your test runner subagent can: run all tests in ultra-verbose mode with full stack traces; use awk, grep, and python to parse gigabytes of application logs, database logs, and system logs; use Git to check when failing files last changed, including full commit diffs; correlate failures with PRs and read entire code review threads; read all the files at fault, their imports, and related modules to hypothesize root causes; analyze performance metrics and memory dumps. It might use 180,000 tokens in the process, reading huge log files, parsing long error traces, and checking hundreds of code files. But what comes back to your main AI is a short, clear summary: "Tests A, B, C are failing; Root cause is in refund.py, introduced by PR #123; Suggested fix: restore the None guard."

**Subagent Token Economics:** Main thread total is 21,000 tokens (16k clean + 2k summary + 3k continuing) while subagent burned 150,000 tokens off-thread, resulting in 76% signal context quality—8x cleaner main thread with same diagnostic capability. The mess stayed with the sidecar; only the useful stuff came back. Your main context remains tight and focused. Real example: A test runner subagent identified failing tests, ran git bisect, and traced the regression back to the PR that introduced it—took ~7 minutes and burned ~180,000 tokens, but the main agent only saw the conclusion. Another friend built a performance optimization subagent: their main agent implemented a UX feature while the subagent ran scripts, parsed logs, did data analysis, and reported: "These three functions cause 70% of latency." The core stayed focused on the feature; the sidecar did the heavy lifting.

**Claude Code Implementation Details:** Slash commands are just prompt injection—when you type /run-tests, Claude Code literally injects that long prompt into your main thread. Everything happens in the same context window: test outputs, git blame, stack traces all flood your main reasoning space. Subagents are separate workers—Claude Code has pre-configured subagents like test-diagnostician and general-purpose that spawn with their own context windows and tool access. They're literally like shadow clones—they go off, do the work, burn 150k tokens parsing logs, and come back with just the insights. The brilliance is in what gets isolated vs. what gets shared.

**Read-Write Coordination Pattern:** Read operations can be massively parallel—multiple subagents can read files, run git operations, parse logs all simultaneously because they don't step on each other (they're just consuming information). This aligns with Anthropic's multi-agent research approach where parallel subagents explore different aspects of complex problems simultaneously. Write operations need to be single-threaded—if multiple agents try to edit the same files, you get merge conflicts and broken state. So Claude Code keeps all actual code implementation in the main thread. Slash commands can orchestrate subagents—you might have /commands that trigger different kinds of subagents to coordinate complex tasks. The slash command is for the orchestrator, and subagents are how you delegate.

**Elegant Orchestration Pattern:** Example workflow: 1) Main agent: "I need to implement authentication"; 2) Research subagent: Goes deep on existing auth patterns (burns 80k tokens); 3) Security subagent: Analyzes requirements and best practices (burns 60k tokens); 4) Main agent: Gets two clean summaries, then implements single-threaded. The research happens in parallel, the implementation happens coordinated. The noise stays in the sidecars, the signal comes to main. A /analyze-performance command might spawn multiple subagents: one parsing application logs, another analyzing database queries, a third reviewing recent code changes. Each burns massive token budgets in parallel, but your main thread only sees the coordinated summary.

**Beyond Code Applications:** This pattern applies far beyond coding assistants. The key insight is read-only research models that burn tokens exploring messy data while keeping your main reasoning thread clean. Comparing data rooms: spin up an agent per data room, each aware of the final report you want to generate, explores its data room independently, then feeds clean insights back to the main orchestrator. Financial due diligence: let subagents parse thousands of documents—regulatory filings, transaction records, legal contracts—while your main thread focuses on strategic analysis and decision-making. Research synthesis: multiple agents can explore different domains or time periods in parallel, each burning massive token budgets on deep research, while your main agent receives only the distilled findings.

**Critical Distinction:** This works because these are read-only operations. Research warns that multi-agent systems become fragile when agents start making conflicting decisions without full context. But for pure research and data exploration, Anthropic's approach shows that parallel subagents excel—they consume information simultaneously without stepping on each other's work. The pattern is universal: burn tokens in specialized workers, preserve focus in the main thread. But recognize these systems are complicated—if you're building a product, you have to decide whether to manually orchestrate these workflows and educate users, or build for expert users who understand the complexity.

**Why This Matters Now:** It's about ergonomics and economics. With 1M+ context windows, we have bigger ambitions for what agents can do—and they're working. But long context makes it hard for users to track what's happening and burns serious money. Bad context is cheap but toxic. The immediate action: audit your current agent workflows to identify which operations generate massive, noisy outputs. Most teams can identify subagent candidates in an afternoon and implement basic context isolation within a week. This architectural choice will define how agent systems scale. Teams that recognize this early will build agents that scale; teams that ignore it will build agents that plateau under their own noise. Coding agents like Claude Code are at the forefront of solving this problem—the patterns emerging here will reach other domains (customer support, financial analysis, medical diagnosis) within months.

---

Title: Two Experiments We Need to Run on AI Agent Compaction
Tags: agents, compaction, context engineering, context pollution, failure modes, gradient descent, in-context learning, long-running tasks, momentum, observability, sub-agents, trajectory analysis
URL: https://jxnl.co/writing/2025/08/30/context-engineering-compaction/
<br/>
Summary:<br/>
This theoretical and experimental essay from Jason Liu's Context Engineering Series proposes two critical research experiments connecting compaction to machine learning theory and practical agent observability. Based on consulting work helping companies build AI systems, the article explores compaction's connection to research showing that in-context learning is gradient descent, providing a theoretical foundation for understanding how context management affects agent learning trajectories.

**Two Core Insights:** 1) If in-context learning is gradient descent, then compaction is momentum; 2) We can use compaction as a compression system to understand how agents actually behave at scale. This builds on foundational concepts explored in context engineering, where the structure of information flow becomes as critical as the information itself.

**Key Terms:** Compaction is automatic summarization of conversation history when context windows approach limits, preserving essential information while freeing memory space. Agent Trajectory is the complete sequence of tool calls, reasoning steps, and responses an agent takes to complete a task (basically the message array). Context Pollution is when valuable reasoning context gets flooded with irrelevant information, degrading agent performance. Momentum (in gradient descent optimization) is a component that accelerates convergence by incorporating the direction of previous updates to smooth out oscillations.

**Why Compaction Is Like Momentum:** Traditional gradient descent with momentum: θ_t+1 = θ_t - α∇L(θ_t) + β(θ_t - θ_t-1). Conversational learning with compaction: context_new = compact(context_full) + β(learning_trajectory). Compaction isn't just storing facts—it's preserving the learned optimization path. When you compact "I tried X, it failed, then Y worked because Z," you're maintaining the gradient direction that led to success. This theoretical connection raises the question: what if we could actually test this? What if we could run experiments that treat compaction as momentum and see what happens?

**Experiment 1: Compaction as Momentum for Long-Running Tasks:** The first experiment is about momentum—if compaction preserves learning trajectories, then timing should matter for success rates. The setup: run million-token agent trajectories on complex coding tasks and test compaction at 50% vs 75% completion vs natural boundaries vs agent-controlled timing. Research questions include: Does compaction timing affect success rates? Can agents learn to self-compact at optimal moments? How does compaction quality correlate with momentum preservation? Does compaction timing affect how well agents maintain their learning trajectory?

**Key Metrics:** Task completion success rate, time to completion, number of backtracking steps after compaction, and quality of final deliverable. The problem: public benchmarks generally run tasks that are very short and don't burn 700,000 tokens. You need those massive trajectories that only companies like Cursor, Claude Code, or GitHub actually have access to. A practical workaround: The rapid prototyping methodology using Claude Code lets you generate long trajectories for testing. Complex multi-step tasks naturally burn through context as they iterate on tool calls and file modifications—you can study compaction behavior in these prototyping sessions before building production systems.

**Real-World Example:** The Claude plays Pokemon experiment generates "enormous amounts of conversation history, far exceeding Claude's 200k context window," so they use sophisticated summarization when the conversation history exceeds limits. That's exactly the kind of trajectory where compaction timing would matter. This connects to broader challenges in AI engineering communication—how do you measure and report progress on systems where the unit of work isn't a feature but a learning trajectory?

**Experiment 2: Compaction for Trajectory Observability and Population-Level Analysis:** The second experiment is more tractable: can we use specialized compaction prompts to understand what's actually happening in agent trajectories? Basically, design different compaction prompts for different kinds of analysis: 1) Failure Mode Detection—"Compact this trajectory focusing on: loops, linter conflicts, recently-deleted code recreation, subprocess errors, and user frustration signals"; 2) Language Switching Analysis—"Compact focusing on: language transitions, framework switches, cross-language debugging, and polyglot development patterns"; 3) User Feedback Clustering—"Compact emphasizing: correction requests, preference statements, workflow interruptions, and satisfaction indicators."

**Expected Discoveries:** Likely findings include: 6% of coding trajectories get stuck with linters (seen constantly in Cursor); a bunch of agents recreate code that was just deleted; excessive subprocess cycling when language servers act up; patterns around when users start giving lots of corrective feedback. These failure modes mirror the common anti-patterns in RAG systems but at the trajectory level rather than the retrieval level. This matters because Clio found that 10% of Claude conversations are coding-related, which probably influenced building Claude Code. But agent trajectories are totally different from chat conversations—what patterns would we find if we did Clio-style analysis specifically on agent behavior?

**Trajectory-Level Observability:** This type of systematic analysis aligns with data flywheel approaches that help AI systems improve through user feedback loops—but applied to multi-step reasoning rather than single predictions. The clustering approach works as follows: 1) Compact trajectories using specialized prompts; 2) Cluster compacted summaries using embedding similarity; 3) Identify patterns across user bases and use cases; 4) Build diagnostic tools for common failure modes. This is trajectory-level observability—instead of just knowing "agents do coding tasks," we could understand "agents get stuck in linter loops" or "agents perform better when users give feedback in this specific way." It's similar to systematic improvement approaches in RAG system optimization, but focused on agent behavior patterns rather than search relevance.

**Missing Infrastructure:** Context windows keep getting bigger, but we still hit limits on complex tasks. More importantly, we have no systematic understanding of how agents actually learn and fail over long interactions. This connects to fundamental questions about how AI engineering teams should run standups—when your "product" is a learning system, traditional software metrics don't capture what matters. Companies building agents could figure out why some trajectories work and others don't. Researchers could connect theory to practice. The field could move beyond single-turn benchmarks toward understanding actual agentic learning.

**Getting Started:** The momentum experiment realistically needs a company already running coding agents at scale. The observability experiment could work for anyone with substantial agent usage data. Both need access to long trajectories and willingness to run controlled experiments. If you're working with agents at scale and want to explore these directions, collaboration is needed at the intersection of ML theory and practical deployment—exactly where the most interesting problems live. The future isn't just about better models—it's about understanding how agents actually learn and optimize over time. Compaction might be the key.

---

Title: Context Engineering: Agent Frameworks and Form Factors
Tags: agents, architecture, autonomy spectrum, chatbots, composability, context engineering, form factors, graph state machine, MCP, prompt chain, prototyping, testing, tool design, workflows
URL: https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/
<br/>
Summary:<br/>
This practical strategic essay from Jason Liu's Context Engineering Series guides companies on choosing agent frameworks and form factors, emphasizing that understanding form factors and complexity levels is essential before building any agentic system. Based on a conversation with Vignesh Mohankumar, a successful consultant who helps companies navigate AI implementation decisions, both consultants help companies build AI systems—Vignesh focuses on implementations and workflows, while Jason helps with overall strategy and execution.

**Three Main Approaches When Companies Want to Build Agents:** When companies say they want to build agents, the focus should be on practical outcomes: What specific functionality do you need? What business value are you trying to create? Choose one of these three approaches first, as all other technical decisions—tool design, prompts, data processing, orchestration—depend on this choice:

**1) The Conversation Interface (Chatbots):** A chat interface that can access tools and APIs where a human oversees the conversation while the system suggests actions. Success means users get connected to the right functionality and can complete their tasks. Focus on tool integration, fast response times, and helping users find what they need quickly.

**2) The Side-Effect Engine (Workflows):** Automated workflow execution triggered by events with no user interface needed—contracts get sent, invoices get processed, tickets get updated. Success is measured by completion rate, accuracy, and processing time. The user experience is the audit trail showing what happened.

**3) The Research Artifact (Reports & Tables):** Produces structured outputs like reports, summaries, or data tables. The system generates documents that follow a consistent format and meet quality standards. Success means the output is accurate, well-formatted, and ready to use in business contexts.

**Critical Guidance:** Don't try to build a chatbot that should be a workflow, or force a report generator to be conversational. Once you know what you're building, focus on two key areas: 1) Clear tool design—your system is limited by the tools you provide (name functions clearly, define inputs and outputs precisely, make error messages helpful); 2) Testing setup—test your concept quickly before building complex systems (create a simple environment to try instructions with tools and verify outputs; one successful test proves the concept works). Everything else is preference.

**When Should We Choose MCP?** A practical question that comes up frequently: should you build custom tools or use MCP servers? The economics are more important than the technical architecture. MCP servers make sense when you need the same tools across multiple applications. If your team uses Claude Desktop, ChatGPT, and other AI platforms that all need Google Drive integration, an MCP server lets you build once and reuse everywhere. However, MCP adds complexity—you're building protocol adapters, managing authentication across clients, and debugging connection issues. If you have tools that only one application will use, MCP is probably overkill. Direct API calls with the OpenAI SDK will be faster to implement.

**MCP Decision Factors:** The decision is straightforward: If your team already uses Claude Enterprise (which includes Google Drive, Atlassian, and calendar integrations), then adding four more APIs via MCP makes sense—you're extending an existing system, not building from scratch. But if your team is using Ruby, or you're in an environment where MCP client libraries don't exist or are immature, you might spend more time on protocol plumbing than on the actual business logic. At that point, you're better off with direct API calls and a simple message loop. Four concrete factors: 1) Client diversity—are you serving multiple agent platforms, or just one application? 2) Team standardization—does your organization already have MCP infrastructure, or are you starting from scratch? 3) Tool complexity—are your tools simple CRUD operations, or do they involve complex authentication and state management? 4) Headcount allocation—do you want to spend engineering time on protocol compliance, or on business logic? If answering "multiple platforms," "existing infrastructure," "complex tools," and "protocol is fine," then MCP is probably worth the investment. Otherwise, start simple and upgrade when reuse pressure appears.

**The Autonomy Spectrum:** When leadership hears "agent," they imagine fully autonomous systems. That's not what works in practice. Successful systems follow a spectrum of increasing autonomy. This progression gives you a clear upgrade path—you don't need to start with the most complex option. Begin with deterministic code, add AI functions where you need flexibility, use chains when tasks have multiple steps, upgrade to graphs when workflows branch, and save the tool-calling loop for cases that truly need improvisation. This builds reliability step by step.

**Step 0: Deterministic System (No AI):** Use traditional programming with if/else logic and clear rules. When inputs are predictable and tasks have one correct solution, code is cheaper, faster, and more reliable than AI. Use this approach when requirements are stable and inputs vary little.

**Step 1: The AI Function:** You control the workflow completely. Call the LLM like any other function: pass in data, get structured output back. Extract action items from transcripts, normalize addresses, classify documents. Test it like any dependency. No loops or complex logic—just a single AI call per task. Why it works: Real-world data is messy, and these functions clean it up so your code can handle it reliably.

**Step 2: The Prompt Chain:** Chain multiple AI calls together when tasks need several steps: draft, then critique, then revise; or extract, then verify, then summarize. You still control the order completely. The AI handles each step, but you decide what comes next and when to stop. Common mistake: Using chains for simple tasks that need only one AI call, or for complex tasks that need branching logic.

**Step 3: The Graph State Machine:** Here the workflow has multiple paths. You define specific states and transitions between them. The AI helps choose which path to take when the data isn't clear. For example: intake leads to triage, which leads to one of three different workflows, each with its own ending conditions. Key difference: You recognize that requests are different and need different handling. You track the current state clearly instead of hiding it in prompts.

**Step 4: The Tool-Calling Loop:** This is the classic "agent": a loop where the AI suggests an action, you execute it with a tool, add the result back to the conversation, and repeat until the task is complete. It's powerful but expensive and easy to get wrong. Use this for unusual cases that can't be handled with fixed workflows. How to control it: Put the steps in your system prompt, tool descriptions, and error messages ("missing user_id; first call lookup_user(email)"). Set clear end conditions. Limit the number of tool calls. Track the cost.

**Composability: Every Level Is a Tool for Higher Levels:** Here's what makes this spectrum powerful: any system at any level can become a tool for systems at higher levels. A deterministic script becomes a tool for an AI function. An AI function becomes a tool for a prompt chain. A complete prompt chain becomes a tool for a graph state machine. Even an entire tool-calling agent can be a single tool in a larger orchestration system. Examples: Level 0 → Level 1 (AI function might call a deterministic validation script to check if extracted data meets business rules); Level 1 → Level 2 (prompt chain might use an AI function to classify documents, then route each document type to specialized processing); Level 2 → Level 3 (graph state machine might have states that are themselves complete prompt chains); Level 3 → Level 4 (tool-calling loop might have access to tools that are actually complete sub-agents, each handling specialized domains like "customer data research" or "contract generation"). This creates an architecture where simple, reliable components compose into more complex systems. The customer support agent that routes to password reset isn't calling a single API—it's calling a complete Level 2 chain that handles authentication, validation, and email generation.

**Why This Matters for Architecture:** Five key benefits: 1) Testability—each level can be tested independently; your Level 1 AI function works reliably before it becomes a tool in your Level 2 chain. 2) Reliability—complex systems are built from proven components; if your document classification AI function has a 95% success rate, you can count on that when designing the higher-level system. 3) Cost Control—you can optimize each level separately; maybe your Level 1 function is expensive but accurate, so you only call it after a cheap deterministic filter. 4) Migration—you can replace any level without changing the levels above it; start with a simple deterministic tool, then upgrade it to an AI function when you need more flexibility—the calling system doesn't change. 5) Team Structure—different teams can own different levels; the infrastructure team builds Level 0 tools, the AI team builds Level 1 functions, the product team composes them into Level 2 chains. This is how you build agent systems that actually work in production: not as monolithic "intelligent" systems, but as compositions of focused, reliable components at different levels of autonomy.

**From Concept to Working System:** A critical question comes up in every agent consulting engagement: How do you test whether an agent idea actually works without building all the infrastructure first? The answer turned into a complete methodology extracted into its own guide: Context Engineering: Rapid Agent Prototyping. The core insight: Use Claude Code's project runner as a testing harness. Write instructions in English, expose tools as simple CLI commands, create test folders with real inputs, and get evidence in hours instead of weeks. This approach has saved multiple teams from months of premature infrastructure work. If you're being asked to "build agents," start there first—get one passing test before you write any orchestration code. The methodology also integrates with all the other context engineering patterns: tool response design, slash commands vs subagents, and compaction behavior. Prototyping reveals which patterns your specific use case actually needs.

**What Leadership Should Ask For:** Ask your team for specific results, not just "agents." Have them pick one of the three approaches—chatbot, workflow, or report generator—and define success. Ask where they'll start on the complexity spectrum and when they'd add more AI. Ask for a testing setup where they can try the idea with real data and measure results. If they can show one successful test, the concept works. If they can't, you know that before investing more time. Share this guide with your team before they start building—understanding these approaches and complexity levels will save months of unnecessary work and help focus on what's actually achievable.

---

Title: Context Engineering: Rapid Agent Prototyping
Tags: agents, CLI wrappers, Claude Code, compaction, context engineering, error handling, prototyping, rapid prototyping, slash commands, sub-agents, testing, tool design, tool response design, validation, workflows
URL: https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/
<br/>
Summary:<br/>
This comprehensive methodology guide from Jason Liu's Context Engineering Series focuses on rapid agent prototyping because testing agent viability quickly is essential for good context engineering decisions. If leadership is asking you to "explore agents," this methodology will provide evidence in days rather than quarters. Most teams waste months building agent frameworks before knowing if their idea actually works—there's a faster way: use Claude Code (or similar coding agents) as your testing harness to validate agent concepts without writing orchestration code.

**Problem Statement:** When teams want to test an agent idea, they typically start by building infrastructure: message management systems, tool call parsing logic, retry mechanisms, UI frameworks, logging and monitoring. By the time they get to testing the actual agent behavior, they've invested weeks in plumbing. Often they discover the fundamental idea doesn't work, but only after significant engineering investment.

**The Claude Code Solution:** Claude Code has a project runner mode (`claude -p`) that turns any directory into an agent execution environment. It reads a CLAUDE.md file as system instructions and executes workflows using CLI tools you provide. This creates a perfect testing harness—you write instructions in English, expose tools as simple commands, and let Claude Code handle the execution loop. The key insight: if it works once in this harness, the idea is viable. If it fails consistently, you know what's missing without building any infrastructure.

**Agent-Agnostic Approach:** While the article demonstrates Claude Code, the approach works with any coding system that can be driven from CLI and read a simple instruction file (CLAUDE.md or agents.md). Compatible systems include: Cursor's coding agent, Devin, AMP Code, Codex, Windsurf Agent. This unlocks cross-agent evaluations: keep the same commands/ and subagents/ folders with success criteria, add a small wrapper per agent that maps a standard command (e.g., `run-agent <scenario-dir>`) to its CLI flags or subcommands, run the same scenarios across agents and compare pass rate, time, and cost. As features converge (slash commands, subagents, instruction files), you can swap the runner without changing your prototype, allowing you to identify useful components of systems that actually work well separate from any single vendor.

**Anatomy of a Rapid Prototype:** The exact structure consists of: `.claude/agents/` (sub-agent instruction files), `CLAUDE.md` (system instruction + tool inventory), `tools/` (CLI wrappers for your APIs), and `tests/` (one folder per test scenario with `request.txt` for input and `check.py` for assertions on expected outputs).

**CLAUDE.md Structure:** This becomes your system prompt, structured for execution with sections including: Mission (what to accomplish), Execution Flow (step-by-step process), Available Tools (CLI commands with descriptions), Success Criteria (concrete requirements for final output), and Error Recovery (fallback strategies for common failure modes). This connects directly to effective system prompt design principles from context engineering—clear, direct instructions at the right altitude, organized with XML tags or Markdown headers.

**CLI Tool Wrappers:** Tools should be deliberately simple—CLI commands that wrap your actual APIs. This connects to tool response design principles where the structure of tool outputs becomes as important as functionality itself. Example wrapper includes error handling, clear usage messages, and success/failure indicators. The simplicity enables rapid iteration without debugging complex tool call parsing.

**Test Validation:** Each test folder represents a real scenario with concrete pass/fail criteria. Validation scripts (e.g., `check.py`) verify output file existence and validate structure using assertions: checking header counts, section organization, bullet density, and formatting requirements. This provides binary success metrics—either output meets specification or it doesn't, with no subjective evaluation.

**Execution Process:** To test any agent idea: (1) Navigate to test scenario: `cd tests/scenario1`; (2) Execute the workflow: `claude -p` (reads CLAUDE.md, runs end-to-end); (3) Validate results: `python check.py` (pass/fail with specific reasons). You observe Claude Code reading instructions, selecting tools, handling errors, and producing artifacts. You can watch it navigate edge cases in real-time—like when a video lacks English subtitles, it explores alternatives rather than simply failing.

**Benefits Over Infrastructure-First Approach:** Iteration speed—edit text files instead of debugging message loops or tool call parsing. Real-world inputs—test with actual URLs, emails, PDFs instead of sanitized examples. Binary success metrics—no subjective evaluation. Tool design feedback—immediately discover whether tool names are intuitive and error messages helpful. Economic transparency—token costs, latency, and failure rates visible in hours instead of sprints.

**Preparing for Production:** Advanced tool design patterns include: (1) Error messages that guide next actions: instead of generic failures, tools should suggest specific next steps (e.g., "NEXT_STEP: Call lookup_user --email first"); (2) Structured tool responses that control output format for easier parsing, providing status, output files, metrics, warnings, and facets (metadata that helps agents make better decisions). This is a practical application of context engineering principles around faceted tool responses—Level 4 faceted responses give Claude Code peripheral vision about task completion, enabling better follow-up decisions.

**Sub-Agent Workflows and Slash Commands:** Handle complexity with specialized instructions. The Claude Code harness naturally supports both approaches—two different ways to manage context pollution. For transcripts exceeding 50,000 characters, you might split content into manageable chunks, call `/analyze-section` on each chunk with specific focus areas, then use `/synthesize-findings` to combine results into final notes. The key insight from prototyping: Claude Code lets you experiment with both approaches. You can implement `/analyze-transcript` as a slash command that dumps everything into main context, or as a subagent that processes off-thread and returns clean summaries. Testing both in your prototype reveals which approach works better for your specific use case—often subagents win for token-heavy operations.

**Economics of Rapid Prototyping:** Time to evidence—validate agent feasibility in hours instead of weeks. Risk mitigation—if Claude Code can't achieve the task with perfect tool access and no UI constraints, your production version likely won't either. Tool clarity discovery—learn whether you need narrow tools (`search_contracts`, `search_invoices`) or broad ones (`search(type=contract)`). Context management insights—because Claude Code handles conversation state automatically, you can focus on testing how much context pollution your tools create, naturally surfacing candidates for subagent architecture vs slash commands. Compaction benefits—Claude Code's automatic compaction behavior means you can prototype long-running tasks without managing conversation state manually, revealing which workflows naturally generate trajectory data worth preserving vs noise that should be compacted away. Failure mode identification—pinpoint exactly where prompts are insufficient and where tools need better error handling. Production migration—successful test folders become your production test suite; tools and instructions transfer directly to any framework you build.

**When This Methodology Doesn't Apply:** The boundaries are narrower than expected. Actual limitations: high-volume production loads (Claude Code isn't designed for concurrent execution at scale—but this rarely matters for prototyping), hardware integration requirements (physical device control or specialized hardware interfaces can't be easily wrapped in CLI tools). Common misconceptions about limitations: Complex authentication actually works well—API keys, service account tokens, and even multi-step auth flows can be handled in CLI wrappers. Multi-session state is managed by Claude Code conversation history and can pick up where it left off across sessions. Real-time interaction through command-line is often simpler than building a chat interface. But for the fundamental question—"Is this agent idea possible?"—this provides the fastest path to evidence in almost all cases.

**Implementation Checklist:** Before writing orchestration code: (1) Define success criteria—what concrete output proves the agent works? (2) Identify 3-6 core tools that would make the task possible; (3) Create 5-10 test scenarios with real-world inputs; (4) Write CLAUDE.md with clear execution flow; (5) Build simple CLI tool wrappers for your APIs; (6) Execute test scenarios and iterate on instructions/tools; (7) Achieve at least one passing test before considering production architecture; (8) Explore architectural patterns—use the prototype to test whether slash commands or subagents work better for your specific use case.

**Bottom Line:** Stop building agent infrastructure before you know if the idea works. Use this methodology to get evidence in hours: (1) Write instructions in English (CLAUDE.md); (2) Expose tools as simple CLI commands; (3) Create tests with real inputs and concrete success criteria; (4) Run `claude -p` and iterate until you get a pass. If Claude Code can't make it work with perfect tool access and no constraints, your production version probably won't either. But if you can get one passing test, you've proven the concept and can invest in hardening with confidence. The fastest way to prototype an agent isn't to build an agent at all—it's to test whether the idea works before you build anything.

**Connection to Context Engineering Framework:** This prototyping methodology integrates with all other context engineering patterns: Tool Response Design (CLI tools naturally implement the four levels from minimal chunks to faceted responses with metadata—prototyping reveals which level your use case actually needs); Context Pollution Management (the harness makes slash commands vs subagents trade-offs visible immediately—you'll see when main context gets flooded with noise and when clean subagent responses perform better); Compaction Understanding (long-running prototypes surface compaction patterns naturally—you'll discover which conversation trajectories preserve learning vs which create maintenance burden); Form Factor Validation (the methodology connects directly to agent framework decisions around chatbots, workflows, and research artifacts—your tests reveal which form factor actually delivers the outcome you need). This is why rapid prototyping belongs in the Context Engineering series—it's not just about speed, it's about discovering the right information architecture for your specific problem before committing to production complexity.

---



Title: Context Engineering
Tags: agents, code agents, compaction, context engineering, context isolation, embeddings, LangGraph, memory, multi-agent, RAG, scratchpads, state management, summarization, tool selection, tools
URL: https://blog.langchain.com/context-engineering-for-agents/
<br/>
Summary:<br/>
This LangChain blog article introduces context engineering as "the art and science of filling the context window with just the right information at each step of an agent's trajectory." The article draws an analogy to operating systems where the LLM functions as a CPU and its context window as RAM—serving as the model's working memory with limited capacity that must be carefully curated.

Context engineering applies across three main context types: (1) Instructions—prompts, memories, few-shot examples, tool descriptions; (2) Knowledge—facts, memories; (3) Tools—feedback from tool calls. The article emphasizes that for agents performing long-running tasks with accumulating tool feedback, context management becomes critical to avoid exceeding context window limits, ballooning costs/latency, and performance degradation.

The article identifies common context problems cited by Drew Breunig: **Context Poisoning** (hallucinations entering context), **Context Distraction** (overwhelming training data), **Context Confusion** (superfluous context influencing responses), and **Context Clash** (disagreeing context parts).

**Four Core Context Engineering Strategies:**

**1. Write Context** (saving outside context window):
- **Scratchpads:** Note-taking mechanisms that persist information during task execution. Anthropic's multi-agent researcher saves plans to memory when approaching the 200K token limit. Can be implemented as tool calls writing to files or as fields in runtime state objects.
- **Memories:** Persisting information across multiple sessions. Reflexion introduced reflection after each agent turn with self-generated memories. Generative Agents created memories synthesized periodically from past feedback. Popular implementations include ChatGPT, Cursor, and Windsurf's auto-generated long-term memories.

**2. Select Context** (pulling into context window):
- **Scratchpad Retrieval:** Via tool calls for file-based scratchpads, or state exposure for runtime state scratchpads.
- **Memory Selection:** Fetching episodic memories (few-shot examples), procedural memories (instructions), or semantic memories (facts). Code agents commonly use specific files always pulled into context: Claude Code uses CLAUDE.md; Cursor and Windsurf use rules files. For larger collections, embeddings and knowledge graphs assist with selection. Challenge: ensuring relevant memory retrieval without unexpected injections.
- **Tool Selection:** Using RAG on tool descriptions to prevent tool overload from overlapping descriptions. Research shows 3-fold improvement in tool selection accuracy.
- **Knowledge Retrieval:** RAG presents significant challenges, especially for code agents. Windsurf's approach combines AST parsing for semantic chunking, embedding search, grep/file search, knowledge graph retrieval, and re-ranking as codebases grow.

**3. Compress Context** (retaining only required tokens):
- **Summarization:** Claude Code's "auto-compact" triggers at 95% context window usage, summarizing the full user-agent interaction trajectory. Can use recursive or hierarchical strategies. Applied at specific points: post-processing token-heavy tool calls, or at agent-agent boundaries for knowledge handoff. Cognition uses fine-tuned models for capturing specific events/decisions.
- **Trimming:** Filtering or pruning context using heuristics (e.g., removing older messages) or trained pruners like Provence for Question-Answering.

**4. Isolate Context** (splitting context):
- **Multi-Agent:** Splitting context across sub-agents with specific tools, instructions, and isolated context windows. OpenAI Swarm library emphasizes separation of concerns. Anthropic's multi-agent researcher showed sub-agents with isolated contexts outperformed single-agent because each context window focuses on narrower sub-tasks. Sub-agents operate in parallel, exploring different aspects simultaneously. Trade-offs: up to 15× more tokens, requiring careful prompt engineering for planning and coordination.
- **Sandboxing:** HuggingFace's CodeAgent outputs code containing tool calls that runs in sandboxes, isolating token-heavy objects (images, audio) from the LLM. Selected context (return values) passes back to the LLM.
- **State Management:** Runtime state objects with schemas isolate context. One field (e.g., messages) exposes to the LLM at each turn while other fields selectively store information for later use.

**LangGraph Implementation:** The article presents LangGraph as purpose-built for context engineering with: (1) Thread-scoped (short-term) memory via checkpointing for scratchpad functionality; (2) Long-term memory persisting context across sessions with flexible storage (LangMem provides memory management abstractions); (3) Fine-grained state control—fetching state within each node to control LLM context exposure; (4) Bigtool library for semantic search over tool descriptions; (5) Built-in compression utilities for summarizing/trimming message lists, with logic for post-processing tool calls or work phases; (6) State schemas and sandbox support (E2B, Pyodide) for context isolation; (7) Multi-agent libraries (supervisor, swarm). LangSmith complements with agent tracing/observability for tracking token usage and evaluation for testing context engineering impact.

The article emphasizes a virtuous feedback loop: identify context engineering opportunities with LangSmith observability → implement with LangGraph → test with LangSmith evaluation → repeat.

---

Title: Prompts are code, .json/.md files are state
Tags: agents, agentic engineering, code agents, context engineering, determinism, prompt engineering, state management, tools, workflow
URL: https://mariozechner.at/posts/2025-06-02-prompts-are-code/
<br/>
Summary:<br/>
See notes: Taming agentic engineering - Prompts are code, .json/.md files are state.

This article presents a structured framework for "agentic engineering" by conceptualizing LLMs as "shitty general purpose computers" that can be programmed using natural language prompts. The author addresses the core challenges of using LLM coding tools on large, established codebases and proposes a metaprogramming approach where prompts serve as "code" and JSON/Markdown files serve as persistent state.

**Core Problems with Current Agentic Tools:**

**Context Limitations:** LLM tools lack comprehensive codebase understanding either due to incomplete context provision or insufficient context window size. Even with full context, LLMs struggle with execution flow beyond sequential scripts—they get lost in multi-process systems, IPC, client-server architectures, and concurrent execution.

**Lack of Taste:** LLMs generate the statistical mean of code they've trained on, resulting in over-engineered solutions rather than elegant, minimal designs. They reach for "best practices" that create maintenance and bug-hiding complexity.

**Context Degradation:** Performance degrades around 100K tokens regardless of benchmark claims. Models lose track of details buried in context middle. Many tools (like Cursor) further reduce context to save token costs, potentially missing crucial information.

**Limited Control:** Most tools inject system prompts, additional instructions, and tool definitions that eat context and provide opportunities for model confusion. Claude Code provides the best control with essentially unlimited tokens on Max plan, though it still has unchangeable system prompts and VS Code integration additions.

**The LLM-as-Computer Framework:**

The author maps traditional programming concepts to LLM interactions:

**Program = Prompt:** Written in natural language, specifying initial inputs, "importing" external functions via tool descriptions, implementing business logic through control flow (sequential steps, loops, conditionals, goto). Tool calls and user input serve as I/O.

**Inputs (Three Sources):**
1. Prepared information (codebase docs, style guides, architecture) baked into prompts or loaded from disk
2. User input during execution (clarifications, corrections, requirements)
3. Tool outputs (file contents, command results, API responses)

**State (Persistent and Ephemeral):**
- Context window state is treated as ephemeral since compaction eventually wipes it
- Substantial state serializes to disk: JSON for structured data (enabling surgical updates via jq), Markdown for smaller unstructured data
- Disk-based state enables resuming from any point with fresh context, completely sidestepping compaction issues

**Outputs (Multiple Artifact Types):**
- Generated code and diffs
- Opened files in editors
- Codebase statistics
- Change summaries
- Any artifact documenting the program's actions

**Real-World Application: Porting Spine Runtimes**

The author applied this framework to port changes in Spine skeletal animation software between releases (4,820 insertions, 4,679 deletions across 79 Java files) to multiple target languages. The manual process was tedious and error-prone: scanning changesets, planning dependency order, porting line-by-line while maintaining compilability, facing walls of errors due to brain fatigue.

**The "Port Java to X" Program Structure:**

**Initial Input and State (porting-plan.json):**
- Metadata: source/target branches, paths, target language
- deletedFiles: removed Java files needing corresponding deletions
- portingOrder: changed files with type arrays containing name, kind, line ranges, porting state, candidate target files
- The portingState field ("pending"/"done") enables resumable sessions

**Pre-generation via generate-porting-plan.js:**
- Runs git diff to find changed Java files
- Uses lsp-cli to extract complete type information from Java and target runtime
- Analyzes dependencies to create porting order (enums → interfaces → classes)
- Finds candidate files in target runtime
- Outputs structured JSON queryable via jq

**Why Pre-generate:**
- Determinism: same inputs always produce same plan
- Context efficiency: avoids wasting tokens/turns on exploration
- Speed: seconds vs. orders of magnitude longer LLM exploration
- Transforms open-ended exploration into structured data processing

**Function Library (Tools):**
- **VS Code Integration (vs-claude MCP):** Opens files/diffs for human review, keeping humans in the loop
- **Progress Tracking (jq queries):** Pre-written, tested queries for progress percentage, types by state, completed types list, remaining count
- **Compile Testing:** Language-specific build commands with explicit warnings about what not to do (preventing wasted time on individual TypeScript/Haxe file compilation)

**Main Workflow (Deterministic Loop):**

1. **Setup (One-time):**
   - Read metadata from porting-plan.json via jq
   - Abort if fails (defensive programming ensuring required input exists)
   - Generate conventions file if missing: analyze target runtime for coding patterns (class syntax, naming, inheritance, file organization, namespace structure, memory management, error handling, documentation format, type system specifics, property patterns). Uses task agents in parallel. User reviews before proceeding.
   - Create porting-notes.md if missing (scratchpad for observations and edge cases discovered during porting)

2. **Port Types Loop:**
   - Find next pending type via precise jq query
   - Open files in VS Code (Java file, Java diff, candidate target files)
   - Human checkpoint: ask "Port this type?" and wait for confirmation (safety mechanism)
   - Read source files: **ENTIRE files** into context for accurate porting (emphasis prevents LLM laziness)
   - Port the type: follow conventions, create target files if needed, port incrementally (structure first, then implementations), use MultiEdit for changes, ensure 100% functional parity, update documentation
   - Human checkpoint: show diff, summarize work, ask "Mark as done?"
   - Update state: use jq to surgically modify portingState field in porting-plan.json
   - Update porting-notes.md with new patterns/edge cases
   - Human checkpoint: show what was ported, ask "Continue to next type?"

**Key Insights:**

The workflow demonstrates structured thinking: initialization, precise function calls, state management, human checkpoints, deterministic loops. Unlike ad hoc prompting where conversations meander, this programmatic approach creates a reproducible, resumable workflow. The LLM becomes a reliable executor of structured instructions rather than an unpredictable chat partner.

**Results:** What previously took 2-3 weeks of manual porting now takes 2-3 days. The tedious mechanical tasks are automated, freeing the author to focus on genuinely difficult problems requiring human insight.

**Future Work:** Testing/debugging workflows (instrumenting prompts to write state at key points for execution traces), structured sub-agent orchestration with observability and communication channels (main agent defines explicit workflows for sub-agents rather than generating them ad hoc).

**Core Philosophy:** By treating LLMs as programmable computers rather than conversational partners, the framework represents a step toward turning AI-assisted coding into an engineering discipline rather than "throwing shit at the wall." The mental model transforms work with established codebases by applying structured, deterministic workflows. The approach acknowledges LLM limitations while maximizing reliability through engineering practices: precise specifications, state persistence, human oversight, and resumability.

---
