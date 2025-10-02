# Part 4: Expert Techniques & Workflows

## Lesson 18: System Prompts & IDE Configuration

### Objectives
- Understand system prompts and their role in consistent AI behavior
- Learn to configure IDE-specific AI settings (Cursor focus)
- Master project-specific prompt configuration
- Create reusable system prompts for your workflow

### Explanation

#### What Are System Prompts?

**System prompts** are instructions that define the AI's role, behavior, and constraints throughout an entire conversation session. They're like global configuration that affects every interaction.

**Think of it as:**
- Your `.eslintrc` for code style
- Your team's coding standards document
- Your component library's design principles

**Key Differences:**

| Type | Scope | When Set | Changes |
|------|-------|----------|---------|
| **User Prompt** | Single message | Each interaction | Every message |
| **System Prompt** | Entire session | Session start | Rarely |
| **Project Rules** | Project-wide | IDE configuration | Per project |

#### Why Use System Prompts?

✅ **Benefits:**
- **Consistency**: Same behavior across all interactions
- **Efficiency**: Don't repeat context in every prompt
- **Team alignment**: Shared standards across developers
- **Quality**: Enforce coding standards, accessibility, etc.
- **Project context**: IDE knows your stack, conventions, patterns

**Use Cases:**
- Define coding style preferences
- Set accessibility requirements
- Specify preferred libraries/frameworks
- Enforce security best practices
- Maintain architectural principles

### Step-by-Step Tutorial

**Creating Effective System Prompts**

**Step 1: Define Your Development Context**

```markdown
# What describes your work?
- Primary tech stack (React, TypeScript, etc.)
- Coding standards (ESLint config, style guide)
- Accessibility requirements (WCAG level)
- Preferred patterns (hooks over classes, composition over inheritance)
- Testing approach (Jest, RTL, Playwright)
```

**Step 2: Identify Recurring Instructions**

What do you tell the AI repeatedly?
- "Use TypeScript with strict typing"
- "Follow our component patterns"
- "Ensure WCAG 2.1 AA compliance"
- "Write testable code"

**Step 3: Create Your System Prompt**

```markdown
# Example: Senior Frontend Developer System Prompt

You are a senior frontend developer with expertise in React, TypeScript, and modern web development.

## Technical Stack
- React 18 with functional components and hooks
- TypeScript with strict mode enabled
- styled-components for styling
- React Testing Library for tests
- Playwright for e2e tests

## Coding Standards
- Use functional components with hooks (no class components)
- Strict TypeScript typing (no `any` types)
- Prefer composition over inheritance
- Write self-documenting code with clear variable names
- Add JSDoc comments for complex functions
- Follow component file structure: types → component → styles → export

## Quality Requirements
- Always consider accessibility (WCAG 2.1 AA compliance)
- Include ARIA attributes where needed
- Ensure keyboard navigation works
- Consider mobile-first responsive design
- Implement proper error boundaries and loading states

## Code Review Focus
When reviewing or generating code:
- Identify potential performance bottlenecks
- Point out accessibility issues
- Suggest maintainability improvements
- Recommend testing strategies
- Consider edge cases and error handling

## Communication Style
- Explain the "why" behind recommendations, not just the "what"
- Provide code examples for complex concepts
- Be concise but thorough
- Ask clarifying questions when requirements are unclear
```

**Step 4: Configure in Your IDE**

### Cursor IDE Configuration

**Option 1: Project Rules File**

Create `.cursor/rules` in your project root:

```markdown
# Project: E-Commerce Platform

## Tech Stack
React 18, TypeScript, Next.js 14, Tailwind CSS, React Query, Zustand

## Code Style
- Functional components with TypeScript
- Use const for components: `const Button: React.FC<ButtonProps> = () => {}`
- Props destructuring in parameters
- Early returns for conditional rendering

## File Organization
- Components: src/components/[ComponentName]/
  - index.tsx (component)
  - [ComponentName].test.tsx (tests)
  - [ComponentName].stories.tsx (Storybook)
  - types.ts (if complex types)

## Naming Conventions
- Components: PascalCase (UserProfile, ProductCard)
- Files: PascalCase for components, camelCase for utilities
- Props interfaces: [ComponentName]Props
- Hooks: use[HookName] (useAuth, useProducts)

## Best Practices
- Use React Query for server state
- Use Zustand for client state
- Lazy load routes and heavy components
- Use Next.js Image component for images
- Implement proper error boundaries

## Accessibility
- All interactive elements keyboard accessible
- Proper semantic HTML
- ARIA labels for icon buttons
- Focus indicators visible
- Color contrast meets WCAG AA

## Testing
- Unit tests for logic and hooks
- Component tests for user interactions
- E2e tests for critical flows
- Aim for 80%+ coverage
```

