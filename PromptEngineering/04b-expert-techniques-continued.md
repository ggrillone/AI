# Part 4: Expert Techniques & Workflows (Continued)

## Lesson 20: Golden Test Sets & Quality Assurance

### Objectives
- Understand golden test sets as validation benchmarks
- Learn to create effective test sets for prompt quality
- Master tracking and improving AI assistance over time
- Build a personal quality assurance system

### Explanation

#### What Are Golden Test Sets?

**Golden test sets** are curated collections of test prompts and expected outputs used to validate and improve prompt effectiveness over time.

**Think of it as:**
- Unit tests for your prompts
- Regression tests for AI quality
- Benchmark suite for improvement tracking

**Components:**
1. **Test Cases**: Specific prompts for common tasks
2. **Expected Criteria**: What good output looks like
3. **Scoring System**: How to evaluate quality
4. **Improvement Tracking**: History of quality over time

#### Why Use Golden Test Sets?

✅ **Benefits:**
- **Quality Validation**: Ensure prompts produce good results
- **Regression Prevention**: Catch when changes degrade quality
- **Team Alignment**: Share proven prompts
- **Continuous Improvement**: Track what works over time
- **Onboarding**: New team members learn from best examples

**Use Cases:**
- Validating prompt templates
- Testing system prompt effectiveness
- Sharing best practices with team
- Tracking improvements in AI models
- Quality benchmarking

### Step-by-Step Tutorial

**Building Your Golden Test Set**

**Step 1: Identify Common Task Categories**

```markdown
Categories for your golden test set:
1. Component Generation
2. Debugging/Code Review
3. Refactoring
4. Test Writing
5. Documentation
6. Performance Optimization
7. Accessibility Review
```

**Step 2: Create Test Cases for Each Category**

```markdown
# Test Case Template

## Test ID: [Category]-[Number]
## Task: [Brief description]
## Prompt: [Exact prompt text]
## Success Criteria:
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Scoring:
- Functionality: [1-5]
- Quality: [1-5]
- Completeness: [1-5]
- Accuracy: [1-5]

## Notes:
- What worked well
- What could be improved
- Variations tried
```

**Step 3: Define Evaluation Criteria**

```markdown
# Evaluation Framework

## Functionality (Does it work?)
5 - Perfect: Fully functional, handles all cases
4 - Good: Works with minor issues
3 - Acceptable: Works for main cases, missing edge cases
2 - Poor: Partially works, significant issues
1 - Failing: Doesn't work

## Quality (Is it well-written?)
5 - Excellent: Production-ready, best practices
4 - Good: Minor improvements needed
3 - Acceptable: Works but needs refinement
2 - Poor: Significant quality issues
1 - Bad: Major problems

## Completeness (Is everything included?)
5 - Complete: All requirements met
4 - Mostly Complete: 1-2 minor items missing
3 - Partially Complete: Several items missing
2 - Incomplete: Many items missing
1 - Minimal: Most items missing

## Accuracy (Is it correct?)
5 - Accurate: No errors, correct implementation
4 - Mostly Accurate: 1-2 minor errors
3 - Somewhat Accurate: Several errors
2 - Inaccurate: Many errors
1 - Wrong: Fundamentally incorrect
```

**Step 4: Build Your Test Set**

```markdown
# Example Test Set Structure

## Category 1: Component Generation

### Test 1.1: Simple Button Component
**Prompt:**
```
Create a Button component with variants (primary, secondary), 
sizes (small, medium, large), and loading state support.
Use TypeScript and styled-components.
```

**Success Criteria:**
- [ ] TypeScript interface with all props
- [ ] All variants implemented
- [ ] All sizes implemented
- [ ] Loading state shows spinner
- [ ] Accessible (ARIA attributes)
- [ ] Styled-components used correctly

**Expected Output Elements:**
- ✅ ButtonProps interface
- ✅ Variant type union
- ✅ Size type union
- ✅ Default props
- ✅ Loading spinner component
- ✅ ARIA attributes (role, aria-label, aria-disabled, aria-busy)
- ❌ Should NOT include: State management, complex logic

### Test 1.2: Form Input with Validation
[Another component test...]

---

## Category 2: Debugging

### Test 2.1: Memory Leak Detection
**Prompt:**
```
This component shows a memory leak warning when unmounting 
during data fetch. Identify and fix the issue.

