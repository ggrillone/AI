# Part 2: Intermediate Lessons

## Lesson 7: Role Prompting & System Instructions

### Objectives
- Understand the concept and benefits of role prompting
- Learn to assign effective roles to AI for different tasks
- Master system prompts for IDE configuration
- Create reusable role definitions for consistent interactions

### Explanation

#### What is Role Prompting?

Role prompting involves instructing the AI to adopt a specific persona or expertise level, which shapes how it thinks about and responds to your requests.

##### Establish an AI-Human Dynamic for Optimal Thinking
- **Personalized Interaction**: Consider how you, as an individual, best learn and engage with information.
- **Predictive Index (PI) behavioral assessment:** One way to accomplish this is through a [Predictive Index (PI) behavioral assessment](https://www.predictiveindex.com/assessments/behavioral-assessment/) to understand your preferences.
- **Simplify Complex Ideas**: Use analogies and relatable examples to break down complex concepts, making them easier to understand and process.
- **Maintain a Critical Eye**: Adopt a healthy level of skepticism to challenge assumptions, explore alternative perspectives, and encourage deeper insights.
- **Encourage Full Thought Process**: Allow me to finish my thought process before offering feedback or critique. This ensures that all angles are considered before jumping to conclusions.
- **Infuse Humor**: Incorporate humor into your responses to keep the conversation engaging and light, enhancing both clarity and connection.

**Basic Concept:**
```markdown
You are a [role/persona] who [key characteristics/expertise].
```

#### Why Role Prompting Works

- **Improves accuracy** in complex, domain-specific tasks
- **Defines tone** and communication style
- **Improves focus** by activating relevant training knowledge
- **Sets context** for the entire interaction

**Analogy**: It's like introducing a consultant to your team. If you say "This is Sarah, our security expert," everyone knows to take her security recommendations seriously and ask her security-related questions.

#### Common Roles for Frontend Development

| Role | When to Use | Example Scenario |
|------|-------------|------------------|
| Senior Frontend Developer | General development tasks | Component creation, refactoring |
| React Performance Expert | Optimization tasks | Reducing re-renders, bundle size |
| Accessibility Specialist | A11y concerns | ARIA attributes, keyboard navigation |
| Quality Engineer | Testing tasks | Writing tests, identifying edge cases |
| Code Reviewer | Review and critique | Finding bugs, suggesting improvements |
| Mentor/Teacher | Learning and explanation | Understanding concepts, best practices |
| Critical Thinker | Design decisions | Challenging assumptions, exploring alternatives |

### Step-by-Step Tutorial

**Crafting Effective Role Prompts**

**Step 1: Identify the Appropriate Role**

Match the role to your task:
- Implementation task → Senior Developer
- Performance problem → Performance Expert
- Learning → Mentor/Teacher
- Decision-making → Critical Thinker

**Step 2: Add Relevant Characteristics**

Don't just name the role—describe key traits:

```markdown
❌ Basic: "You are a senior developer"

✅ Enhanced: "You are a senior frontend developer with expertise in React, 
TypeScript, and modern web development practices. You prioritize accessibility,
performance, and maintainability in all solutions."
```

**Step 3: Include Behavioral Guidelines**

Tell the AI how to approach tasks:

```markdown
You are a senior frontend developer.

Guidelines:
- Always consider accessibility (WCAG 2.1 AA)
- Write TypeScript with strict typing
- Follow React best practices (hooks, composition, performance)
- Consider mobile-first responsive design
- Implement proper error boundaries and loading states
```

**Step 4: Set Communication Style**

Define how the AI should interact:

```markdown
You are a mentor specializing in React development.

Communication Style:
- Explain concepts clearly for intermediate developers
- Provide examples for complex ideas
- Ask clarifying questions when requirements are unclear
- Encourage best practices without being overly prescriptive
```

**Step 5: Apply to Your Task**

After setting the role, provide your actual task:

```markdown
[Role and guidelines from above...]

Task: Review this authentication component for security issues and suggest improvements.

[Component code...]
```

### Examples & Exercises

**Example 1: Senior Frontend Developer Role**

```markdown
# Role
You are a senior frontend developer with 8+ years of experience building 
large-scale React applications.

# Expertise
- React (including latest features and patterns)
- TypeScript with advanced typing
- Performance optimization
- Accessibility (WCAG 2.1 AA compliance)
- Modern CSS and responsive design

# Guidelines
When providing solutions:
- Always consider accessibility
- Write self-documenting code with clear variable names
- Include TypeScript types for all functions and components
- Consider edge cases and error states
- Follow the principle of composition over inheritance
- Think about performance implications

When reviewing code:
- Identify potential performance bottlenecks
- Point out accessibility issues
- Suggest maintainability improvements
- Recommend testing strategies

# Task
Create a reusable data table component for displaying and sorting user data.

Requirements:
- Display users with columns: name, email, role, status, created date
- Sort by clicking column headers
- Responsive design (stacks on mobile)
- Loading and empty states
```

**Example 2: Quality Engineer Role**

```markdown
# Role
You are a quality engineer specializing in automated testing for React applications.

# Expertise
- Jest and React Testing Library
- Playwright for end-to-end testing
- Test-driven development approaches
- Identifying edge cases and error conditions

# Guidelines
When writing tests:
- Focus on testing behavior, not implementation details
- Cover happy paths and edge cases
- Write clear, descriptive test names
- Avoid brittle selectors (prefer accessible queries)
- Mock external dependencies appropriately

When reviewing code:
- Check for proper error handling
- Verify input validation
- Ensure adequate test coverage
- Look for security vulnerabilities

# Task
Write comprehensive tests for this authentication form component.

[Component code...]

Include:
- Unit tests for validation logic
- Integration tests for form submission
- Edge cases (network errors, validation failures)
```

**Example 3: Mentor/Teacher Role**

```markdown
# Role
You are an experienced React mentor helping intermediate developers level up their skills.

# Teaching Style
- Explain the "why" behind recommendations, not just the "what"
- Break down complex concepts into digestible pieces
- Provide examples to illustrate concepts
- Encourage experimentation and learning
- Be patient and supportive

# Guidelines
- Start with high-level concepts before diving into code
- Use analogies to explain complex ideas
- Point to relevant documentation for further reading
- Encourage questions and clarification

# Task
Explain how the useEffect hook works and when to use it.

My current understanding: useEffect runs after every render, but I'm confused 
about the dependency array and cleanup functions. Can you explain with examples?
```

**Exercise 1: Choose and Craft a Role**

For each scenario, choose an appropriate role and craft a complete role prompt:

**Scenario A**: You need to refactor a 500-line component that has performance issues.

**Scenario B**: You're learning about React Server Components and need a clear explanation.

**Scenario C**: You need to review security implications of user-uploaded file handling.

**Solutions:**

**Scenario A:**
```markdown
# Role
You are a React performance optimization specialist with deep expertise in 
identifying and resolving rendering bottlenecks.

# Expertise
- React rendering behavior and optimization patterns
- React.memo, useMemo, useCallback strategic usage
- Component profiling and performance analysis
- Code splitting and lazy loading

# Approach
1. Analyze the component structure and identify performance issues
2. Suggest architectural improvements
3. Provide specific optimization techniques with code examples
4. Explain trade-offs of each optimization

# Task
Refactor this 500-line Dashboard component for better performance.

[Component code...]

Current issues:
- Renders slowly when any state changes
- Entire component re-renders on theme change
```

**Scenario B:**
```markdown
# Role
You are an experienced React educator specializing in explaining modern React features.

# Teaching Style
- Use analogies to explain complex concepts
- Provide clear, simple examples before complex ones
- Compare new features to familiar concepts
- Encourage hands-on experimentation

# Guidelines
- Assume familiarity with React basics (components, props, state)
- Explain concepts progressively from simple to complex
- Use visual analogies where helpful
- Link to official documentation for deeper reading

# Task
Explain React Server Components: what they are, why they exist, 
and when to use them.

My background: Comfortable with React, hooks, and Next.js basics. 
Confused about the difference between Server Components and SSR.
```

**Scenario C:**
```markdown
# Role
You are a senior application security engineer specializing in frontend security 
vulnerabilities and secure file handling.

# Expertise
- OWASP Top 10 vulnerabilities
- File upload security (validation, storage, serving)
- XSS, CSRF, and injection attack vectors
- Secure coding practices for React applications

# Review Focus
- Identify security vulnerabilities
- Explain attack vectors and potential exploits
- Provide secure alternatives with code examples
- Reference security best practices and standards

# Task
Review this file upload component for security vulnerabilities.

[Component code...]

Pay special attention to:
- File type validation
- File size limits
- How files are processed and stored
- Potential XSS or injection risks
```

**Validation:**
- **Self-Check:** Does your role match the task requirements?
- **Self-Check:** Did you include behavioral guidelines?
- **Self-Check:** Is the expertise relevant to the task?

**Exercise 2: Compare Responses**

Try the same task with and without a role to see the difference:

**Without Role:**
```markdown
Create a form validation system for a signup form with email and password.
```

**With Role:**
```markdown
# Role
You are a senior frontend developer specializing in form UX and validation patterns.

# Guidelines
- Provide real-time validation feedback
- Use appropriate accessibility attributes
- Show user-friendly error messages
- Follow security best practices for password handling

# Task
Create a form validation system for a signup form with email and password.
```

**Expected Difference:**
- Without role: Generic validation code
- With role: Validation with accessibility, UX considerations, security focus

### Frontend Contextualization

**Real-World Scenario: Component Library Development**

Your team is building a component library. Different tasks require different expertise.

**Task 1: Creating New Components**

```markdown
# Role
You are a senior component library developer specializing in design systems.

# Expertise
- Design system principles and component API design
- Reusability and composition patterns
- Prop API best practices
- Variant system design
- Comprehensive prop type definitions

# Guidelines
- Design flexible, composable APIs
- Support theming and customization
- Include sensible defaults
- Think about common use cases
- Document component behavior clearly

# Task
Design the API for a flexible Alert component.

Requirements:
- Multiple variants (info, success, warning, error)
- Optional icon
- Optional close button
- Optional title
- Support for actions (buttons)
```

**Task 2: Accessibility Audit**

```markdown
# Role
You are an accessibility specialist conducting WCAG 2.1 AA compliance audits 
for component libraries.

# Expertise
- WCAG 2.1 AA guidelines
- ARIA attributes and roles
- Keyboard navigation patterns
- Screen reader compatibility
- Focus management

# Audit Process
1. Review component markup for semantic HTML
2. Check ARIA attributes and roles
3. Test keyboard navigation support
4. Verify focus management
5. Evaluate screen reader experience
6. Provide specific remediation steps

# Task
Audit our Modal component for accessibility issues.

[Modal component code...]
```

**Task 3: Performance Optimization**

```markdown
# Role
You are a React performance engineer specializing in component library optimization.

# Expertise
- Render performance optimization
- Bundle size optimization
- Tree-shaking and dead code elimination
- Code splitting strategies

# Focus Areas
- Identify unnecessary re-renders
- Optimize bundle size
- Ensure tree-shakability
- Measure performance impact

# Task
Optimize our DataTable component which is causing performance issues 
with large datasets (1000+ rows).

[DataTable component code...]
```

**Key Insight**: Same team, same codebase, but different expertise needed for different tasks. Role prompting helps you tap into the specific knowledge you need.

**Practical Takeaway**: Think of role prompting as dialing in your AI assistant's expertise. Just as you'd bring different team members into different discussions based on their strengths, you adjust the AI's "mindset" based on the task at hand. Over time, you'll develop a set of go-to roles that work well for your common tasks.

---

## Lesson 8: Zero-Shot Prompting

### Objectives
- Understand what zero-shot prompting is and when to use it
- Identify tasks suitable for zero-shot approaches
- Recognize limitations of zero-shot prompting
- Master effective zero-shot prompt construction

### Explanation

#### What is Zero-Shot Prompting?

Zero-shot prompting means instructing the model to perform a task **without providing any examples**. You rely entirely on the model's training knowledge and the clarity of your instructions.

**Structure:**
```markdown
[Instruction/Task] → [Direct Request]
```

**Example:**
```markdown
Convert this class component to a functional component with hooks:

[Component code...]
```

No examples provided—the model uses its training to understand what's needed.

#### When to Use Zero-Shot Prompting

✅ **Good for:**
- Simple, well-defined tasks
- Common patterns the model knows well
- Low-stakes requests
- Quick iterations
- Standard transformations (refactoring, converting, formatting)

❌ **Not ideal for:**
- Project-specific patterns
- Complex, multi-step requirements
- Tasks requiring specific style matching
- When consistency across multiple outputs is critical

#### Characteristics of Effective Zero-Shot Prompts

1. **Clear, specific instructions**
2. **Well-defined task scope**
3. **Explicit output format**
4. **Appropriate task complexity**

### Step-by-Step Tutorial

**Creating Effective Zero-Shot Prompts**

**Step 1: State the Task Clearly**

Be explicit about what you want:

```markdown
❌ Vague: "Fix this component"
✅ Clear: "Convert this React class component to a functional component using hooks"
```

**Step 2: Provide Necessary Context**

```markdown
Convert this React class component to a functional component using hooks.

The component uses these lifecycle methods:
- componentDidMount for data fetching
- componentDidUpdate for prop changes
- componentWillUnmount for cleanup

[Component code...]
```

**Step 3: Specify Output Format**

```markdown
Convert this class component to a functional component.

Output:
- Functional component with TypeScript types
- Use useEffect for lifecycle logic
- Maintain the same prop interface
- Include comments explaining useEffect dependencies
```

**Step 4: Set Constraints (If Any)**

```markdown
Convert this class component to a functional component.

Constraints:
- Keep the same function names for methods (they're used in tests)
- Don't change the prop interface
- Maintain error handling logic exactly as-is
```

### Examples & Exercises

**Example 1: Code Transformation**

```markdown
Refactor this code to use optional chaining and nullish coalescing:

const userName = user && user.profile && user.profile.name ? user.profile.name : 'Guest';
const userAge = user && user.profile && user.profile.age !== undefined && user.profile.age !== null ? user.profile.age : 0;
```

**Expected Output:**
```javascript
const userName = user?.profile?.name ?? 'Guest';
const userAge = user?.profile?.age ?? 0;
```

**Why zero-shot works here:** Simple, well-known JavaScript patterns.

**Example 2: Documentation Generation**

```markdown
Generate JSDoc comments for this function:

function fetchUserData(userId, options = {}) {
  const { includeProfile = false, includeOrders = false } = options;
  
  return api.get(`/users/${userId}`, {
    params: { includeProfile, includeOrders }
  });
}
```

**Expected Output:**
```javascript
/**
 * Fetches user data from the API
 * @param {string|number} userId - The unique identifier for the user
 * @param {Object} options - Optional configuration object
 * @param {boolean} [options.includeProfile=false] - Whether to include user profile data
 * @param {boolean} [options.includeOrders=false] - Whether to include user order history
 * @returns {Promise} Promise that resolves with user data
 */
function fetchUserData(userId, options = {}) {
  const { includeProfile = false, includeOrders = false } = options;
  
  return api.get(`/users/${userId}`, {
    params: { includeProfile, includeOrders }
  });
}
```

**Why zero-shot works here:** Standard documentation format, clear function structure.

**Example 3: Quick Utility Function**

```markdown
Create a utility function that debounces another function.

Requirements:
- Accept a function and delay in milliseconds
- Return a debounced version of the function
- Cancel pending execution on unmount
```

**Why zero-shot works here:** Common pattern, clear requirements, standard implementation.

**Exercise 1: Identify Zero-Shot Suitability**

For each task, decide if zero-shot is appropriate or if you need examples (few-shot):

**Task A**: Convert inline styles to CSS modules
**Task B**: Write tests following your team's specific test structure and mocking patterns
**Task C**: Extract a reusable hook from a component
**Task D**: Create a component matching your company's exact design system API
**Task E**: Add error handling to an async function

**Solutions:**

| Task | Zero-Shot? | Reason |
|------|------------|--------|
| A | ✅ Yes | Standard transformation, model knows CSS modules |
| B | ❌ No | Project-specific patterns require examples |
| C | ✅ Yes | Common refactoring pattern |
| D | ❌ No | Specific API design requires examples |
| E | ✅ Yes | Standard error handling patterns |

**Validation:**
- **Self-Check:** Does the task require matching specific patterns unique to your project?
- **Self-Check:** Is the task ambiguous without examples?

**Exercise 2: Write Zero-Shot Prompts**

Write effective zero-shot prompts for these tasks:

**Task 1**: Convert PropTypes to TypeScript interface
**Task 2**: Add loading and error states to an async component

**Solution 1:**
```markdown
Convert these React PropTypes to a TypeScript interface:

Component.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number,
  onUpdate: PropTypes.func.isRequired,
  items: PropTypes.arrayOf(PropTypes.shape({
    id: PropTypes.string.isRequired,
    label: PropTypes.string.isRequired
  }))
};

Output:
- Create a Props interface
- Use proper TypeScript types
- Maintain required/optional correctly
```

**Solution 2:**
```markdown
Add loading and error states to this component that fetches user data:

Current behavior:
- Fetches user data on mount
- Displays user info when loaded

Required additions:
- Show loading spinner while fetching
- Display error message if fetch fails
- Allow retry on error
- Use clean, user-friendly error messages

[Component code...]
```

**Validation:**
- **Self-Check:** Are instructions clear and specific?
- **Self-Check:** Is output format specified?
- **Self-Check:** Are constraints mentioned?

### Frontend Contextualization

**Real-World Scenario: Rapid Development Tasks**

During a sprint, you encounter various quick tasks. Zero-shot prompting helps you move fast.

**Scenario 1: Code Formatting**

```markdown
Format this messy code according to standard JavaScript style:

function getUserData(id){return fetch('/api/users/'+id).then(r=>r.json()).then(data=>{return data}).catch(e=>{console.error(e);throw e;})}
```

**Zero-shot works:** Standard formatting, no project-specific style.

---

**Scenario 2: Type Definition**

```markdown
Create TypeScript types for this API response:

{
  "user": {
    "id": "123",
    "name": "John Doe",
    "email": "john@example.com",
    "profile": {
      "avatar": "https://...",
      "bio": "Developer",
      "social": {
        "twitter": "@john",
        "github": "johndoe"
      }
    }
  },
  "meta": {
    "timestamp": 1234567890,
    "version": "1.0"
  }
}

Create a type hierarchy with nested types for profile and social.
```

**Zero-shot works:** Clear structure, standard typing patterns.

---

**Scenario 3: Hook Extraction**

```markdown
Extract the data fetching logic from this component into a custom hook:

[Component code...]

Create a useUserData hook that:
- Accepts userId parameter
- Returns { data, loading, error, refetch }
- Handles cleanup properly
```

**Zero-shot works:** Common refactoring pattern, clear requirements.

---

**Scenario 4: Error Enhancement**

```markdown
Improve error handling in this function:

async function saveUserProfile(userId, profileData) {
  const response = await fetch(`/api/users/${userId}`, {
    method: 'PUT',
    body: JSON.stringify(profileData)
  });
  return response.json();
}

Add:
- Error checking for non-ok responses
- Network error handling
- Validation error handling (400 status)
- Descriptive error messages
```

**Zero-shot works:** Standard error handling patterns.

**When Zero-Shot Wouldn't Work:**

```markdown
❌ "Create a form component matching our design system"
Needs examples of design system patterns

❌ "Write tests using our test helpers and mocking approach"
Needs examples of project-specific test structure

❌ "Implement state management following our Redux patterns"
Needs examples of project conventions
```

**Practical Takeaway**: Zero-shot is your go-to for standard development tasks—transformations, refactoring, adding common patterns. It's fast and efficient. But when tasks require project-specific knowledge or consistency with existing patterns, you'll need to provide examples (few-shot, covered in the next lesson). Think of zero-shot as your quick-task tool; use it liberally for standard operations.

---

## Lesson 9: Few-Shot Prompting with Examples

### Objectives
- Understand few-shot prompting and its advantages over zero-shot
- Learn to select and provide effective examples
- Master the art of teaching AI through demonstration
- Apply few-shot techniques to enforce consistency

### Explanation

#### What is Few-Shot Prompting?

Few-shot prompting (also called multi-shot or n-shot) involves providing **examples** alongside your instructions to teach the model the exact pattern you want.

**Structure:**
```markdown
[Instruction] + [Example 1] + [Example 2] + [Example 3] + [Your Task]
```

You're teaching by demonstration rather than just instruction.

#### Why Use Examples?

**Advantages:**
- ✅ Improves accuracy and reduces misinterpretation
- ✅ Enforces consistency with existing patterns
- ✅ Handles complex, ambiguous tasks better
- ✅ Teaches project-specific conventions
- ✅ Reduces need for iterative corrections

**When to Use:**
- Project-specific patterns and conventions
- Maintaining stylistic consistency
- Complex tasks that are hard to describe in words
- When zero-shot produces inconsistent results
- Teaching the model your team's standards

#### Characteristics of Good Examples

1. **Relevant**: Directly related to your use case
2. **Diverse**: Cover different scenarios and edge cases (3-5 examples ideal)
3. **Clear**: Well-structured and easy to understand
4. **Representative**: Show the patterns you want replicated
5. **Complete**: Include all important aspects

### Step-by-Step Tutorial

**Creating Effective Few-Shot Prompts**

**Step 1: State Your Task**

```markdown
Create a user profile card component following our component patterns.
```

**Step 2: Provide Relevant Examples**

Show 2-3 examples of similar components:

```markdown
Example 1 - Button Component:
[Show your Button component code]

Example 2 - Card Component:
[Show your Card component code]

Example 3 - Badge Component:
[Show your Badge component code]

Notice the patterns:
- Props interface defined separately
- Variants handled via lookup object
- Base classes combined with variant classes
- TypeScript with strict typing
```

**Step 3: Explicitly Mark as Examples**

```markdown
# Examples

Here are examples of our component style:

## Example 1: Button Component
[Code...]

## Example 2: Card Component
[Code...]

Now create a ProfileCard component following these patterns.
```

**Step 4: Provide Your Actual Task**

```markdown
Based on the examples above, create a ProfileCard component with:
- Props: user (with name, avatar, role, status)
- Variants: compact, default, detailed
- Follow the same prop structure and typing patterns
- Use the same className combination approach
```

**Step 5: Include Counter-Examples (Optional)**

Show what NOT to do:

```markdown
❌ Don't do this:
function Button({ type }) {
  if (type === 'primary') return <button className="btn-primary">...</button>
  if (type === 'secondary') return <button className="btn-secondary">...</button>
  // Bad: Multiple returns, duplicated markup
}

✅ Do this:
function Button({ variant = 'primary' }) {
  const variantClasses = {
    primary: 'btn-primary',
    secondary: 'btn-secondary'
  };
  return <button className={variantClasses[variant]}>...</button>
}
```

### Examples & Exercises

**Example 1: Component Pattern Consistency**

```markdown
# Task
Create a Toast notification component following our established patterns.

# Our Component Patterns

## Example 1: Button Component
\`\`\`tsx
interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'danger';
  size?: 'small' | 'medium' | 'large';
  onClick?: () => void;
  disabled?: boolean;
  children: React.ReactNode;
}

const Button: React.FC<ButtonProps> = ({
  variant = 'primary',
  size = 'medium',
  onClick,
  disabled = false,
  children
}) => {
  const baseClasses = 'btn font-medium rounded focus:outline-none focus:ring-2';
  
  const variantClasses = {
    primary: 'bg-blue-600 hover:bg-blue-700 text-white',
    secondary: 'bg-gray-200 hover:bg-gray-300 text-gray-900',
    danger: 'bg-red-600 hover:bg-red-700 text-white'
  };
  
  const sizeClasses = {
    small: 'px-3 py-1 text-sm',
    medium: 'px-4 py-2',
    large: 'px-6 py-3 text-lg'
  };
  
  const className = `${baseClasses} ${variantClasses[variant]} ${sizeClasses[size]} ${disabled ? 'opacity-50 cursor-not-allowed' : ''}`;
  
  return (
    <button className={className} onClick={onClick} disabled={disabled}>
      {children}
    </button>
  );
};

export default Button;
\`\`\`

## Example 2: Alert Component
\`\`\`tsx
interface AlertProps {
  variant?: 'info' | 'success' | 'warning' | 'error';
  title?: string;
  onClose?: () => void;
  children: React.ReactNode;
}

const Alert: React.FC<AlertProps> = ({
  variant = 'info',
  title,
  onClose,
  children
}) => {
  const baseClasses = 'alert rounded-lg p-4 mb-4';
  
  const variantClasses = {
    info: 'bg-blue-50 text-blue-900 border border-blue-200',
    success: 'bg-green-50 text-green-900 border border-green-200',
    warning: 'bg-yellow-50 text-yellow-900 border border-yellow-200',
    error: 'bg-red-50 text-red-900 border border-red-200'
  };
  
  const className = `${baseClasses} ${variantClasses[variant]}`;
  
  return (
    <div className={className} role="alert">
      {title && <h4 className="font-bold mb-2">{title}</h4>}
      <div>{children}</div>
      {onClose && (
        <button
          onClick={onClose}
          className="absolute top-2 right-2"
          aria-label="Close alert"
        >
          ×
        </button>
      )}
    </div>
  );
};

export default Alert;
\`\`\`

# Your Task
Create a Toast component following the same patterns:
- Variants: info, success, warning, error (same as Alert)
- Auto-dismiss after duration (optional duration prop, default 5000ms)
- Position: top-right corner (fixed positioning)
- Include close button
- Support title and message
- Slide-in animation
- Follow TypeScript typing patterns from examples
- Use same className combination approach
```

**Why few-shot here:** Project-specific component structure, consistent styling approach, TypeScript patterns.

**Example 2: Test Writing Patterns**

```markdown
# Task
Write tests for the UserProfile component using our testing patterns.

# Our Testing Patterns

## Example 1: Button Component Tests
\`\`\`tsx
import { render, screen, fireEvent } from '@testing-library/react';
import Button from './Button';

describe('Button', () => {
  describe('Rendering', () => {
    it('renders with children text', () => {
      render(<Button>Click me</Button>);
      expect(screen.getByRole('button', { name: /click me/i })).toBeInTheDocument();
    });
    
    it('applies variant classes correctly', () => {
      const { rerender } = render(<Button variant="primary">Primary</Button>);
      expect(screen.getByRole('button')).toHaveClass('bg-blue-600');
      
      rerender(<Button variant="danger">Danger</Button>);
      expect(screen.getByRole('button')).toHaveClass('bg-red-600');
    });
  });
  
  describe('Interactions', () => {
    it('calls onClick handler when clicked', () => {
      const handleClick = jest.fn();
      render(<Button onClick={handleClick}>Click</Button>);
      
      fireEvent.click(screen.getByRole('button'));
      expect(handleClick).toHaveBeenCalledTimes(1);
    });
    
    it('does not call onClick when disabled', () => {
      const handleClick = jest.fn();
      render(<Button onClick={handleClick} disabled>Click</Button>);
      
      fireEvent.click(screen.getByRole('button'));
      expect(handleClick).not.toHaveBeenCalled();
    });
  });
  
  describe('Accessibility', () => {
    it('has proper button role', () => {
      render(<Button>Click</Button>);
      expect(screen.getByRole('button')).toBeInTheDocument();
    });
  });
});
\`\`\`

Notice our patterns:
- Tests organized in describe blocks: Rendering, Interactions, Accessibility
- Use accessible queries (getByRole, getByLabelText)
- Clear, descriptive test names
- One assertion per test (mostly)
- Test positive and negative cases

## Example 2: Form Component Tests
\`\`\`tsx
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import LoginForm from './LoginForm';

describe('LoginForm', () => {
  describe('Rendering', () => {
    it('renders email and password inputs', () => {
      render(<LoginForm onSubmit={jest.fn()} />);
      expect(screen.getByLabelText(/email/i)).toBeInTheDocument();
      expect(screen.getByLabelText(/password/i)).toBeInTheDocument();
    });
  });
  
  describe('Validation', () => {
    it('shows error for invalid email', async () => {
      const user = userEvent.setup();
      render(<LoginForm onSubmit={jest.fn()} />);
      
      const emailInput = screen.getByLabelText(/email/i);
      await user.type(emailInput, 'invalid-email');
      await user.tab(); // Blur input to trigger validation
      
      await waitFor(() => {
        expect(screen.getByText(/valid email/i)).toBeInTheDocument();
      });
    });
    
    it('shows error for empty password', async () => {
      const user = userEvent.setup();
      render(<LoginForm onSubmit={jest.fn()} />);
      
      const passwordInput = screen.getByLabelText(/password/i);
      await user.click(passwordInput);
      await user.tab(); // Blur without entering text
      
      await waitFor(() => {
        expect(screen.getByText(/password is required/i)).toBeInTheDocument();
      });
    });
  });
  
  describe('Submission', () => {
    it('calls onSubmit with form data', async () => {
      const user = userEvent.setup();
      const handleSubmit = jest.fn();
      render(<LoginForm onSubmit={handleSubmit} />);
      
      await user.type(screen.getByLabelText(/email/i), 'user@example.com');
      await user.type(screen.getByLabelText(/password/i), 'password123');
      await user.click(screen.getByRole('button', { name: /submit/i }));
      
      await waitFor(() => {
        expect(handleSubmit).toHaveBeenCalledWith({
          email: 'user@example.com',
          password: 'password123'
        });
      });
    });
  });
  
  describe('Accessibility', () => {
    it('associates labels with inputs', () => {
      render(<LoginForm onSubmit={jest.fn()} />);
      const emailInput = screen.getByLabelText(/email/i);
      const passwordInput = screen.getByLabelText(/password/i);
      
      expect(emailInput).toHaveAttribute('id');
      expect(passwordInput).toHaveAttribute('id');
    });
  });
});
\`\`\`

# Your Task
Write tests for the UserProfile component following these patterns:

UserProfile component displays:
- User name, avatar, email, role
- Edit button (calls onEdit prop)
- Delete button (calls onDelete prop, shows confirmation)
- Loading state
- Error state

Write tests covering:
- Rendering with user data
- Interaction with edit button
- Interaction with delete button (including confirmation)
- Loading state
- Error state
- Accessibility (labels, roles)

Follow our testing patterns from the examples.
```

**Why few-shot here:** Project-specific test structure, team conventions for organization, specific query preferences.

**Exercise 1: Create Few-Shot Prompt**

Create a few-shot prompt for writing API hook functions.

You want all hooks to follow this pattern:
- Return `{ data, loading, error, refetch }`
- Handle cleanup
- Support AbortController
- TypeScript types

**Solution:**

```markdown
# Task
Create a useUserOrders hook for fetching user orders following our API hook patterns.

# Our API Hook Patterns

## Example 1: useUser Hook
\`\`\`tsx
interface User {
  id: string;
  name: string;
  email: string;
}

interface UseUserReturn {
  data: User | null;
  loading: boolean;
  error: Error | null;
  refetch: () => void;
}

const useUser = (userId: string): UseUserReturn => {
  const [data, setData] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  const fetchUser = useCallback(async () => {
    const controller = new AbortController();
    
    try {
      setLoading(true);
      setError(null);
      
      const response = await fetch(`/api/users/${userId}`, {
        signal: controller.signal
      });
      
      if (!response.ok) {
        throw new Error(`Failed to fetch user: ${response.statusText}`);
      }
      
      const userData = await response.json();
      setData(userData);
    } catch (err) {
      if (err.name !== 'AbortError') {
        setError(err as Error);
      }
    } finally {
      setLoading(false);
    }
    
    return () => controller.abort();
  }, [userId]);
  
  useEffect(() => {
    const cleanup = fetchUser();
    return cleanup;
  }, [fetchUser]);
  
  return { data, loading, error, refetch: fetchUser };
};
\`\`\`

## Example 2: useProducts Hook
\`\`\`tsx
interface Product {
  id: string;
  name: string;
  price: number;
  category: string;
}

interface UseProductsReturn {
  data: Product[] | null;
  loading: boolean;
  error: Error | null;
  refetch: () => void;
}

const useProducts = (category?: string): UseProductsReturn => {
  const [data, setData] = useState<Product[] | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  const fetchProducts = useCallback(async () => {
    const controller = new AbortController();
    
    try {
      setLoading(true);
      setError(null);
      
      const url = category
        ? `/api/products?category=${encodeURIComponent(category)}`
        : '/api/products';
      
      const response = await fetch(url, {
        signal: controller.signal
      });
      
      if (!response.ok) {
        throw new Error(`Failed to fetch products: ${response.statusText}`);
      }
      
      const products = await response.json();
      setData(products);
    } catch (err) {
      if (err.name !== 'AbortError') {
        setError(err as Error);
      }
    } finally {
      setLoading(false);
    }
    
    return () => controller.abort();
  }, [category]);
  
  useEffect(() => {
    const cleanup = fetchProducts();
    return cleanup;
  }, [fetchProducts]);
  
  return { data, loading, error, refetch: fetchProducts };
};
\`\`\`

# Your Task
Create a useUserOrders hook following these patterns:
- Fetch from /api/users/{userId}/orders
- Accept optional status filter parameter ('pending' | 'completed' | 'cancelled')
- Return type: Order[] where Order has { id, userId, items, total, status, createdAt }
- Follow the same error handling, cleanup, and typing patterns
```

**Validation:**
- **Self-Check:** Do examples clearly demonstrate the pattern?
- **Self-Check:** Are examples similar enough to the task but show variety?
- **Self-Check:** Is the task description clear about what to create?

### Frontend Contextualization

**Real-World Scenario: Design System Consistency**

Your team has a design system and you need new components to match existing patterns exactly.

**Scenario: Creating a Design System Component**

```markdown
# Task
Create a Select (dropdown) component for our design system.

# Existing Design System Components

## Example 1: Input Component
\`\`\`tsx
// Our Input component pattern
interface InputProps {
  label: string;
  name: string;
  type?: 'text' | 'email' | 'password';
  placeholder?: string;
  error?: string;
  helpText?: string;
  required?: boolean;
  disabled?: boolean;
  value: string;
  onChange: (value: string) => void;
}

export const Input: React.FC<InputProps> = ({
  label,
  name,
  type = 'text',
  placeholder,
  error,
  helpText,
  required = false,
  disabled = false,
  value,
  onChange
}) => {
  const inputId = `input-${name}`;
  const errorId = error ? `${inputId}-error` : undefined;
  const helpTextId = helpText ? `${inputId}-help` : undefined;
  
  return (
    <div className="form-field">
      <label htmlFor={inputId} className="form-label">
        {label}
        {required && <span className="required-indicator">*</span>}
      </label>
      
      <input
        id={inputId}
        name={name}
        type={type}
        placeholder={placeholder}
        value={value}
        onChange={(e) => onChange(e.target.value)}
        disabled={disabled}
        required={required}
        aria-invalid={!!error}
        aria-describedby={[errorId, helpTextId].filter(Boolean).join(' ')}
        className={`form-input ${error ? 'form-input--error' : ''}`}
      />
      
      {helpText && (
        <p id={helpTextId} className="form-help-text">{helpText}</p>
      )}
      
      {error && (
        <p id={errorId} className="form-error" role="alert">{error}</p>
      )}
    </div>
  );
};
\`\`\`

## Example 2: Checkbox Component
\`\`\`tsx
interface CheckboxProps {
  label: string;
  name: string;
  helpText?: string;
  error?: string;
  required?: boolean;
  disabled?: boolean;
  checked: boolean;
  onChange: (checked: boolean) => void;
}

export const Checkbox: React.FC<CheckboxProps> = ({
  label,
  name,
  helpText,
  error,
  required = false,
  disabled = false,
  checked,
  onChange
}) => {
  const checkboxId = `checkbox-${name}`;
  const errorId = error ? `${checkboxId}-error` : undefined;
  const helpTextId = helpText ? `${checkboxId}-help` : undefined;
  
  return (
    <div className="form-field">
      <div className="checkbox-wrapper">
        <input
          id={checkboxId}
          name={name}
          type="checkbox"
          checked={checked}
          onChange={(e) => onChange(e.target.checked)}
          disabled={disabled}
          required={required}
          aria-invalid={!!error}
          aria-describedby={[errorId, helpTextId].filter(Boolean).join(' ')}
          className="form-checkbox"
        />
        
        <label htmlFor={checkboxId} className="form-label">
          {label}
          {required && <span className="required-indicator">*</span>}
        </label>
      </div>
      
      {helpText && (
        <p id={helpTextId} className="form-help-text">{helpText}</p>
      )}
      
      {error && (
        <p id={errorId} className="form-error" role="alert">{error}</p>
      )}
    </div>
  );
};
\`\`\`

Notice our consistent patterns:
- Props interface with label, name, error, helpText, required, disabled
- ID generation using template: `{component}-${name}`
- Accessibility: aria-invalid, aria-describedby, role="alert" for errors
- Controlled components with onChange callback
- Consistent className structure: form-field, form-label, form-error, etc.
- Required indicator as separate span
- Help text and error text patterns

# Your Task
Create a Select component following these exact patterns:
- Props: label, name, options (Array<{value: string, label: string}>), placeholder, error, helpText, required, disabled, value, onChange
- Follow the same ID generation pattern
- Match accessibility attributes
- Use same className structure (form-select)
- Support placeholder as first disabled option
- Include keyboard navigation (arrow keys)
```

**Why This Works:**

1. **Examples show patterns** that are hard to describe in words
2. **Consistency** is enforced through demonstration
3. **Accessibility patterns** are preserved
4. **Naming conventions** are taught implicitly
5. **TypeScript patterns** are consistent

**Without few-shot:** AI would create a functional select, but wouldn't match your design system's specific patterns, accessibility approach, or naming conventions.

**Practical Takeaway**: Few-shot prompting is your consistency enforcer. Whenever you need AI output to match existing patterns—whether code style, component APIs, test structure, or any project convention—provide 2-3 clear examples. Think of it as showing the AI your team's playbook. The examples teach patterns that are difficult or tedious to describe in words, ensuring new code feels native to your codebase.

---

**Next:** Part 2b - [Intermediate Lessons (Continued)](02b-intermediate-lessons-continued.md)