**Option 2: Custom Instructions (per conversation)**

In Cursor settings, set default instructions for new chats:

```markdown
I'm working on a React TypeScript project. Follow our team's conventions:
- TypeScript strict mode
- Functional components only
- Accessibility (WCAG AA)
- Comprehensive error handling
- Follow existing patterns in the codebase
```

**Option 3: Slash Commands (reusable prompts)**

Create `.cursor/commands/[command-name].md`:

**File: `.cursor/commands/create-component.md`**
```markdown
Create a new React component following our design system patterns.

Component structure:
1. TypeScript functional component
2. Props interface with JSDoc
3. styled-components for styling
4. Proper accessibility (ARIA, keyboard nav)
5. Loading and error states if applicable
6. Unit tests using React Testing Library

Example structure:
```tsx
interface [ComponentName]Props {
  /** Description */
  prop: type;
}

const [ComponentName]: React.FC<[ComponentName]Props> = ({ prop }) => {
  // Implementation
};

export default [ComponentName];
```

Ask user for:
- Component name
- Required props
- Variants (if applicable)
- Special requirements
```

### Examples & Exercises

**Example 1: Team-Specific System Prompt**

**For an Enterprise Component Library Team:**

```markdown
# System Prompt: Component Library Developer

You are a senior component library developer building enterprise-grade React components.

## Primary Focus
- Developer experience (DX)
- API consistency across components
- Type safety
- Performance at scale
- Accessibility by default

## Component Standards
- Compound component pattern where appropriate (Card.Header, Card.Body, Card.Footer)
- Polymorphic components with 'as' prop support
- Full TypeScript generics for type inference
- Forward refs for all components
- Comprehensive prop documentation with JSDoc

## API Design Principles
- Consistent prop naming across components
  - `variant` for style variations
  - `size` for sizing options  
  - `disabled` for disabled state
  - `loading` for loading state
  - `error` for error display
- Controlled and uncontrolled modes supported
- Sensible defaults for all optional props
- Escape hatches for advanced customization

## Testing Requirements
- Unit tests for all component logic
- Visual regression tests (Storybook + Chromatic)
- Accessibility tests (jest-axe)
- Browser compatibility tests
- Performance benchmarks for complex components

## Documentation Standards
- Storybook story for each variant
- Props table auto-generated from TypeScript
- Usage examples (basic and advanced)
- Accessibility notes
- Migration guides for breaking changes

## Code Review Checklist
When generating or reviewing components:
- [ ] API is intuitive and consistent with existing components
- [ ] TypeScript types are accurate and helpful
- [ ] Component is accessible (keyboard, screen reader)
- [ ] Performance is acceptable (no unnecessary renders)
- [ ] Tests cover key functionality and edge cases
- [ ] Documentation is complete
- [ ] Storybook stories demonstrate all variants
```

**Example 2: Security-Focused System Prompt**

**For a Fintech Application:**

```markdown
# System Prompt: Fintech Security Engineer

You are a security-conscious full-stack developer working on a financial application.

## Security Requirements (Non-Negotiable)
- Never log sensitive data (tokens, PII, financial data)
- All user inputs must be validated and sanitized
- Use parameterized queries (prevent SQL injection)
- Implement CSRF protection on all mutations
- Enforce HTTPS in production
- Set secure cookie flags (httpOnly, secure, sameSite)
- Implement rate limiting on auth endpoints
- Use constant-time comparisons for credentials

## Data Handling
- Encrypt sensitive data at rest
- Use HTTPS for data in transit
- Minimize data collection (only what's needed)
- Implement data retention policies
- Secure deletion of sensitive data
- Audit logging for financial transactions

## Authentication & Authorization
- Multi-factor authentication required
- Session timeout after inactivity
- Password requirements: min 12 chars, complexity rules
- Account lockout after failed attempts
- Secure password reset flow
- Verify authorization on every request

## Code Review Focus
- Identify potential security vulnerabilities
- Check for OWASP Top 10 issues
- Verify input validation
- Check for information disclosure
- Ensure proper error handling (no stack traces to users)
- Validate authentication and authorization

## Compliance
- SOC 2 compliance requirements
- PCI DSS for payment handling
- GDPR for EU users
- Regular security audits

When uncertain about security implications, recommend:
1. Most secure approach first
2. Trade-offs clearly explained
3. Request security team review for critical paths
```

