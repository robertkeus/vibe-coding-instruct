# Lovable Development Standards

## Primary Objective
Generate production-ready React + TypeScript code that prioritizes these three binding pillars above all else:

1. **MAINTAINABILITY** - Easy to read, refactor, and extend for years
2. **ACCESSIBILITY** - Meets WCAG 2.2 AA standards, inclusive for all users  
3. **SUSTAINABILITY** - Follows green software engineering principles

All other goals (speed, optimizations, flashy UI) are secondary to these three pillars.

## Technology Stack
- **Frontend**: React with TypeScript (strict mode)
- **Styling**: CSS Modules, styled-components, or Tailwind CSS with accessibility plugins
- **State Management**: React hooks and Context API (Redux Toolkit/Zustand for complex cases)
- **Testing**: Jest, React Testing Library, axe-core for accessibility testing
- **Build Tools**: Vite, Webpack with optimal performance configuration
- **Package Manager**: npm

## 1. MAINTAINABILITY RULES

### Code Quality Standards
- **Clarity over cleverness** - Use straightforward, self-documenting code
- **Strict TypeScript** - Explicit types, avoid `any`, use `unknown` if type is truly unknown
- **Descriptive naming** - PascalCase for components, camelCase for variables/functions
- **Function size limit** - Keep functions under 40 lines of code
- **Pure functions** - Prefer pure functions and immutable data patterns

### Architecture Requirements
```
src/
├── components/     # Reusable UI components
├── hooks/         # Custom React hooks
├── services/      # API calls, external services
├── types/         # TypeScript type definitions
├── utils/         # Pure utility functions
├── config/        # App configuration
└── tests/         # Test files
```

### Component Pattern
```typescript
/**
 * Accessible button component following WCAG 2.2 guidelines
 * Supports multiple variants and provides proper semantic markup
 * 
 * @param props ButtonProps interface
 */
interface ButtonProps {
  readonly children: React.ReactNode;
  readonly onClick: () => void;
  readonly variant?: 'primary' | 'secondary';
  readonly disabled?: boolean;
  readonly ariaLabel?: string;
  readonly type?: 'button' | 'submit' | 'reset';
}

export const Button: React.FC<ButtonProps> = ({
  children,
  onClick,
  variant = 'primary',
  disabled = false,
  ariaLabel,
  type = 'button'
}) => {
  return (
    <button
      type={type}
      onClick={onClick}
      disabled={disabled}
      aria-label={ariaLabel}
      className={`btn btn--${variant} ${disabled ? 'btn--disabled' : ''}`}
    >
      {children}
    </button>
  );
};

Button.displayName = 'Button';
```

### Documentation Requirements
```typescript
/**
 * File: UserProfile.tsx
 * Purpose: Displays user profile information with edit capabilities
 * Accessibility: Full keyboard navigation, screen reader support
 * Performance: Lazy loads avatar images, memoized for optimal re-renders
 */

/**
 * Custom hook for managing user profile data with optimistic updates
 * 
 * @param userId - Unique identifier for the user
 * @returns Object containing user data, loading state, and update functions
 * 
 * @example
 * ```tsx
 * const { user, loading, updateProfile } = useUserProfile('123');
 * ```
 */
export function useUserProfile(userId: string): UseUserProfileReturn {
  // Implementation
}
```

### Security Standards
- **Never hardcode secrets** - Use environment variables only (`process.env.VITE_*`)
- **Input validation** - Validate all user inputs and sanitize outputs
- **TypeScript safety** - Use proper typing to catch potential security issues
- **Error boundaries** - Implement proper error handling without exposing sensitive data

## 2. ACCESSIBILITY RULES (WCAG 2.2 AA COMPLIANCE)

### Semantic HTML First
```typescript
// ✅ Use native HTML elements
const Navigation = () => (
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/home">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
  </nav>
);

// ✅ Proper heading hierarchy
const PageLayout = () => (
  <main>
    <h1>Page Title</h1>
    <section>
      <h2>Section Title</h2>
      <h3>Subsection</h3>
    </section>
  </main>
);

// ❌ Avoid generic elements for interactive content
const BadButton = () => <div onClick={handleClick}>Click me</div>;
```

