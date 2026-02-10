# Frontend Rules

> Guidelines and best practices for NexusFlow frontend development.

## Overview

NexusFlow frontend is built with Next.js 14, TypeScript, and TailwindCSS. These rules ensure consistency, performance, and maintainability.

---

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Next.js | 14.x | React framework |
| TypeScript | 5.x | Type safety |
| TailwindCSS | 3.x | Styling |
| React Query | 5.x | Server state |
| Zustand | 4.x | Client state |
| React Hook Form | 7.x | Forms |
| Zod | 3.x | Validation |

---

## Project Structure

```
src/
├── app/                    # Next.js App Router
│   ├── (auth)/            # Auth route group
│   ├── (dashboard)/       # Dashboard route group
│   └── api/               # API routes
├── components/
│   ├── ui/                # Primitive components
│   ├── features/          # Feature components
│   └── layouts/           # Layout components
├── hooks/                 # Custom hooks
├── lib/                   # Utilities
├── services/              # API clients
├── stores/                # Zustand stores
└── types/                 # TypeScript types
```

---

## Component Guidelines

### Component Structure

```tsx
// components/features/workflow/WorkflowCard.tsx

import { memo } from 'react';
import { cn } from '@/lib/utils';
import type { Workflow } from '@/types';

interface WorkflowCardProps {
  workflow: Workflow;
  onActivate?: (id: string) => void;
  className?: string;
}

export const WorkflowCard = memo(function WorkflowCard({
  workflow,
  onActivate,
  className,
}: WorkflowCardProps) {
  return (
    <div className={cn('rounded-lg border p-4', className)}>
      <h3 className="font-semibold">{workflow.name}</h3>
      <p className="text-sm text-muted-foreground">
        {workflow.description}
      </p>
      {onActivate && (
        <button onClick={() => onActivate(workflow.id)}>
          Activate
        </button>
      )}
    </div>
  );
});
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `WorkflowCard.tsx` |
| Hooks | camelCase with use | `useWorkflows.ts` |
| Utils | camelCase | `formatDate.ts` |
| Types | PascalCase | `Workflow`, `WorkflowStatus` |
| Constants | SCREAMING_SNAKE | `MAX_WORKFLOWS` |

### File Organization

```
WorkflowCard/
├── index.ts              # Public exports
├── WorkflowCard.tsx      # Main component
├── WorkflowCard.test.tsx # Tests
└── WorkflowCard.stories.tsx # Storybook
```

---

## State Management

### Server State (React Query)

```tsx
// hooks/useWorkflows.ts
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
import { workflowService } from '@/services/workflow';

export function useWorkflows() {
  return useQuery({
    queryKey: ['workflows'],
    queryFn: workflowService.list,
    staleTime: 5 * 60 * 1000, // 5 minutes
  });
}

export function useCreateWorkflow() {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: workflowService.create,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['workflows'] });
    },
  });
}
```

### Client State (Zustand)

```tsx
// stores/uiStore.ts
import { create } from 'zustand';

interface UIState {
  sidebarOpen: boolean;
  toggleSidebar: () => void;
}

export const useUIStore = create<UIState>((set) => ({
  sidebarOpen: true,
  toggleSidebar: () => set((s) => ({ sidebarOpen: !s.sidebarOpen })),
}));
```

### State Guidelines

| State Type | Solution | Example |
|------------|----------|---------|
| Server data | React Query | Workflows, contacts |
| Form state | React Hook Form | Create workflow form |
| UI state | Zustand | Sidebar, modals |
| URL state | Next.js router | Filters, pagination |

---

## Styling

### TailwindCSS Usage

```tsx
// ✅ Good: Utility classes with cn()
<div className={cn(
  'rounded-lg border bg-card p-4',
  isActive && 'border-primary',
  className
)}>

// ❌ Bad: Inline styles
<div style={{ borderRadius: 8, padding: 16 }}>
```

### Design Tokens

```tsx
// Use design system tokens from tailwind.config.js
<div className="bg-background text-foreground">
  <h1 className="text-primary">Title</h1>
  <p className="text-muted-foreground">Description</p>
</div>
```

### Responsive Design

```tsx
// Mobile-first approach
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  {/* Content */}
</div>
```

---

## Forms

### React Hook Form + Zod

```tsx
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const workflowSchema = z.object({
  name: z.string().min(1, 'Name is required').max(100),
  description: z.string().optional(),
  triggerType: z.enum(['manual', 'scheduled', 'webhook']),
});

type WorkflowFormData = z.infer<typeof workflowSchema>;