[Component code with useEffect and fetch]
```

**Success Criteria:**
- [ ] Correctly identifies missing cleanup
- [ ] Explains why memory leak occurs
- [ ] Provides correct fix (cleanup function)
- [ ] Mentions alternative approaches (AbortController)

**Expected Analysis:**
- ✅ Identifies setState after unmount
- ✅ Explains component lifecycle
- ✅ Provides cleanup pattern
- ✅ Mentions best practices

---

## Category 3: Code Review

### Test 3.1: Security Review
[Security review test case...]
```

**Step 5: Track and Improve**

```markdown
# Test Results Log

## Date: 2024-01-15
## Model: Claude 3.5 Sonnet
## Prompt Version: System Prompt v2.1

| Test ID | Functionality | Quality | Completeness | Accuracy | Total | Notes |
|---------|--------------|---------|--------------|----------|-------|-------|
| 1.1 | 5 | 4 | 5 | 5 | 19/20 | Missing one ARIA attribute |
| 1.2 | 5 | 5 | 4 | 5 | 19/20 | Validation could be more robust |
| 2.1 | 5 | 5 | 5 | 5 | 20/20 | Perfect |
| 3.1 | 4 | 4 | 3 | 4 | 15/20 | Missed timing attack vector |

**Average: 18.25/20 (91%)**

## Improvements for Next Version:
- Add explicit ARIA requirements to system prompt
- Include security checklist in code review template
- Test timing attack scenarios
```

### Examples & Exercises

**Example 1: Component Generation Golden Test**

```markdown
# Golden Test: Button Component

## Test Metadata
- ID: COMP-001
- Category: Component Generation
- Difficulty: Beginner
- Last Updated: 2024-01-15

## Prompt
```
Create a Button component for our design system.

Requirements:
- Variants: primary, secondary, danger, ghost
- Sizes: small, medium, large
- States: default, hover, active, disabled, loading
- Props: variant, size, disabled, loading, onClick, children
- TypeScript with strict typing
- Styled-components for styling
- Accessible (WCAG 2.1 AA)

Follow the pattern in our existing Input component.
```

## Expected Output Quality Criteria

### Must Have (Required)
- [ ] TypeScript interface with JSDoc
- [ ] All 4 variants implemented
- [ ] All 3 sizes implemented
- [ ] Disabled state prevents onClick
- [ ] Loading state shows spinner
- [ ] ARIA attributes: role="button", aria-label, aria-disabled, aria-busy
- [ ] Keyboard accessibility (Enter, Space)
- [ ] Focus visible indicator
- [ ] Proper PropTypes or TypeScript types

### Should Have (Expected)
- [ ] Default props defined
- [ ] Consistent naming with design system
- [ ] Comments for complex logic
- [ ] Usage example provided
- [ ] Handles both icon and text children

### Nice to Have (Bonus)
- [ ] Compound variants (e.g., primary-small has specific styles)
- [ ] Theme support (light/dark)
- [ ] Animation/transition on state changes
- [ ] Ref forwarding
- [ ] Polymorphic 'as' prop

### Must Not Have (Anti-patterns)
- ❌ Inline styles (should use styled-components)
- ❌ Class components (should be functional)
- ❌ console.log statements
- ❌ Hardcoded colors (should use theme)
- ❌ Missing accessibility attributes

## Scoring Rubric

### Functionality: [  /5]
- 5: All variants, sizes, states work perfectly
- 4: Minor state handling issues
- 3: Some variants/sizes missing
- 2: Significant functional problems
- 1: Doesn't work

### Code Quality: [  /5]
- 5: Production-ready, follows all patterns
- 4: Minor improvements needed
- 3: Works but needs refactoring
- 2: Significant quality issues
- 1: Poor quality

### Accessibility: [  /5]
- 5: Full WCAG AA, keyboard nav, ARIA perfect
- 4: Minor ARIA improvements needed
- 3: Basic accessibility, missing some ARIA
- 2: Poor accessibility
- 1: Not accessible

### TypeScript: [  /5]
- 5: Strict typing, no any, comprehensive types
- 4: Mostly typed, minor improvements
- 3: Basic typing, some anys
- 2: Minimal typing
- 1: No typing

## Previous Results

| Date | Model | Func | Quality | A11y | TS | Total | Notes |
|------|-------|------|---------|------|----|----|-------|
| 2024-01-10 | GPT-4 | 5 | 4 | 4 | 5 | 18 | Missing aria-busy |
| 2024-01-12 | Claude Sonnet | 5 | 5 | 5 | 5 | 20 | Perfect |
| 2024-01-15 | GPT-4o | 5 | 4 | 5 | 5 | 19 | Minor styling issue |

## Improvement Tracking

**Prompt Iterations:**
- v1.0: Initial prompt - Average score: 16/20
- v2.0: Added "Follow Input component pattern" - Average: 18/20
- v2.1: Added explicit accessibility requirements - Average: 19/20

**Key Learnings:**
- Referencing existing components improves consistency
- Explicit accessibility requirements significantly improve output
- Showing both good and bad examples helps
```