### Keyboard & Focus Management
```typescript
// ✅ Focus trap for modals
const Modal = ({ isOpen, onClose, children }) => {
  const modalRef = useRef<HTMLDivElement>(null);
  
  useEffect(() => {
    if (isOpen) {
      // Focus first focusable element
      const focusableElements = modalRef.current?.querySelectorAll(
        'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
      );
      const firstElement = focusableElements?.[0] as HTMLElement;
      firstElement?.focus();
    }
  }, [isOpen]);

  return (
    <div
      ref={modalRef}
      role="dialog"
      aria-modal="true"
      aria-labelledby="modal-title"
      onKeyDown={(e) => {
        if (e.key === 'Escape') onClose();
      }}
    >
      {children}
    </div>
  );
};

// ✅ Skip links for keyboard navigation
const SkipLinks = () => (
  <div className="skip-links">
    <a href="#main-content" className="skip-link">
      Skip to main content
    </a>
    <a href="#navigation" className="skip-link">
      Skip to navigation
    </a>
  </div>
);
```

### Visual & Content Accessibility
```typescript
// ✅ Proper image handling
const AccessibleImage = ({ src, alt, decorative = false }) => (
  <img 
    src={src} 
    alt={decorative ? "" : alt}
    loading="lazy"
  />
);

// ✅ Color contrast and reduced motion support
const AnimatedComponent = () => {
  const prefersReducedMotion = useMediaQuery('(prefers-reduced-motion: reduce)');
  
  return (
    <div 
      className={`component ${prefersReducedMotion ? 'no-animation' : 'with-animation'}`}
      style={{
        // Ensure WCAG 2.2 AA contrast ratios
        color: '#1a1a1a', // 4.5:1 contrast on white
        backgroundColor: '#ffffff'
      }}
    >
      Content
    </div>
  );
};
```

### Forms & Dynamic Content
```typescript
// ✅ Accessible form with proper labeling and error handling
const AccessibleForm = () => {
  const [email, setEmail] = useState('');
  const [emailError, setEmailError] = useState('');
  const emailId = useId();
  const errorId = useId();

  return (
    <form>
      <fieldset>
        <legend>Contact Information</legend>
        
        <div>
          <label htmlFor={emailId}>Email Address *</label>
          <input
            id={emailId}
            type="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
            aria-describedby={emailError ? errorId : undefined}
            aria-invalid={!!emailError}
            required
          />
          {emailError && (
            <div id={errorId} role="alert" aria-live="polite">
              {emailError}
            </div>
          )}
        </div>
      </fieldset>
    </form>
  );
};

// ✅ Dynamic content announcements
const LiveRegionExample = () => {
  const [status, setStatus] = useState('');

  return (
    <div>
      <button onClick={() => setStatus('Data saved successfully')}>
        Save Data
      </button>
      <div 
        role="status" 
        aria-live="polite" 
        aria-atomic="true"
        className="sr-only"
      >
        {status}
      </div>
    </div>
  );
};
```

## 3. SUSTAINABILITY RULES

### Performance Optimization
```typescript
// ✅ Lazy loading and code splitting
const LazyComponent = React.lazy(() => import('./ExpensiveComponent'));

const App = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <LazyComponent />
  </Suspense>
);

// ✅ Efficient image handling
const OptimizedImage = ({ src, alt, width, height }) => (
  <picture>
    <source srcSet={`${src}.avif`} type="image/avif" />
    <source srcSet={`${src}.webp`} type="image/webp" />
    <img 
      src={`${src}.jpg`} 
      alt={alt}
      width={width}
      height={height}
      loading="lazy"
      decoding="async"
    />
  </picture>
);
```

### Resource Efficiency
```typescript
// ✅ Efficient data fetching with caching
const useApiData = <T>(url: string) => {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    const abortController = new AbortController();
    
    const fetchData = async () => {
      try {
        const response = await fetch(url, { 
          signal: abortController.signal,
          // Respect user's data saving preferences
          cache: navigator.connection?.saveData ? 'force-cache' : 'default'
        });
        const result = await response.json();
        setData(result);
      } catch (error) {
        if (error.name !== 'AbortError') {
          console.error('Fetch error:', error);
        }
      } finally {
        setLoading(false);
      }
    };
    
    fetchData();
    return () => abortController.abort();
  }, [url]);
  
  return { data, loading };
};

// ✅ Efficient React patterns
const OptimizedList = React.memo(({ items, onItemClick }) => {
  const handleItemClick = useCallback((id: string) => {
    onItemClick(id);
  }, [onItemClick]);

  return (
    <ul>
      {items.map((item) => (
        <ListItem 
          key={item.id}
          item={item}
          onClick={handleItemClick}
        />
      ))}
    </ul>
  );
});
```

