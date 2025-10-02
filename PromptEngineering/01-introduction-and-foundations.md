# AI & Prompt Engineering: Interactive Learning Guide for Frontend Developers

## Welcome

Welcome to your journey into AI-assisted development! This guide is designed to take you from zero AI experience to confidently leveraging AI tools in your daily frontend development workflow.

**Important Opening Notes:**
- AI is not a silver bullet or magical solution—it's a powerful tool that requires practice and skill to use effectively
- Learning to work with AI effectively takes time and experimentation, but the investment pays off
- Building good AI collaboration habits may feel like more work initially, but becomes second nature with practice
- You'll learn not just *what* to prompt, but *how* to think about prompting strategically

<div align="center">
   <img align="center" src="images/one_does_not_simply_write_a_prompt.png" alt="One does not simply meme" width="40%">
</div>

---

## How to Use This Guide

### Structure
This guide is organized into progressive skill levels:
1. **Foundations** (Lessons 1-6): Core concepts and basic techniques
2. **Intermediate** (Lessons 7-12): Practical prompting strategies
3. **Advanced** (Lessons 13-18): Sophisticated techniques and workflows
4. **Expert** (Lessons 19-22): Personal workflows and optimization

### Learning Approach
Each lesson follows this format:
- **Objectives**: Clear, measurable goals
- **Explanation**: Concepts broken down with practical context
- **Step-by-Step Tutorial**: Hands-on instructions
- **Examples & Exercises**: Real-world practice with solutions
- **Frontend Contextualization**: Direct application to frontend development
- **Validation**: Self-check criteria or provided answers

### Prerequisites
**None!** This guide assumes no prior AI or prompt engineering experience.

---

## Curriculum Overview

| Lesson | Title | Skill Level |
|--------|-------|-------------|
| 1 | Understanding AI Models: The Foundation | Foundational |
| 2 | Tokens & Context Windows | Foundational |
| 3 | Anatomy of an Effective Prompt | Foundational |
| 4 | Prompt Formatting & Structure | Foundational |
| 5 | The AI Fluency Framework | Foundational |
| 6 | Vague vs Specific Prompts | Foundational |
| 7 | Role Prompting & System Instructions | Intermediate |
| 8 | Zero-Shot Prompting | Intermediate |
| 9 | Few-Shot Prompting with Examples | Intermediate |
| 10 | Chain of Thought (CoT) Reasoning | Intermediate |
| 11 | Reducing Hallucinations & Verification | Intermediate |
| 12 | Meta Prompting & Workflow Design | Advanced |
| 13 | Prompt Chaining for Complex Tasks | Advanced |
| 14 | Self-Consistency & Multi-Path Reasoning | Advanced |
| 15 | Tree of Thoughts (ToT) | Advanced |
| 16 | ReAct: Reasoning + Acting | Advanced |
| 17 | Reflexion & Self-Improvement | Advanced |
| 18 | System Prompts & IDE Configuration | Expert |
| 19 | Prompt Templates & Variables | Expert |
| 20 | Golden Test Sets & Quality Assurance | Expert |
| 21 | Personal Workflows | Workflows |

---

# Part 1: Foundational Lessons

## Lesson 1: Understanding AI Models: The Foundation

### Objectives
- Understand what Large Language Models (LLMs) are and how they work at a high level
- Learn about key model configuration settings and when they matter
- Recognize the capabilities and limitations of AI models
- Develop realistic expectations for AI-assisted development

### Explanation

#### What Are LLMs?
Large Language Models are AI systems trained on vast amounts of text data to understand and generate human-like text. They work by predicting the most likely next token (word or word piece) based on patterns learned during training.

**Key Concept**: LLMs don't "know" things the way humans do—they recognize patterns and generate statistically probable responses based on their training data.

#### Model Configuration Settings

While you won't typically adjust these settings in IDE tools like Cursor (they're pre-configured), understanding them helps you craft better prompts:

