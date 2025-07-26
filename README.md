# Vibe Coding Instruct

**Production-ready React + TypeScript development standards for AI coding platforms**

A comprehensive collection of configuration files that ensure consistent, high-quality React + TypeScript development across multiple AI coding platforms. This project provides unified standards focusing on accessibility, security, maintainability, and sustainability.

## 🎯 Project Overview

This repository contains meticulously crafted configuration files for three major AI coding platforms, each optimized for React + TypeScript development:

- **[Cursor Rules](#cursor-rules)** - Advanced project rules for Cursor IDE
- **[Replit Configuration](#replit-configuration)** - Agent behavior customization for Replit
- **[Lovable Standards](#lovable-standards)** - Development standards for Lovable platform

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
├── .cursor/
│   └── rules/
│       ├── always-apply/
│       │   ├── core-principles.mdc
│       │   └── typescript-standards.mdc
│       └── file-specific/
│           ├── components.mdc
│           └── hooks.mdc
├── replit.md
├── lovable.md
└── README.md
```

## 🎨 Platform Configurations

### Cursor Rules

Based on [Cursor's Rules documentation](https://docs.cursor.com/context/rules), our configuration provides:

**Always Apply Rules:**
- `core-principles.mdc` - Non-negotiable React + TypeScript principles
- `typescript-standards.mdc` - Strict TypeScript patterns with React examples

**File-Specific Rules:**
- `components.mdc` - React component patterns with accessibility focus
- `hooks.mdc` - Custom hook patterns with proper TypeScript typing

**Features:**
- **Plan → Implement → Review workflow** enforced in core principles
- **MDC format** with metadata for rule scoping
- **Automatic application** based on file patterns
- **Version-controlled** rules in `.cursor/rules`

### Replit Configuration

Following [Replit's replit.md documentation](https://docs.replit.com/replitai/replit-dot-md), our `replit.md` includes:

**Comprehensive Project Guidance:**
- Technology stack preferences (React, TypeScript, testing frameworks)
- Four core pillars with specific implementation requirements
- Development workflow with three-phase approach
- Performance budgets and bundle size limits

**AI Agent Behavior:**
- Communication style preferences
- Code review requirements
- Error handling standards
- Forbidden patterns with clear refusal conditions

### Lovable Standards

Optimized for [Lovable's knowledge features](https://docs.lovable.dev/features/knowledge), our `lovable.md` focuses on:

**Three Binding Pillars:**
1. **MAINTAINABILITY** - Code that lasts and scales
2. **ACCESSIBILITY** - WCAG 2.2 AA compliance
3. **SUSTAINABILITY** - Green software engineering

**Production-Ready Patterns:**
- Detailed component and hook examples
- Accessibility-first development approach
- Performance optimization with Core Web Vitals targets
- Comprehensive testing requirements

## 🚀 Quick Start

### 1. Choose Your Platform

**For Cursor IDE:**
```bash
# Copy the .cursor directory to your project root
cp -r .cursor/ /path/to/your/project/
```

**For Replit:**
```bash
# Copy replit.md to your project root
cp replit.md /path/to/your/project/
```

**For Lovable:**
```bash
# Copy lovable.md to your project root
cp lovable.md /path/to/your/project/
```

### 2. Customize for Your Project

Each configuration file can be customized:

- **Update technology stack** preferences
- **Modify coding standards** for your team
- **Adjust performance budgets** based on your requirements
- **Add project-specific context** and constraints

### 3. Verify Setup

**Cursor:** Check that rules appear in the Agent sidebar
**Replit:** Verify Agent automatically reads the configuration
**Lovable:** Confirm the platform applies the development standards

## 📋 Development Workflow

All configurations enforce a **three-phase development approach**:

### Phase 1: Planning
- Describe proposed changes before implementing
- Ask clarifying questions with numbered items
- Challenge approaches if simpler alternatives exist
- Ensure idiomatic React + TypeScript patterns

### Phase 2: Implementation
- Make small, incremental changes
- Stay focused on agreed-upon tasks
- Stop and ask questions if scope expands
- Never implement anticipated features without approval

### Phase 3: Review
- Review implemented changes for issues
- Identify opportunities to simplify code
- Complete code review and identify technical debt
- Wait for explicit direction before starting new work

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
- Initial page load: ≤50KB gzipped React bundle

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
 */
interface ButtonProps {
  readonly children: React.ReactNode;
  readonly onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
  readonly variant?: 'primary' | 'secondary' | 'danger';
  readonly disabled?: boolean;
  readonly ariaLabel?: string;
}

export const Button: React.FC<ButtonProps> = ({
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

Button.displayName = 'Button';
```

## 🔧 Platform-Specific Features

### Cursor Rules Features
- **Rule Types**: Always, Auto Attached, Agent Requested, Manual
- **File Scoping**: Automatic attachment based on glob patterns
- **Nested Rules**: Directory-specific rule organization
- **Rule Generation**: Create rules directly from chat conversations

### Replit Features
- **Automatic Detection**: Agent automatically reads `replit.md` from project root
- **Dynamic Updates**: Agent can update the file as it learns about your project
- **Web Search Integration**: Combines external research with project-specific guidance
- **Context Scope**: Provides context for Agent conversations

### Lovable Features
- **Three-Pillar Focus**: Maintainability, Accessibility, Sustainability
- **Production Standards**: Enterprise-ready code patterns
- **Performance Budgets**: Specific bundle size and Core Web Vitals targets
- **Green Software**: Environmental impact considerations

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
- [WCAG 2.2 Guidelines](https://www.w3.org/WAI/WCAG22/quickref/)
- [React TypeScript Best Practices](https://react-typescript-cheatsheet.netlify.app/)

---

**Remember:** Every decision should align with our four pillars - Accessibility, Security, Maintainability, and Sustainability. When in doubt, prioritize user experience and code quality over quick implementation. 