# Settings for Next.js

## Target Project structure

When installing Tailwind 3, DO NOT opt for a `src/` folder.

```txt
- node_modules/             # Dependencies installed by npm/yarn/pnpm
- public/                   # Static assets like images, fonts, and files
- app/(routes)              # Contains all route pages grouped together
- app/api/                  # Backend endpoints for data operations and external services
- app/layout.tsx            # Root layout component that wraps all pages
- app/page.tsx              # Homepage component (root page of the application)
- app/globals.css            # Project-wide CSS styles including Shadcn/ui variables
- components/               # Custom components in the root like UserDashboard.tsx
- components/ui/            # Reusable UI components like buttons, inputs, etc.
- components/shared/        # Layout and site-wide components like headers, navigation
- store/                    # State management (Zustand, Redux, Context, etc.)
- lib/                      # Config for external services like supabase.ts, stripe.ts
- lib/utils/                # Reusable functions for common tasks like parseDate.ts
- hooks/                    # Reusable React logic for state and effects
- types/                    # TypeScript type definitions and interfaces like user.ts
- tests/                    # Unit and integration tests (Zest, Cypress, etc.)
- .env.local                # Environment variables (local development)
- .env.example              # Example environment variables (for documentation)
- next.config.mjs           # Next.js configuration
- tailwind.config.ts        # Tailwind CSS configuration
- tsconfig.json             # TypeScript configuration
- .gitignore                # Files and directories to ignore in git
- README.md                 # Project documentation
```

## Next.js Project with Tailwind 3 and Shadcn/ui

### 1. Next.js installation

Install Next.js 15.3.1 with with these options:

```bash
npx create-next-app@15.3.1 my-app \
  --typescript \
  --eslint \
  --tailwind \
  --app \
  --no-turbo \
  --import-alias="@/*"
```

IMPORTANT: Ensure `tsconfig.json` and `tailwind.config.ts` are correctly configured for aliases.

### Shadcn/ui installation and config

1. Install shadcn/ui with these options:

```bash
npx shadcn@2.3.0 init \
  --typescript \
  --style=new-york \
  --color=stone \
  --css-variables=yes \
  --tailwind-css=app/globals.css \
  --tailwind-config=tailwind.config.ts \
  --components-dir=components \
  --utils-dir=lib/utils \
  --rsc \
  --yes
```

2. Install the Hericons library, run: `npm install @heroicons/react` and update `components.json` with: `"iconLibrary": "heroicons"`.

3. Ensure Shadcn/ui configuration in `components.json` exactly matches the below (i.e., ensure all 15 fields are defined):

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "app/globals.css",
    "baseColor": "stone",
    "cssVariables": true,
    "rsc": true,
    "tsx": true
  },
  "aliases": {
    "utils": "@/lib/utils",
    "components": "@/components",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  },
  "iconLibrary": "heroicons"
}
```

## Add light/dark theme toggle functionality
Install and configure a theme toggle below buttons on Root page.

1. **Step 1:** Install needed package, run: `npm install next-themes`

2. **Step 2:** Create file `components/theme-provider.tsx`

```typescript
"use client"

import * as React from "react"
import { ThemeProvider as NextThemesProvider } from "next-themes"

export function ThemeProvider({
  children,
  ...props
}: React.ComponentProps<typeof NextThemesProvider>) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>
}
```

3. **Step 3:** Wrap root layout (`app/layout.tsx`) with `ThemeProvider` and add `suppressHydrationWarning` prop

```typescript
import { ThemeProvider } from "@/components/theme-provider"

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en" suppressHydrationWarning>
      <body>
        <ThemeProvider
          attribute="class"
          defaultTheme="system"
          enableSystem
          disableTransitionOnChange
        >
          {children}
        </ThemeProvider>
      </body>
    </html>
  )
}
```

4. Create `components/light-dark-toggle.tsx` component and then place on root page below buttons:

```typescript
"use client"
import * as React from "react"
import { MoonIcon, SunIcon } from "@heroicons/react/24/outline"
import { useTheme } from "next-themes"
import { Button } from "@/components/ui/button"

export function LightDarkToggle() {
  const { theme, setTheme } = useTheme()
  
  const toggleTheme = () => {
    setTheme(theme === "dark" ? "light" : "dark")
  }

  return (
    <Button 
      variant="outline" 
      size="icon" 
      onClick={toggleTheme}
      aria-label="Toggle theme"
    >
      <SunIcon className="h-5 w-5 rotate-0 scale-100 transition-all dark:scale-0" />
      <MoonIcon className="absolute h-5 w-5 rotate-0 scale-0 transition-all dark:scale-100" />
    </Button>
  )
}
```