# Part 3: Advanced Lessons (Continued)

## Lesson 15: Tree of Thoughts (ToT)

### Objectives
- Understand Tree of Thoughts as an exploration framework
- Learn to generate and evaluate multiple reasoning branches
- Master backtracking and path selection techniques
- Apply ToT to complex problem-solving scenarios

### Explanation

#### What is Tree of Thoughts?

Tree of Thoughts extends Chain of Thought by enabling the model to **explore multiple reasoning branches simultaneously**, evaluate each path, and backtrack if needed—like exploring a decision tree.

**Key Difference:**
- **Chain of Thought**: Linear reasoning (A → B → C)
- **Tree of Thoughts**: Branching exploration (A → [B1, B2, B3] → evaluate → continue best path)

**Analogy**: Think of learning a new framework like React.
- You start with a problem: "Can React solve this?"
- You explore different React features (hooks, context, etc.)
- For each feature, you evaluate: "Does this help?"
- You backtrack from dead ends
- You combine successful branches into a solution

#### Structure of ToT

```
                    Initial Problem
                         |
        ┌────────────────┼────────────────┐
        │                │                │
    Branch 1         Branch 2         Branch 3
    (Approach A)     (Approach B)     (Approach C)
        │                │                │
    Evaluate         Evaluate         Evaluate
        │                │                │
   [Continue]       [Backtrack]      [Continue]
        │                                 │
    ┌───┴───┐                        ┌────┴────┐
 Sub-B1  Sub-B2                   Sub-C1   Sub-C2
```

#### Components of ToT

1. **Thought Generation**: Create multiple possible next steps
2. **Evaluation**: Assess each thought's promise
3. **Selection**: Choose which path(s) to explore
4. **Backtracking**: Abandon unproductive paths
5. **Aggregation**: Combine successful branches

#### When to Use ToT

✅ **Good for:**
- Complex problems with multiple approaches
- Situations requiring exploration of alternatives
- Architecture decisions with many options
- Optimization problems
- When you need to understand the solution space

❌ **Not needed for:**
- Problems with one clear path
- Simple, straightforward tasks
- Time-sensitive decisions
- When you already know the approach

### Step-by-Step Tutorial

**Implementing Tree of Thoughts**

**Step 1: Frame the Problem**

```markdown
Problem: Design a state management solution for a complex React application

Requirements:
- 50+ components need shared state
- Real-time updates from WebSocket
- Offline support with sync
- Complex forms with validation
- Performance is critical
```

**Step 2: Generate Initial Branches**

```markdown
Explore different architectural approaches:

Branch 1: Redux + Redux Toolkit
- Evaluate: How well does this fit our needs?
- Strengths: [List]
- Weaknesses: [List]
- Score: [1-10]

Branch 2: Zustand
- Evaluate: How well does this fit our needs?
- Strengths: [List]
- Weaknesses: [List]
- Score: [1-10]

Branch 3: Jotai + TanStack Query
- Evaluate: How well does this fit our needs?
- Strengths: [List]
- Weaknesses: [List]
- Score: [1-10]

Branch 4: XState + React Context
- Evaluate: How well does this fit our needs?
- Strengths: [List]
- Weaknesses: [List]
- Score: [1-10]
```

**Step 3: Evaluate and Prune**

```markdown
Based on evaluation scores:
- Branches 1 and 3 scored 8+: Continue exploring
- Branches 2 and 4 scored below 7: Set aside (may revisit)

Focus exploration on Branch 1 (Redux) and Branch 3 (Jotai+TQ)
```

**Step 4: Deepen Promising Branches**

```markdown
Branch 1: Redux + Redux Toolkit
├─ Sub-branch 1a: Standard Redux patterns
│  ├─ How to handle real-time updates?
│  ├─ How to handle offline sync?
│  └─ Evaluation: [Score]
│
├─ Sub-branch 1b: Redux + RTK Query
│  ├─ How does RTK Query help with real-time?
│  ├─ How does it handle offline?
│  └─ Evaluation: [Score]
│
└─ Sub-branch 1c: Redux + custom middleware
   ├─ Custom WebSocket middleware
   ├─ Offline sync middleware
   └─ Evaluation: [Score]

Branch 3: Jotai + TanStack Query
├─ Sub-branch 3a: Standard approach
│  └─ Evaluation: [Score]
│
└─ Sub-branch 3b: Jotai for local state, TQ for server state
   ├─ Clear separation of concerns
   ├─ Each tool for its strength
   └─ Evaluation: [Score]
```

**Step 5: Compare Final Candidates**

