# TL;DR

## Complete Lesson Overview

### All 21 Lessons at a Glance

| # | Lesson Title | Level | Key Skill | When to Use |
|---|-------------|-------|-----------|-------------|
| 1 | Understanding AI Models | Foundation | Model behavior | Always - foundation knowledge |
| 2 | Tokens & Context Windows | Foundation | Resource management | Every interaction |
| 3 | Anatomy of Effective Prompts | Foundation | Prompt structure | Every prompt |
| 4 | Prompt Formatting & Structure | Foundation | Organization | Medium+ complexity prompts |
| 5 | AI Fluency Framework | Foundation | Strategic thinking | Every AI collaboration |
| 6 | Vague vs Specific Prompts | Foundation | Intentional specificity | Every prompt decision |
| 7 | Role Prompting & System Instructions | Intermediate | Context setting | Start of projects/sessions |
| 8 | Zero-Shot Prompting | Intermediate | Simple tasks | Standard transformations |
| 9 | Few-Shot Prompting | Intermediate | Pattern consistency | Project-specific patterns |
| 10 | Chain of Thought (CoT) | Intermediate | Reasoning transparency | Complex tasks, debugging |
| 11 | Reducing Hallucinations | Intermediate | Accuracy | Critical code, security |
| 12 | Meta Prompting | Advanced | Workflow design | Multi-phase projects |
| 13 | Prompt Chaining | Advanced | Task decomposition | Large features |
| 14 | Self-Consistency | Advanced | Decision validation | Architecture choices |
| 15 | Tree of Thoughts | Advanced | Solution exploration | Complex decisions |
| 16 | ReAct | Advanced | Dynamic problem-solving | Research, adaptive tasks |
| 17 | Reflexion | Advanced | Iterative improvement | Quality-critical code |
| 18 | System Prompts & IDE Config | Expert | Environment setup | Project initialization |
| 19 | Prompt Templates | Expert | Reusability | Repeated tasks |
| 20 | Golden Test Sets | Expert | Quality assurance | Ongoing validation |
| 21 | Personal Workflows | Workflows | Process optimization | Multi-session projects, debugging, etc... |

---

## Quick Reference Guides

### Guide 1: Technique Selection Matrix

**"Which technique should I use?"**

| Your Situation | Recommended Technique | Why |
|----------------|---------------------|-----|
| Simple code transformation | Zero-Shot | Model knows standard patterns |
| Match your team's style | Few-Shot + Examples | Show your patterns |
| Complex debugging | Chain of Thought + ReAct | Need reasoning + investigation |
| Architecture decision | Tree of Thoughts + Self-Consistency | Explore options + validate |
| Multi-day feature | Prompt Chaining + Meta Prompting + AILog | Manage complexity |
| Production code | Reflexion + Golden Tests | Iterate to quality |
| Security review | Chain of Thought + Verification + Few-Shot | Systematic + thorough |
| Quick bug fix | Zero-Shot or Simple Prompt | Don't overcomplicate |
| Learning new tech | ReAct + Vague prompts | Explore + discover |
| Team consistency | System Prompts + Templates | Shared standards |

### Guide 2: Prompt Quality Checklist

Before sending a prompt, check:

**Context (Clear? Complete?)**
- [ ] Specific task stated
- [ ] Relevant background provided
- [ ] Code/files included if needed
- [ ] Constraints mentioned

**Specificity (Intentional level?)**
- [ ] Vague for exploration OR specific for implementation
- [ ] Not accidentally ambiguous
- [ ] Examples provided if needed

**Output Guidance (Clear expectations?)**
- [ ] Desired format specified
- [ ] Success criteria defined
- [ ] Validation requirements stated

**Quality Requirements (Standards clear?)**
- [ ] Accessibility mentioned (if applicable)
- [ ] Security considerations noted (if applicable)
- [ ] Testing expectations set
- [ ] Performance requirements stated

**Technique Application (Right tool?)**
- [ ] Using appropriate technique for task complexity
- [ ] Role set if needed
- [ ] CoT requested for complex reasoning
- [ ] Examples provided for consistency

### Guide 3: Common Scenarios & Solutions

#### Scenario 1: "AI keeps giving me code that doesn't match our style"