### Adaptive Performance
```typescript
// ✅ Respect user preferences and device capabilities
const useAdaptivePerformance = () => {
  const [saveData, setSaveData] = useState(false);
  const [prefersReducedMotion, setPrefersReducedMotion] = useState(false);
  const [darkMode, setDarkMode] = useState(false);

  useEffect(() => {
    // Respect data saving preferences
    if ('connection' in navigator) {
      setSaveData(navigator.connection.saveData);
    }

    // Respect motion preferences
    const mediaQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
    setPrefersReducedMotion(mediaQuery.matches);

    // Respect color scheme preferences
    const colorSchemeQuery = window.matchMedia('(prefers-color-scheme: dark)');
    setDarkMode(colorSchemeQuery.matches);

    // Listen for changes
    const handleMotionChange = (e) => setPrefersReducedMotion(e.matches);
    const handleColorSchemeChange = (e) => setDarkMode(e.matches);

    mediaQuery.addEventListener('change', handleMotionChange);
    colorSchemeQuery.addEventListener('change', handleColorSchemeChange);

    return () => {
      mediaQuery.removeEventListener('change', handleMotionChange);
      colorSchemeQuery.removeEventListener('change', handleColorSchemeChange);
    };
  }, []);

  return { saveData, prefersReducedMotion, darkMode };
};
```

## 4. CODE FORMATTING & STANDARDS

### TypeScript Configuration
```json
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "noImplicitReturns": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "exactOptionalPropertyTypes": true,
    "noUncheckedIndexedAccess": true,
    "jsx": "react-jsx",
    "target": "ES2020",
    "lib": ["DOM", "DOM.Iterable", "ES6"],
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "isolatedModules": true
  }
}
```

### File Organization Standards
```typescript
// ✅ Import order and grouping
import React, { useState, useEffect, useCallback } from 'react';

import { Button } from '@/components/Button';
import { useApi } from '@/hooks/useApi';

import { UserService } from './UserService';
import { validateEmail } from './utils';

import type { User } from '@/types/User';

// ✅ Interface definitions
interface ComponentProps {
  readonly user: User;
  readonly onUpdate: (user: User) => void;
}

// ✅ Component implementation
export const Component: React.FC<ComponentProps> = ({ user, onUpdate }) => {
  // Implementation
};

// ✅ Export at bottom
export type { ComponentProps };
```

## 5. ERROR HANDLING & VALIDATION

### Input Validation
```typescript
// ✅ Schema-based validation
import { z } from 'zod';

const UserSchema = z.object({
  email: z.string().email('Please enter a valid email address'),
  age: z.number().min(13, 'Must be at least 13 years old'),
  name: z.string().min(1, 'Name is required')
});

type User = z.infer<typeof UserSchema>;

const validateUser = (data: unknown): User => {
  try {
    return UserSchema.parse(data);
  } catch (error) {
    if (error instanceof z.ZodError) {
      throw new Error(error.errors.map(e => e.message).join(', '));
    }
    throw error;
  }
};
```

### Error Boundaries
```typescript
// ✅ Accessible error boundary
interface ErrorBoundaryState {
  hasError: boolean;
  error: Error | null;
}

class ErrorBoundary extends React.Component<
  { children: React.ReactNode },
  ErrorBoundaryState
> {
  constructor(props: { children: React.ReactNode }) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error: Error): ErrorBoundaryState {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return (
        <div role="alert" className="error-boundary">
          <h2>Something went wrong</h2>
          <p>We're sorry, but an unexpected error occurred.</p>
          <button onClick={() => this.setState({ hasError: false, error: null })}>
            Try again
          </button>
        </div>
      );
    }

    return this.props.children;
  }
}
```

## 6. TESTING & QUALITY ASSURANCE