```markdown
After exploration, strongest candidates:
1. Redux + RTK Query (Branch 1b)
2. Jotai + TanStack Query with separation (Branch 3b)

Final comparison:
- Team familiarity
- Learning curve
- Performance
- Maintenance burden
- Community support

Recommendation: [Based on trade-offs]
```

### Examples & Exercises

**Example 1: Performance Optimization with ToT**

**Problem:**
```markdown
React app has performance issues. Users experience lag during interactions.
```

**ToT Prompt:**
```markdown
Explore different causes and solutions for this performance problem.

Initial Problem: Lag during user interactions

# Branch 1: Investigate Rendering Performance
1. Could it be excessive re-renders?
   - How would we verify this?
   - What solutions exist?
   - Evaluate: How likely is this the cause? [1-10]

2. Could it be large component trees?
   - How would we verify this?
   - What solutions exist?
   - Evaluate: How likely is this the cause? [1-10]

# Branch 2: Investigate Data/State
1. Could it be inefficient state updates?
   - What patterns would cause this?
   - How to verify?
   - Evaluate likelihood: [1-10]

2. Could it be large state objects?
   - What would indicate this?
   - Solutions?
   - Evaluate likelihood: [1-10]

# Branch 3: Investigate External Factors
1. Could it be API slowness?
   - How to verify?
   - Solutions?
   - Evaluate: [1-10]

2. Could it be bundle size/parsing?
   - Metrics to check?
   - Solutions?
   - Evaluate: [1-10]

For branches scoring 7+, explore deeper.
For branches scoring below 5, set aside.

Then, explore the most promising branch with sub-solutions.
```

**Expected Flow:**
1. Generate all branches
2. Evaluate each (maybe rendering scores 9, state scores 7, external scores 4)
3. Prune external factors (score too low)
4. Explore rendering and state branches deeper
5. Identify specific issues
6. Propose combined solution

**Example 2: Component Design with ToT**

**Problem:**
```markdown
Design a flexible, reusable Table component for our design system.

Requirements:
- Sortable columns
- Filterable rows
- Pagination
- Row selection
- Expandable rows
- Custom cell renderers
- Responsive
- Accessible
```

**ToT Approach:**
```markdown
# Initial Branches: Architecture Patterns

Branch 1: Monolithic Component
├─ All features in one component
├─ Props-based configuration
└─ Evaluate:
   - Flexibility: [Score]
   - Complexity: [Score]
   - Reusability: [Score]
   - Overall: [Score]

Branch 2: Compound Components
├─ Table, Table.Header, Table.Row, Table.Cell pattern
├─ Composition-based
└─ Evaluate:
   - Flexibility: [Score]
   - Complexity: [Score]
   - Reusability: [Score]
   - Overall: [Score]

Branch 3: Headless Component + UI
├─ Separate logic (hooks) from presentation
├─ Multiple UI implementations possible
└─ Evaluate:
   - Flexibility: [Score]
   - Complexity: [Score]
   - Reusability: [Score]
   - Overall: [Score]

Branch 4: Render Props Pattern
├─ Maximum flexibility via render functions
└─ Evaluate:
   - Flexibility: [Score]
   - Complexity: [Score]
   - Reusability: [Score]
   - Overall: [Score]

---

Based on scores, explore top 2 branches deeper.

# Deeper Exploration (assuming Branches 2 and 3 scored highest)

Branch 2: Compound Components
├─ Sub-branch 2a: How to handle sorting?
│  ├─ Option A: Built-in sort logic
│  ├─ Option B: onSort callback, user controls
│  └─ Evaluation: Which fits better?
│
├─ Sub-branch 2b: How to handle state?
│  ├─ Option A: Controlled (user provides state)
│  ├─ Option B: Uncontrolled (internal state)
│  ├─ Option C: Both modes supported
│  └─ Evaluation: Which is most flexible?
│
└─ Assess: Does this approach meet all requirements?

Branch 3: Headless + UI
├─ Sub-branch 3a: What does headless hook expose?
│  ├─ Table state management
│  ├─ Sort/filter/pagination logic
│  ├─ Row selection logic
│  └─ Accessibility helpers
│
├─ Sub-branch 3b: UI layer flexibility
│  ├─ Can support different styling approaches?
│  ├─ Can support different HTML structures?
│  └─ Evaluation: Future-proof enough?
│
└─ Assess: Implementation complexity worth the flexibility?

---

Final Decision:
Compare refined approaches from Branches 2 and 3.
Consider:
- Team skill level
- Maintenance burden
- Usage patterns
- Extensibility needs

Recommendation: [Choice with reasoning]
```

