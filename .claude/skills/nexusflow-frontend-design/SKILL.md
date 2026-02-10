---
name: nexusflow-frontend-design
description: Provides the NexusFlow design system components, patterns, and guidelines for building consistent, accessible, and beautiful user interfaces.
---

# NexusFlow Frontend Design System

## Capabilities

- Apply NexusFlow design tokens
- Generate component code
- Ensure accessibility compliance
- Maintain visual consistency
- Create responsive layouts
- Apply interaction patterns

## Design Tokens

### Colors

```css
/* Primary Palette */
--nf-primary-50: #EFF6FF;
--nf-primary-100: #DBEAFE;
--nf-primary-200: #BFDBFE;
--nf-primary-300: #93C5FD;
--nf-primary-400: #60A5FA;
--nf-primary-500: #3B82F6;  /* Primary */
--nf-primary-600: #2563EB;  /* Primary Dark */
--nf-primary-700: #1D4ED8;
--nf-primary-800: #1E40AF;
--nf-primary-900: #1E3A8A;

/* Semantic Colors */
--nf-success: #10B981;
--nf-success-light: #D1FAE5;
--nf-warning: #F59E0B;
--nf-warning-light: #FEF3C7;
--nf-error: #EF4444;
--nf-error-light: #FEE2E2;
--nf-info: #3B82F6;
--nf-info-light: #DBEAFE;

/* Neutral Palette */
--nf-gray-50: #F9FAFB;
--nf-gray-100: #F3F4F6;
--nf-gray-200: #E5E7EB;
--nf-gray-300: #D1D5DB;
--nf-gray-400: #9CA3AF;
--nf-gray-500: #6B7280;
--nf-gray-600: #4B5563;
--nf-gray-700: #374151;
--nf-gray-800: #1F2937;
--nf-gray-900: #111827;

/* Background */
--nf-bg-primary: #FFFFFF;
--nf-bg-secondary: #F9FAFB;
--nf-bg-tertiary: #F3F4F6;

/* Text */
--nf-text-primary: #111827;
--nf-text-secondary: #6B7280;
--nf-text-tertiary: #9CA3AF;
--nf-text-inverse: #FFFFFF;
```

### Typography

```css
/* Font Family */
--nf-font-sans: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
--nf-font-mono: 'JetBrains Mono', 'Fira Code', monospace;

/* Font Sizes */
--nf-text-xs: 0.75rem;     /* 12px */
--nf-text-sm: 0.875rem;    /* 14px */
--nf-text-base: 1rem;      /* 16px */
--nf-text-lg: 1.125rem;    /* 18px */
--nf-text-xl: 1.25rem;     /* 20px */
--nf-text-2xl: 1.5rem;     /* 24px */
--nf-text-3xl: 1.875rem;   /* 30px */
--nf-text-4xl: 2.25rem;    /* 36px */

/* Font Weights */
--nf-font-normal: 400;
--nf-font-medium: 500;
--nf-font-semibold: 600;
--nf-font-bold: 700;

/* Line Heights */
--nf-leading-tight: 1.25;
--nf-leading-normal: 1.5;
--nf-leading-relaxed: 1.75;
```

### Spacing

```css
/* Based on 4px grid */
--nf-space-0: 0;
--nf-space-1: 0.25rem;   /* 4px */
--nf-space-2: 0.5rem;    /* 8px */
--nf-space-3: 0.75rem;   /* 12px */
--nf-space-4: 1rem;      /* 16px */
--nf-space-5: 1.25rem;   /* 20px */
--nf-space-6: 1.5rem;    /* 24px */
--nf-space-8: 2rem;      /* 32px */
--nf-space-10: 2.5rem;   /* 40px */
--nf-space-12: 3rem;     /* 48px */
--nf-space-16: 4rem;     /* 64px */
--nf-space-20: 5rem;     /* 80px */
```

### Shadows

```css
--nf-shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
--nf-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
--nf-shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
--nf-shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
--nf-shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
```

### Border Radius

```css
--nf-radius-sm: 0.25rem;   /* 4px */
--nf-radius: 0.375rem;     /* 6px */
--nf-radius-md: 0.5rem;    /* 8px */
--nf-radius-lg: 0.75rem;   /* 12px */
--nf-radius-xl: 1rem;      /* 16px */
--nf-radius-full: 9999px;
```

## Component Library

### Button

```tsx
// Button variants
<Button variant="primary">Primary Action</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="outline">Outline</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="destructive">Delete</Button>

// Button sizes
<Button size="sm">Small</Button>
<Button size="md">Medium</Button>
<Button size="lg">Large</Button>

// With icon
<Button>
  <PlusIcon className="mr-2 h-4 w-4" />
  Add Workflow
</Button>
```

### Input

```tsx
// Basic input
<Input placeholder="Enter workflow name" />

// With label and error
<div className="space-y-2">
  <Label htmlFor="name">Workflow Name</Label>
  <Input id="name" error={errors.name} />
  {errors.name && (
    <p className="text-sm text-error">{errors.name}</p>
  )}
</div>

// Input with icon
<div className="relative">
  <SearchIcon className="absolute left-3 top-1/2 -translate-y-1/2 h-4 w-4 text-gray-400" />
  <Input className="pl-10" placeholder="Search..." />
</div>
```