| Setting | Purpose | Low Value | High Value |
|---------|---------|-----------|------------|
| **Temperature** | Controls output randomness | More deterministic, focused | More creative, diverse |
| **Top P** | Controls token selection scope | More factual, confident | More exploratory, varied |
| **Max Length** | Limits response length | Shorter responses | Longer responses |
| **Frequency Penalty** | Reduces word repetition | Words can repeat freely | Repeated words discouraged |
| **Presence Penalty** | Encourages topic diversity | Focused on topic | Explores related topics |

**Important Rules:**
- Don't use Temperature and Top P simultaneously (they conflict)
- Don't use Frequency Penalty and Presence Penalty simultaneously (they conflict)

#### Stop Sequences
A stop sequence tells the model when to stop generating content. While this is typically a configuration setting, you can use similar concepts in prompts:

```markdown
Generate a brief summary of this component. Stop after 3 sentences.
```

This explicit instruction mimics the behavior of stop sequences, preventing overly long responses and reducing token usage.

### Step-by-Step Tutorial

**Understanding Model Behavior Through Prompting**

1. **Experiment with Deterministic vs Creative Requests**
   - Try: "List the steps to create a React component" (deterministic)
   - Try: "Brainstorm creative ways to animate a button hover state" (creative)
   - Notice how the model responds differently based on the nature of your request

2. **Test Model Boundaries**
   - Ask: "What is the capital of France?" (factual, within training)
   - Ask: "What happened in the news yesterday?" (likely outside training data)
   - Observe how the model handles questions outside its knowledge

3. **Explore Response Control**
   - Prompt: "Explain React hooks in one sentence"
   - Prompt: "Explain React hooks with detailed examples"
   - See how explicit length guidance affects output

### Examples & Exercises

**Example 1: Temperature Effect (Simulated)**

*High "Temperature" Request (Creative):*
```
Brainstorm 5 unique ways to display loading states in a React app
```

*Low "Temperature" Request (Deterministic):*
```
Provide the standard React pattern for implementing a loading state with useState
```

**Exercise 1: Model Awareness**

Try these prompts and observe the differences in responses:

1. "Create a button component" (vague, invites creativity)
2. "Create a button component with primary and secondary variants, using styled-components, with TypeScript types" (specific, deterministic)

**Solution & Validation:**
- First prompt: Should give varied creative responses across attempts
- Second prompt: Should give consistent, specific implementation
- **Self-Check**: Did the specific prompt yield more predictable, implementation-ready code?

**Exercise 2: Stop Conditions**

Create two prompts about useEffect:
1. Without length guidance
2. With explicit constraint: "Explain in exactly 2 sentences"

**Solution & Validation:**
- Second prompt should produce concise output
- **Self-Check**: Is the second response noticeably shorter and more focused?

### Frontend Contextualization

**Real-World Scenario: Debugging a Component**

When you encounter a bug, the model's response will differ based on your prompt style:

❌ **Too Vague**: "This component isn't working"
- Model must guess what "working" means
- Response will be generic and exploratory (high "temperature")

✅ **Appropriately Specific**: "My UserProfile component throws 'Cannot read property name of undefined' when the API returns null. I need error handling that displays a fallback UI."
- Model has clear constraints
- Response will be deterministic and solution-focused (low "temperature")

**Practical Takeaway**: You control the model's behavior through prompt specificity, effectively simulating temperature adjustments without touching configuration.

---

## Lesson 2: Tokens & Context Windows

### Objectives
- Understand what tokens are and how they relate to costs
- Learn practical token estimation for code and text
- Master context window management strategies
- Optimize prompts for token efficiency

### Explanation

#### What Are Tokens?

Tokens are the basic units that language models process. Think of them as word pieces:
- "Hello" = 1 token
- "JavaScript" = 2 tokens ("Java" + "Script")
- "useState" = 2-3 tokens

**Token Types:**
- **Input tokens**: Everything you send (prompt + context + files)
- **Output tokens**: Everything the model generates
- Output tokens typically cost 3-5x more than input tokens

#### Token Counting Rules of Thumb