**Solution:**
1. Add your style to system prompts (`.cursor/rules`)
2. Use few-shot prompting with your existing code as examples
3. Explicitly reference existing files: "Follow pattern in src/components/Button.tsx"

#### Scenario 2: "The response is too generic/not specific enough"

**Solution:**
1. Increase specificity - add more constraints and requirements
2. Provide examples of what you want
3. Reference specific technologies, versions, patterns
4. Define success criteria explicitly

#### Scenario 3: "I'm not sure if the AI's solution is correct"

**Solution:**
1. Request Chain of Thought - ask for reasoning
2. Use self-consistency - run prompt multiple times, compare
3. Ask for verification steps
4. Request explanation of trade-offs
5. Have AI review its own code (Reflexion)

#### Scenario 4: "The task is too large for one prompt"

**Solution:**
1. Use prompt chaining - break into phases
2. Create planning file first
3. Use meta prompting for workflow
4. Maintain AILog.md across sessions
5. Save artifacts (markdown files) between steps

#### Scenario 5: "AI is hallucinating or making things up"

**Solution:**
1. Constrain to provided context only
2. Request citations/sources
3. Explicitly allow "I don't know" responses
4. Ask for verification against documentation
5. Use Chain of Thought to catch logical errors

#### Scenario 6: "Need to switch contexts but don't want to lose progress"

**Solution:**
1. Save progress to markdown file (AILog.md, plan file)
2. Document current state and next steps
3. Start new chat with reference to saved artifacts
4. Use execution checklists to track completion

#### Scenario 7: "Team members all using AI differently, inconsistent quality"

**Solution:**
1. Create shared system prompts (`.cursor/rules` in repo)
2. Build prompt template library
3. Develop golden test sets for validation
4. Share successful prompts in team wiki
5. Regular knowledge sharing sessions

### Guide 4: Complexity Ladder

**Match technique to task complexity:**

```
SIMPLE TASKS
├─ Zero-shot prompting
├─ Clear, direct instruction
└─ Minimal context

MODERATE TASKS
├─ Few-shot with examples
├─ Chain of Thought
├─ Role prompting
└─ Structured format

COMPLEX TASKS
├─ Prompt chaining
├─ Meta prompting
├─ Tree of Thoughts
├─ ReAct
└─ Planning files

LARGE PROJECTS (Multi-session)
├─ All advanced techniques
├─ AILog.md tracking
├─ Execution checklists
├─ Reflexion for quality
└─ Team coordination
```

### Guide 5: Quality Assurance Decision Tree

```
Is this code critical?
├─ YES (security, payments, auth, data)
│   ├─ Use Reflexion (iterate to quality)
│   ├─ Use Self-Consistency (validate decisions)
│   ├─ Add to golden test set
│   ├─ Explicit security/accessibility requirements
│   ├─ Request verification steps
│   └─ Thorough human review
│
└─ NO (internal tools, prototypes, learning)
    ├─ Use appropriate technique for complexity
    ├─ Standard quality checks
    └─ Normal review process
```

---

## Complete Technique Reference

### Foundational Techniques