**Exercise 1: Apply ToT to a Real Problem**

**Scenario:** Your app needs to support multiple languages (i18n). Explore the solution space.

**Your Task:** Create a ToT prompt exploring at least 3 main branches and 2 sub-branches for the most promising approaches.

**Solution:**

```markdown
# Problem: Implement Internationalization (i18n)

Requirements:
- Support 10+ languages
- Dynamic language switching
- Pluralization support
- Number/date formatting
- TypeScript type safety for translation keys
- Server-side rendering compatible

# Initial Branches

## Branch 1: react-i18next
Evaluate this popular i18n library:
- Pros:
  - Most popular React i18n solution
  - Rich feature set
  - Strong community
  - SSR support
- Cons:
  - Large bundle size (~35kb)
  - Complex setup
  - Learning curve
- Score: [1-10]
- Decision: [Continue/Prune]

## Branch 2: next-i18next (if using Next.js)
Evaluate Next.js-specific solution:
- Pros:
  - Optimized for Next.js
  - Built-in SSR/SSG support
  - Uses react-i18next under hood
- Cons:
  - Tied to Next.js
  - Same bundle size issues
- Score: [1-10]
- Decision: [Continue/Prune]

## Branch 3: Format.js (react-intl)
Evaluate Format.js approach:
- Pros:
  - Standards-based (ICU message format)
  - Comprehensive formatting
  - TypeScript support
- Cons:
  - Larger API surface
  - Different mental model
- Score: [1-10]
- Decision: [Continue/Prune]

## Branch 4: Build Custom Solution
Evaluate custom implementation:
- Pros:
  - Minimal bundle size
  - Exactly what we need
  - Full control
- Cons:
  - Maintenance burden
  - Missing advanced features
  - Reinventing wheel
- Score: [1-10]
- Decision: [Continue/Prune]

---

# Deeper Exploration (Top 2 Branches)

Assuming Branch 1 (react-i18next) and Branch 3 (Format.js) scored highest:

## Branch 1: react-i18next - Detailed Analysis

### Sub-branch 1a: Translation File Structure
Options for organizing translations:
- 1a-1: Single file per language
  - `en.json`, `es.json`, `fr.json`
  - Pros: Simple
  - Cons: Large files
  
- 1a-2: Namespaced files
  - `en/common.json`, `en/auth.json`, `en/dashboard.json`
  - Pros: Code splitting possible
  - Cons: More files to manage
  
- Evaluation: Which scales better?

### Sub-branch 1b: Type Safety Approach
Options for TypeScript integration:
- 1b-1: Manual type definitions
  - Write types by hand
  - Pros: Full control
  - Cons: Maintenance burden
  
- 1b-2: Auto-generated from JSON
  - Use i18next-typescript or similar
  - Pros: Always in sync
  - Cons: Build step complexity
  
- Evaluation: Which ensures better DX?

### Sub-branch 1c: Loading Strategy
- 1c-1: Bundle all translations
  - Pros: No loading delay
  - Cons: Initial bundle size
  
- 1c-2: Lazy load by language
  - Pros: Smaller initial bundle
  - Cons: Loading spinner needed
  
- Evaluation: What's the bundle size impact?

## Branch 3: Format.js - Detailed Analysis

### Sub-branch 3a: Message Extraction
- How to extract messages from code?
- CLI tools available?
- TypeScript integration?
- Evaluation: DX impact?

### Sub-branch 3b: Bundle Optimization
- Can we tree-shake unused translations?
- What's the minimum bundle size?
- Evaluation: vs. react-i18next?

---

# Final Comparison

Based on deep exploration:

| Aspect | react-i18next (Branch 1) | Format.js (Branch 3) |
|--------|-------------------------|---------------------|
| Bundle Size | ~35kb | ~40kb |
| TypeScript DX | Good with auto-gen | Native support |
| Loading Strategy | Flexible | Flexible |
| Learning Curve | Moderate | Steeper |
| Community | Larger | Smaller but quality |

# Decision

Recommendation: [Choose based on priorities]

If bundle size critical: Might reconsider Branch 4 (custom) with limited features
If DX critical: Branch 1 with auto-generated types (Sub-branch 1b-2)
If standards-based important: Branch 3

Final choice: [With full reasoning]
```

**Validation:**
- **Self-Check**: Did you explore multiple paths?
- **Self-Check**: Did you evaluate and prune appropriately?
- **Self-Check**: Did you go deeper on promising branches?

### Frontend Contextualization

**Real-World Scenario: Choosing a Data Fetching Strategy**