**Exercise 1: Create Your System Prompt**

**Your Task**: Create a system prompt for your current project/team.

**Template:**

```markdown
# System Prompt: [Your Role/Project]

## Context
[Describe your project, tech stack, team]

## Technical Requirements
[Languages, frameworks, tools you use]

## Coding Standards
[Your team's conventions]

## Quality Requirements
[Accessibility, performance, testing standards]

## Code Review Focus
[What to look for when generating/reviewing code]

## Communication Preferences
[How you want the AI to interact with you]
```

**Solution Example (E-Commerce Storefront):**

```markdown
# System Prompt: E-Commerce Storefront Developer

## Context
Building a high-traffic e-commerce storefront serving 1M+ monthly users.
Focus on conversion optimization, performance, and accessibility.

## Technical Requirements
- Next.js 14 (App Router)
- TypeScript strict mode
- Tailwind CSS + headlessUI
- React Query for data fetching
- Vercel for deployment
- Stripe for payments

## Coding Standards
- Server Components by default, Client Components when needed
- Use Next.js optimized components (Image, Link, Font)
- Implement proper loading states (Suspense)
- Progressive enhancement approach
- Error boundaries at route level

## Quality Requirements
- Core Web Vitals: Green scores required
  - LCP < 2.5s
  - FID < 100ms
  - CLS < 0.1
- Accessibility: WCAG 2.1 AA minimum
- Mobile-first responsive design
- SEO optimized (metadata, structured data)
- Conversion tracking implemented

## Performance Priorities
- Image optimization (WebP, lazy loading, responsive images)
- Code splitting and lazy loading
- Bundle size monitoring (keep < 100KB initial load)
- Caching strategies (SWR, stale-while-revalidate)
- Database query optimization

## E-Commerce Specific
- Product schema.org structured data
- Inventory synchronization
- Cart abandonment handling
- Checkout flow optimization
- Payment security (PCI compliance)

## Code Review Focus
- Performance impact (bundle size, rendering)
- Conversion funnel preservation
- Mobile usability
- SEO implications
- Analytics tracking completeness
```

**Validation:**
- **Self-Check**: Does your system prompt reflect your actual work context?
- **Self-Check**: Would a new team member understand your standards from this?
- **Self-Check**: Is it specific enough to guide AI behavior consistently?

### Frontend Contextualization

**Real-World Scenario: Design System Team**

Your team maintains a component library used by 50+ developers across 10 products.

**System Prompt Configuration:**

**`.cursor/rules` file:**

```markdown
# Design System: Acme UI Component Library

## Mission
Provide consistent, accessible, performant components that enable product teams to build quickly without sacrificing quality.

## Component Development Principles
1. API Consistency: Similar components should have similar APIs
2. Accessibility First: WCAG AA out of the box
3. Type Safety: Leverage TypeScript for great DX
4. Performance: Optimized for production scale
5. Documentation: Self-documenting code + comprehensive Storybook

## Tech Stack
- React 18.2+
- TypeScript 5.0+
- Styled-components 6.0+
- Storybook 7.0+
- Jest + React Testing Library
- Chromatic for visual regression

## File Structure (per component)
src/components/[ComponentName]/
├── index.tsx                 # Component implementation
├── [ComponentName].test.tsx  # Unit tests
├── [ComponentName].stories.tsx # Storybook stories
├── types.ts                  # TypeScript types
├── styles.ts                 # Styled components
└── README.md                 # Usage documentation

## API Design Standards

### Prop Naming (be consistent)
- `variant`: Style variants (e.g., 'primary', 'secondary')
- `size`: Size variants (e.g., 'small', 'medium', 'large')
- `disabled`: Disabled state (boolean)
- `loading`: Loading state (boolean)
- `error`: Error state (boolean or string)
- `children`: Component children
- `className`: Additional CSS classes
- `as`: Polymorphic component type

### TypeScript Patterns
```typescript
// Props interface with JSDoc
interface ComponentNameProps {
  /** Brief description of prop */
  variant?: 'primary' | 'secondary';
  /** Size variant */
  size?: 'small' | 'medium' | 'large';
  /** Click handler */
  onClick?: () => void;
  /** Component children */
  children: React.ReactNode;
}