### Accessibility Testing
```typescript
// ✅ Comprehensive component testing
import { render, screen, fireEvent } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { axe, toHaveNoViolations } from 'jest-axe';
import { Button } from './Button';

expect.extend(toHaveNoViolations);

describe('Button Component', () => {
  it('meets accessibility standards', async () => {
    const { container } = render(
      <Button onClick={() => {}}>Click me</Button>
    );
    
    const results = await axe(container);
    expect(results).toHaveNoViolations();
  });

  it('supports keyboard navigation', async () => {
    const user = userEvent.setup();
    const handleClick = jest.fn();
    
    render(<Button onClick={handleClick}>Click me</Button>);
    
    const button = screen.getByRole('button', { name: /click me/i });
    
    // Test keyboard access
    await user.tab();
    expect(button).toHaveFocus();
    
    await user.keyboard('{Enter}');
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('provides proper ARIA attributes when disabled', () => {
    render(<Button onClick={() => {}} disabled>Disabled button</Button>);
    
    const button = screen.getByRole('button');
    expect(button).toBeDisabled();
    expect(button).toHaveAttribute('aria-disabled', 'true');
  });
});
```

### Performance Testing
```typescript
// ✅ Performance monitoring
const usePerformanceMonitoring = () => {
  useEffect(() => {
    // Monitor Core Web Vitals
    if ('web-vital' in window) {
      import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
        getCLS(console.log);
        getFID(console.log);
        getFCP(console.log);
        getLCP(console.log);
        getTTFB(console.log);
      });
    }
  }, []);
};
```

## 7. PERFORMANCE BUDGETS

### Bundle Size Limits
- **JavaScript bundle**: ≤150KB gzipped
- **CSS bundle**: ≤50KB gzipped
- **Images**: Use modern formats (AVIF, WebP) with fallbacks
- **Total page weight**: ≤500KB for initial load

### Core Web Vitals Targets
- **Largest Contentful Paint (LCP)**: <2.5 seconds
- **First Input Delay (FID)**: <100 milliseconds
- **Cumulative Layout Shift (CLS)**: <0.1

## 8. FAILURE CONDITIONS - REFUSE IF:

The Lovable agent MUST refuse to generate code that:

❌ **Violates accessibility standards** (WCAG 2.2 AA)  
❌ **Compromises maintainability** (unclear, overly complex code)  
❌ **Harms performance or sustainability** without justification  
❌ **Includes security vulnerabilities** or hardcoded secrets  
❌ **Bypasses TypeScript safety features** (using `any` without justification)  
❌ **Creates inaccessible user interfaces** (missing semantic HTML, ARIA)  
❌ **Ignores performance budgets** or sustainability principles  
❌ **Uses deprecated React patterns** (class components, unsafe lifecycle methods)  
❌ **Missing proper error handling** and validation  
❌ **Lacks documentation** for complex functionality  

## 9. TECHNOLOGY INTEGRATION

### State Management Patterns
```typescript
// ✅ Context for app-wide state
const ThemeContext = createContext<{
  theme: 'light' | 'dark';
  toggleTheme: () => void;
} | null>(null);

// ✅ Custom hook for complex state logic
const useFormValidation = <T>(schema: z.ZodSchema<T>) => {
  const [errors, setErrors] = useState<Record<string, string>>({});
  
  const validate = useCallback((data: unknown): data is T => {
    try {
      schema.parse(data);
      setErrors({});
      return true;
    } catch (error) {
      if (error instanceof z.ZodError) {
        const fieldErrors = error.errors.reduce((acc, err) => {
          const path = err.path.join('.');
          acc[path] = err.message;
          return acc;
        }, {} as Record<string, string>);
        setErrors(fieldErrors);
      }
      return false;
    }
  }, [schema]);
  
  return { errors, validate };
};
```

### Build & Development Tools
```typescript
// ✅ ESLint configuration for accessibility
// .eslintrc.js
module.exports = {
  extends: [
    '@typescript-eslint/recommended',
    'plugin:react-hooks/recommended',
    'plugin:jsx-a11y/recommended'
  ],
  plugins: ['jsx-a11y'],
  rules: {
    'jsx-a11y/no-autofocus': 'error',
    'jsx-a11y/anchor-is-valid': 'error',
    '@typescript-eslint/no-explicit-any': 'error',
    '@typescript-eslint/explicit-function-return-type': 'warn'
  }
};
```

## REMEMBER: Three Binding Pillars

1. **MAINTAINABILITY** - Code that lasts and scales
2. **ACCESSIBILITY** - Inclusive for all users  
3. **SUSTAINABILITY** - Minimal environmental impact

When conflicts arise, always prioritize these pillars over convenience, speed, or visual appeal. Code quality and user inclusivity are never optional. 