Your team is building a complex dashboard with multiple data sources.

**ToT Exploration:**

```markdown
# Problem: Data Fetching Architecture

Context:
- Dashboard with 10+ widgets
- Each widget fetches different data
- Some data shared across widgets
- Real-time updates needed
- Offline support desired
- Performance critical

# Branch Exploration

## Branch 1: REST APIs + React Query
├─ How to handle shared data?
│  ├─ Sub 1a: Query key strategy
│  ├─ Sub 1b: Cache invalidation
│  └─ Evaluation: Complexity vs. performance
│
├─ How to handle real-time?
│  ├─ Sub 1c: Polling
│  ├─ Sub 1d: WebSockets + manual cache updates
│  └─ Evaluation: Which integrates better?
│
└─ Overall evaluation: [Score]

## Branch 2: GraphQL + Apollo Client
├─ How to handle shared data?
│  ├─ Automatic via normalized cache
│  └─ Evaluation: Out-of-box benefit
│
├─ How to handle real-time?
│  ├─ Subscriptions (built-in)
│  └─ Evaluation: Seamless integration
│
├─ Backend changes needed?
│  ├─ Requires GraphQL server
│  └─ Evaluation: Migration cost
│
└─ Overall evaluation: [Score]

## Branch 3: REST + SWR + WebSockets
├─ Similar to Branch 1 but with SWR
├─ How does SWR compare to React Query?
│  ├─ Features comparison
│  ├─ Bundle size
│  └─ DX differences
│
└─ Overall evaluation: [Score]

## Branch 4: tRPC + React Query
├─ End-to-end type safety
├─ No GraphQL complexity
├─ Backend requirements?
│  ├─ Needs tRPC server
│  ├─ Migration path from REST
│  └─ Evaluation: Feasibility
│
└─ Overall evaluation: [Score]

---

# Pruning Decision

Based on scores:
- Branch 2 (GraphQL): Scores high on features, low on migration feasibility [Prune for now, revisit later]
- Branch 4 (tRPC): Scores high on DX, medium on migration [Keep for consideration]
- Branch 1 (React Query): Scores well across board [Deep dive]
- Branch 3 (SWR): Similar to Branch 1 [Deep dive for comparison]

Focus on: Branch 1 vs Branch 3, with Branch 4 as alternative

---

# Deep Dive: React Query vs SWR

## Detailed Feature Comparison
[Explore specific features needed for dashboard]

## Real-time Integration
Branch 1 (React Query):
├─ Option A: WebSocket + queryClient.setQueryData
├─ Option B: Polling with refetchInterval
└─ Evaluation: Which fits better?

Branch 3 (SWR):
├─ Similar patterns available
├─ useSWRSubscription experimental
└─ Evaluation: Maturity?

## Performance Benchmarking
├─ Bundle size comparison
├─ Runtime performance
└─ Developer experience

## Decision Factors
├─ Team already familiar with React Query: +1 for Branch 1
├─ SWR lighter bundle: +1 for Branch 3
├─ React Query more features: +1 for Branch 1
└─ Conclusion: React Query wins slightly

---

# Final Recommendation

Primary: React Query (Branch 1) with WebSocket integration
Rationale:
- Team familiarity reduces risk
- Comprehensive feature set
- Strong community and ecosystem
- Well-documented real-time patterns

Alternative: tRPC + React Query (Branch 4)
- Consider for next project
- Requires backend migration
- Future-proofing option

Set aside for now: GraphQL (Branch 2)
- Revisit if backend moves to GraphQL
- Benefits are clear but migration cost too high currently
```

**Key ToT Benefits in This Scenario:**
1. **Explored multiple architectures** systematically
2. **Evaluated feasibility** not just features
3. **Pruned unrealistic options** early (GraphQL migration)
4. **Went deep on viable candidates** (React Query vs SWR)
5. **Made informed decision** based on exploration
6. **Identified future considerations** (tRPC)

**Without ToT:**
- Might jump to first familiar solution (React Query)
- Miss considering alternatives (SWR, tRPC)
- Not fully evaluate migration costs (GraphQL)
- Less confident in decision

**Practical Takeaway**: Tree of Thoughts is your structured exploration framework. Use it when you're facing decisions with multiple viable approaches and you want to thoroughly understand the solution space before committing. It's especially valuable for architecture decisions, technology choices, and complex refactorings where the "right answer" isn't obvious. The branching, evaluation, and pruning process mirrors how experienced developers think through complex problems—exploring paths, abandoning dead ends, combining successful approaches. Don't use it for every decision (overkill for simple choices), but for significant decisions where exploration adds value, ToT ensures you've considered the landscape before deciding.