// Use React.FC for simple components
const ComponentName: React.FC<ComponentNameProps> = ({
  variant = 'primary',
  size = 'medium',
  onClick,
  children
}) => {
  // Implementation
};

// Use forwardRef for components that need ref
const ComponentName = React.forwardRef<HTMLDivElement, ComponentNameProps>(
  ({ variant = 'primary', ...props }, ref) => {
    // Implementation
  }
);
```

## Accessibility Requirements (Non-Negotiable)
- All interactive elements keyboard accessible
- Proper ARIA attributes (roles, labels, states)
- Focus management (visible indicators, logical order)
- Screen reader announcements for dynamic content
- Color contrast ≥ 4.5:1 for normal text, ≥ 3:1 for large text
- Touch targets ≥ 44x44px

## Testing Standards
```typescript
// Test file structure
describe('ComponentName', () => {
  describe('Rendering', () => {
    it('renders with default props', () => {});
    it('renders with all variants', () => {});
  });
  
  describe('Interactions', () => {
    it('handles user interactions', () => {});
  });
  
  describe('Accessibility', () => {
    it('has no accessibility violations', () => {});
    it('supports keyboard navigation', () => {});
  });
});
```

## Storybook Standards
```typescript
// Story file structure
export default {
  title: 'Components/ComponentName',
  component: ComponentName,
  argTypes: {
    variant: {
      control: 'select',
      options: ['primary', 'secondary'],
    },
  },
} as Meta;

// Template
const Template: Story<ComponentNameProps> = (args) => <ComponentName {...args} />;

// Stories
export const Primary = Template.bind({});
Primary.args = { variant: 'primary' };

export const WithLoading = Template.bind({});
WithLoading.args = { loading: true };
```

## Performance Requirements
- Components should not cause unnecessary re-renders
- Use React.memo for components with expensive renders
- Use useCallback/useMemo where appropriate
- Bundle size impact: aim for < 5KB per component (gzipped)

## Documentation Requirements
- README.md with:
  - Component purpose
  - When to use / when not to use
  - Props API table
  - Usage examples
  - Accessibility notes
  - Known issues/limitations

## Code Review Checklist
When generating or reviewing components:
- [ ] API matches existing component patterns
- [ ] TypeScript types are accurate and helpful
- [ ] All variants demonstrated in Storybook
- [ ] Accessibility tested (jest-axe, manual testing)
- [ ] Unit tests cover key functionality
- [ ] Performance is acceptable (no excessive re-renders)
- [ ] Documentation is complete
- [ ] No breaking changes without migration guide

## Common Patterns to Follow

### Error Handling
```typescript
const [error, setError] = useState<Error | null>(null);

if (error) {
  return <ErrorState error={error} onRetry={() => setError(null)} />;
}
```

### Loading States
```typescript
const [loading, setLoading] = useState(false);

return (
  <Button disabled={loading}>
    {loading ? <Spinner /> : 'Submit'}
  </Button>
);
```

### Compound Components
```typescript
const Card = ({ children }) => <div className="card">{children}</div>;
Card.Header = ({ children }) => <div className="card-header">{children}</div>;
Card.Body = ({ children }) => <div className="card-body">{children}</div>;
Card.Footer = ({ children }) => <div className="card-footer">{children}</div>;

// Usage
<Card>
  <Card.Header>Title</Card.Header>
  <Card.Body>Content</Card.Body>
  <Card.Footer>Actions</Card.Footer>
</Card>
```

## When in Doubt
- Prioritize consistency with existing components
- Ask in #design-system Slack channel
- Reference our Figma design specs
- Check similar components for patterns

**Benefits of This Configuration:**
- ✅ Every interaction respects design system standards
- ✅ New components automatically follow patterns
- ✅ Accessibility built-in from the start
- ✅ Consistency across all team members' AI interactions
- ✅ Reduces code review time (standards are enforced upfront)

**Practical Takeaway**: System prompts are your project's DNA for AI interactions. Invest time in creating comprehensive project rules that capture your team's standards, conventions, and requirements. Store them in version control (`.cursor/rules`) so the entire team benefits. Think of it as documentation that actively guides AI behavior rather than passively waiting to be read. Update your system prompts as your standards evolve. Good system prompts reduce repetition in every prompt, ensure consistency, and help onboard AI to your project just like you'd onboard a new developer. The upfront investment pays dividends in every interaction.

---

## Lesson 19: Prompt Templates & Variables

### Objectives
- Understand prompt templates as reusable patterns
- Learn to use variables/placeholders for flexibility
- Master creating template libraries for common tasks
- Apply templates in IDE workflows

### Explanation

#### What Are Prompt Templates?

**Prompt templates** are reusable prompt structures with **placeholders (variables)** that you fill in for specific tasks. They're like function templates or code snippets—write once, reuse many times.

**Structure:**
```markdown
# Template with variables (placeholders)
Create a {{ComponentType}} component called {{ComponentName}} with {{PropsList}}.

