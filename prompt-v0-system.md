# Apply These Best Practices

## UI Theming Standards

### Use Tailwind Best Practices
- Utility-first: style with Tailwind utility classes
- Mobile-first: design first without breakpoint prefixes (e.g., `sm:`, `md:`, etc) then add responsive variants only where needed

### Implement Dynamic Theming (Tailwind 3.x)
- Define CSS variables in `globals.css` (e.g., colors, typography, etc.)
- Map CSS variables to utility classes in `tailwind.config.ts`

### Avoid custom styling whenever possible
- Style with Tailwind utility classes
- Use shadcn/ui component variants over custom css

## Code Architecture

### Apply Modern Next.js practices
- Structure with Next.js App Router - use `(routes)` folder for page organization
- Implement Server Components by default, Client Components only when necessary
- Follow strict file naming conventions: `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`

### Components
- Create reusable components with clear prop interfaces and default values
- Maintain separation between UI components and data fetching/state logic
- Keep UI component structure clean and modular