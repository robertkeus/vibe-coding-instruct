# React + TypeScript Project Guidelines

## Project Overview
A modern React application built with TypeScript, prioritizing accessibility, security, maintainability, and sustainability through strict coding standards and comprehensive testing.

## Technology Stack
- **Frontend**: React with TypeScript (strict mode)
- **Styling**: CSS Modules, Tailwind CSS, or styled-components
- **State Management**: React Query/SWR for server state, Zustand/Redux Toolkit for client state
- **Testing**: Jest, React Testing Library, @testing-library/jest-dom
- **Build Tools**: Vite or Create React App with TypeScript template
- **Package Manager**: npm (prefer over yarn or pnpm)

## Four Core Pillars (Non-Negotiable)

### 1. Accessibility (WCAG 2.2 AA Compliance)
- Use semantic HTML elements in JSX (`<button>`, `<nav>`, `<header>`, `<main>`, `<footer>`)
- Include proper ARIA attributes and keyboard navigation support
- Add skip links
- Maintain proper heading hierarchy with one `<h1>` per page
- Ensure minimum 44px touch targets for interactive elements
- Meet WCAG 2.2 AA color contrast ratios (≥4.5:1)

### 2. Security (Type-Safe and Secure)
- Never use `dangerouslySetInnerHTML` without proper sanitization
- Validate all props with explicit TypeScript interfaces (never `any`)
- Use environment variables for API keys (`process.env.REACT_APP_*`)
- Implement proper error boundaries with typed error states
- Sanitize user inputs before rendering

### 3. Maintainability (Scalable Architecture)
- Use strict TypeScript with explicit return types
- Apply consistent naming: PascalCase for components, camelCase for hooks
- Keep components under 40 lines, extract complex logic to custom hooks
- Include JSDoc comments for all exported components and hooks
- Handle async operations with proper loading/error states

### 4. Sustainability (Performance Optimization)
- Implement lazy loading with React.Suspense
- Use React.memo, useMemo, useCallback strategically
- Implement code splitting with React.lazy for heavy components
- Respect user preferences (`prefers-reduced-motion`, system theme)
- Cache API responses effectively

## Coding Standards

### Component Structure
```typescript
// ✅ Always use this pattern
interface ComponentProps {
  readonly children: React.ReactNode;
  readonly onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
  readonly variant?: 'primary' | 'secondary' | 'danger';
  readonly disabled?: boolean;
  readonly ariaLabel?: string;
}

/**
 * Component description with accessibility and usage information
 */
export const Component: React.FC<ComponentProps> = ({
  children,
  onClick,
  variant = 'primary',
  disabled = false,
  ariaLabel,
  ...restProps
}) => {
  return (
    <button
      onClick={disabled ? undefined : onClick}
      disabled={disabled}
      aria-label={ariaLabel}
      className={`btn btn--${variant}`}
      type="button"
      {...restProps}
    >
      {children}
    </button>
  );
};

Component.displayName = 'Component';
```

### Custom Hook Patterns
```typescript
// ✅ Always define explicit interfaces and return types
interface UseApiState<T> {
  readonly data: T | null;
  readonly loading: boolean;
  readonly error: Error | null;
}

interface UseApiReturn<T> extends UseApiState<T> {
  readonly refetch: () => Promise<void>;
  readonly reset: () => void;
}

/**
 * Custom hook description with usage examples
 */
export function useApi<T>(url: string): UseApiReturn<T> {
  // Implementation with proper error handling and cleanup
}
```

### TypeScript Requirements
- Enable strict mode in `tsconfig.json`
- Use `readonly` for all interface properties
- Implement discriminated unions for complex state
- Always specify return types for functions and hooks
- Use proper event handler types (`React.MouseEvent<HTMLButtonElement>`)

### File Organization
```
src/
├── components/           # Reusable UI components
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.module.css
│   │   ├── Button.test.tsx
│   │   └── index.ts
├── hooks/               # Custom React hooks
├── pages/               # Page components
├── utils/               # Utility functions
├── types/               # TypeScript type definitions
└── __tests__/           # Test utilities and setup
```

## Development Workflow (Required Process)

### Phase 1: Planning
- **MUST** describe proposed changes before implementing
- **MUST** await explicit confirmation before making changes
- Ask numbered clarifying questions with default answers
- Challenge approaches if simpler alternatives exist
- Ensure idiomatic React + TypeScript patterns
- Check existing conventions for consistency

### Phase 2: Implementation
- Begin only with explicit instruction to implement
- Make small, incremental changes that are easy to verify
- Stay strictly focused on agreed-upon tasks
- Stop and ask questions if scope expands beyond plan
- Never implement anticipated future features without approval
- Fix only trivial issues; discuss substantial changes in review

### Phase 3: Review
- Review implemented changes and check for issues
- Identify opportunities to remove or simplify existing code
- Complete code review and identify technical debt
- Wait for explicit direction before starting new work
- Raise improvement ideas for next planning phase