**Example 2: Debugging Test Case**

```markdown
# Golden Test: Race Condition Debugging

## Test Metadata
- ID: DEBUG-003
- Category: Debugging
- Difficulty: Intermediate
- Last Updated: 2024-01-15

## Prompt
```
This component sometimes shows stale data when rapidly changing the userId prop.

Component Code:
\`\`\`tsx
const UserProfile = ({ userId }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(false);
  
  useEffect(() => {
    setLoading(true);
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => {
        setUser(data);
        setLoading(false);
      });
  }, [userId]);
  
  if (loading) return <div>Loading...</div>;
  return <div>{user?.name}</div>;
};
\`\`\`

Debug this issue:
1. Identify the root cause
2. Explain why it happens
3. Provide a fix
4. Suggest prevention strategies
```

## Expected Analysis

### Root Cause Identification
**Must Identify:**
- Race condition when userId changes rapidly
- Multiple fetch requests in flight
- Later-started request completes first
- setState called with stale data

### Explanation Quality
**Should Explain:**
- Request lifecycle and timing
- Why responses can arrive out of order
- Impact on user experience
- Component lifecycle interaction

### Solution Quality
**Must Provide:**
- Cleanup function in useEffect
- Either: ignore flag or AbortController
- Working code example
- Explanation of how fix works

### Prevention Strategies
**Should Mention:**
- Always cleanup async operations
- Use AbortController for fetch
- Consider using data fetching libraries (React Query, SWR)
- ESLint rules to catch missing cleanup

## Scoring Rubric

### Problem Identification: [  /5]
- 5: Correctly identifies race condition with clear explanation
- 4: Identifies issue, minor details missing
- 3: Identifies issue but explanation unclear
- 2: Partial identification
- 1: Misidentifies or doesn't find

### Solution Correctness: [  /5]
- 5: Correct solution with proper cleanup
- 4: Correct solution, minor improvements possible
- 3: Works but not optimal
- 2: Partially correct
- 1: Incorrect solution

### Explanation Clarity: [  /5]
- 5: Clear, thorough, educational
- 4: Clear, minor details missing
- 3: Understandable but could be clearer
- 2: Confusing explanation
- 1: No useful explanation

### Prevention Advice: [  /5]
- 5: Comprehensive prevention strategies
- 4: Good strategies, minor additions possible
- 3: Basic prevention advice
- 2: Minimal advice
- 1: No prevention strategies

## Expected Solution Pattern

```typescript
useEffect(() => {
  let cancelled = false; // ignore flag
  
  setLoading(true);
  fetch(`/api/users/${userId}`)
    .then(res => res.json())
    .then(data => {
      if (!cancelled) {  // Only update if not cancelled
        setUser(data);
        setLoading(false);
      }
    });
  
  return () => {
    cancelled = true;  // Cleanup
  };
}, [userId]);
```

OR with AbortController:

```typescript
useEffect(() => {
  const controller = new AbortController();
  
  setLoading(true);
  fetch(`/api/users/${userId}`, { signal: controller.signal })
    .then(res => res.json())
    .then(data => {
      setUser(data);
      setLoading(false);
    })
    .catch(err => {
      if (err.name !== 'AbortError') {
        // Handle error
      }
    });
  
  return () => {
    controller.abort();  // Cleanup
  };
}, [userId]);
```

