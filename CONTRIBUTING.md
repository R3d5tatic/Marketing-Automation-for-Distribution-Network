# Contributing to Marketing Automation for Distribution Network

Welcome to the **Marketing Automation for Distribution Network** project! This guide will help you understand the project architecture, design system, and best practices for contributing as we scale.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Getting Started](#getting-started)
- [Project Architecture](#project-architecture)
- [Design System](#design-system)
- [Development Workflow](#development-workflow)
- [Code Standards](#code-standards)
- [Feature Development](#feature-development)
- [Testing Guidelines](#testing-guidelines)
- [Pull Request Process](#pull-request-process)
- [Scaling Strategy](#scaling-strategy)

---

## Project Overview

This is a **React + TypeScript + Vite** application designed to automate marketing operations for distribution networks. The platform provides:

- **Dashboard Analytics**: Real-time metrics and KPIs for distributors
- **Data Scraping**: Automated customer data collection and management
- **Email Automation**: Targeted email campaigns for customer segments
- **Social Media Management**: AI-powered content generation for Instagram, TikTok, and YouTube
- **Product Catalog**: Centralized product management and inventory

### Tech Stack

- **Frontend**: React 19.2, TypeScript 5.8
- **Routing**: React Router DOM 7.9
- **Build Tool**: Vite 6.2
- **UI Components**: Custom components with Glass Morphism design
- **Icons**: Phosphor Icons (Duotone variant)
- **Charts**: Recharts 3.5
- **Styling**: CSS Variables + Utility Classes

---

## Getting Started

### Prerequisites

- **Node.js** (v18+ recommended)
- **npm** or **yarn**
- **Git**

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd Marketing-Automation-for-Distribution-Network

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

### Environment Setup

Create a `.env.local` file in the root directory:

```env
GEMINI_API_KEY=your_api_key_here
```

---

## Project Architecture

We follow the **Bulletproof React** architecture pattern for scalability and maintainability. As the project grows, we'll transition from the current flat structure to a feature-based architecture.

### Current Structure

```
Marketing-Automation-for-Distribution-Network/
├── components/          # Shared components
│   ├── Layout.tsx
│   └── StatsCard.tsx
├── pages/              # Route components
│   ├── Dashboard.tsx
│   ├── Scraping.tsx
│   ├── EmailAutomation.tsx
│   ├── SocialMedia.tsx
│   └── Products.tsx
├── types.ts            # Shared TypeScript types
├── App.tsx             # Main application component
├── index.tsx           # Application entry point
├── index.html          # HTML template
├── STYLES.md           # Design system documentation
└── vite.config.ts      # Vite configuration
```

### Target Structure (As We Scale)

Following the [Bulletproof React](https://github.com/alan2207/bulletproof-react) pattern:

```
src/
├── app/                # Application layer
│   ├── routes/        # Route definitions
│   ├── App.tsx        # Main app component
│   └── router.tsx     # Router configuration
│
├── assets/            # Static files (images, fonts, etc.)
│
├── components/        # Shared components used across features
│   ├── ui/           # Base UI components (Button, Input, Card, etc.)
│   ├── layout/       # Layout components (Header, Sidebar, Footer)
│   └── common/       # Common components (Loading, Error, etc.)
│
├── config/           # Global configurations and env variables
│   └── constants.ts
│
├── features/         # Feature-based modules
│   ├── dashboard/
│   │   ├── api/      # Dashboard API calls
│   │   ├── components/  # Dashboard-specific components
│   │   ├── hooks/    # Dashboard-specific hooks
│   │   ├── types/    # Dashboard TypeScript types
│   │   └── utils/    # Dashboard utility functions
│   │
│   ├── email-automation/
│   │   ├── api/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── types/
│   │   └── utils/
│   │
│   ├── social-media/
│   ├── scraping/
│   └── products/
│
├── hooks/            # Shared hooks
│   ├── useAuth.ts
│   ├── useLocalStorage.ts
│   └── useDebounce.ts
│
├── lib/              # Third-party library configurations
│   ├── axios.ts
│   └── react-query.ts
│
├── stores/           # Global state management (if needed)
│   └── authStore.ts
│
├── styles/           # Global styles
│   ├── base.css
│   ├── variables.css
│   ├── utilities.css
│   ├── components.css
│   └── animations.css
│
├── types/            # Shared TypeScript types
│   ├── api.ts
│   └── common.ts
│
└── utils/            # Shared utility functions
    ├── format.ts
    ├── validation.ts
    └── helpers.ts
```

### Key Architectural Principles

1. **Feature-Based Organization**: Group related code by feature, not by file type
2. **Colocation**: Keep related files close together
3. **Separation of Concerns**: Each feature is self-contained
4. **No Cross-Feature Imports**: Features should not import from each other
5. **Composition Over Inheritance**: Compose features at the application level

---

## Design System

Our design system is based on **Glass Morphism + Neon Aesthetics**. All design tokens and guidelines are documented in [STYLES.md](./STYLES.md).

### Core Principles

- **Dark backgrounds** with frosted glass overlays
- **Cyan neon accents** (`#00d6cb`) for highlights and CTAs
- **Clean typography** using Exo 2 font family
- **Smooth animations** and transitions
- **Consistent spacing** using the spacing scale

### Using the Design System

#### CSS Variables

Always use CSS variables instead of hardcoded values:

```css
/* ❌ Bad */
.my-button {
  background: rgba(0, 214, 203, 0.15);
  color: #00d6cb;
  border-radius: 8px;
}

/* ✅ Good */
.my-button {
  background: var(--color-primary-alpha-15);
  color: var(--color-primary);
  border-radius: var(--radius-base);
}
```

#### Utility Classes

Use predefined utility classes when available:

```tsx
// Glass card with neon border
<div className="glass-card">
  <h3>Card Title</h3>
  <p>Card content...</p>
</div>

// Neon button
<button className="neon-button-glass">
  Click Me
</button>

// Gradient text
<h1 className="gradient-text">Highlighted Heading</h1>
```

#### Icons

Use **Phosphor Icons Duotone** variant exclusively:

```tsx
import { PiRobotDuotone, PiEnvelopeDuotone } from 'react-icons/pi';

function MyComponent() {
  return (
    <div className="icon-container">
      <PiRobotDuotone size={32} className="icon-glow" />
    </div>
  );
}
```

**Icon Size Guidelines:**
- Feature grids & cards: 48px
- Section headers: 32px
- Card icons: 20-24px
- Navigation: 16px
- Inline text: 14-16px

---

## Development Workflow

### Branch Strategy

- `main` - Production-ready code
- `develop` - Integration branch for features
- `feature/feature-name` - Feature development
- `fix/bug-description` - Bug fixes
- `refactor/description` - Code refactoring

### Commit Convention

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add email template builder
fix: resolve chart rendering issue on mobile
refactor: reorganize dashboard components
docs: update contributing guidelines
style: apply glass morphism to product cards
test: add unit tests for customer segmentation
```

### Development Process

1. **Create a branch** from `develop`
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** following code standards

3. **Test your changes** locally
   ```bash
   npm run dev
   ```

4. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat: add your feature description"
   ```

5. **Push to remote**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create a Pull Request** to `develop`

---

## Code Standards

### TypeScript

- **Always use TypeScript** - No `.js` or `.jsx` files
- **Define types** for all props, state, and API responses
- **Use interfaces** for object shapes
- **Avoid `any`** - Use `unknown` if type is truly unknown

```tsx
// ✅ Good
interface CustomerCardProps {
  customer: Customer;
  onSelect: (id: string) => void;
}

const CustomerCard: React.FC<CustomerCardProps> = ({ customer, onSelect }) => {
  // Component logic
};

// ❌ Bad
const CustomerCard = (props: any) => {
  // Component logic
};
```

### Component Structure

```tsx
import React from 'react';
import { IconComponent } from 'react-icons/pi';
import type { MyComponentProps } from './types';

// 1. Type definitions (if not in separate file)
interface MyComponentProps {
  title: string;
  onAction: () => void;
}

// 2. Component definition
const MyComponent: React.FC<MyComponentProps> = ({ title, onAction }) => {
  // 3. Hooks
  const [state, setState] = React.useState(false);

  // 4. Event handlers
  const handleClick = () => {
    setState(true);
    onAction();
  };

  // 5. Render
  return (
    <div className="glass-card">
      <h3>{title}</h3>
      <button onClick={handleClick}>Action</button>
    </div>
  );
};

// 6. Export
export default MyComponent;
```

### File Naming Conventions

- **Components**: PascalCase - `CustomerCard.tsx`
- **Utilities**: camelCase - `formatDate.ts`
- **Hooks**: camelCase with `use` prefix - `useCustomerData.ts`
- **Types**: PascalCase - `Customer.ts` or `types.ts`
- **Constants**: UPPER_SNAKE_CASE - `API_ENDPOINTS.ts`

### Styling Guidelines

1. **Use CSS Variables** from `STYLES.md`
2. **Mobile-first** responsive design
3. **Use utility classes** when available
4. **Component-specific CSS** should be minimal
5. **Add vendor prefixes** for backdrop-filter

```css
/* Component-specific styles */
.my-component {
  background: var(--glass-bg-medium);
  backdrop-filter: var(--glass-blur-lg);
  -webkit-backdrop-filter: var(--glass-blur-lg); /* Vendor prefix */
  border: 1px solid var(--glass-border-accent);
  border-radius: var(--radius-lg);
  transition: all var(--transition-base) var(--ease-out);
}

/* Responsive */
@media (min-width: 768px) {
  .my-component {
    padding: var(--space-6);
  }
}
```

### ESLint & Prettier

- **ESLint** enforces code quality and standards
- **Prettier** handles code formatting
- **Format on save** should be enabled in your IDE

---

## Feature Development

### Creating a New Feature

When adding a new feature, follow this process:

#### 1. Plan the Feature

- Define the feature scope
- Identify required components
- Plan API integrations
- Design the UI following `STYLES.md`

#### 2. Create Feature Structure

For small features, add to existing structure:

```
pages/
└── NewFeature.tsx

components/
└── NewFeatureCard.tsx
```

For larger features, create a feature module:

```
features/
└── new-feature/
    ├── components/
    │   ├── FeatureCard.tsx
    │   └── FeatureList.tsx
    ├── hooks/
    │   └── useFeatureData.ts
    ├── types/
    │   └── index.ts
    ├── utils/
    │   └── helpers.ts
    └── api/
        └── featureApi.ts
```

#### 3. Define Types

```typescript
// features/new-feature/types/index.ts
export interface FeatureItem {
  id: string;
  name: string;
  status: 'active' | 'inactive';
  createdAt: string;
}

export interface FeatureCardProps {
  item: FeatureItem;
  onSelect: (id: string) => void;
}
```

#### 4. Create Components

```tsx
// features/new-feature/components/FeatureCard.tsx
import React from 'react';
import { PiCheckCircleDuotone } from 'react-icons/pi';
import type { FeatureCardProps } from '../types';

const FeatureCard: React.FC<FeatureCardProps> = ({ item, onSelect }) => {
  return (
    <div className="glass-card p-6 rounded-2xl hover:border-primary/40 transition-all">
      <div className="flex items-center gap-3 mb-4">
        <PiCheckCircleDuotone size={24} className="text-primary" />
        <h3 className="text-lg font-bold text-white">{item.name}</h3>
      </div>
      <button 
        onClick={() => onSelect(item.id)}
        className="neon-button-glass w-full"
      >
        Select
      </button>
    </div>
  );
};

export default FeatureCard;
```

#### 5. Add Route

```tsx
// App.tsx
import NewFeature from './pages/NewFeature';

// Add to routes
<Route path="new-feature" element={<NewFeature />} />
```

#### 6. Update Navigation

```tsx
// components/Layout.tsx
const navItems = [
  // ... existing items
  { path: '/new-feature', label: 'New Feature', icon: PiIconDuotone },
];
```

---

## Testing Guidelines

### Manual Testing Checklist

Before submitting a PR, verify:

- [ ] Feature works in Chrome, Firefox, and Safari
- [ ] Responsive design works on mobile, tablet, and desktop
- [ ] All interactive elements have hover states
- [ ] Loading states are displayed appropriately
- [ ] Error states are handled gracefully
- [ ] Accessibility: keyboard navigation works
- [ ] Accessibility: proper ARIA labels are used
- [ ] No console errors or warnings
- [ ] Design follows `STYLES.md` guidelines

### Future: Automated Testing

As we scale, we'll implement:

- **Unit Tests**: Jest + React Testing Library
- **Integration Tests**: Testing user flows
- **E2E Tests**: Playwright or Cypress
- **Visual Regression Tests**: Chromatic or Percy

---

## Pull Request Process

### PR Checklist

- [ ] Code follows project standards
- [ ] Design matches `STYLES.md` guidelines
- [ ] TypeScript types are properly defined
- [ ] No ESLint errors or warnings
- [ ] Code is properly formatted (Prettier)
- [ ] Responsive design is tested
- [ ] Manual testing completed
- [ ] PR description explains changes
- [ ] Screenshots/videos included (for UI changes)

### PR Template

```markdown
## Description
Brief description of what this PR does.

## Type of Change
- [ ] New feature
- [ ] Bug fix
- [ ] Refactoring
- [ ] Documentation update
- [ ] Style/UI update

## Changes Made
- Change 1
- Change 2
- Change 3

## Screenshots/Videos
(Include for UI changes)

## Testing
- [ ] Tested on Chrome
- [ ] Tested on Firefox
- [ ] Tested on mobile
- [ ] No console errors

## Related Issues
Closes #123
```

### Review Process

1. **Self-review** your code before requesting review
2. **Request review** from at least one team member
3. **Address feedback** promptly and professionally
4. **Merge** only after approval and passing checks

---

## Scaling Strategy

### Phase 1: Current State (MVP)
- Flat structure with `pages/` and `components/`
- Shared types in `types.ts`
- Basic routing and navigation

### Phase 2: Feature Modules (Next Step)
- Migrate to feature-based structure
- Create `features/` directory
- Organize code by domain (dashboard, email, social, etc.)
- Implement absolute imports with `@/` prefix

### Phase 3: Advanced Architecture
- Add state management (Zustand or Redux Toolkit)
- Implement API layer with React Query
- Add authentication and authorization
- Implement error boundaries
- Add logging and monitoring

### Phase 4: Enterprise Scale
- Micro-frontends (if needed)
- Monorepo with Turborepo or Nx
- Shared component library
- Design system package
- CI/CD pipeline with automated testing

### Migration Path

#### Step 1: Set Up Absolute Imports

Update `tsconfig.json`:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
      "@/components/*": ["./src/components/*"],
      "@/features/*": ["./src/features/*"],
      "@/hooks/*": ["./src/hooks/*"],
      "@/utils/*": ["./src/utils/*"],
      "@/types/*": ["./src/types/*"]
    }
  }
}
```

Update `vite.config.ts`:

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
});
```

#### Step 2: Create Feature Modules

Move page-specific code into feature modules:

```bash
# Before
pages/Dashboard.tsx
components/StatsCard.tsx

# After
features/dashboard/
├── components/
│   ├── StatsCard.tsx
│   └── RevenueChart.tsx
├── hooks/
│   └── useDashboardData.ts
└── types/
    └── index.ts
```

#### Step 3: Extract Shared Components

Create a `components/ui/` directory for reusable components:

```
components/
├── ui/
│   ├── Button.tsx
│   ├── Card.tsx
│   ├── Input.tsx
│   └── Select.tsx
└── layout/
    ├── Layout.tsx
    ├── Header.tsx
    └── Sidebar.tsx
```

#### Step 4: Implement ESLint Rules

Prevent cross-feature imports:

```javascript
// .eslintrc.cjs
'import/no-restricted-paths': [
  'error',
  {
    zones: [
      {
        target: './src/features/dashboard',
        from: './src/features',
        except: ['./dashboard'],
      },
      {
        target: './src/features/email-automation',
        from: './src/features',
        except: ['./email-automation'],
      },
      // Add more features...
    ],
  },
],
```

---

## Additional Resources

- [STYLES.md](./STYLES.md) - Complete design system documentation
- [Bulletproof React](https://github.com/alan2207/bulletproof-react) - Architecture reference
- [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/) - TypeScript best practices
- [Phosphor Icons](https://phosphoricons.com/) - Icon library

---

## Questions or Issues?

If you have questions or encounter issues:

1. Check existing documentation
2. Search for similar issues
3. Ask in team chat
4. Create a GitHub issue with detailed description

---

## License

This project is proprietary and confidential. Do not share or distribute without authorization.

---

**Thank you for contributing to the Marketing Automation for Distribution Network project!** 🚀
