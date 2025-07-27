# Vibe Coding Instruct

**Production-ready React + TypeScript development standards for AI coding platforms**

A comprehensive collection of configuration files that ensure consistent, high-quality React + TypeScript development across multiple AI coding platforms. This project provides unified standards focusing on accessibility, security, maintainability, and sustainability.

## 🎯 Project Overview

This repository contains meticulously crafted configuration files for four major AI coding platforms, each optimized for React + TypeScript development with proper prompt engineering principles:

- **[Cursor Rules](#cursor-rules)** - Advanced project rules for Cursor IDE
- **[Replit Configuration](#replit-configuration)** - Agent behavior customization for Replit
- **[Lovable Standards](#lovable-standards)** - Development standards for Lovable platform
- **[Windsurf Configuration](#windsurf-configuration)** - Enterprise-scale development for Windsurf platform

## 🏗️ Core Principles

All configurations are built around these **four binding pillars**:

### 1. 🔥 **Accessibility (WCAG 2.2 AA)**
- Semantic HTML elements in JSX
- Proper ARIA attributes and keyboard navigation
- Color contrast compliance (≥4.5:1 ratio)
- Screen reader and assistive technology support

### 2. 🔒 **Security**
- Type-safe data handling with strict TypeScript
- Environment variable management
- Input validation and sanitization
- Secure React patterns (no `dangerouslySetInnerHTML` without sanitization)

### 3. 🛠️ **Maintainability**
- Scalable React architecture
- Comprehensive TypeScript interfaces
- Modular component structure
- Extensive documentation requirements

### 4. 🌱 **Sustainability**
- Performance-optimized React with minimal re-renders
- Bundle size limits and lazy loading
- Efficient resource usage
- Green software engineering principles

## 📁 File Structure

```
vibe-coding-instruct/
├── cursor/
│   └── rules/
│       └── cursor.mdc                        # Complete markup & React + TypeScript standards
├── replit.md
├── lovable.md
├── windsurf.md
└── README.md
```

## 🎨 Platform Configurations

### Cursor Rules

Based on [Cursor's Rules documentation](https://docs.cursor.com/context/rules), our configuration provides comprehensive markup guidance for React + TypeScript applications:

**Markup-Focused Approach:**
- `cursor.mdc` - Complete semantic HTML/JSX patterns with accessibility, security, maintainability, and sustainability

**Features:**
- **Semantic HTML First** - Proper document structure, landmarks, and ARIA patterns
- **Comprehensive Examples** - Forms, tables, modals, buttons, images, and interactive elements
- **Four Essential Pillars** - Accessibility (WCAG 2.2 AA), Security (XSS prevention), Maintainability (clear patterns), Sustainability (performance optimization)
- **Real-World Patterns** - Production-ready JSX components with TypeScript
- **Always Applied** - Automatic enforcement of markup standards across all development

### Replit Configuration

Following [Replit's replit.md documentation](https://docs.replit.com/replitai/replit-dot-md), our `replit.md` includes:

**Prompt Engineering Structure:**
- **Role**: Senior React + TypeScript developer for Replit platform
- **Context**: Scale, team maintenance, and diverse user requirements  
- **Implementation Rules**: Comprehensive code examples and patterns
- **Constraints**: Clear boundaries and failure conditions

**Features:**
- **Four core pillars** with specific implementation requirements
- **Three-phase development workflow** (Planning → Implementation → Review)
- **Performance budgets** and bundle size limits
- **Comprehensive testing requirements** with accessibility focus

### Lovable Standards

Optimized for [Lovable's knowledge features](https://docs.lovable.dev/features/knowledge), our `lovable.md` focuses on:

**Three Binding Pillars (Lovable-Specific):**
1. **MAINTAINABILITY** - Code that lasts and scales
2. **ACCESSIBILITY** - WCAG 2.2 AA compliance
3. **SUSTAINABILITY** - Green software engineering

**Prompt Engineering Format:**
- **Role**: Senior React + TypeScript developer for Lovable platform
- **Context**: Production applications with long-term maintenance needs
- **Implementation Rules**: Detailed component and hook examples
- **Constraints**: Accessibility-first development approach

**Setup Instructions:**
- Copy the content of `lovable.md` and paste it into your Lovable project's **Settings > Instructions/Knowledge** section
- This configuration will guide the AI assistant for all development within that project

### Windsurf Configuration

Designed for enterprise-scale development on the Windsurf platform, our `windsurf.md` provides comprehensive standards following the [Windsurf Rules Directory](https://windsurf.com/editor/directory) best practices:

**Four Essential Pillars:**
1. **ACCESSIBILITY** - WCAG 2.2 AA compliance, inclusive for all users
2. **SECURITY** - Type-safe, validated, and protected against vulnerabilities  
3. **MAINTAINABILITY** - Easy to read, refactor, and extend for years
4. **SUSTAINABILITY** - Follows green software engineering principles

**Enterprise Features:**
- **Role**: Senior developer for enterprise-scale Windsurf applications
- **Context**: Distributed teams, global audiences, long-term maintenance
- **Implementation Rules**: Advanced patterns for complex applications
- **Constraints**: Strict three-phase workflow with quality gates

**Additional Resources:**
- Browse the [Windsurf Rules Directory](https://windsurf.com/editor/directory) for more curated examples and community-contributed rules

## 🚀 Quick Start

### 1. Choose Your Platform

**For Cursor IDE:**
```bash
# Copy the cursor directory to your project root
cp -r cursor/ /path/to/your/project/.cursor/
```

**For Replit:**
```bash
# Copy replit.md to your project root
cp replit.md /path/to/your/project/
```

**For Lovable:**
1. Copy the content from `lovable.md`
2. Go to your Lovable project Settings
3. Navigate to the **Instructions/Knowledge** section  
4. Paste the content to configure the AI assistant for your project

**For Windsurf:**
```bash
# Copy windsurf.md to your project root
cp windsurf.md /path/to/your/project/
```

### 2. Customize for Your Project

Each configuration file can be customized:

- **Update technology stack** preferences
- **Modify coding standards** for your team
- **Adjust performance budgets** based on your requirements
- **Add project-specific context** and constraints

### 3. Verify Setup

**Cursor:** Check that cursor.mdc appears in the Agent sidebar and loads automatically
**Replit:** Verify Agent automatically reads the configuration
**Lovable:** Check that your Instructions/Knowledge appear in the project settings and AI responses follow the standards
**Windsurf:** Ensure enterprise workflow patterns are recognized

## 📋 Development Workflow

All configurations enforce a **three-phase development approach**:

### Phase 1: Planning
- **MUST** describe proposed changes before implementing
- **MUST** await explicit confirmation before making changes
- Ask numbered clarifying questions with sensible defaults
- Challenge approaches if simpler alternatives exist
- Ensure idiomatic React + TypeScript patterns

### Phase 2: Implementation
- Begin ONLY with explicit instruction to implement changes
- Make small, incremental changes that are easy to test and verify
- Stay strictly focused on the agreed-upon task
- Stop and ask questions if changes become larger than expected
- Never implement anticipated future features without approval

### Phase 3: Review
- Review implemented changes and check for issues
- Identify opportunities to remove or simplify existing code
- Complete code review and identify technical debt
- Wait for explicit direction before starting new work
- Raise improvement ideas for next planning phase

## 🧪 Testing Requirements

All configurations mandate comprehensive testing:

### Accessibility Testing
```typescript
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

it('should be accessible', async () => {
  const { container } = render(<Component />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

### Performance Testing
```typescript
// Bundle size limits
- Component bundle: ≤25KB gzipped per route
- Initial page load: ≤150KB gzipped React bundle

// Core Web Vitals targets
- LCP: <2.5 seconds
- FID: <100 milliseconds  
- CLS: <0.1
```

## 🚫 Failure Conditions

All platforms are configured to **refuse** generating code that:

❌ Violates WCAG 2.2 AA accessibility standards  
❌ Compromises maintainability (unclear, complex code)  
❌ Harms performance or sustainability  
❌ Includes security vulnerabilities  
❌ Bypasses TypeScript safety features  
❌ Uses deprecated React patterns  
❌ Missing proper error handling  
❌ Violates the three-phase workflow

## 🛠️ TypeScript Configuration

Required `tsconfig.json` settings:

```json
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
    "forceConsistentCasingInFileNames": true
  }
}
```

## 📖 Component Example

All configurations enforce this component pattern:

```typescript
/**
 * Accessible button component following WCAG 2.2 guidelines
 * 
 * @param children - Button content
 * @param onClick - Click handler function
 * @param variant - Button style variant
 * @param disabled - Whether button is disabled
 * @param ariaLabel - Accessible label for screen readers
 * 
 * @example
 * ```tsx
 * <Button variant="primary" onClick={handleSave} ariaLabel="Save document">
 *   Save Changes
 * </Button>
 * ```
 */
interface ButtonProps {
  readonly children: React.ReactNode;
  readonly onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
  readonly variant?: 'primary' | 'secondary' | 'danger';
  readonly disabled?: boolean;
  readonly ariaLabel?: string;
}

export const Button: React.FC<ButtonProps> = React.memo(({
  children,
  onClick,
  variant = 'primary',
  disabled = false,
  ariaLabel,
  ...restProps
}) => {
  const handleClick = useCallback((event: React.MouseEvent<HTMLButtonElement>) => {
    if (!disabled && onClick) {
      onClick(event);
    }
  }, [disabled, onClick]);

  return (
    <button
      onClick={handleClick}
      disabled={disabled}
      aria-label={ariaLabel}
      className={`btn btn--${variant}`}
      type="button"
      {...restProps}
    >
      {children}
    </button>
  );
});

Button.displayName = 'Button';
```

## 🔧 Platform-Specific Features

### Cursor Rules Features
- **Semantic Markup Focus**: Comprehensive HTML/JSX patterns for accessible, secure applications
- **Production-Ready Examples**: Complete components (forms, modals, tables, buttons, images)
- **WCAG 2.2 AA Compliance**: Built-in accessibility patterns and ARIA implementation
- **Security-First**: XSS prevention, safe content rendering, input validation
- **Performance Optimized**: Virtualization, lazy loading, efficient rendering patterns

### Replit Features
- **Automatic Detection**: Agent automatically reads `replit.md` from project root
- **Four Core Pillars**: Accessibility, Security, Maintainability, Sustainability
- **Three-Phase Workflow**: Structured development process
- **Performance Budgets**: Specific bundle size and Core Web Vitals targets

### Lovable Features
- **Settings Integration**: Add configuration directly to project Instructions/Knowledge
- **Three-Pillar Focus**: Maintainability, Accessibility, Sustainability
- **Production Standards**: Enterprise-ready code patterns
- **Green Software**: Environmental impact considerations
- **Comprehensive Examples**: Detailed React + TypeScript patterns

### Windsurf Features
- **Rules Directory Integration**: Following [Windsurf's curated best practices](https://windsurf.com/editor/directory)
- **Enterprise Scale**: Optimized for large, distributed teams
- **Four Essential Pillars**: Complete coverage of quality standards
- **Advanced Patterns**: Complex component and architecture guidance
- **Strict Workflow**: Three-phase approach with quality gates

## 🧠 Prompt Engineering Principles

All configurations follow established prompt engineering best practices:

### **Role Definition**
Each platform configuration clearly defines the AI assistant's role as a specialist developer for that specific platform.

### **Context Setting**
Comprehensive context about:
- Target application scale and complexity
- Team structure and maintenance requirements
- User diversity and accessibility needs
- Long-term sustainability goals

### **Implementation Examples**
Extensive code examples demonstrating:
- Component and hook patterns
- Accessibility implementations
- Security practices
- Performance optimizations

### **Clear Constraints**
Explicit boundaries defining:
- What to never do (anti-patterns)
- What to always do (required practices)
- Failure conditions that trigger refusal
- Priority guidance for conflict resolution

## 🤝 Contributing

To contribute to this project:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/improvement`)
3. **Follow the development workflow** (Plan → Implement → Review)
4. **Ensure all configurations** maintain the four pillars
5. **Test with your preferred AI platform**
6. **Submit a pull request**

## 📜 License

MIT License - see LICENSE file for details.

## 🔗 References

- [Cursor Rules Documentation](https://docs.cursor.com/context/rules)
- [Replit.md Documentation](https://docs.replit.com/replitai/replit-dot-md)
- [Lovable Knowledge Features](https://docs.lovable.dev/features/knowledge)
- [Windsurf Rules Directory](https://windsurf.com/editor/directory)
- [WCAG 2.2 Guidelines](https://www.w3.org/WAI/WCAG22/quickref/)
- [React TypeScript Best Practices](https://react-typescript-cheatsheet.netlify.app/)
- [Prompt Engineering Guide](https://www.promptingguide.ai/)

---

**Remember:** Every decision should align with our four pillars - Accessibility, Security, Maintainability, and Sustainability. When in doubt, prioritize user experience and code quality over quick implementation. 