export function WorkflowForm() {
  const form = useForm<WorkflowFormData>({
    resolver: zodResolver(workflowSchema),
    defaultValues: {
      name: '',
      triggerType: 'manual',
    },
  });

  const onSubmit = (data: WorkflowFormData) => {
    // Handle submission
  };

  return (
    <form onSubmit={form.handleSubmit(onSubmit)}>
      {/* Form fields */}
    </form>
  );
}
```

---

## API Integration

### Service Layer

```tsx
// services/workflow.ts
import { api } from '@/lib/api';
import type { Workflow, CreateWorkflowDTO } from '@/types';

export const workflowService = {
  list: async (): Promise<Workflow[]> => {
    const { data } = await api.get('/workflows');
    return data;
  },

  create: async (dto: CreateWorkflowDTO): Promise<Workflow> => {
    const { data } = await api.post('/workflows', dto);
    return data;
  },

  activate: async (id: string): Promise<Workflow> => {
    const { data } = await api.post(`/workflows/${id}/activate`);
    return data;
  },
};
```

### Error Handling

```tsx
// Global error boundary
export function ErrorBoundary({ children }: { children: React.ReactNode }) {
  return (
    <QueryErrorResetBoundary>
      {({ reset }) => (
        <ErrorBoundaryComponent onReset={reset} fallback={<ErrorFallback />}>
          {children}
        </ErrorBoundaryComponent>
      )}
    </QueryErrorResetBoundary>
  );
}

// Component-level error handling
export function WorkflowList() {
  const { data, error, isLoading } = useWorkflows();

  if (error) return <ErrorMessage error={error} />;
  if (isLoading) return <Skeleton />;

  return <WorkflowGrid workflows={data} />;
}
```

---

## Performance

### Code Splitting

```tsx
// Lazy load heavy components
const WorkflowBuilder = dynamic(
  () => import('@/components/features/workflow/WorkflowBuilder'),
  { loading: () => <Skeleton /> }
);
```

### Memoization

```tsx
// Memoize expensive computations
const sortedWorkflows = useMemo(
  () => workflows.sort((a, b) => b.runCount - a.runCount),
  [workflows]
);

// Memoize callbacks
const handleActivate = useCallback((id: string) => {
  activateMutation.mutate(id);
}, [activateMutation]);
```

### Image Optimization

```tsx
import Image from 'next/image';

<Image
  src="/logo.png"
  alt="NexusFlow"
  width={120}
  height={40}
  priority // Above the fold
/>
```

---

## Accessibility

### ARIA Guidelines

```tsx
// Accessible button
<button
  aria-label="Activate workflow"
  aria-pressed={isActive}
  onClick={handleActivate}
>
  {isActive ? 'Active' : 'Activate'}
</button>

// Accessible form
<label htmlFor="workflow-name">Name</label>
<input
  id="workflow-name"
  aria-required="true"
  aria-invalid={!!errors.name}
  aria-describedby="name-error"
/>
{errors.name && (
  <span id="name-error" role="alert">
    {errors.name.message}
  </span>
)}
```

### Keyboard Navigation

```tsx
// Support keyboard interactions
<div
  role="button"
  tabIndex={0}
  onKeyDown={(e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      handleClick();
    }
  }}
  onClick={handleClick}
>
  Click me
</div>
```

---

## Testing

### Component Tests

```tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { WorkflowCard } from './WorkflowCard';

describe('WorkflowCard', () => {
  const workflow = {
    id: '1',
    name: 'Test Workflow',
    status: 'active',
  };

  it('renders workflow name', () => {
    render(<WorkflowCard workflow={workflow} />);
    expect(screen.getByText('Test Workflow')).toBeInTheDocument();
  });

  it('calls onActivate when button clicked', async () => {
    const onActivate = jest.fn();
    render(<WorkflowCard workflow={workflow} onActivate={onActivate} />);

    await userEvent.click(screen.getByRole('button'));
    expect(onActivate).toHaveBeenCalledWith('1');
  });
});
```

### Hook Tests

```tsx
import { renderHook, waitFor } from '@testing-library/react';
import { useWorkflows } from './useWorkflows';

describe('useWorkflows', () => {
  it('fetches workflows', async () => {
    const { result } = renderHook(() => useWorkflows(), {
      wrapper: QueryClientProvider,
    });

    await waitFor(() => expect(result.current.isSuccess).toBe(true));
    expect(result.current.data).toHaveLength(3);
  });
});
```

---

## Code Quality

### ESLint Rules

```json
{
  "extends": ["next/core-web-vitals", "prettier"],
  "rules": {
    "react/prop-types": "off",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "@typescript-eslint/no-unused-vars": "error",
    "@typescript-eslint/explicit-function-return-type": "off"
  }
}
```

### Prettier Config

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80
}
```

---

*Document Owner: Frontend Team*
*Last Updated: January 2026*