## Test Results

| Date | Model | Identification | Solution | Explanation | Prevention | Total |
|------|-------|---------------|----------|-------------|------------|-------|
| 2024-01-10 | GPT-4 | 5 | 5 | 4 | 3 | 17/20 |
| 2024-01-12 | Claude | 5 | 5 | 5 | 5 | 20/20 |
| 2024-01-15 | GPT-4o | 5 | 5 | 5 | 4 | 19/20 |
```

**Exercise 1: Build Your Golden Test Set**

**Your Task**: Create 5 test cases for your most common development tasks.

**Template:**

```markdown
# My Golden Test Set

## Test 1: [Category] - [Task Name]
**Prompt:** [Exact prompt]
**Success Criteria:**
- [ ] Must have 1
- [ ] Must have 2
**Scoring:** [Rubric]
**Expected Output:** [Description]

## Test 2: [Next task]
...

[Continue for 5 tests]
```

**Solution Example:**

```markdown
# My Golden Test Set: Frontend Development

## Test 1: Component Generation - Data Table
**Prompt:**
```
Create a responsive data table component with sorting and pagination.
Tech stack: React, TypeScript, Tailwind CSS.
Props: data (array), columns (column config), pageSize.
```

**Success Criteria:**
- [ ] TypeScript props interface
- [ ] Column sorting (asc/desc)
- [ ] Pagination controls
- [ ] Responsive (stacks on mobile)
- [ ] Accessible table markup
- [ ] Loading state
- [ ] Empty state

**Scoring:**
- Functionality: Works, sorts, paginates [/5]
- Responsiveness: Mobile-friendly [/5]
- Accessibility: Proper table semantics, ARIA [/5]
- TypeScript: Full typing [/5]

**Expected Output:**
- Component with proper table markup
- Sort indicators in headers
- Pagination component
- Mobile-friendly layout

---

## Test 2: API Integration - Custom Hook
**Prompt:**
```
Create a custom hook useProducts for fetching product data.
API: GET /api/products?category=...
Should support filtering by category.
Return: { data, loading, error, refetch }
```

**Success Criteria:**
- [ ] Hook returns correct shape
- [ ] Handles loading state
- [ ] Handles error state
- [ ] Supports category filter
- [ ] Refetch function works
- [ ] Cleanup on unmount

**Scoring:**
- API Integration: Correct fetch logic [/5]
- State Management: Loading/error handling [/5]
- TypeScript: Proper types [/5]
- Cleanup: Memory leak prevention [/5]

---

## Test 3: Code Review - Performance
**Prompt:**
```
Review this component for performance issues:
[Component with expensive computation, unnecessary re-renders]

Identify bottlenecks and suggest optimizations.
```

**Success Criteria:**
- [ ] Identifies unnecessary re-renders
- [ ] Suggests React.memo where appropriate
- [ ] Recommends useMemo for computations
- [ ] Recommends useCallback for functions
- [ ] Explains impact of each optimization

**Scoring:**
- Issue Identification: Finds all issues [/5]
- Solution Quality: Correct optimizations [/5]
- Explanation: Clear reasoning [/5]
- Impact Analysis: Before/after assessment [/5]

---

## Test 4: Accessibility - Form Validation
**Prompt:**
```
Add comprehensive accessibility to this login form.
Form has email and password fields.
Ensure WCAG 2.1 AA compliance.
```

**Success Criteria:**
- [ ] Labels properly associated
- [ ] Error messages announced
- [ ] Required fields indicated
- [ ] Keyboard navigation works
- [ ] Focus management correct
- [ ] ARIA attributes appropriate

**Scoring:**
- Label Association: htmlFor + id [/5]
- Error Handling: aria-invalid, aria-describedby [/5]
- Keyboard Nav: Tab order, focus visible [/5]
- Screen Reader: Proper announcements [/5]

---

## Test 5: Testing - Integration Test
**Prompt:**
```
Write integration tests for checkout flow:
1. Add product to cart
2. Proceed to checkout
3. Fill shipping info
4. Complete purchase

Use React Testing Library and Mock Service Worker.
```