### Card

```tsx
<Card>
  <CardHeader>
    <CardTitle>Workflow Performance</CardTitle>
    <CardDescription>Last 30 days</CardDescription>
  </CardHeader>
  <CardContent>
    {/* Content */}
  </CardContent>
  <CardFooter>
    <Button variant="outline">View Details</Button>
  </CardFooter>
</Card>
```

### Data Table

```tsx
<Table>
  <TableHeader>
    <TableRow>
      <TableHead>Name</TableHead>
      <TableHead>Status</TableHead>
      <TableHead>Last Run</TableHead>
      <TableHead className="text-right">Actions</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    {workflows.map((workflow) => (
      <TableRow key={workflow.id}>
        <TableCell className="font-medium">{workflow.name}</TableCell>
        <TableCell>
          <Badge variant={workflow.status}>{workflow.status}</Badge>
        </TableCell>
        <TableCell>{workflow.lastRun}</TableCell>
        <TableCell className="text-right">
          <DropdownMenu>...</DropdownMenu>
        </TableCell>
      </TableRow>
    ))}
  </TableBody>
</Table>
```

## Layout Patterns

### Page Layout

```tsx
<div className="min-h-screen bg-nf-bg-secondary">
  {/* Sidebar */}
  <aside className="fixed inset-y-0 left-0 w-64 bg-white border-r">
    <Sidebar />
  </aside>

  {/* Main Content */}
  <main className="ml-64">
    {/* Header */}
    <header className="sticky top-0 z-10 bg-white border-b px-6 py-4">
      <PageHeader />
    </header>

    {/* Content */}
    <div className="p-6">
      <PageContent />
    </div>
  </main>
</div>
```

### Dashboard Grid

```tsx
<div className="grid gap-6 md:grid-cols-2 lg:grid-cols-4">
  <MetricCard title="Total Workflows" value="127" change="+12%" />
  <MetricCard title="Active Users" value="3,240" change="+8%" />
  <MetricCard title="Success Rate" value="94.2%" change="+2.1%" />
  <MetricCard title="Avg Run Time" value="1.2s" change="-0.3s" />
</div>
```

## Accessibility

### WCAG 2.1 AA Compliance

| Requirement | Implementation |
|-------------|----------------|
| Color Contrast | 4.5:1 minimum for text |
| Focus Indicators | Visible focus ring on all interactive |
| Keyboard Navigation | Full keyboard support |
| Screen Readers | ARIA labels and roles |
| Motion | Respect prefers-reduced-motion |

### Focus States

```css
/* Focus visible for keyboard navigation */
:focus-visible {
  outline: 2px solid var(--nf-primary-500);
  outline-offset: 2px;
}

/* Remove default outline when not keyboard navigating */
:focus:not(:focus-visible) {
  outline: none;
}
```

### ARIA Patterns

```tsx
// Accessible button
<button
  aria-label="Close dialog"
  aria-pressed={isPressed}
>
  <XIcon aria-hidden="true" />
</button>

// Accessible alert
<div role="alert" aria-live="polite">
  {message}
</div>

// Accessible modal
<Dialog
  aria-labelledby="dialog-title"
  aria-describedby="dialog-description"
>
  <h2 id="dialog-title">Confirm Delete</h2>
  <p id="dialog-description">This action cannot be undone.</p>
</Dialog>
```

## Animation

### Transitions

```css
/* Standard transition */
--nf-transition: 150ms cubic-bezier(0.4, 0, 0.2, 1);

/* Hover transitions */
.hover-lift {
  transition: transform var(--nf-transition), box-shadow var(--nf-transition);
}
.hover-lift:hover {
  transform: translateY(-2px);
  box-shadow: var(--nf-shadow-lg);
}
```

### Loading States

```tsx
// Spinner
<div className="animate-spin h-5 w-5 border-2 border-primary border-t-transparent rounded-full" />

// Skeleton
<div className="animate-pulse space-y-3">
  <div className="h-4 bg-gray-200 rounded w-3/4" />
  <div className="h-4 bg-gray-200 rounded w-1/2" />
</div>
```

## Responsive Breakpoints

```css
/* Mobile first approach */
--nf-screen-sm: 640px;   /* Small devices */
--nf-screen-md: 768px;   /* Tablets */
--nf-screen-lg: 1024px;  /* Laptops */
--nf-screen-xl: 1280px;  /* Desktops */
--nf-screen-2xl: 1536px; /* Large screens */
```

## Integration

| Agent | Usage |
|-------|-------|
| ai-frontend-engineer | Component implementation |
| ai-product-designer | Design decisions |

## Metadata

- **Owner**: Design Team
- **Created**: 2025-05-01
- **Updated**: 2026-01-15
- **Figma**: https://figma.com/nexusflow/design-system
