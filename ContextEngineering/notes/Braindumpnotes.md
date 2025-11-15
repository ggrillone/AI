Context Engineering Knowledge Share

What is context engineering
* TODO
* https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents 

What problem(s) does context engineering solve
* TODO
* https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents 

Context engineering vs. prompt engineering
* TODO
* https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents 

Strategies for managing context
* Breaking tasks into smaller pieces (Decomposition)
* Having the agent write to planning / AI log files (structured note-taking)
  * Agents can summarize for you, but this gives you more control
  * Can more easily switch to a new chat and continue from where you left off
* Context editing
  * If you find your chat going in the wrong direction or want to branch off at multiple points
    * In Cursor you can branch off from a past point find the user prompt you want as the “last left off point”
      * Click the “…”
      * Click “Duplicate Chat”
  * The chat goes in the wrong direction and you want to backtrack
    * Find your user prompt where the agent started to diverge and click into it
    * Change the prompt and hit enter
    * You will get a pop-up from Cursor - Submit from previous message?
      * Select “Continue and revert”
      * Observe how the context % used goes down, that “bad context” is cleared and you can continue in the same chat
  * The agent makes a tool call, but it’s the wrong tool call
    * Revert back to the point before it made that tool call
    * This wrong tool call only pollutes your context window with irrelevant information
* “Just in time” context strategies
  * “Rather than pre-processing all relevant data up front, agents built with the “just in time” approach maintain lightweight identifiers (file paths, stored queries, web links, etc.) and use these references to dynamically load data into context at runtime using tools.” (https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents )
* Sub-agents (multi-agent architecture)
  * Several other concepts are needed to leverage sub-agents
    * Decomposition
    * Research / planning
    * Structured note taking (planning file & AI log file)
  * You break your task into stages and store relevant context/memoy for sub-agents to use
    * e.g.
      * An initial agent that does the research
      * 2nd agent does the planning
      * All of the context goes into a md file (or multiple files)
      * Now sub-agents can follow instructions and execute
      * The md file(s) from the initial agent(s) should contain all context that the sub-agents need
        * Each sub-agent now does not need to go make the same tool calls to gather context
        * The context is complete and the sub-agents can reference the information they need to complete their individual tasks
        * Each sub-agent has its own context window
      * Achieves a clear separation of concerns

Important to be aware of
* A larger context window does not necessarily equate to “I can use this single chat longer”
  * https://research.trychroma.com/context-rot 
  * TODO: expand on this area more

Best practices
* Don’t wait until your context window to reach 100%, stay closer to 70%
  * When you get to 60% context usage, start thinking about wrapping up the current chat
  * Write all necessary information to a md file so you can continue in a new chat (Compaction)
    * If you prefer ask the agent to summarize (e.g. in Cursor the “/Summarize” slash command)
    * But this hands over the reigns to the agent, I prefer explicitly writing to a file and taking the extra time to include what I want specifically in my prompt to the agent when telling it to create this file

* What is a token
* Token cost
* Input vs Output tokens
  * https://token-calculator.net/ 
    * Use to show cost differences
    * Not really a good way to estimate input tokens (and definitely can’t estimate output tokens) because the agent can look at code files you didn’t specify and you can’t predict caching it will use
  * Output tokens cost more
  * Output tokens
    * Chat output + code generated = output token
    * Think about what you want it to output - might want the chat to output concise bullet points to reduce token usage
* Context windows
  * https://docs.anthropic.com/en/docs/build-with-claude/context-windows
  * There’s a practical limit to how much information a model can consider at once = context window
  * Working memory
  * Your prompts + AI response + other information you provide —> context window
  * TODO
* Context poisoning 
* Context confusion
* Context distraction
* Context conflict
* Context rot



* https://www.promptingguide.ai/guides/context-engineering-guide 
  * https://cognition.ai/blog/dont-build-multi-agents
  * https://rlancemartin.github.io/2025/06/23/context_engineering/
  * https://www.philschmid.de/context-engineering
  * https://simple.ai/p/the-skill-thats-replacing-prompt-engineering?
  * https://github.com/humanlayer/12-factor-agents 
  * https://blog.langchain.com/the-rise-of-context-engineering/ 
* https://www.promptingguide.ai/techniques/rag 
* RAG vs. Long Context
  * https://arxiv.org/abs/2501.01880
  * See RAG tutorial: https://www.anthropic.com/learn/build-with-claude 
* https://github.com/NirDiamant/RAG_Techniques 
* https://docs.anthropic.com/en/docs/build-with-claude/context-windows 
* https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html 
  * https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html 
* The New Skill in AI is Not Prompting, It's Context Engineering
* Context Engineering
* Taming agentic engineering - Prompts are code, .json/.md files are state
* https://www.fuzzycomputer.com/posts/onboarding 
* https://tomtunguz.com/input-output-ratio/
* https://research.trychroma.com/context-rot
* https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md 
* https://www.vincirufus.com/posts/context-engineering/ 
* https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents 
* https://www.motivenotes.ai/p/what-makes-5-of-ai-agents-actually 
* https://mbleigh.dev/posts/context-engineering-with-links/ 
* https://blog.abdellatif.io/production-rag-processing-5m-documents 
* https://www.anthropic.com/news/context-management 
  * “The memory tool operates entirely client-side through tool calls. Developers manage the storage backend, giving them complete control over where the data is stored and how it’s persisted.”
  * Context Editing
    * “Enable longer conversations by automatically removing stale tool results from context”
    * “Context editing clears old file reads and test results while memory preserves debugging insights and architectural decisions, enabling agents to work on large codebases without losing progress.”
    * “Memory stores key findings while context editing removes old search results, building knowledge bases that improve performance over time.”
    * “Agents store intermediate results in memory while context editing clears raw data, handling workflows that would otherwise exceed token limits.”
* https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents 
* https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/memory_cookbook.ipynb 
* https://jxnl.co/writing/2025/08/28/context-engineering-index 
* https://www.anthropic.com/engineering/contextual-retrieval 
  * https://github.com/anthropics/claude-cookbooks/tree/main/capabilities/contextual-embeddings 
* https://www.anthropic.com/engineering/code-execution-with-mcp
* https://refactoring.fm/p/managing-context-for-ai-coding
* https://jxnl.co/writing/2025/08/28/context-engineering-index/ 
  * https://jxnl.co/writing/2025/08/27/facets-context-engineering/
  * https://jxnl.co/writing/2025/08/29/context-engineering-slash-commands-subagents/
  * https://jxnl.co/writing/2025/08/30/context-engineering-compaction/
  * https://jxnl.co/writing/2025/09/04/context-engineering-agent-frameworks-and-form-factors/
  * https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/ 