| Content Type | Tokens per Word (Approximate) |
|--------------|-------------------------------|
| Natural language (English) | ~0.75 tokens |
| JavaScript/TypeScript code | ~1.2-1.5 tokens |
| JSON data | ~1.8-2.2 tokens |
| Commented code | ~0.8-1.0 tokens |
| Whitespace & formatting | Counts toward tokens |

**Note:** Cost estimates are approximates. Check current model pricing for accurate estimates.

**Example:**
```javascript
// This function validates email (commented code: ~0.8-1.0 tokens/word)
const validateEmail = (email) => { // (code: ~1.2-1.5 tokens/word)
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
};
```

#### Context Windows Explained

The **context window** is the model's "working memory"—the maximum amount of information it can consider at once.

**What Fills the Context Window:**
- Your prompt text
- Files you've attached or referenced
- Previous messages in the conversation
- System instructions
- AI's responses

**Current Model Context Windows (as of 2024):**
- Claude 3.5 Sonnet: 200K tokens (~150K words)
- GPT-4: 128K tokens (~96K words)
- GPT-4o: 128K tokens (~96K words)

#### Context Window Strategies

1. **File Organization**: Keep related code together when working with AI
2. **Context Compression**: Use comments to summarize large sections
3. **Session Management**: Break large refactoring into focused sessions
4. **Progressive Enhancement**: Build features incrementally

### Step-by-Step Tutorial

**Managing Context Effectively**

1. **Estimate Your Context Usage**
   - In Cursor, check the chat window for context percentage
   - Aim to keep context usage below 70% for best performance
   - If context exceeds 80%, consider starting a fresh conversation

2. **Compress Context with Summaries**
   ```javascript
   // Instead of including entire Redux store (1000+ lines):
   /* Redux Store Summary:
    * - User slice: authentication state, profile data
    * - UI slice: modal state, loading flags
    * - Data slice: API cache with user, products, orders
    */
   
   // Now work with specific slice
   ```

3. **Use Progressive Disclosure**
   - Start with high-level question
   - Add details incrementally
   - Let the model request what it needs

4. **Reference, Don't Paste**
   ```markdown
   # Instead of pasting entire file:
   "Review the UserProfile component in src/components/UserProfile.jsx 
   for performance issues"
   
   # The IDE will automatically include the file
   ```

### Examples & Exercises

**Example 1: Token Cost Estimation**

Typical coding session costs using Claude 3.5 Sonnet:

| Task | Input Tokens | Output Tokens | Cost |
|------|--------------|---------------|------|
| Simple bug fix | ~5,000 | ~500 | $0.01-$0.05 |
| Component refactoring | ~15,000 | ~3,000 | $0.10-$0.30 |
| Large feature implementation | ~50,000 | ~10,000 | $0.50-$2.00 |
| Architecture review | ~30,000 | ~5,000 | $0.20-$1.00 |

**Exercise 1: Context Optimization**

You need to ask about a React component in a 500-line file. Which approach is more token-efficient?

**Option A:**
```markdown
Here's my entire component: [paste 500 lines]
How do I add a loading state?
```

**Option B:**
```markdown
In MyComponent.tsx, I need to add a loading state. 
The component currently has:
- Props: userId, onUpdate
- State: user data
- useEffect that fetches user data

How should I implement the loading state?
```

**Solution:**
- **Option B is significantly more efficient**
- Option A: ~750-1,000 tokens for the code paste
- Option B: ~50-75 tokens for the summary
- **10-20x token reduction**

**Validation:**
- Option B provides necessary context without waste
- Model can request the full file if needed
- **Self-Check**: Does your approach include only essential context?

**Exercise 2: Session Management**

You're refactoring a large component with 8 functions. Plan your approach:

**Solution:**
Break into 3 sessions:
1. **Session 1**: Analyze structure, identify refactoring opportunities → save analysis to `refactor-plan.md`
2. **Session 2**: Refactor functions 1-4 using the plan
3. **Session 3**: Refactor functions 5-8, final integration

**Validation:**
- Each session stays under 60% context usage
- Plan file allows context sharing between sessions
- **Self-Check**: Could you start Session 3 fresh using only the plan file?