# Filled-in instance
Create a Button component called SubmitButton with variant, size, onClick, disabled props.
```

**Think of it as:**
- Code templates in your IDE
- Reusable SQL query patterns
- Email templates with merge fields

#### Why Use Templates?

✅ **Benefits:**
- **Efficiency**: Don't rewrite common prompts
- **Consistency**: Same structure every time
- **Completeness**: Don't forget important elements
- **Team sharing**: Everyone uses best practices
- **Onboarding**: New team members get proven patterns

**Use Cases:**
- Component generation
- Code review workflows
- Refactoring patterns
- Documentation generation
- Test creation

### Step-by-Step Tutorial

**Creating Prompt Templates**

**Step 1: Identify Repetitive Tasks**

What prompts do you write repeatedly?
- Creating components
- Writing tests
- Refactoring patterns
- Code reviews
- API integration

**Step 2: Extract the Pattern**

Take a specific prompt and identify the variables:

**Specific Prompt:**
```markdown
Create a Modal component with the following props:
- isOpen: boolean
- onClose: function
- title: string
- children: ReactNode

The component should:
- Use React Portal
- Trap focus inside
- Close on ESC key
- Backdrop click closes
```

**Extract Pattern:**
```markdown
Create a {{ComponentName}} component with the following props:
{{PropsList}}

The component should:
{{Requirements}}
```

**Step 3: Add Context and Instructions**

```markdown
# Component Generation Template

Create a {{ComponentType}} component called {{ComponentName}}.

## Props
{{PropsList}}

## Requirements
{{RequirementsList}}

## Technical Details
- Use TypeScript with strict typing
- Functional component with hooks
- Include prop interface with JSDoc
- Follow our component patterns (see src/components/Button for reference)

## Output
- Component implementation
- TypeScript types
- Usage example

## Accessibility
- {{AccessibilityRequirements}}
```

**Step 4: Create a Template Library**

Organize templates by category:

```
.cursor/commands/
├── component/
│   ├── create-component.md
│   ├── create-form-component.md
│   └── create-modal-component.md
├── refactoring/
│   ├── extract-hook.md
│   ├── split-component.md
│   └── optimize-performance.md
├── testing/
│   ├── create-component-tests.md
│   ├── create-integration-test.md
│   └── create-e2e-test.md
└── documentation/
    ├── create-component-docs.md
    └── create-api-docs.md
```

### Examples & Exercises

**Example 1: Component Generation Template**

**File: `.cursor/commands/create-component.md`**

```markdown
# Create Component Template

Create a {{ComponentType}} component called {{ComponentName}} for our design system.

## Context
This component will be used across {{UsageContext}} in our application.

## Props Interface
{{PropsList}}

Example:
- variant: 'primary' | 'secondary' | 'danger'
- size: 'small' | 'medium' | 'large'
- onClick?: () => void
- disabled?: boolean
- loading?: boolean
- children: React.ReactNode

## Requirements

### Functionality
{{FunctionalRequirements}}

### Styling
- Use styled-components
- Follow design tokens from src/styles/tokens.ts
- Support theme variants (light/dark)
- Responsive design (mobile-first)

### Accessibility
- WCAG 2.1 AA compliant
- Proper ARIA attributes
- Keyboard navigation
- Focus indicators
- {{AdditionalA11yRequirements}}

### Code Quality
- TypeScript with strict typing
- Props interface with JSDoc documentation
- Meaningful variable names
- Inline comments for complex logic

## Output Structure

1. TypeScript interface with JSDoc:
\`\`\`typescript
interface {{ComponentName}}Props {
  /** Description */
  prop: type;
}
\`\`\`

2. Component implementation:
\`\`\`typescript
const {{ComponentName}}: React.FC<{{ComponentName}}Props> = ({
  // props
}) => {
  // implementation
};
\`\`\`

3. Styled components:
\`\`\`typescript
const Container = styled.div`
  // styles
