# modern-ui

Production-grade React component library. 43 accessible, typed, and tree-shakeable components built on Radix UI + Tailwind CSS v4.

Designed for teams who want shadcn/ui quality with a proper monorepo structure — shared design tokens, Storybook docs, and Vitest coverage included.

## Packages

| Package | Description |
|---|---|
| `packages/ui` | 43 React components — Radix UI + Tailwind CSS v4 + TypeScript strict |
| `packages/tailwind-config` | Shared Tailwind config and PostCSS setup |

## Components

| Category | Components |
|---|---|
| Inputs & Forms | Button, Input, Textarea, Checkbox, Switch, Slider, RadioGroup, Select, InputOTP, Form, **AutoForm** |
| Data Display | **DataTable**, Table, Badge, Avatar, Skeleton, Progress, Card |
| Overlays | Dialog, Sheet, Drawer, Popover, HoverCard, Tooltip |
| Menus | DropdownMenu, ContextMenu, Menubar, Command + CommandDialog |
| Navigation | Breadcrumb, Pagination, NavigationMenu, Tabs |
| Layout | Separator, AspectRatio, ScrollArea, Accordion, Collapsible |
| Feedback | Alert, Toaster |
| Controls | Toggle, ToggleGroup, Calendar |

## Highlights

**AutoForm** — generate a complete, validated form from a Zod schema in one line:

```tsx
import { AutoForm } from '@repo/ui'
import { z } from 'zod'

const schema = z.object({
  name:  z.string().min(2),
  email: z.string().email(),
  role:  z.enum(['admin', 'editor', 'viewer']),
  active: z.boolean(),
})

<AutoForm schema={schema} onSubmit={save} submitText="Save" />
```

**DataTable** — 20+ opt-in features: sorting, filtering, pagination, drag-to-reorder columns, inline cell editing, column-level RBAC, and CSV/JSON export:

```tsx
import { DataTable } from '@repo/ui'
import type { ColumnDef } from '@tanstack/react-table'

const columns: ColumnDef<User>[] = [
  { accessorKey: 'name', header: 'Name' },
  {
    accessorKey: 'role',
    header: 'Role',
    meta: {
      editable: true,
      editType: 'select',
      editOptions: ['admin', 'editor', 'viewer'],
      roles: ['admin', 'hr'],
    },
  },
]

<DataTable
  columns={columns}
  data={users}
  getRowId={(r) => r.id}
  rbac={{ userRole: currentUser.role }}
  features={{ sorting: true, filtering: true, pagination: true, editableCells: true, exportCsv: true }}
/>
```

## Quick start

```sh
pnpm install

# start Storybook
pnpm --filter @repo/ui storybook
# opens at http://localhost:6006

# run tests
pnpm --filter @repo/ui test

# build
pnpm build
```

## Using in your project

```tsx
// import CSS once at app root
import '@repo/ui/styles.css'

// import components
import { Button, DataTable, AutoForm, Card } from '@repo/ui'
```

## Design tokens

All colour, spacing, and radius values are CSS custom properties — override in your global CSS to theme the entire library:

```css
:root {
  --primary: 240 5.9% 10%;
  --radius: 0.5rem;
  /* see packages/ui/src/styles.css for all tokens */
}
```

## Stack

- React 19 · TypeScript strict · Tailwind CSS v4
- Radix UI primitives
- Tanstack Table (DataTable)
- React Hook Form + Zod (Form, AutoForm)
- Framer Motion (animations)
- Vitest + React Testing Library
- Storybook 8

## License

MIT