#### AI Fluency Framework (4 D's)
[From Anthropic](https://anthropic.skilljar.com/ai-fluency-framework-foundations)

**When to use**: Every interaction (mental model)

**Structure:**
```
Delegation → What AI vs. you handles
Description → How you communicate
Discernment → How you evaluate  
Diligence → Responsible use
```

**Key Questions:**
- Delegation: What should AI do vs. what should I own?
- Description: What context does AI need?
- Discernment: Is this output good enough?
- Diligence: Am I being responsible?

#### Vague vs. Specific Prompts

**When to use**: Every prompt (conscious choice)

**Decision Matrix:**
- Exploring options → Vague
- Know what you want → Specific
- Learning → Vague
- Implementing → Specific

**Hybrid Approach**: Specific requirements + vague on solution

### Intermediate Techniques

#### Role Prompting

**Template:**
```markdown
You are a [role] with expertise in [domain].

Guidelines:
- [Behavior 1]
- [Behavior 2]

Focus on: [Priorities]
```

**Common Roles:**
- Senior Frontend Developer
- Accessibility Specialist
- Security Engineer
- Performance Expert
- Quality Engineer

#### Zero-Shot Prompting

**When**: Simple, standard tasks

**Structure**: Direct instruction, no examples

**Example:**
```markdown
Convert this function to TypeScript with strict typing.
[Code...]
```

#### Few-Shot Prompting

**When**: Project-specific patterns, consistency needed

**Structure**: Instruction + Examples + Task

**Example:**
```markdown
Create a component following these patterns:

Example 1: [Button component]
Example 2: [Input component]

Now create: [Your component]
```

#### Chain of Thought (CoT)

**When**: Complex reasoning, debugging, planning

**Trigger Phrases:**
- "Think step-by-step"
- "Explain your reasoning"
- "Before implementing, analyze..."

**Structure:**
```markdown
Task: [Problem]

Think through:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Then provide solution.
```

### Advanced Techniques

#### Meta Prompting

**When**: Multi-phase workflows, complex projects

**Structure:**
```markdown
Follow this workflow:

Phase 1: [Actions] → Output: [Format]
Phase 2: [Actions] → Output: [Format]
Phase 3: [Actions] → Output: [Format]

After each phase, summarize and confirm.
```

#### Prompt Chaining

**When**: Large tasks, multiple domains, context limits

**Pattern:**
```
Prompt 1 → Output saved to file
Prompt 2 → Uses file from Prompt 1
Prompt 3 → Uses files from 1 & 2
```

**Example Flow:**
```
1. Analyze requirements → requirements.md
2. Design architecture → architecture.md (uses requirements.md)
3. Implement → code (uses architecture.md)
4. Test → tests (uses code + architecture.md)
```

#### Self-Consistency

**When**: Critical decisions, architecture choices

**Process:**
```
1. Run same prompt 3-5 times (vary temperature, model, or role)
2. Compare reasoning paths
3. Look for consensus
4. If disagreement, investigate why
5. Trust majority or explore alternatives
```

#### Tree of Thoughts (ToT)

**When**: Exploring solution space, multiple approaches

**Structure:**
```
Problem
├─ Branch 1: Approach A
│  ├─ Evaluate
│  └─ Sub-branches if promising
├─ Branch 2: Approach B
│  ├─ Evaluate
│  └─ Sub-branches if promising
└─ Branch 3: Approach C
   ├─ Evaluate
   └─ Prune if score too low
```

#### ReAct (Reasoning + Acting)

**When**: Research, dynamic investigation, adaptive problem-solving

**Structure:**
```
Thought: [Reasoning]
Action: [Tool use or info gathering]
Observation: [Result]

[Repeat until sufficient information]

Final Answer: [Solution]
```

#### Reflexion

**When**: Quality-critical code, iterative improvement

**Cycle:**
```
1. Generate → Initial output
2. Evaluate → Against criteria
3. Reflect → Identify gaps
4. Revise → Improved version
5. Validate → Check criteria again
[Repeat if needed]
```

### Expert Techniques

#### System Prompts

**Setup:** `.cursor/rules` file

**Template:**
```markdown
# Project: [Name]

## Tech Stack
[Languages, frameworks, tools]

## Coding Standards
[Conventions, patterns]

## Quality Requirements
[Accessibility, performance, testing]

## Code Review Focus
[What to check]
```

#### Prompt Templates

**Syntax:** Use {{VariableName}} as placeholders

**Example:**
```markdown
Create a {{ComponentType}} called {{ComponentName}}.

Props: {{PropsList}}
Requirements: {{Requirements}}
```

#### Golden Test Sets

**Structure:**
```markdown
## Test ID: [Category]-[Number]
Prompt: [Exact text]
Success Criteria: [Checklist]
Scoring: [Rubric]
Results: [History]
```

**Categories:**
- Component generation
- Debugging
- Code review
- Refactoring
- Testing
- Documentation

#### Personal Workflows

**AILog.md:**
```markdown
# AILog - [Project]

## 2024-01-15 - Session 1
Completed: [Items]
Decisions: [Choices made]
Next: [Next steps]
Blockers: [Issues]
```

**Planning Files:**
```markdown
# Feature Plan: [Name]

## Requirements
## Technical Analysis
## Implementation Plan
## Architecture Decisions
## Risks & Mitigations
```

**Execution Checklists:**
```markdown
# Checklist: [Feature]

## Phase 1
- [ ] Task 1
- [ ] Task 2

## Phase 2
- [ ] Task 3
```

---

**Next:** [Part 1 - Introduction and Foudations](01-introduction-and-foundations.md)