### Frontend Contextualization

**Real-World Scenario: Large Component Refactoring**

You have a 800-line `Dashboard.jsx` that handles:
- Data fetching
- User authentication checks
- Multiple charts
- Settings panel
- Notification system

**❌ Inefficient Approach:**
```markdown
[Paste entire 800-line component]
Help me refactor this
```
Result: Uses 1,200+ tokens, overwhelms context, vague guidance

**✅ Efficient Approach:**
```markdown
Dashboard.jsx is 800 lines handling data fetching, auth, charts, settings, 
and notifications. I want to split into smaller components.

First, analyze the component structure and suggest a component hierarchy.
Save the plan to dashboard-refactor-plan.md.
```

**Then in follow-up sessions:**
```markdown
Using dashboard-refactor-plan.md, let's extract the data fetching logic 
into a custom hook.
```

**Benefits:**
- Saves ~1,000 tokens per prompt
- Keeps context focused
- Creates reusable artifacts (plan files)
- Enables progress tracking

**Practical Takeaway**: Think of context like RAM—keep only what's actively needed loaded. Use files and summaries as your "disk storage" for reference.

---

## Lesson 3: Anatomy of an Effective Prompt

### Objectives
- Identify the core components of a well-structured prompt
- Understand when to use each prompt element
- Learn to balance detail with clarity
- Apply the principle of intentional prompting

### Explanation

#### Core Prompt Components

Not every prompt needs all elements—use what's appropriate for your task:

1. **Instruction**: The specific task or action you want performed
2. **Context**: Background information that guides better responses
3. **Input Data**: The specific data/code you're asking about
4. **Output Format**: How you want the response structured
5. **Constraints**: Limitations, requirements, or boundaries

#### Optional Advanced Elements

For complex tasks, consider adding:

6. **Role/Objective**: Who the AI should act as and why
7. **Validation**: How to verify the output meets requirements
8. **Stop Conditions**: When to pause or seek clarification
9. **Error Handling**: How to handle unknowns or failures

#### The Intentionality Principle

> **Before engaging with AI, know your desired outcome**

Ask yourself:
- What does success look like for this task?
- What specific problem am I trying to solve?
- What constraints or requirements must be met?

**Analogy**: Think of proposing a new framework to your team. You wouldn't say "Let's use this because it's cool." You'd present clear evidence: why it fits, what problems it solves, how it aligns with goals. Similarly with AI—back requests with specific objectives.

### Step-by-Step Tutorial

**Building a Prompt from Scratch**

Let's build a prompt for creating a React component:

**Step 1: Start with the Instruction**
```markdown
Create a React component
```

**Step 2: Add Context**
```markdown
Create a React component for our e-commerce site's product listing page
```

**Step 3: Include Input Data / Specifications**
```markdown
Create a React component for our e-commerce site's product listing page.

Requirements:
- Display products in a grid layout
- Show product image, name, price, and rating
- Include "Add to Cart" button
- Handle loading and error states
```

**Step 4: Specify Output Format**
```markdown
Create a React component for our e-commerce site's product listing page.

Requirements:
- Display products in a grid layout
- Show product image, name, price, and rating
- Include "Add to Cart" button
- Handle loading and error states

Output:
- TypeScript functional component
- Include prop interface
- Use styled-components for styling
```

**Step 5: Add Constraints (Optional)**
```markdown
Create a React component for our e-commerce site's product listing page.

Requirements:
- Display products in a grid layout
- Show product image, name, price, and rating
- Include "Add to Cart" button
- Handle loading and error states

Output:
- TypeScript functional component
- Include prop interface
- Use styled-components for styling

Constraints:
- Must be accessible (WCAG 2.1 AA)
- Mobile-first responsive design
- No external UI libraries (we have custom design system)
```

**Step 6: Add Validation (For Complex Tasks)**
```markdown
[Previous content...]

Validation:
- Verify accessibility attributes are present
- Confirm responsive breakpoints match our design system (320px, 768px, 1024px)
- Check that error states have appropriate user feedback
```

### Examples & Exercises