---

## Lesson 16: ReAct - Reasoning + Acting

### Objectives
- Understand ReAct as a framework combining reasoning and action
- Learn to enable AI to use tools dynamically during task execution
- Master the observe-think-act cycle
- Apply ReAct patterns to research and implementation tasks

### Explanation

#### What is ReAct?

ReAct (Reasoning + Acting) is a prompting framework where the model alternates between **reasoning** about the task and **taking actions** (using tools, gathering information) in an iterative cycle.

**Key Quote from the Research:**
> "A unique feature of human intelligence is the ability to seamlessly combine task-oriented actions with verbal reasoning...which has been theorized to play an important role in human cognition for enabling self-regulation or strategization and maintaining a working memory."

**Structure:**
```
Thought → Action → Observation → Thought → Action → Observation → ... → Answer
```

**Think of it as:**
- **Thought**: Reasoning about what to do next
- **Action**: Using a tool or gathering info
- **Observation**: Results from the action
- **Loop**: Continue until task is complete

#### Components of ReAct

1. **Thoughts**: Internal reasoning steps
2. **Actions**: Tool usage or information gathering
3. **Observations**: Results from actions
4. **Tracking**: Maintaining context across iterations
5. **Termination**: Knowing when to stop

#### ReAct vs. Chain of Thought

| Aspect | Chain of Thought | ReAct |
|--------|-----------------|-------|
| Focus | Pure reasoning | Reasoning + action |
| Tools | No tool usage | Uses tools |
| Adaptation | Fixed path | Adapts based on observations |
| Information | Static context | Dynamic information gathering |

### Step-by-Step Tutorial

**Implementing ReAct Patterns**

**Step 1: Set Up the Framework**

```markdown
You are an agent that alternates between Thoughts and Actions.

After each Thought, you can take an Action to gather information.
After each Action, you'll receive an Observation.
Continue until you have enough information to answer.

Available Actions:
- search[query]: Search for information
- read_file[path]: Read a file
- grep[pattern]: Search code for pattern
- inspect[component]: Analyze a component
- finish[answer]: Provide final answer

Format:
Thought: [Your reasoning about what to do next]
Action: [Action to take]
Observation: [Result of action - I'll provide this]
```

**Step 2: Provide the Task**

```markdown
Task: Find where the `calculateTotal` function is used in the codebase 
and explain what it does.
```

**Step 3: Guide the ReAct Loop**

```markdown
Thought 1: I need to find the calculateTotal function first
Action: grep[calculateTotal]
Observation: [System provides results - 3 files found]

Thought 2: I found it in utils/pricing.js, components/Cart.js, and tests/pricing.test.js. 
Let me read the implementation to understand what it does.
Action: read_file[utils/pricing.js]
Observation: [File contents shown]

Thought 3: Now I understand the function. Let me check how it's used in Cart.js
Action: read_file[components/Cart.js]
Observation: [File contents shown]

Thought 4: I have enough information to explain
Action: finish[calculateTotal computes the order total including taxes and shipping...]
```

**Step 4: Enable Self-Correction**

```markdown
If an Action doesn't provide useful information:
- Reflect on why
- Try a different approach
- Document the learning

Example:
Thought: Let me search for "calculateTotal"
Action: search[calculateTotal documentation]
Observation: No documentation found

Thought: The search didn't help. Let me grep the codebase instead.
Action: grep[function calculateTotal]
Observation: [Found in utils/pricing.js]
```

### Examples & Exercises

**Example 1: Research Task with ReAct**

**Prompt:**
```markdown
# Task
Research the best practices for implementing real-time collaborative editing 
in a React application.

# ReAct Framework

You can use these actions:
- search[query]: Search web/documentation
- summarize[source]: Summarize findings
- compare[optionA, optionB]: Compare approaches
- finish[answer]: Provide final recommendations

Start with your first Thought about how to approach this research.

After each thought, propose an Action.
I'll provide the Observation.
Continue until you have comprehensive findings.
```