**Success Criteria:**
- [ ] Tests complete user flow
- [ ] Mocks API calls correctly
- [ ] Validates each step
- [ ] Handles loading states
- [ ] Handles success/error states
- [ ] Uses accessible queries

**Scoring:**
- Flow Coverage: All steps tested [/5]
- API Mocking: MSW used correctly [/5]
- Assertions: Meaningful checks [/5]
- Best Practices: Accessible queries, userEvent [/5]
```

**Validation:**
- **Self-Check**: Do your tests cover your most common tasks?
- **Self-Check**: Are success criteria specific and measurable?
- **Self-Check**: Can you run these tests repeatedly?

### Frontend Contextualization

**Real-World Scenario: Team Quality Assurance**

Your team wants to ensure consistent quality across all AI-assisted development.

**Golden Test Set Strategy:**

```markdown
# Team Golden Test Set (10 developers)

## Purpose
Validate that AI assistance meets team quality standards across:
- Component generation
- Code reviews
- Testing
- Documentation
- Refactoring

## Test Set Organization

### Tier 1: Essential (Run Weekly)
Must pass 95%+ to maintain standards
- Component: Button, Input, Modal (3 tests)
- Code Review: Security, Performance, Accessibility (3 tests)
- Testing: Unit, Integration (2 tests)

### Tier 2: Important (Run Monthly)
Target 90%+ pass rate
- Complex Components: DataTable, Form (2 tests)
- Refactoring: Extract Hook, Split Component (2 tests)
- Documentation: API Docs, Component Docs (2 tests)

### Tier 3: Advanced (Run Quarterly)
Target 85%+ pass rate
- Architecture: Design decisions (2 tests)
- Optimization: Bundle size, Performance (2 tests)

## Shared Test Results

Team Dashboard: https://team-ai-quality.internal/

| Developer | Tier 1 | Tier 2 | Tier 3 | Overall |
|-----------|--------|--------|--------|---------|
| Alice | 98% | 95% | 88% | 94% |
| Bob | 96% | 92% | 85% | 91% |
| Carol | 100% | 97% | 90% | 96% |
| Team Avg | 97% | 94% | 87% | 93% |

## Improvement Process

1. **Individual Review**: Run tests monthly
2. **Team Review**: Discuss results quarterly
3. **Prompt Refinement**: Update system prompts based on learnings
4. **Template Updates**: Improve templates for better results
5. **Knowledge Sharing**: Share top-scoring approaches

## Success Stories

**Before Golden Tests:**
- Inconsistent component quality
- Missing accessibility features
- Security issues in code reviews
- Average component creation: 2 hours

**After Golden Tests (6 months):**
- 94% test pass rate
- Zero accessibility regressions
- Caught 15 security issues preemptively
- Average component creation: 45 minutes

**ROI:**
- Time saved: 15 hours/week team-wide
- Quality improvements: 23% fewer bugs in production
- Onboarding time: Reduced from 2 weeks to 3 days
```

**Practical Takeaway**: Golden test sets are your quality assurance system for AI collaboration. Start small (5-10 tests for your most common tasks), run them regularly, and track improvements over time. Share successful tests with your team. Think of them as continuous integration for your prompts—they catch regressions, validate improvements, and ensure consistent quality. The real value isn't just in passing tests, but in the learning process: when a test fails, you improve your prompt or system configuration, raising the bar for all future work. Invest in building your golden test set early; it pays dividends by making quality improvements systematic rather than accidental.

---

# Summary: Expert Techniques

Congratulations! You've completed all expert lessons!

| Lesson | Key Takeaway | Application |
|--------|-------------|-------------|
| 18: System Prompts & IDE Config | Configure AI behavior project-wide | Consistency, quality standards |
| 19: Prompt Templates & Variables | Reusable prompt patterns | Efficiency, team alignment |
| 20: Golden Test Sets | Quality validation and tracking | Continuous improvement |

## Expert Skills Self-Assessment

**Can you:**
1. ✅ Configure system prompts for your project?
2. ✅ Create and use prompt templates?
3. ✅ Build golden test sets for quality assurance?

---

**Next:**
[Resource List](05-resources.md)
or
[Workflows](06-workflows.md)