**Example 1: Minimal Prompt (Simple Task)**

```markdown
Convert this function to an arrow function:

function getTotal(items) {
  return items.reduce((sum, item) => sum + item.price, 0);
}
```

**Why this works**: Simple transformation task, no ambiguity, context is implicit.

**Example 2: Comprehensive Prompt (Complex Task)**

```markdown
# Role
You are a senior React developer specializing in performance optimization.

# Objective
Refactor the UserDashboard component to improve render performance.

# Context
The component currently re-renders every time any user action occurs, 
causing lag with 100+ dashboard widgets.

# Current Implementation
[Code here...]

# Requirements
- Implement React.memo where appropriate
- Use useMemo and useCallback strategically
- Split into smaller components if beneficial
- Maintain current functionality

# Output Format
- Explain each optimization decision
- Provide refactored code with comments
- Include before/after performance analysis

# Validation
- Verify widgets only re-render when their data changes
- Confirm no functionality is lost
```

**Why this works**: Complex task requiring judgment, context explains the problem, validation ensures quality.

**Exercise 1: Identify Missing Elements**

What's missing from this prompt?

```markdown
Fix the bug in this component. It's not working right.

[Component code...]
```

**Solution:**
Missing elements:
1. **Context**: What is the expected behavior?
2. **Input Data**: What specifically isn't working? Error messages?
3. **Constraints**: Any requirements for the fix?

**Improved version:**
```markdown
Fix the bug in the LoginForm component where the submit button remains 
disabled even after both email and password fields are filled.

Expected behavior: Button should enable when both fields have valid values.
Current behavior: Button stays disabled.

[Component code...]

Constraints:
- Maintain existing validation logic
- Preserve accessibility attributes
```

**Validation:**
- **Self-Check**: Does the improved prompt provide enough information for someone unfamiliar with the code to understand the problem?

**Exercise 2: Build a Complete Prompt**

Task: Create a prompt for building a custom dropdown component.

**Your Turn**: Build the prompt including all relevant elements.

**Solution:**
```markdown
# Instruction
Create a custom dropdown component for form inputs

# Context
Our design system requires a dropdown that matches our existing input styles.
The component will be used in forms across the application.

# Requirements
- Single and multi-select variants
- Keyboard navigation (arrow keys, Enter, Escape)
- Search/filter functionality
- Custom option rendering support

# Output Format
- TypeScript functional component
- Props interface with JSDoc comments
- CSS modules for styling
- Unit tests for key functionality

# Constraints
- Must work with React Hook Form
- Accessible (keyboard + screen reader)
- No external libraries (build from scratch)

# Validation
- Test with keyboard only navigation
- Verify ARIA attributes are correct
- Confirm compatibility with React Hook Form's Controller
```

**Validation:**
- **Self-Check**: Does your prompt include instruction, context, requirements, output format, and constraints?
- **Self-Check**: Could another developer build this component from your prompt alone?

### Frontend Contextualization

**Real-World Scenario: API Integration**

You're integrating a new API endpoint into your React app.

**❌ Weak Prompt:**
```markdown
How do I call an API in React?
```

**✅ Strong Prompt:**
```markdown
# Context
I need to integrate a new REST API endpoint that returns user profile data.

# API Details
- Endpoint: GET /api/users/{userId}
- Requires Bearer token authentication
- Returns: { id, name, email, avatar, preferences }

# Requirements
- Fetch on component mount and when userId prop changes
- Handle loading, success, and error states
- Cache response to prevent duplicate calls
- Show user-friendly error messages

# Current Setup
- Using fetch API (no axios)
- Auth token available from useAuth() hook
- Error boundary implemented at app level

# Output
- Custom hook implementation
- TypeScript types
- Error handling approach
- Integration example in component

# Constraints
- Must work with existing auth system
- No new dependencies
- Follow our existing data fetching patterns (check useFetchOrders hook)
```

**Practical Takeaway**: The time spent crafting a detailed prompt is saved many times over in fewer iterations and more accurate responses. Think of prompts as specifications—the better your spec, the better the implementation.

---

