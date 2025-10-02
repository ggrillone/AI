# Part 1: Foundational Lessons (Continued)

## Lesson 5: The AI Fluency Framework
[From Anthropic](https://anthropic.skilljar.com/ai-fluency-framework-foundations)

### Objectives
- Master the 4 core dimensions of AI collaboration: Delegation, Description, Discernment, Diligence
- Understand the feedback loops that connect these dimensions
- Apply framework thinking to improve AI interactions
- Develop a strategic approach to working with AI

### Explanation

The AI Fluency Framework provides a comprehensive mental model for effective AI collaboration. Think of it as your cognitive compass for navigating AI-assisted development.

#### The Four Dimensions

**1. Delegation: What to Delegate**

Strategic decisions about dividing work between you and the AI.

**Problem Awareness:**
- Understand the problem you're solving
- Define what success looks like
- Identify what thinking and work is needed
- **Without clarity here, you'll struggle with AI**

**Platform Awareness:**
- Know what the model can and can't provide
- Understand available tools and capabilities
- Know whether you need speed or depth, accuracy or creativity
- Understand which model works best for each task

**Task Delegation:**
- Break complex work into smaller pieces
- Decide when human involvement is necessary
- Determine what can be automated vs. augmented
- Make thoughtful choices about human-AI division of labor

**Example Decision Tree:**
```
Problem: Refactor large component
├─ Human handles: Architecture decisions, breaking down requirements
├─ AI handles: Code transformation, identifying patterns
└─ Collaborative: Review and validation
```

**2. Description: How to Communicate**

Clearly explain tasks, provide context, and guide interaction.

**Product Description:**
- Clearly describe what you want
- Explain every relevant detail—don't make AI guess
- Specify format, audience, and constraints
- Avoid assumptions

**Process Description:**
- Guide how the AI approaches the task
- Sometimes "how" is more important than "what"
- Share your problem-solving process
- Specify workflows, data sources, dependencies

**Process Instructions Examples:**
- "Think step-by-step before implementing"
- "Cite React documentation for validation"
- "Consider backwards compatibility"
- "Prioritize reusable code patterns"

**Performance Description:**
- Define how you want AI to behave
- Determine the kind of thinking partner you need:
  - Factual response vs. creative brainstorming
  - Challenging assumptions vs. validation
  - Educational explanation vs. direct answer

**Analogy**: Think of describing a task to a new team member. You wouldn't just say "build the login page." You'd explain the authentication flow, security requirements, design patterns, and how it fits into the larger application.

**3. Discernment: How to Evaluate**

Critically evaluate outputs—the quality control system.

**Product Discernment:**
- Did output accomplish the task?
- Is it factually accurate?
- Is it coherent and well-structured?
- Does it add value?

**Process Discernment:**
- Is the AI's thinking aligned with yours?
- Are there logical errors in reasoning?
- Were there unnecessary or irrelevant steps?
- Did it get stuck in a loop?
- How can you improve the AI-human dynamic?

**Performance Discernment:**
- Is the communication style appropriate?
- Is information clear and meaningful?
- Does the model respond to feedback and steering?

**Evaluation Questions:**
- "Does this solution actually solve my problem?"
- "What assumptions did the AI make?"
- "What would break if I used this code?"
- "Is this the approach I would have taken?"

**4. Diligence: Responsible Use**

Ethical and safety aspects of AI interaction.

**Creation Diligence:**
- Choosing appropriate AI systems
- Being thoughtful about how you work with them
- Understanding capabilities and limitations

**Transparency Diligence:**
- Being open about AI's role in your work
- Acknowledging AI assistance appropriately
- Setting clear expectations with team

**Deployment Diligence:**
- Taking ownership of AI-assisted outputs
- Reviewing before sharing with others
- Understanding implications of what's created
- Considering who might be affected

**Key Principle**: **You are responsible, not the AI**

**Questions to Consider:**
- Can I provide this data to AI? (sensitive info, PII, proprietary code)
- Who might be affected by what is created?
- What are the implications of this AI interaction?
- Am I being transparent about AI's role?

#### The Framework Loops

**Loop 1: Delegation ↔ Diligence**

Handles big-picture strategic and ethical decision-making.

- Delegation and Diligence inform each other bidirectionally
- Develops clear rationales for choices
- Helps articulate why your approach aligns with goals and values
- Accountability and transparency enhance creative possibilities

**Example:**
```
Delegation Decision: "Use AI to generate unit tests"
      ↓
Diligence Check: "Are we testing proprietary algorithms? (No) Can I share 
                  this code structure? (Yes) Will I review tests? (Yes)"
      ↓
Refined Delegation: "Use AI to generate unit test scaffolding, I'll add 
                     edge cases and proprietary business logic tests"
```

**Loop 2: Description ↔ Discernment**

Transforms commands into conversations that build cognitive environments.

- Product, Process, and Performance as different lenses
- Context builds shared understanding
- Moves beyond automation to genuine augmentation
- Creates shared vocabulary and interaction patterns

**Example:**
```
Description: "Create a modal component" (initial)
      ↓
Discernment: Output is functional but doesn't match our patterns
      ↓
Refined Description: "Create a modal matching our design system patterns 
                      (see src/components/Button for reference)"
      ↓
Discernment: Now matches our style, but accessibility could improve
      ↓
Refined Description: "Add ARIA attributes and focus trap like our Dialog 
                      component"
```

### Step-by-Step Tutorial

**Applying the Framework to a Real Task**

**Scenario**: You need to add real-time notifications to your React app.

**Step 1: Delegation (Strategic Planning)**

Before prompting, answer:
- **Problem**: What exactly needs solving? (Real-time notification delivery)
- **Success**: What does working look like? (Notifications appear within 2 seconds, persist across page nav, dismissible)
- **Platform**: Which model/tools? (Claude for architecture, Cursor for implementation)
- **Division of labor**: 
  - Human: Architecture decisions, security requirements, UX design
  - AI: Implementation patterns, WebSocket setup, state management

**Step 2: Description (Crafting the Prompt)**

Based on delegation decisions:

```markdown
# Role
You are a senior React developer with WebSocket expertise.

# Task
Design and implement a real-time notification system.

# Product Requirements
- Receive notifications via WebSocket connection
- Display toast notifications in top-right corner
- Persist notifications (store in state)
- Users can dismiss notifications
- Notifications auto-dismiss after 5 seconds (optional per notification)

# Process Requirements
- First, propose the architecture (WebSocket client, state management, UI components)
- Then, implement step-by-step
- Use existing auth token for WebSocket authentication

# Technical Constraints
- Use native WebSocket API (no socket.io)
- Integrate with our existing React Context
- Follow our component patterns (see src/components/Toast)

# Performance Requirements
- Explain architectural decisions
- Think through edge cases (connection drops, rapid notifications)
```

**Step 3: Discernment (Evaluate Output)**

Review the AI's response:

**Product Check:**
- ✅ Does it solve the real-time delivery problem?
- ✅ Are all requirements addressed?
- ❓ Is the WebSocket reconnection logic robust?

**Process Check:**
- ✅ Did it explain architecture first?
- ❌ It didn't consider notification deduplication
- ✅ Edge cases were considered

**Performance Check:**
- ✅ Explanations are clear
- ✅ Responds well to follow-up questions

**Step 4: Refine Based on Discernment**

```markdown
The architecture looks good. Please add:
1. Notification deduplication logic (prevent duplicate notifications with same ID)
2. Exponential backoff for WebSocket reconnection
3. How to handle notifications received while user is on different tab
```

**Step 5: Diligence Check**

Before implementing:
- ✅ Can I share our WebSocket endpoint format? (Check with team - generic pattern OK)
- ✅ Am I taking ownership of this implementation?
- ✅ Will I test thoroughly before deploying?
- ❌ Need to verify: Does this handle sensitive notification content properly?

**Step 6: Final Refinement**

```markdown
One more requirement: Notifications may contain user email addresses.
Ensure notifications are not logged to console and are cleared from
memory when dismissed. Add a notification privacy section to your implementation.
```

### Examples & Exercises

**Example: Framework in Action - Code Review**

**Delegation:**
- Problem: Need second pair of eyes on complex reducer logic
- Platform: AI can catch logical errors, suggest improvements
- Division: AI reviews, human makes final decisions on changes

**Description:**
```markdown
Review this reducer for logical errors and potential improvements.

Context: Manages shopping cart state with add/remove/update quantity operations.
Focus on: Edge cases, immutability, performance.

[Code here...]

Provide:
1. Any bugs or logical errors
2. Potential edge cases not handled
3. Performance optimization opportunities
```

**Discernment:**
- AI identified 2 bugs: quantity going negative, duplicate items
- Suggestions are practical and specific
- Explanations are clear

**Diligence:**
- AI output needs human verification (logic is complex)
- I'm responsible for implementing fixes correctly
- Will add test cases for identified edge cases

**Exercise 1: Framework Application**

Apply the framework to this scenario:

**Scenario**: You're building a CSV export feature for a data table.

**Your Task**: 
1. What do you delegate to AI vs handle yourself?
2. Write a description prompt
3. List 3 discernment checks you'll perform
4. Identify 2 diligence considerations

**Solution:**

**1. Delegation:**
- Human: Decide which columns to export, date format preferences, security requirements
- AI: Generate CSV formatting logic, handle special characters escaping, create download mechanism
- Collaborative: Testing with edge cases

**2. Description Prompt:**
```markdown
# Task
Implement CSV export functionality for our data table.

# Requirements
- Export visible columns only
- Format dates as YYYY-MM-DD
- Escape special characters properly
- Trigger download with meaningful filename

# Context
- Data structure: Array<{ id, name, email, createdAt, status }>
- Current table component in src/components/DataTable.tsx

# Constraints
- Client-side export only (no server processing)
- Must handle 10,000+ rows without freezing UI
- Follow our existing file export patterns

# Output
- Export function with TypeScript types
- Integration approach with DataTable component
- Performance considerations for large datasets
```

**3. Discernment Checks:**
- ✅ Does CSV output format correctly in Excel and Google Sheets?
- ✅ Are special characters (commas, quotes, newlines) properly escaped?
- ✅ Does it handle large datasets without UI freeze?
- ✅ Is the filename generation appropriate?
- ✅ Are edge cases handled (empty data, missing fields)?

**4. Diligence Considerations:**
- 🔒 Exported CSVs may contain PII—ensure user has permission to export
- 📋 Document that this exports client-side data only (filtered/sorted view)
- ⚠️ Verify no sensitive data appears in console logs during export
- ✅ Take ownership of testing with various data scenarios

**Validation:**
- **Self-Check**: Did you consider both strategic (delegation) and ethical (diligence) aspects?
- **Self-Check**: Is your description prompt specific enough to guide implementation?
- **Self-Check**: Do your discernment checks cover functionality, quality, and user experience?

### Frontend Contextualization

**Real-World Scenario: Building a Form Builder**

Your team needs a drag-and-drop form builder component—a complex, multi-week project.

**Applying the Framework:**

**1. Delegation Strategy**

**Human Responsibilities:**
- Overall architecture and component hierarchy
- UX decisions (drag feedback, validation rules)
- Integration points with backend
- Security requirements

**AI Responsibilities:**
- Drag-and-drop implementation patterns
- Form state management code
- Validation logic implementation
- Component boilerplate generation

**Collaborative:**
- Code reviews
- Edge case identification
- Performance optimization
- Testing strategies

**2. Description Evolution**

**Initial Exploration (Vague):**
```markdown
What are the best approaches for building a drag-and-drop form builder in React?
```

**Architecture Planning (Specific):**
```markdown
# Context
Building a form builder where users drag fields (text, email, select) onto a canvas.

# Question
Propose an architecture including:
- Component hierarchy
- State management approach (Context vs Redux vs Zustand)
- Drag-and-drop library recommendation
- Form data schema structure

Consider:
- Performance with 50+ form fields
- Undo/redo functionality
- Real-time preview
- Export to JSON format

Compare trade-offs of different approaches.
```

**Implementation Phase (Very Specific):**
```markdown
Implement the FormField component based on our architecture plan (see form-builder-architecture.md).

Requirements:
- Accept fieldType prop: 'text' | 'email' | 'select' | 'checkbox'
- Render appropriate input with validation
- Support custom validation rules
- Display error messages
- Draggable using react-beautiful-dnd

Follow patterns from our existing Input component (src/components/Input.tsx).

Output TypeScript component with full typing.
```

**3. Discernment at Each Phase**

**After Architecture Planning:**
- ✅ Are proposed patterns suitable for our team's expertise?
- ✅ Does the state management choice fit our existing stack?
- ❓ Is the drag-and-drop library actively maintained?
- ✅ Can this scale to our requirements?

**After Implementation:**
- ✅ Does the component match our architecture?
- ✅ Are TypeScript types comprehensive?
- ❌ Accessibility attributes are missing → request additions
- ✅ Code follows our style guide

**4. Diligence Throughout**

**Creation:**
- ✅ Choosing Claude Sonnet for architecture (depth), GPT-4 for rapid iteration (speed)
- ✅ Breaking project into manageable AI-assisted chunks

**Transparency:**
- 📝 Document: "Form builder components scaffolded with AI assistance, implementation reviewed and tested by team"
- 👥 Share prompt templates with team for consistency

**Deployment:**
- ✅ Thoroughly test all AI-generated form validation logic
- ✅ Security review of form data handling
- ✅ Accessibility audit before shipping
- ✅ Take ownership of any bugs in AI-generated code

**Practical Takeaway**: The Framework isn't a rigid checklist—it's a thinking tool. As you gain experience, these considerations become automatic. Early on, explicitly work through each dimension. Eventually, it becomes second nature, like how experienced developers automatically think about edge cases, performance, and maintainability.

---

## Lesson 6: Vague vs Specific Prompts

### Objectives
- Understand when to use vague (open-ended) vs specific prompts
- Recognize the spectrum of prompt specificity
- Learn to intentionally choose prompt specificity level
- Combine vague and specific approaches strategically

### Explanation

#### The Specificity Spectrum

Prompts exist on a spectrum from completely open-ended to highly constrained:

```
Vague                                                                    Specific
|-----------|-----------|-----------|-----------|-----------|-----------|
Exploration   Discovery    Guidance    Direction   Precision   Strict Rules
```

**Important**: Neither end is inherently better—**the key is being intentional** about where you land on this spectrum based on your goal.

#### When to Use Vague Prompts

**Characteristics:**
- Open-ended and exploratory
- Allow wide solution space
- Encourage creative thinking
- Minimal constraints

**Use Cases:**
- 🎨 Brainstorming ideas
- 🗺️ Exploring alternative solutions
- 📚 Learning about possibilities
- 🔓 Getting unstuck
- 🔍 Discovery phase of a project

**Benefits:**
- Can lead to novel ideas you hadn't considered
- Exposes you to different approaches
- Good for learning and exploration

**Downsides:**
- Can produce off-topic or overly general results
- May require more refinement
- Less predictable outputs

**Example Vague Prompts:**
```markdown
"What are best practices for validating email addresses?"
"Suggest UI improvements for a signup form"
"How can I make my React component update when data changes?"
"What are some approaches for managing application state?"
```

#### When to Use Specific Prompts

**Characteristics:**
- Clear instructions and constraints
- Defined parameters and requirements
- Explicit guard rails
- Targeted outcomes

**Use Cases:**
- 🎯 Getting structured, repeatable outputs
- 📋 Following strict design patterns or business logic
- ⚡ Optimizing or debugging something specific
- 🏗️ Implementing known solutions
- ⏱️ Saving time on boilerplate

**Benefits:**
- More control and consistency
- Predictable, actionable output
- Efficient for known problems

**Downsides:**
- Might miss creative or alternative approaches
- Can over-constrain and limit valuable suggestions
- Requires you to know what you want

**Example Specific Prompts:**
```markdown
"Write a React functional component that renders a signup form with email and 
password inputs, client-side validation using Yup, and submits to /api/auth/signup"

"Create a custom hook called useDebounce that accepts a value and delay, returns 
the debounced value, and cleans up the timeout on unmount"

"Refactor this UserProfile component to use React.memo and useMemo to prevent 
re-renders when the parent theme context updates"
```

#### The Hybrid Approach: Vague Goal + Specific Constraints

Sometimes it can be an effective approach to combine both:
- **Vague** about the solution approach (don't constrain thinking)
- **Specific** about the requirements and constraints (provide clarity)

**Example:**
```markdown
I need to overlay help text on top of a specific HTML element. 

Requirements:
- Text displays to the right of the target element
- Text remains next to element as user scrolls
- Works with multiple screen sizes
- Adapts if user resizes browser

Note: I'm open to different implementation approaches—don't assume a specific 
solution like absolute positioning or getBoundingClientRect unless it's the 
best option.
```

This prompt:
- ✅ Clear about requirements (specific)
- ✅ Open about implementation approach (vague)
- ✅ Encourages AI to consider various solutions

### Step-by-Step Tutorial

**Choosing Your Specificity Level**

**Step 1: Identify Your Starting Point**

Ask yourself:
- ❓ Do I know what I want, or am I exploring?
- ❓ Do I need one right answer, or multiple options?
- ❓ Am I stuck, or implementing a known solution?

**Step 2: Map to Specificity Level**

| Your Situation | Specificity Level | Example Prompt |
|----------------|-------------------|----------------|
| "I have no idea how to approach this" | Very Vague | "What are ways to handle real-time data in React?" |
| "I want to see options" | Vague | "Show me 3 different patterns for managing modal state" |
| "I know generally what I want" | Moderate | "Create a modal component with these features: [list]" |
| "I know exactly what I need" | Specific | "Create a modal using React Portal, with backdrop, focus trap, and ESC key support" |
| "I need it done a specific way" | Very Specific | "Create a modal matching this exact API: [interface], using these exact libraries: [list], following this pattern: [example]" |

**Step 3: Test and Adjust**

If the response is:
- Too generic or off-topic → Increase specificity
- Missing creative alternatives → Decrease specificity
- Perfect → You found the right level

**Step 4: Iterate with Refinement**

Start vague to explore, then get specific:

```markdown
Iteration 1 (Vague): "How should I structure a large React form with validation?"
→ Review options

Iteration 2 (Moderate): "Implement the form using React Hook Form with 
Zod validation as you suggested"
→ Get implementation

Iteration 3 (Specific): "Add conditional field logic where the 'Company' 
field only shows when 'Account Type' is 'Business'"
→ Refine details
```

### Examples & Exercises

**Example 1: Exploring Architectural Patterns**

**Vague Approach (Exploration):**
```markdown
What are some approaches for managing application state in a React application?
```

**Expected Response:** Multiple options (Context API, Redux, Zustand, Recoil, etc.) with brief explanations, helping you explore the solution space.

**Specific Approach (Implementation):**
```markdown
How do I implement Redux Toolkit for state management in a React application 
with TypeScript? Include store setup, slice creation, and component integration.
```

**Expected Response:** Detailed implementation steps, code examples, and specific configurations for Redux Toolkit.

**Comparison:** Use vague when exploring and learning. Use specific when you know what you want and need implementation details.

**Example 2: Component Development**

**Vague Prompt:**
```markdown
How can I make my React component update when data changes?
```

**Expected Response:** Discusses useState, useEffect, props, various update mechanisms without knowing your exact need.

**Specific Prompt:**
```markdown
I have a UserProfile component that receives userId as a prop. When userId 
changes, I need to fetch new user data from /api/users/{userId} and update 
the display. The component should show a loading state while fetching and 
handle errors gracefully. Please provide a React functional component using hooks.
```

**Expected Response:** Complete, specific implementation with useEffect, useState, error handling, and loading states.

**Comparison:** Vague for learning possibilities. Specific for precise implementation with clear requirements.

**Example 3: Combined Approach for Complex Refactoring**

**Step 1 - Initial Vague Prompt:**
```markdown
I have a large component that handles user authentication, form validation, 
and API calls. What are some strategies for improving this code?
```

**Expected Response:** Patterns like separation of concerns, custom hooks, composition, etc.

**Step 2 - Follow-up Specific Prompt:**
```markdown
Based on your suggestion to use custom hooks, help me refactor the authentication 
logic. The component currently has login/logout functions, token management, and 
user state. Extract these into a useAuth hook following React best practices.
```

**Expected Response:** Detailed custom hook implementation.

**This demonstrates:** Start vague to explore options, then get specific once you've decided on an approach.

**Exercise 1: Adjust Specificity**

For each prompt, identify if it's too vague, too specific, or just right for the stated goal. Then rewrite if needed.

**Prompt A:**
Goal: Learn about form validation options
Prompt: "Implement form validation using Formik with Yup schema validation, including async email uniqueness checking, password strength requirements, and custom error messages styled with our design system"

**Prompt B:**
Goal: Implement a specific validation rule
Prompt: "How do I validate forms?"

**Prompt C:**
Goal: Explore animation libraries
Prompt: "What are popular React animation libraries and what are the trade-offs of each?"

**Solution:**

**Prompt A:** TOO SPECIFIC for the goal
- Goal is to learn options, but prompt prescribes exact implementation
- **Rewrite:** "What are effective approaches for form validation in React? Compare trade-offs of different libraries and patterns."

**Prompt B:** TOO VAGUE for the goal
- Goal is specific implementation, but prompt is exploratory
- **Rewrite:** "I need to validate that a password field contains at least 8 characters, one uppercase letter, and one number. How do I implement this validation in React Hook Form?"

**Prompt C:** JUST RIGHT
- Goal is exploration, prompt encourages comparison
- No rewrite needed

**Validation:**
- **Self-Check:** Does specificity level match the goal?
- **Self-Check:** Would the response be actionable for your actual need?

**Exercise 2: Progressive Refinement**

Start with a vague prompt, then progressively make it more specific based on "responses."

**Scenario:** You need to add search functionality to your app.

**Your Task:** Write 3 prompts of increasing specificity.

**Solution:**

**Prompt 1 (Vague - Exploration):**
```markdown
What are effective approaches for implementing search functionality in a React application?
```
*Imagine response discusses: client-side filtering, debouncing, server-side search APIs, search libraries like Fuse.js, etc.*

**Prompt 2 (Moderate - Direction):**
```markdown
Based on using a server-side search API, how should I implement a search input 
component with debouncing? The API is GET /api/search?q=query and returns 
{results: Array, total: number}.
```
*Imagine response provides component structure with useState, useEffect, debouncing logic.*

**Prompt 3 (Specific - Implementation):**
```markdown
Implement the search component with these specific requirements:

- 300ms debounce delay
- Show loading indicator while searching
- Display "No results" message when results are empty
- Cancel pending requests if query changes
- Use AbortController for request cancellation
- TypeScript with strict typing
- Follow our existing API hook pattern (see src/hooks/useFetchData.ts)

Return a complete component with a custom useSearch hook.
```

**Validation:**
- **Self-Check:** Does each prompt build on insights from the previous?
- **Self-Check:** Does the final prompt have everything needed for implementation?
- **Self-Check:** Could you skip directly to Prompt 3 if you already knew your requirements?

### Frontend Contextualization

**Real-World Scenario: Adding Dark Mode**

You're tasked with adding dark mode to your application.

**Phase 1: Exploration (Vague)**

```markdown
What are the best practices for implementing dark mode in a React application?
Consider maintainability, performance, and user experience.
```

**Why vague here:** You want to understand different approaches before committing.

**Expected insights:** CSS variables, theme context, system preference detection, toggle persistence, etc.

---

**Phase 2: Architecture (Moderate)**

```markdown
I want to implement dark mode using CSS variables and React Context.

Requirements:
- Support system preference detection
- Allow manual toggle
- Persist user preference
- Smooth transitions between themes

What's the best way to structure this? Provide high-level architecture, 
not full implementation yet.
```

**Why moderate:** You've chosen an approach but want architectural guidance before coding.

**Expected insights:** Context structure, CSS variable organization, localStorage strategy.

---

**Phase 3: Implementation (Specific)**

```markdown
Implement a ThemeProvider component based on this architecture:

Context Structure:
- theme: 'light' | 'dark' | 'system'
- setTheme: (theme) => void
- resolvedTheme: 'light' | 'dark' (accounts for system preference)

Requirements:
- Detect system preference using matchMedia
- Store preference in localStorage as 'theme-preference'
- Apply theme by setting 'data-theme' attribute on <html>
- Listen for system preference changes
- Prevent flash of wrong theme on page load

Constraints:
- TypeScript with full typing
- Custom hook useTheme for consuming context
- SSR-compatible (Next.js)

CSS variables are already defined in globals.css as:
[data-theme='light'] { --bg: white; --text: black; }
[data-theme='dark'] { --bg: black; --text: white; }
```

**Why specific:** You know exactly what you need, provide all details for correct implementation.

**Expected output:** Complete, implementation-ready code.

---

**Phase 4: Refinement (Very Specific)**

```markdown
The ThemeProvider is working but has a flash on page load. Implement the 
blocking script approach:

1. Create a theme-script.ts that can be injected in <head>
2. Script should run before React hydration
3. Read localStorage and apply theme immediately
4. Set data-theme attribute synchronously
5. Export as string for Next.js Script component with strategy="beforeInteractive"

Current issue: theme flashes on page refresh in Next.js when user has dark mode preference.
```

**Why very specific:** Solving a specific technical problem with known solution pattern.

---

**Key Insight from Scenario:**

Notice the progression:
1. **Vague:** Learn possibilities → Informed decision-making
2. **Moderate:** Get guidance → Architecture clarity
3. **Specific:** Get implementation → Working code
4. **Very Specific:** Solve edge case → Production ready

You could skip steps if you already have that knowledge, but following the progression:
- Exposes you to alternatives you might not have considered
- Validates your approach before heavy implementation
- Builds understanding, not just copy-paste code

**Practical Takeaway**: Think of prompt specificity as a zoom level. Zoomed out (vague) gives you the landscape; zoomed in (specific) gives you the details. Most complex tasks benefit from starting zoomed out, then progressively zooming in. But if you already know the landscape, zoom directly to the detail level you need.

---

# Summary: Foundational Lessons

Congratulations! You've completed the foundational lessons. Let's recap what you've learned:

| Lesson | Key Takeaway | Application |
|--------|-------------|-------------|
| 1: Understanding AI Models | LLMs are pattern predictors, not knowledge bases | Set realistic expectations, understand limitations |
| 2: Tokens & Context Windows | Tokens cost money; context is limited working memory | Optimize prompts, manage session context strategically |
| 3: Anatomy of Effective Prompts | Prompts need instruction, context, input, format, constraints | Structure requests for clarity and completeness |
| 4: Prompt Formatting & Structure | Structure reduces ambiguity and improves clarity | Choose format based on task complexity |
| 5: AI Fluency Framework | Master Delegation, Description, Discernment, Diligence | Strategic approach to AI collaboration |
| 6: Vague vs Specific Prompts | Intentionally choose specificity based on goal | Start vague for exploration, specific for implementation |

## Before Moving to Intermediate Lessons

**Self-Assessment Questions:**
1. ✅ Can you identify which prompt elements are missing from an incomplete prompt?
2. ✅ Do you understand when to use vague vs specific prompts?
3. ✅ Can you apply the AI Fluency Framework to evaluate an AI interaction?
4. ✅ Are you comfortable with basic prompt formatting?

If you answered yes to these, you're ready for intermediate techniques!

**Practice Exercise Before Proceeding:**

Create a complete prompt for this scenario using everything you've learned:

**Scenario:** Your app needs a component that displays a list of notifications with real-time updates, filtering, and the ability to mark as read.

**Your prompt should include:**
- Appropriate specificity level (explain why you chose it)
- Proper formatting
- Framework application (delegation, description, discernment, diligence considerations)
- All necessary prompt elements

Try this on your own before moving forward!

---

**Next:** Part 2 - [Intermediate Lessons](02-intermediate-lessons.md)