**Expected Flow:**
```
Thought 1: I should start by understanding what technologies exist for 
real-time collaboration
Action: search["real-time collaborative editing React"]
Observation: [Results mention Yjs, Automerge, ShareDB, OT]

Thought 2: I found several options. Let me understand the two main approaches: 
Operational Transformation (OT) and CRDTs
Action: search["Operational Transformation vs CRDT"]
Observation: [Comparison details]

Thought 3: CRDTs seem more suitable for React. Let me research Yjs specifically 
since it's mentioned most
Action: search["Yjs React integration"]
Observation: [Yjs docs, examples]

Thought 4: I have information on Yjs. Let me compare it with Automerge to ensure 
I'm recommending the right one
Action: compare[Yjs, Automerge]
Observation: [Comparison details]

Thought 5: I have enough information to make a recommendation
Action: finish[
For real-time collaborative editing in React:

1. Use CRDTs over OT (better offline support, simpler model)
2. Recommend Yjs because:
   - Excellent React integration
   - Better performance
   - Larger community
   - Good documentation
3. Implementation pattern:
   - Use yjs + y-websocket for sync
   - Use y-react for React bindings
   - Store docs in IndexedDB for offline

Alternative: Automerge if you need better TypeScript support
]
```

**Example 2: Debugging with ReAct**

**Prompt:**
```markdown
# Task
Debug why the user profile form isn't submitting after validation passes.

# Available Actions
- inspect[component]: Analyze a component
- check[hypothesis]: Verify a hypothesis
- trace[execution]: Trace code execution path
- read_logs[]: Check console/error logs
- finish[solution]: Provide fix

Start debugging. After each thought, take an action.

Initial information:
- Validation shows no errors
- Submit button is enabled
- Clicking submit does nothing
- No network requests made
```

**Expected Flow:**
```
Thought 1: If validation passes and button is enabled but nothing happens, 
the issue is likely in the submit handler. Let me inspect the form component.
Action: inspect[UserProfileForm]
Observation: [Component code shown]

Thought 2: I see the form has an onSubmit prop. Let me trace where that's connected.
Action: trace[onSubmit handler]
Observation: [Shows: <form onSubmit={handleSubmit(onSubmit)}>]

Thought 3: It's using React Hook Form's handleSubmit. The issue might be that 
onSubmit isn't defined or there's an error in it. Let me check the logs.
Action: read_logs[]
Observation: [Shows: "onSubmit is not a function"]

Thought 4: Aha! The onSubmit callback isn't being passed to the component. 
Let me check how the component is being used.
Action: inspect[component usage in parent]
Observation: [Shows: <UserProfileForm /> - no onSubmit prop passed]

Thought 5: Found it! The parent component isn't passing the onSubmit handler.
Action: finish[
Root cause: Parent component renders <UserProfileForm /> without passing 
the required onSubmit prop.

Fix: In the parent component, add the onSubmit handler:

<UserProfileForm onSubmit={handleUserProfileUpdate} />

where handleUserProfileUpdate handles the form submission.

The form component should also have a default prop or validation to catch this:
UserProfileForm.defaultProps = {
  onSubmit: () => console.warn('onSubmit handler not provided')
};
]
```

**Example 3: Frontend Development with ReAct**

**Prompt:**
```markdown
# Task
Implement a dark mode feature for the application. Use the ReAct framework 
to work through this systematically.

# Available Actions
- research[topic]: Research best practices
- check_existing[feature]: See if related code exists
- plan[approach]: Create implementation plan
- implement[step]: Implement a specific step
- verify[implementation]: Check if it works
- finish[result]: Complete with final implementation

Context:
- React 18 application
- Using styled-components
- Need to support system preference
- Need manual toggle
- Must persist user choice

Start with your first thought about approaching this.
```

**Expected Flow:**
```
Thought 1: Before implementing, I should research best practices for dark mode 
and check if any related code exists
Action: research[React dark mode best practices]
Observation: [Common patterns: CSS variables, Context API, system preference detection]

Thought 2: Good, I have patterns. Let me check if we have any existing theme 
infrastructure
Action: check_existing[theme or ThemeProvider]
Observation: [Found: ThemeProvider from styled-components is already used]

Thought 3: Great! We already have ThemeProvider. I can extend that. Let me plan 
the implementation
Action: plan[dark mode with existing ThemeProvider]
Observation: [Plan created:
1. Define light/dark theme objects
2. Create theme context to manage state
3. Add system preference detection
4. Add localStorage persistence
5. Create toggle component
]

Thought 4: Good plan. Let me start with step 1: defining the themes
Action: implement[theme definitions]
Observation: [Code implemented]

Thought 5: Themes defined. Now let me implement the context for managing state
Action: implement[theme context with state]
Observation: [Code implemented with useState, system preference detection, localStorage]

Thought 6: Context is ready. Let me verify it works before continuing
Action: verify[theme context]
Observation: [Tested: system preference detected correctly, state updates work]

Thought 7: Working! Now let me create the toggle UI component
Action: implement[theme toggle button]
Observation: [Component implemented]

Thought 8: All pieces are in place. Let me do a final verification
Action: verify[complete dark mode feature]
Observation: [Tested: 
- System preference detected ✓
- Manual toggle works ✓
- Preference persists ✓
- Themes apply correctly ✓
]

Thought 9: Everything works! Ready to wrap up
Action: finish[
Dark mode implementation complete!

Components created:
1. themes.ts - Light/dark theme definitions
2. ThemeContext.tsx - Theme state management with:
   - System preference detection
   - localStorage persistence
   - Theme toggle function
3. ThemeToggle.tsx - Toggle button component

Usage:
- Wrap app with ThemeProvider
- Use useTheme() hook to access theme
- Place <ThemeToggle /> in header

All requirements met:
✓ System preference support
✓ Manual toggle
✓ Persistence
✓ Integrates with existing styled-components
]
```