## Lesson 4: Prompt Formatting & Structure

### Objectives
- Master different prompt formatting techniques
- Choose appropriate formatting for various tasks
- Improve prompt clarity and parseability
- Reduce model misinterpretation through structure

### Explanation

#### Why Formatting Matters

Structured formatting provides:
- **Clarity**: Separate different parts of your prompt clearly
- **Accuracy**: Reduce errors from misinterpretation
- **Flexibility**: Easily modify parts without rewriting everything
- **Parseability**: Help model extract specific response elements

#### Formatting Approaches

**1. Natural Flow (No Explicit Labels)**

Organize content clearly with logical paragraphs:

```markdown
I'm working on a navbar component that needs to collapse on mobile.
The component should show a hamburger menu below 768px and a full 
horizontal menu above. It needs smooth animations and keyboard navigation.

Create a React component with these features using CSS modules.
```

**When to use**: Simple, straightforward requests where structure is implicit.

**2. Simple Labels**

Use clear markers for sections:

```markdown
Task: Create a responsive navbar

Requirements:
- Hamburger menu below 768px
- Full horizontal menu above 768px
- Smooth animations
- Keyboard navigation

Output: React component with CSS modules
```

**When to use**: Moderate complexity, need clear separation of concerns.

**3. Markdown Headers**

Use hierarchical structure:

```markdown
# Task: Create Responsive Navbar

## Requirements
- Hamburger menu below 768px
- Full horizontal menu above 768px
- Smooth animations
- Keyboard navigation

## Technical Specifications
- React functional component
- TypeScript with strict typing
- CSS modules for styling

## Validation
- Test on mobile and desktop viewports
- Verify keyboard accessibility
```

**When to use**: Complex tasks requiring hierarchical organization.

**4. XML-Style Tags**

Use explicit, semantic tags:

```markdown
<task>
Create a responsive navbar component
</task>

<requirements>
- Hamburger menu below 768px
- Full horizontal menu above 768px
- Smooth animations
- Keyboard navigation
</requirements>

<output>
React component with TypeScript and CSS modules
</output>

<validation>
Test on multiple viewports and verify keyboard accessibility
</validation>
```

**When to use**: Maximum clarity needed, especially when the model needs to extract specific sections in its response, or when dealing with complex, multi-part tasks.

### Step-by-Step Tutorial

**Choosing the Right Format**

**Step 1: Assess Task Complexity**

- **Simple** (1-2 requirements): Natural flow or simple labels
- **Moderate** (3-5 requirements): Simple labels or markdown headers
- **Complex** (6+ requirements or multi-phase): Markdown headers or XML tags

**Step 2: Consider Response Parsing**

Do you need to programmatically extract parts of the response?
- **Yes**: XML-style tags (most parseable)
- **No**: Any format works

**Step 3: Maintain Consistency**

Within a project or conversation:
- Use the same formatting style
- Keep naming consistent
- Maintain hierarchy rules

**Step 4: Apply Best Practices**

✅ **DO:**
- Be consistent with naming conventions
- Properly nest hierarchical elements
- Use semantic, descriptive labels
- Keep structure simple and clear

❌ **DON'T:**
- Mix formatting styles within one prompt
- Create unnecessary nesting
- Use ambiguous labels
- Over-complicate simple tasks

### Examples & Exercises

**Example 1: Format Evolution (Same Task, Different Formats)**

**Natural Flow:**
```markdown
Create a loading spinner component for our app. It should accept a size prop 
(small, medium, large) and an optional color. Use CSS animations for the 
spinning effect. Export as a reusable component.
```

**Simple Labels:**
```markdown
Task: Create loading spinner component

Props:
- size: 'small' | 'medium' | 'large'
- color: string (optional)

Implementation: CSS animations for spinning

Output: Reusable React component
```

**Markdown Headers:**
```markdown
# Task: Loading Spinner Component

## Props Interface
- size: 'small' | 'medium' | 'large'
- color: string (optional)

## Implementation Details
- CSS animations for spinning effect
- Accessible loading announcement

## Output Requirements
- Reusable React component
- TypeScript types included
```

