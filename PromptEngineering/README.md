# Table of Contents

1. [TLDR](00-TLDR.md)
2. [Introduction and Foundations](01-introduction-and-foundations.md)
3. [Foundations Continued](01b-foundations-continued.md)
4. [Intermediate Lessons](02-intermediate-lessons.md)
5. [Intermediate Lessons Continued](02b-intermediate-lessons-continued.md)
6. [Advanced Lessons](03-advanced-lessons.md)
7. [Advanced Lessons Continued](03b-advanced-lessons-continued.md)
8. [Advanced Lesson 18 Summary](03c-advanced-lesson-18-summary.md)
9. [Expert Techniques](04-expert-techniques.md)
10. [Expert Techniques Continued](04b-expert-techniques-continued.md)
11. [Resources](05-resources.md)
12. [Workflows](06-workflows.md)


# Building Effective Prompts - A Visual Thought Process

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    BEFORE YOU START: FOUNDATION                         │
│                                                                         │
│  • Understand: AI predicts patterns, not "knows" truth                 │
│  • Context Window = AI's "working memory" (finite)                     │
│  • Tokens = cost (input + output)                                      │
│  • Your prompt competes with context limits                            │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                  START: AI FLUENCY FRAMEWORK (4 D's)                    │
│                   [Always apply this mental model]                      │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                    ┌───────────────┴───────────────┐
                    │                               │
                    ▼                               ▼
        ┌─────────────────────┐         ┌─────────────────────┐
        │   1. DELEGATION     │◄───────►│   4. DILIGENCE      │
        │  What AI vs You?    │         │  Responsible Use?   │
        └──────────┬──────────┘         └──────────┬──────────┘
                   │                               │
                   │  ┌─────────────────────────┐  │
                   └─►│  Strategic & Ethical    │◄─┘
                      │  Decision Loop          │
                      └─────────────────────────┘
                                    │
                    ┌───────────────┴───────────────┐
                    │                               │
                    ▼                               ▼
        ┌─────────────────────┐         ┌─────────────────────┐
        │   2. DESCRIPTION    │◄───────►│   3. DISCERNMENT    │
        │  How to Communicate?│         │  How to Evaluate?   │
        └──────────┬──────────┘         └──────────┬──────────┘
                   │                               │
                   │  ┌─────────────────────────┐  │
                   └─►│  Tactical Interaction   │◄─┘
                      │  & Refinement Loop      │
                      └─────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│              DECISION POINT 1: Do I know what I want?                   │
└─────────────────────────────────────────────────────────────────────────┘
                    │
        ┌───────────┴────────────┐
        │                        │
    NO  │                        │  YES
        ▼                        ▼
┌──────────────────┐    ┌──────────────────┐
│  EXPLORATION     │    │  IMPLEMENTATION  │
│  (Vague Prompt)  │    │ (Specific Prompt)│
└────────┬─────────┘    └────────┬─────────┘
         │                       │
         │                       │
         ▼                       ▼
┌──────────────────┐    ┌──────────────────┐
│ Use Cases:       │    │ Use Cases:       │
│ • Brainstorming  │    │ • Known solution │
│ • Learning       │    │ • Following      │
│ • Getting unstuck│    │   patterns       │
│ • Exploring      │    │ • Implementing   │
│   alternatives   │    │   requirements   │
└──────────────────┘    └──────────────────┘
         │                       │
         └──────────┬────────────┘
                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│              DECISION POINT 2: Task Complexity Level?                   │
└─────────────────────────────────────────────────────────────────────────┘
         │
         ├────── SIMPLE ────────────────────────────┐
         │       (1-2 requirements)                 │
         │                                          ▼
         │                              ┌─────────────────────┐
         │                              │  BASIC PROMPT       │
         │                              │  ===============    │
         │                              │  • Clear instruction│
         │                              │  • Input data       │
         │                              │  • Output format    │
         │                              │                     │
         │                              │  Technique:         │
         │                              │  → Zero-Shot        │
         │                              └─────────────────────┘
         │
         ├────── MODERATE ──────────────────────────┐
         │       (3-5 requirements)                 │
         │                                          ▼
         │                              ┌─────────────────────┐
         │                              │ STRUCTURED PROMPT   │
         │                              │ ===============     │
         │                              │ • Role prompting    │
         │                              │ • Context           │
         │                              │ • Examples (if      │
         │                              │   project-specific) │
         │                              │ • Constraints       │
         │                              │                     │
         │                              │ Techniques:         │
         │                              │ → Few-Shot          │
         │                              │ → Chain of Thought  │
         │                              └─────────────────────┘
         │
         └────── COMPLEX ───────────────────────────┐
                 (6+ requirements,                  │
                  multi-phase)                      ▼
                                         ┌─────────────────────┐
                                         │ ADVANCED PROMPT     │
                                         │ ===============     │
                                         │ • Meta prompting    │
                                         │ • Prompt chaining   │
                                         │ • Planning files    │
                                         │ • Validation steps  │
                                         │                     │
                                         │ Techniques:         │
                                         │ → Meta Prompting    │
                                         │ → Prompt Chaining   │
                                         │ → Tree of Thoughts  │
                                         │ → ReAct             │
                                         │ → Reflexion         │
                                         └─────────────────────┘
                                                  │
                                                  ▼
┌─────────────────────────────────────────────────────────────────────────┐
│           PROMPT ANATOMY: Essential Components to Include               │
└─────────────────────────────────────────────────────────────────────────┘
         │
         ▼
    ┌─────────────────────────────────────────────────┐
    │  BASIC ELEMENTS (choose what's needed):         │
    │  ──────────────────────────────────────────     │
    │  1. Instruction - What to do                    │
    │  2. Context - Why & background                  │
    │  3. Input Data - What to work with              │
    │  4. Output Format - How to structure response   │
    │  5. Constraints - Boundaries & requirements     │
    │                                                  │
    │  ADVANCED ELEMENTS (for complex tasks):         │
    │  ──────────────────────────────────────────     │
    │  6. Role/Objective - Who AI should act as       │
    │  7. Validation - How to verify correctness      │
    │  8. Stop Conditions - When to pause/clarify     │
    │  9. Error Handling - How to handle unknowns     │
    │  10. Examples - Show desired patterns           │
    └─────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────────────┐
│            PROMPT FORMATTING: Structure for Clarity                     │
└─────────────────────────────────────────────────────────────────────────┘
         │
         ├─── Simple Task ──► Natural flow / Simple labels
         │
         ├─── Moderate ────► Markdown headers (##)
         │
         └─── Complex ─────► XML-style tags <task></task>
                             (maximum parseability)
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────────────┐
│              TECHNIQUE SELECTION: Match Task to Method                  │
└─────────────────────────────────────────────────────────────────────────┘
                          │
              ┌───────────┴───────────┐
              │                       │
              ▼                       ▼
    ┌──────────────────┐    ┌──────────────────┐
    │ FOUNDATIONAL     │    │  INTERMEDIATE    │
    │ ──────────────   │    │  ──────────────  │
    │                  │    │                  │
    │ Zero-Shot        │    │ Role Prompting   │
    │ ├─ When?         │    │ ├─ Set context   │
    │ └─ Simple,       │    │ │  & expertise   │
    │    standard      │    │ └─ Start of      │
    │    tasks         │    │    sessions      │
    │                  │    │                  │
    │ Few-Shot         │    │ Chain of Thought │
    │ ├─ When?         │    │ ├─ When?         │
    │ └─ Project       │    │ └─ Complex       │
    │    patterns,     │    │    reasoning,    │
    │    consistency   │    │    debugging     │
    │                  │    │                  │
    │ Vague vs Specific│    │ Reducing         │
    │ ├─ Intentional   │    │ Hallucinations   │
    │ │  choice        │    │ ├─ Allow "I      │
    │ └─ Based on goal │    │ │  don't know"   │
    │                  │    │ ├─ Cite sources  │
    └──────────────────┘    │ └─ Constrain to  │
              │             │    context       │
              │             └──────────────────┘
              │                       │
              └───────────┬───────────┘
                          ▼
    ┌─────────────────────────────────────────────┐
    │           ADVANCED TECHNIQUES               │
    │           ──────────────────────            │
    │                                             │
    │  Meta Prompting                             │
    │  ├─ When? Multi-phase workflows             │
    │  └─ Defines HOW to think & respond          │
    │                                             │
    │  Prompt Chaining                            │
    │  ├─ When? Large tasks, context limits       │
    │  └─ Output₁ → Prompt₂ → Output₂ → ...     │
    │                                             │
    │  Self-Consistency                           │
    │  ├─ When? Critical decisions                │
    │  └─ Run 3-5x, compare reasoning             │
    │                                             │
    │  Tree of Thoughts                           │
    │  ├─ When? Explore solution space            │
    │  └─ Branch → Evaluate → Prune → Continue   │
    │                                             │
    │  ReAct (Reasoning + Acting)                 │
    │  ├─ When? Research, adaptive tasks          │
    │  └─ Thought → Action → Observation → Loop  │
    │                                             │
    │  Reflexion                                  │
    │  ├─ When? Quality-critical code             │
    │  └─ Generate → Evaluate → Reflect → Revise │
    └─────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                DECISION POINT 3: Did the prompt work?                   │
└─────────────────────────────────────────────────────────────────────────┘
                          │
              ┌───────────┴────────────┐
              │                        │
          YES │                        │ NO
              ▼                        ▼
      ┌──────────────┐       ┌─────────────────────────────┐
      │  SUCCESS!    │       │  DIAGNOSTIC QUESTIONS       │
      │  ──────────  │       │  ───────────────────────    │
      │ Proceed with │       │  (Ask these systematically) │
      │ implementation│      └─────────────────────────────┘
      └──────────────┘                   │
                                         ▼
         ┌────────────────────────────────────────────────────┐
         │ 1. CLARITY & CONTEXT                               │
         │    • Was there enough context?                     │
         │    • Was there too much context? (Check % used)    │
         │    • Was wording too vague?                        │
         │    • Did I clearly state goal/output format?       │
         │    • Did I specify what NOT to include?            │
         │    • Was I mixing too many tasks?                  │
         │                                                    │
         │ 2. ASSUMPTIONS & MENTAL MODELS                     │
         │    • What assumptions did I make that AI didn't?   │
         │    • Did I assume domain knowledge?                │
         │    • Did I assume AI "knows" my intent?            │
         │                                                    │
         │ 3. STRUCTURE & SCOPE                               │
         │    • Was prompt too open-ended or constrained?     │
         │    • Was scope too large for single response?      │
         │    • Did I include step-by-step or just outcome?   │
         │    • Was detail level appropriate?                 │
         │                                                    │
         │ 4. ITERATION & OUTPUT QUALITY                      │
         │    • Were more changes made than expected?         │
         │    • What parts were correct? Incorrect?           │
         │    • Did AI hallucinate? Why?                      │
         │    • Did it follow all instructions?               │
         │    • Was tone/structure/format off?                │
         │                                                    │
         │ 5. PROMPT FORMULATION                              │
         │    • Could I break into multiple prompts?          │
         │    • Did I use examples (few-shot)?                │
         │    • Could I rephrase as user story?               │
         │    • Too much fluff or too few directives?         │
         └────────────────────────────────────────────────────┘
                                │
                                ▼
                    ┌────────────────────────┐
                    │   REFINEMENT ACTIONS   │
                    │   ──────────────────   │
                    │                        │
                    │ • Adjust specificity   │
                    │ • Add examples         │
                    │ • Break into sub-tasks │
                    │ • Clarify constraints  │
                    │ • Add validation steps │
                    │ • Try different model  │
                    │ • Start fresh chat     │
                    └────────────────────────┘
                                │
                                ▼
                    ┌────────────────────────┐
                    │  ITERATE & RETRY       │
                    └────────────────────────┘
                                │
                                └──────┐
                                       │
                                       ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                EXPERT LEVEL: Optimization & Scale                       │
└─────────────────────────────────────────────────────────────────────────┘
         │
         ├─── System Prompts ──────────────┐
         │    (Project-wide standards)      │
         │                                  ▼
         │                    ┌──────────────────────────┐
         │                    │ .cursor/rules            │
         │                    │ • Tech stack             │
         │                    │ • Coding standards       │
         │                    │ • Quality requirements   │
         │                    │ • Team conventions       │
         │                    └──────────────────────────┘
         │
         ├─── Prompt Templates ────────────┐
         │    (Reusable patterns)           │
         │                                  ▼
         │                    ┌──────────────────────────┐
         │                    │ {{Variable}} placeholders │
         │                    │ • Component generation   │
         │                    │ • Refactoring patterns   │
         │                    │ • Test creation          │
         │                    │ • Code review            │
         │                    └──────────────────────────┘
         │
         └─── Golden Test Sets ────────────┐
              (Quality validation)         │
                                           ▼
                             ┌──────────────────────────┐
                             │ Test prompt quality      │
                             │ • Track improvements     │
                             │ • Team benchmarks        │
                             │ • Regression prevention  │
                             └──────────────────────────┘
                                           │
                                           ▼
┌─────────────────────────────────────────────────────────────────────────┐
│              PERSONAL WORKFLOWS: For Large/Complex Work                 │
└─────────────────────────────────────────────────────────────────────────┘
         │
         ├─── AILog.md ─────────────────────────────────────────┐
         │    For multi-session continuity                      │
         │    • Track progress                                  │
         │    • Document decisions                              │
         │    • Enable context switching                        │
         │    • Handoff to another session/agent               │
         │                                                      │
         ├─── Planning Files ───────────────────────────────────┤
         │    For complex features                              │
         │    Phase 1: Create plan → plan.md                   │
         │    Phase 2: Execute sequentially                     │
         │    • Manage large context                            │
         │    • Clear implementation steps                      │
         │                                                      │
         ├─── Execution Checklists ─────────────────────────────┤
         │    For tracking progress                             │
         │    • Break into tasks                                │
         │    • Mark completion                                 │
         │    • Validate each step                              │
         │                                                      │
         └─── Code Comment Stubbing ───────────────────────────┘
              For tests & structured implementation
              • Write intent as comments
              • Have AI implement following structure
              • Ensures coverage & organization
                                           │
                                           ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     FINAL VALIDATION CHECKLIST                          │
└─────────────────────────────────────────────────────────────────────────┘
         │
         ▼
    ┌─────────────────────────────────────────────────────┐
    │  Before Accepting AI Output:                        │
    │  ─────────────────────────────                      │
    │  □ Meets all stated requirements                    │
    │  □ No hallucinations or invented APIs               │
    │  □ Follows project conventions                      │
    │  □ Handles edge cases                               │
    │  □ Includes error handling                          │
    │  □ Accessible (if UI component)                     │
    │  □ Secure (if handling data/auth)                   │
    │  □ Tested or testable                               │
    │  □ Documented appropriately                         │
    │  □ YOU understand the solution                      │
    │                                                     │
    │  Remember: YOU ARE RESPONSIBLE, NOT THE AI          │
    └─────────────────────────────────────────────────────┘
```