**Exercise 1: Create a ReAct Prompt**

**Scenario**: You need to optimize bundle size for a React application.

**Your Task**: Create a ReAct prompt that guides the AI through investigating 
and solving bundle size issues.

**Solution:**

```markdown
# Task
Our React application's production bundle is 2.5MB (gzipped), which is too large. 
Investigate and optimize the bundle size.

# ReAct Framework

You are an agent investigating and fixing bundle size issues.

## Available Actions
- analyze_bundle[]: Examine bundle composition
- identify[issue]: Identify specific large dependencies
- research[solution]: Research optimization techniques
- implement[optimization]: Apply a specific optimization
- measure[impact]: Measure size reduction
- finish[summary]: Provide final summary

## Guidelines
- After each Thought, propose one Action
- I'll provide the Observation
- Continue until bundle size is significantly reduced (target: under 1MB gzipped)
- Try multiple optimizations if needed

## Initial Context
- React 18 application
- Using Create React App (CRA)
- Deployed to production
- Current bundle: 2.5MB gzipped
- Target: under 1MB gzipped

Begin with your first thought about how to approach this.

---

Expected Usage:

Thought 1: I need to understand what's making the bundle large. Let me analyze 
the bundle composition.
Action: analyze_bundle[]
Observation: [I provide bundle analysis showing: 
- moment.js: 500KB
- lodash: 300KB
- Some unused dependencies
- Large images bundled
]

Thought 2: Moment.js is a major contributor. Modern alternatives like date-fns 
or day.js are much smaller. Let me research date-fns vs moment.
Action: research[date-fns vs moment.js bundle size]
Observation: [date-fns is modular, ~10KB per function vs moment's 500KB monolith]

Thought 3: Switching to date-fns could save 490KB. Let me implement that.
Action: implement[replace moment with date-fns]
Observation: [Migration completed]

Thought 4: Great! Now let me measure the impact.
Action: measure[bundle size after moment replacement]
Observation: [New bundle: 2.1MB gzipped - saved 400KB]

Thought 5: Good progress but not enough. Lodash is the next target. Let me 
research tree-shaking lodash.
Action: research[lodash tree-shaking optimization]
Observation: [Use lodash-es or import individual functions]

Thought 6: Let me implement the lodash optimization.
Action: implement[use lodash-es with proper imports]
Observation: [Implemented]

Thought 7: Let me measure again.
Action: measure[bundle after lodash optimization]
Observation: [New bundle: 1.9MB - saved 200KB more]

[Continue until target reached...]

Thought N: We've reached 950KB gzipped through optimizations. Success!
Action: finish[
Bundle optimizations completed:

Starting size: 2.5MB gzipped
Final size: 950KB gzipped
Reduction: 62% reduction

Optimizations applied:
1. Replaced moment.js with date-fns (-400KB)
2. Switched to lodash-es with tree-shaking (-200KB)
3. Enabled code splitting for routes (-300KB)
4. Lazy loaded heavy components (-350KB)
5. Optimized images and moved to CDN (-300KB)

Recommendations:
- Monitor bundle size in CI/CD
- Use bundle analyzer regularly
- Consider dynamic imports for rarely-used features
]
```

**Validation:**
- **Self-Check**: Does your ReAct prompt define clear actions?
- **Self-Check**: Does it create a thought-action-observation loop?
- **Self-Check**: Are there success criteria for termination?

### Frontend Contextualization

**Real-World Scenario: Implementing a New Feature End-to-End**

Your PM requests: "Add user mentions in comments (like @username)"

**ReAct Approach:**