**XML-Style:**
```markdown
<task>
Create a loading spinner component
</task>

<props>
- size: 'small' | 'medium' | 'large'  
- color: string (optional)
</props>

<implementation>
Use CSS animations for spinning effect.
Include accessible loading announcement.
</implementation>

<output>
Reusable React component with TypeScript types
</output>
```

All four formats are valid—choose based on complexity and preference.

**Exercise 1: Format Selection**

For each scenario, choose the most appropriate format:

**Scenario A**: "Convert this class component to a functional component"

**Scenario B**: "Create a comprehensive form validation system with error handling, async validation, field dependencies, and custom validation rules"

**Scenario C**: "Add a loading state to this button component"

**Solution:**

- **Scenario A**: Natural flow or simple labels (simple task)
- **Scenario B**: Markdown headers or XML-style (complex task)
- **Scenario C**: Natural flow (very simple task)

**Validation:**
- **Self-Check**: Does your format choice match task complexity?
- **Self-Check**: Would someone else understand the structure immediately?

**Exercise 2: Reformat a Prompt**

Take this unstructured prompt and reformat using markdown headers:

```markdown
I need a modal component that can be used throughout the app. It should have a backdrop that closes the modal when clicked. The modal should be centered and have a close button in the top right. Support different sizes like small medium and large. Animation when opening and closing. Trap focus inside when open. Close on Escape key. Use React Portal for rendering. TypeScript please.
```

**Solution:**
```markdown
# Task: Reusable Modal Component

## Core Functionality
- Backdrop that closes modal on click
- Centered positioning
- Close button in top-right corner
- Close on Escape key press

## Features
- Multiple size variants: small, medium, large
- Opening and closing animations
- Focus trap when modal is open
- Render using React Portal

## Technical Requirements
- TypeScript implementation
- Functional component with hooks
- Accessible keyboard navigation

## Accessibility
- Focus management
- ARIA attributes
- Keyboard controls (Escape to close)
```

**Validation:**
- **Self-Check**: Is all information from the original prompt included?
- **Self-Check**: Is the structure clear and scannable?
- **Self-Check**: Are related requirements grouped logically?

### Frontend Contextualization

**Real-World Scenario: Complex Feature Request**

Your team needs a new data table component with sorting, filtering, and pagination.

**❌ Unstructured:**
```markdown
Make a data table that can sort and filter and paginate. Needs to work with our API. Should look good on mobile. TypeScript. Use our design system colors. Needs column customization. Accessible. Export to CSV would be nice.
```

**✅ Well-Structured (Markdown Headers):**
```markdown
# Task: Data Table Component

## Core Features
- Sorting (multi-column support)
- Filtering (per-column)
- Pagination (client and server-side)
- CSV export

## API Integration
- Compatible with our REST API pagination format
- Request format: ?page=1&limit=10&sort=name&filter[status]=active
- Response format: { data: [], total: number, page: number }

## Responsive Design
- Full table on desktop (>1024px)
- Card layout on mobile (<768px)
- Horizontal scroll for tablet (768px-1024px)

## Column Configuration
- Customizable column visibility
- Resizable columns
- Reorderable columns (drag and drop)

## Technical Requirements
- TypeScript with strict typing
- React functional component
- Integration with our design system
- Follows WCAG 2.1 AA accessibility

## Design System
- Use theme colors from src/theme/colors
- Follow spacing scale from src/theme/spacing
- Match existing table styles in design system

## Validation
- Test with 1000+ row dataset
- Verify keyboard navigation works
- Confirm mobile card layout is usable
- Check screen reader announcements
```

**Benefits of structure:**
- Easy to reference specific sections during development
- Clear priorities and requirements
- Nothing is ambiguous or forgotten
- Model can organize response to match structure

**Practical Takeaway**: Time spent formatting a prompt is time saved in clarification rounds. A well-structured prompt is like a well-written Jira ticket—it sets up success from the start.

---

**Next:** Part 1b - [Foundational Lessons (Continued)](01b-foundations-continued.md)