`;
\`\`\`

4. Usage example:
\`\`\`typescript
<{{ComponentName}} 
  variant="primary"
  size="medium"
  onClick={handleClick}
>
  Click me
</{{ComponentName}}>
\`\`\`

## Validation
- [ ] All props in interface
- [ ] Accessibility attributes present
- [ ] Styled according to design system
- [ ] Usage example works
- [ ] TypeScript compilation passes

---

## How to Use This Template

1. Fill in the variables:
   - ComponentType: (e.g., "form input", "modal", "card")
   - ComponentName: (e.g., "TextField", "Modal", "ProductCard")
   - UsageContext: (e.g., "forms", "dashboards", "product pages")
   - PropsList: (list all required and optional props)
   - FunctionalRequirements: (specific features)
   - AdditionalA11yRequirements: (any special a11y needs)

2. Run the filled template with Cursor's command palette

3. Review generated component

4. Make adjustments as needed
```

**Example Usage:**

```markdown
# Filled Template Instance

Create a Button component called PrimaryButton for our design system.

## Context
This component will be used across all forms and actions in our application.

## Props Interface
- variant: 'primary' | 'secondary' | 'danger' | 'ghost'
- size: 'small' | 'medium' | 'large'
- onClick: () => void
- disabled?: boolean
- loading?: boolean
- icon?: React.ReactNode
- children: React.ReactNode

## Requirements

### Functionality
- Click handler with ripple effect
- Loading state shows spinner
- Disabled state prevents clicks
- Icon can be positioned left or right

[Rest of template filled in...]
```

**Example 2: Refactoring Template**

**File: `.cursor/commands/extract-custom-hook.md`**

```markdown
# Extract Custom Hook Template

Extract {{HookFunctionality}} into a custom hook called {{HookName}}.

## Current Implementation
The logic is currently in {{CurrentLocation}}.

[Paste relevant code here]

## Extraction Goals
{{ExtractionGoals}}

## Hook API Design

### Parameters
{{HookParameters}}

Example:
- userId: string
- options?: { includeProfile: boolean }

### Return Value
{{ReturnValue}}

Example:
\`\`\`typescript
{
  data: User | null;
  loading: boolean;
  error: Error | null;
  refetch: () => void;
}
\`\`\`

## Requirements

### Functionality
- Encapsulate {{Functionality}}
- Handle {{EdgeCases}}
- Cleanup on unmount

### Code Quality
- TypeScript with full typing
- JSDoc documentation
- Meaningful variable names
- Proper dependency arrays

### Testing
- Create test file: {{HookName}}.test.ts
- Test {{TestScenarios}}

## Process

1. **Analysis Phase**
   - Identify state variables to extract
   - Identify side effects to extract
   - Identify functions to extract
   - Note dependencies

2. **Design Phase**
   - Design hook parameters
   - Design return value
   - Plan cleanup logic
   - Consider edge cases

3. **Implementation Phase**
   - Create hook file: hooks/{{HookName}}.ts
   - Implement hook
   - Add TypeScript types
   - Add JSDoc documentation

4. **Integration Phase**
   - Update {{CurrentLocation}} to use hook
   - Remove extracted code
   - Test integration

5. **Testing Phase**
   - Create test file
   - Test all scenarios
   - Test cleanup

## Validation
- [ ] Hook encapsulates all relevant logic
- [ ] Original component uses hook successfully
- [ ] TypeScript types are comprehensive
- [ ] Tests pass
- [ ] No memory leaks

---

## How to Use

1. Fill in variables:
   - HookFunctionality: "data fetching", "form validation", "authentication"
   - HookName: "useUserData", "useFormValidation", "useAuth"
   - CurrentLocation: Component/file name
   - ExtractionGoals: What you want to achieve
   - HookParameters: Input parameters
   - ReturnValue: What the hook returns
   - Functionality, EdgeCases, TestScenarios

2. Paste current code in "Current Implementation"

3. Run the template

4. Review and adjust extracted hook
```

**Example 3: Test Generation Template**

**File: `.cursor/commands/create-component-tests.md`**