```markdown
# Task
Implement @mention functionality in comment system

# Available Actions
- research[topic]: Research implementation approaches
- review_existing[feature]: Check existing code
- design[component]: Design solution
- implement[part]: Implement a piece
- test[feature]: Test implementation
- document[usage]: Write documentation
- finish[deliverable]: Complete feature

# Context
- React application
- Comments use markdown
- Need to notify mentioned users
- Should work with keyboard navigation

---

Thought 1: Before implementing, I should understand how @mentions typically work 
and check if we have related infrastructure.
Action: research[@mention best practices React]
Observation: [Common patterns: contenteditable, textarea with overlay, 
autocomplete dropdown, mention detection]

Thought 2: I have patterns. Let me check our existing comment component to 
understand current implementation.
Action: review_existing[comment component]
Observation: [Currently uses textarea with markdown preview]

Thought 3: We use textarea, so I can't use contenteditable. I'll need an 
autocomplete dropdown triggered by @. Let me check if we have autocomplete 
components.
Action: review_existing[autocomplete or dropdown components]
Observation: [Found: Autocomplete component in design system]

Thought 4: Perfect! I can reuse that. Let me design the solution.
Action: design[@mention integration]
Observation: [Design:
- Detect @ character in textarea
- Show Autocomplete dropdown below cursor
- Fetch/filter user list
- Insert mention on selection
- Store mention metadata for notifications
]

Thought 5: Good design. Let me start implementing the @ detection.
Action: implement[@ detection and cursor position tracking]
Observation: [Implemented: onInput handler, cursor position calculation]

Thought 6: Detection works. Now implement the autocomplete integration.
Action: implement[autocomplete dropdown trigger]
Observation: [Implemented: Autocomplete shows on @, positioned at cursor]

Thought 7: UI works. Now I need the user search/filter logic.
Action: implement[user search for mentions]
Observation: [Implemented: searches users by name, filters as user types]

Thought 8: Search working. Let me implement mention insertion.
Action: implement[mention insertion on select]
Observation: [Implemented: inserts @username, stores mention data]

Thought 9: Basic feature done. Let me test it.
Action: test[@mention workflow]
Observation: [Testing found issues:
- Dropdown doesn't close on ESC
- No keyboard navigation in list
- Mentions not highlighted in preview
]

Thought 10: Issues found. Let me fix keyboard interaction first.
Action: implement[keyboard navigation for mentions]
Observation: [Fixed: ESC closes, arrow keys navigate, Enter selects]

Thought 11: Much better. Now fix the preview highlighting.
Action: implement[highlight mentions in markdown preview]
Observation: [Implemented: custom markdown renderer highlights @mentions]

Thought 12: All features working. Let me test again comprehensively.
Action: test[complete @mention feature]
Observation: [All tests pass:
- @ triggers dropdown ✓
- User search works ✓
- Keyboard navigation works ✓
- Mentions insert correctly ✓
- Preview highlights mentions ✓
- Mention data saved for notifications ✓
]

Thought 13: Feature complete and tested. Let me document it.
Action: document[usage and API]
Observation: [Documentation created]

Thought 14: Everything done! Ready to wrap up.
Action: finish[
@Mention feature implementation complete!

Delivered:
1. MentionInput component (enhanced textarea)
2. User search integration
3. Autocomplete dropdown
4. Keyboard navigation (arrows, ESC, Enter)
5. Markdown preview with mention highlighting
6. Mention metadata storage for notifications
7. Documentation and usage examples

Technical details:
- Extends existing comment component
- Reuses Autocomplete from design system
- Accessible (keyboard navigation, ARIA labels)
- Performant (debounced search, virtualized list)

Ready for code review!
]
```

**Key Benefits of ReAct in This Scenario:**
1. **Adaptive**: Discovered existing Autocomplete component through investigation
2. **Iterative**: Fixed issues found during testing
3. **Comprehensive**: Covered research, implementation, testing, documentation
4. **Trackable**: Clear progress through thought-action pairs
5. **Resilient**: Self-corrected when testing revealed issues

**Practical Takeaway**: ReAct is your dynamic problem-solving framework. Unlike static prompts, ReAct allows the AI to gather information, try approaches, observe results, and adapt—mirroring how you actually work through complex tasks. It's especially powerful in IDE tools like Cursor that can execute actions (grep, read files, run tests). The thought-action-observation loop makes reasoning visible and enables course correction. Use it for complex tasks where you don't know all requirements upfront, for debugging where you need to investigate, or for implementation where research and testing are needed. The framework naturally creates documentation of the problem-solving process. Think of it as pair programming where your AI partner can think out loud, try things, and learn from results.

---

**Next:** Part 3c - [Advanced Lesson (Final)](03c-advanced-lesson-18-summary.md)