## Performance Requirements

### Bundle Size Limits
- Component bundle: ≤25KB gzipped per route
- Initial page load: ≤50KB gzipped React bundle
- CSS bundle: ≤50KB gzipped
- Total page weight: ≤500KB

### React Performance Patterns
```typescript
// ✅ Memoized components with proper comparison
export const ExpensiveComponent = React.memo<Props>(({ data, onSelect }) => {
  const handleClick = useCallback(() => {
    onSelect(data.id);
  }, [onSelect, data.id]);

  return <div onClick={handleClick}>{data.title}</div>;
});

// ✅ Custom comparison when needed
const areEqual = (prevProps: Props, nextProps: Props): boolean => {
  return prevProps.data.id === nextProps.data.id;
};

export const OptimizedComponent = React.memo(ExpensiveComponent, areEqual);
```

## Testing Requirements

### Component Testing
```typescript
// ✅ Always include accessibility tests
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

describe('Component', () => {
  it('should be accessible', async () => {
    const { container } = render(<Component />);
    const results = await axe(container);
    expect(results).toHaveNoViolations();
  });

  it('should handle user interactions', async () => {
    const user = userEvent.setup();
    const handleClick = jest.fn();
    
    render(<Component onClick={handleClick} />);
    
    await user.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });
});
```

### Hook Testing
```typescript
// ✅ Test custom hooks with proper TypeScript
import { renderHook, act } from '@testing-library/react';

describe('useCustomHook', () => {
  it('should handle state updates correctly', async () => {
    const { result } = renderHook(() => useCustomHook());
    
    await act(async () => {
      result.current.updateState('new value');
    });
    
    expect(result.current.state).toBe('new value');
  });
});
```

## Error Handling Standards

### Error Boundaries
```typescript
// ✅ Always implement typed error boundaries
interface ErrorBoundaryState {
  readonly hasError: boolean;
  readonly error: Error | null;
}

export class ErrorBoundary extends React.Component<
  { children: React.ReactNode },
  ErrorBoundaryState
> {
  // Implementation with proper TypeScript typing
}
```

### Async Error Handling
```typescript
// ✅ Use discriminated unions for async states
type AsyncState<T> = 
  | { readonly status: 'idle' }
  | { readonly status: 'loading' }
  | { readonly status: 'success'; readonly data: T }
  | { readonly status: 'error'; readonly error: Error };
```

## Communication Style

### Before Implementation
- Explain what you're going to do and why
- Break down complex tasks into clear, numbered steps
- Ask for clarification if requirements are unclear
- Suggest simpler alternatives when appropriate

### During Implementation
- Focus only on agreed-upon changes
- Stop and ask questions if scope expands
- Provide brief explanations for technical decisions
- Use proper React + TypeScript patterns consistently

### Code Review
- Point out accessibility improvements
- Identify performance optimization opportunities
- Suggest refactoring for better maintainability
- Check for TypeScript type safety issues

## Forbidden Patterns (REFUSE IF REQUESTED)

### React Anti-Patterns
```typescript
// ❌ NEVER: Class components
class BadComponent extends React.Component {}

// ❌ NEVER: any types for props
interface BadProps { data: any; }

// ❌ NEVER: Conditional hooks
if (condition) { useState(0); }

// ❌ NEVER: Missing dependency arrays
useEffect(() => { fetchData(userId); }); // Missing [userId]

// ❌ NEVER: Direct state mutation
setState(prev => { prev.items.push(item); return prev; });
```

### Security Anti-Patterns
```typescript
// ❌ NEVER: Unsafe HTML injection
<div dangerouslySetInnerHTML={{__html: userInput}} />

// ❌ NEVER: Exposing secrets
const API_KEY = 'secret-key-here'; // Use environment variables

// ❌ NEVER: any types for user data
const handleUserData = (data: any) => { /* ... */ };
```

## Dependencies and Package Management

### Preferred Libraries
- **UI Components**: Radix UI, Headless UI, or custom components
- **Forms**: React Hook Form with Zod validation
- **HTTP Client**: Axios or native fetch with proper error handling
- **Date/Time**: date-fns (prefer over moment.js)
- **Utilities**: Lodash (import specific functions only)

### Package Installation
```bash
# ✅ Always check for TypeScript support
npm install @types/package-name

# ✅ Use exact versions for critical dependencies
npm install --save-exact react@18.2.0
```

## Current Development Priorities

1. **Component Library**: Building accessible, reusable UI components
2. **Type Safety**: Eliminating all `any` types and improving interfaces
3. **Performance**: Implementing code splitting and optimization
4. **Testing**: Achieving 90%+ test coverage with accessibility tests
5. **Documentation**: Adding comprehensive JSDoc comments

Remember: Every decision should align with our four pillars - Accessibility, Security, Maintainability, and Sustainability. When in doubt, prioritize user experience and code quality over quick implementation. 