```markdown
# Component Test Generation Template

Create comprehensive tests for the {{ComponentName}} component.

## Component Location
{{ComponentPath}}

## Test Coverage Requirements

### Rendering Tests
Test that component renders correctly with:
- Default props
- All prop variants
- Edge cases: {{RenderingEdgeCases}}

### Interaction Tests
Test user interactions:
{{InteractionScenarios}}

Example:
- Click events
- Keyboard navigation
- Form submission
- Drag and drop

### Accessibility Tests
- No a11y violations (jest-axe)
- Keyboard navigation
- Screen reader compatibility
- Focus management

### Edge Cases
{{EdgeCaseScenarios}}

Example:
- Empty states
- Error states
- Loading states
- Boundary conditions

## Test Structure

\`\`\`typescript
import { render, screen, fireEvent } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { axe, toHaveNoViolations } from 'jest-axe';
import {{ComponentName}} from './{{ComponentName}}';

expect.extend(toHaveNoViolations);

describe('{{ComponentName}}', () => {
  describe('Rendering', () => {
    it('renders with default props', () => {
      // Test
    });
    
    it('renders with all variants', () => {
      // Test each variant
    });
  });
  
  describe('Interactions', () => {
    it('handles user interactions correctly', () => {
      // Test interactions
    });
  });
  
  describe('Accessibility', () => {
    it('has no accessibility violations', async () => {
      const { container } = render(<{{ComponentName}} />);
      const results = await axe(container);
      expect(results).toHaveNoViolations();
    });
    
    it('supports keyboard navigation', () => {
      // Test keyboard
    });
  });
  
  describe('Edge Cases', () => {
    it('handles edge cases', () => {
      // Test edge cases
    });
  });
});
\`\`\`

## Testing Best Practices
- Test behavior, not implementation
- Use accessible queries (getByRole, getByLabelText)
- Use userEvent over fireEvent for interactions
- Mock external dependencies
- Isolate tests (no shared state)

## Validation
- [ ] All rendering scenarios covered
- [ ] All interactions tested
- [ ] Accessibility verified
- [ ] Edge cases handled
- [ ] Tests pass
- [ ] Coverage ≥ 80%

---

## How to Use

1. Fill variables:
   - ComponentName
   - ComponentPath
   - RenderingEdgeCases
   - InteractionScenarios
   - EdgeCaseScenarios

2. Run template

3. Review generated tests

4. Add any missing test cases

5. Run tests and verify coverage
```

**Exercise 1: Create Your Template Library**

**Your Task**: Create 3 prompt templates for your most common development tasks.

**Solution Structure:**

```markdown
# Template 1: [Task Name]

## Purpose
[What this template generates]

## Variables
- {{Variable1}}: [Description]
- {{Variable2}}: [Description]

## Template Content
[Full template with placeholders]

## Usage Instructions
1. [How to fill it in]
2. [Expected output]
3. [Validation steps]

---

# Template 2: [Next Task]
...

# Template 3: [Another Task]
...
```

**Example Solution:**

```markdown
# Template 1: API Integration

## Purpose
Generate a custom hook for API endpoint integration with React Query.

## Variables
- {{EndpointName}}: Name of the API endpoint (e.g., "users", "products")
- {{HTTPMethod}}: GET, POST, PUT, DELETE
- {{RequestParams}}: Parameters for the request
- {{ResponseType}}: TypeScript type for response
- {{ErrorHandling}}: Specific error scenarios

## Template Content
[Complete template as shown in examples above...]

---

# Template 2: Form Component with Validation

## Purpose
Create a form component with React Hook Form and Zod validation.

## Variables
- {{FormName}}: Form component name
- {{Fields}}: List of form fields
- {{ValidationRules}}: Zod validation schema
- {{SubmitAction}}: What happens on submission

[Template content...]

---

# Template 3: Performance Optimization

## Purpose
Optimize a React component for performance.

## Variables
- {{ComponentName}}: Component to optimize
- {{PerformanceIssue}}: Specific issue (re-renders, slow computation, etc.)
- {{CurrentMetrics}}: Baseline performance metrics

[Template content...]
```

### Frontend Contextualization

**Real-World Scenario: Scaling Development with Templates**

Your team of 10 developers builds features rapidly. Templates ensure consistency and speed.

**Template Library Setup:**

```
.cursor/commands/
├── README.md                     # Template usage guide
├── component/
│   ├── button.md                 # Button-specific template
│   ├── form-input.md             # Form input template
│   ├── modal.md                  # Modal template
│   └── data-display.md           # Tables, lists, cards
├── feature/
│   ├── crud-feature.md           # Complete CRUD feature
│   ├── search-feature.md         # Search with filters
│   └── auth-flow.md              # Authentication flow
├── optimization/
│   ├── bundle-size.md            # Bundle size analysis
│   ├── render-performance.md     # React rendering optimization
│   └── api-caching.md            # API caching strategy
└── quality/
    ├── accessibility-audit.md    # A11y review template
    ├── security-review.md        # Security checklist
    └── code-review.md            # Code review template
```

**Sample: Complete CRUD Feature Template**

**File: `.cursor/commands/feature/crud-feature.md`**

```markdown
# CRUD Feature Template

Generate a complete CRUD feature for {{EntityName}}.

## Entity Definition
{{EntityName}}: {{EntityDescription}}

## Data Model
\`\`\`typescript
interface {{EntityName}} {
  {{Fields}}
}
\`\`\`

Example:
\`\`\`typescript
interface Product {
  id: string;
  name: string;
  description: string;
  price: number;
  category: string;
  inStock: boolean;
  createdAt: Date;
  updatedAt: Date;
}
\`\`\`

## API Endpoints
- GET /api/{{entityPlural}} - List all
- GET /api/{{entityPlural}}/:id - Get one
- POST /api/{{entityPlural}} - Create
- PUT /api/{{entityPlural}}/:id - Update
- DELETE /api/{{entityPlural}}/:id - Delete

## Components to Generate

### 1. List View
File: `components/{{EntityName}}List.tsx`
- Display {{entityPlural}} in table/grid
- Search and filter
- Pagination
- Sort by columns
- Delete confirmation
- Link to edit

### 2. Detail View
File: `components/{{EntityName}}Detail.tsx`
- Display single {{entityName}}
- Edit button
- Delete button with confirmation

### 3. Form Component
File: `components/{{EntityName}}Form.tsx`
- Create and update modes
- Form validation (React Hook Form + Zod)
- Loading states
- Error handling
- Success feedback

### 4. API Hooks
File: `hooks/use{{EntityName}}.ts`
- useGet{{EntityName}}s() - List
- useGet{{EntityName}}(id) - Single
- useCreate{{EntityName}}() - Create
- useUpdate{{EntityName}}() - Update
- useDelete{{EntityName}}() - Delete

Using React Query for all hooks.

## Validation Rules
{{ValidationRules}}

Example:
- name: required, min 3 chars, max 100 chars
- price: required, positive number
- category: required, one of predefined list

## Business Logic
{{BusinessRules}}

Example:
- Cannot delete if inStock = true
- Price changes require approval
- Category change triggers recategorization workflow

## Testing Requirements

### Unit Tests
- Form validation
- API hooks
- Business logic functions

### Integration Tests
- Complete CRUD flow
- Search and filter
- Pagination

### E2E Tests
- Create → Edit → Delete flow
- Validation error handling
- Success feedback

## Generated File Structure
\`\`\`
src/
├── components/
│   ├── {{EntityName}}List.tsx
│   ├── {{EntityName}}Detail.tsx
│   └── {{EntityName}}Form.tsx
├── hooks/
│   └── use{{EntityName}}.ts
├── types/
│   └── {{entityName}}.ts
├── validation/
│   └── {{entityName}}Schema.ts
└── __tests__/
    ├── {{EntityName}}List.test.tsx
    ├── {{EntityName}}Form.test.tsx
    └── use{{EntityName}}.test.ts
\`\`\`

## Step-by-Step Generation

Generate in this order:
1. TypeScript types and interfaces
2. Zod validation schema
3. API hooks with React Query
4. Form component
5. List component
6. Detail component
7. Tests for each component
8. Integration in routes

After each step, confirm before proceeding.

## Success Criteria
- [ ] All CRUD operations work
- [ ] Validation enforced
- [ ] Loading states displayed
- [ ] Errors handled gracefully
- [ ] Tests pass with ≥80% coverage
- [ ] Accessible (keyboard nav, screen readers)
- [ ] Responsive design
```

**Benefits:**
- ✅ New developer can generate complete feature in 30 minutes
- ✅ Ensures consistent patterns across all CRUD features
- ✅ Nothing forgotten (validation, tests, accessibility)
- ✅ Team scales efficiently
- ✅ Onboarding simplified

**Practical Takeaway**: Prompt templates are your development accelerators. Build a template library for your team's common patterns—component creation, testing, refactoring, feature generation. Store templates in version control so everyone benefits. Think of templates as your team's "expert knowledge" encoded—the best way to do common tasks, captured once, reused forever. Start with templates for tasks you do weekly, then expand. Good templates don't just save time; they enforce best practices, ensure consistency, and make AI collaboration more powerful. They're especially valuable for onboarding (new devs use proven patterns immediately) and scaling (team maintains consistency as it grows).

---

**Next**: [Part 4b - Expert Techniques & Workflows (Continued)](04b-expert-techniques-continued.md)

