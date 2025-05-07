# Best Practices

## Table of Contents

1. [Introduction](#introduction)

2. [Tech Stack](#tech-stack)

3. [Folder Structure & Architecture](#folder-structure-architecture)

4. [Next.js App Router Patterns](#nextjs-app-router-patterns)

5. [Styling & UI Components](#styling-ui-components)

6. [Data Fetching & State Management](#data-fetching-state-management)

7. [Forms & Validation](#forms-validation)

8. [Localization & Internationalization](#localization-internationalization)

9. [Theming & Dark Mode](#theming-dark-mode)

10. [Linting & Formatting](#linting-formatting)

11. [Environment Variables & Config](#environment-variables-config)

12. [Developer Environment & Setup](#developer-environment-setup)

13. [Editor & IDE Configuration](#editor-ide-configuration)

14. [UI/UX Testing and Design Fidelity](#uiux-testing-and-design-fidelity)

15. [Performance & Caching](#performance-caching)

16. [SEO & Accessibility](#seo-accessibility)

17. [Logging & Monitoring](#logging-monitoring)

18. [Security Best Practices](#security-best-practices)

19. [Docker & Deployment](#docker-deployment)

20. [Git Workflow & Code Reviews](#git-workflow-code-reviews)

21. [Do's & Don'ts](#dos-donts)

22. [Code Examples](#code-examples)

23. [Additional Resources](#additional-resources)

## Introduction

Welcome to **AutomatedPros**! This document outlines the best practices, architectural patterns, and coding conventions used throughout this project to help you onboard quickly and maintain consistency.

## Tech Stack

- **Next.js v15** with the App Router

- **TypeScript** for type safety

- **Tailwind CSS** for utility-first styling

- **React Query (@tanstack/react-query)** for data fetching and caching

- **React Hook Form** + **Zod** for form state management and validation

- **Radix UI** & **Lucide** for accessible UI primitives and icons

- **Next-Intl** for localization

- **Next-Themes** for theme management

- **ESLint** with `next/core-web-vitals` and Prettier (implicit)

- **Docker & Docker Compose** for containerization

## Folder Structure & Architecture

```

orderific-bms-new/

├─ public/                # Static assets (images, icons)
├─ src/
│  ├─ app/                # Next.js App Router pages and layouts
│  │  ├─ [locale]/        # Internationalized routes
│  │  ├─ components/      # Shared components at app level
│  │  └─ ...              # Feature modules (dashboard, orders, etc.)
│  ├─ components/         # Global reusable components
│  ├─ hooks/              # Custom React hooks (e.g., queries/users)
│  ├─ api/                # API clients and services
│  ├─ lib/                # Utility functions and helpers
│  ├─ providers/          # React context and providers
│  └─ styles/             # Global styles and Tailwind overrides
├─ next.config.ts         # Next.js configuration (webpack, i18n plugin)
├─ tailwind.config.js     # Tailwind CSS configuration
├─ .eslintrc.json         # ESLint settings
└─ Dockerfile             # Container image definition

```

### Key Patterns

- **Feature Modules**: Each domain (e.g., `orders`, `dashboard`) has its own folder under `app/[locale]` with dedicated `page.tsx`, `layout.tsx`, `route.ts` files.

- **Layouts**: Shared layouts defined in `app/layout.tsx` and localized versions in `app/[locale]/layout.tsx`.

- **Nested Routing**: File-system-based routing with dynamic segments (`[id]`, `[...rest]`).

## Next.js App Router Patterns

- Use **Server Components** by default; opt-in to Client Components with `'use client'` at the top of files.

- Fetch data in async Server Components via direct calls to your `src/api` services.

- Use `page.tsx`, `layout.tsx`, and `route.ts` to define pages, shared wrappers, and API routes.

- Leverage **next-intl** plugin for locale detection and translations (`createNextIntlPlugin`).

## Styling & UI Components

- **Tailwind CSS** is the primary styling solution; configure custom themes and breakpoints in `tailwind.config.js`.

- Use **class-variance-authority (cva)** + **clsx** for conditional and variant-based styling patterns.

- Leverage **Radix UI** primitives for accessible components (e.g., `@radix-ui/react-dialog`, `Tabs`, `Popover`).

- Import SVGs as React components via **@svgr/webpack** (configured in `next.config.ts`).

## Data Fetching & State Management

- Centralize HTTP calls in `src/api/*`. Each resource has its own folder/service.

- Use **React Query** hooks (`useQuery`, `useMutation`) wrapped in custom hooks under `src/hooks/queries` for data fetching and caching.

- Configure global React Query provider in `_app.tsx` or root layout with devtools enabled (`@tanstack/react-query-devtools`).

## Forms & Validation

- Build forms using **react-hook-form** for performant uncontrolled inputs.

- Integrate **Zod** schemas for validation, using `@hookform/resolvers/zod`.

- Keep schemas colocated with form components for clarity.

## Localization & Internationalization

- Use **next-intl** for server- and client-side translations.

- Place translation files under `src/i18n` organized by namespace.

- Surround your app with `<NextIntlProvider>` in the root layout.

## Theming & Dark Mode

- Manage light/dark themes with **next-themes**.

- Define color palettes and animations in `tailwind.config.js` using `tailwindcss-animate`.

- Use `data-theme` attribute or CSS variables to switch themes.

## Linting & Formatting

- **ESLint** extends `next/core-web-vitals`; TypeScript rules adjusted in `.eslintrc.json`.

- Run `yarn lint` before commits.

- Pre-commit hooks (if added) should enforce lint and formatting.

## Environment Variables & Config

- Store secrets in `.env.local`; register variables in `next.config.ts` if needed.

- Default values and required variables should be documented in `.env.example`.

## Developer Environment & Setup

- Use Node.js v18.x or above; manage versions with `nvm` or `fnm`.

- Install dependencies with `yarn install`; do not mix npm, Yarn, or pnpm in the same repo.

- Use the provided `yarn.lock` to reproduce consistent installs across environments.

- Copy `.env.example` to `.env.local` and set all required variables; never commit `.env.local`.

- Run `yarn dev` (with Turbopack) to start the development server on port 3000.

## Editor & IDE Configuration

- Recommended editor: **VSCode**; install extensions:

- ESLint

- Prettier - Code formatter

- Tailwind CSS IntelliSense

- EditorConfig for file consistency

- Import Cost

- GitLens for Git insights

- Enable `formatOnSave` and `eslint.autoFixOnSave` in settings.

- (Optional) Add a `.editorconfig` to enforce consistent tabs/spaces, line endings, and charset.

## UI/UX Testing and Design Fidelity

Ensure all UI elements and interactions align with the designs provided in Figma. Pay close attention to the following aspects during testing and development:

- **Cross-Device Testing**: Verify screens and components render correctly and are functional on Desktop, Tablet, and Mobile viewports.
- **Typography**:
  - **Font Style**: Ensure the correct font families are used as specified in Figma.
  - **Font Size**: Verify all text elements match the defined font sizes for different devices and states.
- **Color Palette**: Confirm all colors used (text, backgrounds, borders, icons, etc.) match the Figma specifications, including states like hover, focus, and disabled.
- **Spacing & Layout**:
  - **Margins & Padding**: Check that all spacing (margins, paddings) between elements and within components matches the design.
  - **Alignment**: Ensure elements are correctly aligned as per the Figma layouts.
- **Responsiveness**: Test that the layout adapts correctly to different screen sizes and orientations, maintaining usability and visual consistency.
- **Dimensions**: If specific widths and heights are defined for elements in Figma, ensure they are implemented accurately.
- **Interactive Elements**:
  - **Hover Functionality**: Verify that all interactive elements (buttons, links, cards, etc.) have the correct hover states (style changes, animations) as designed.
  - **Page Links**: Test all internal and external links to ensure they navigate to the correct destinations.
  - **Disabled/Default States**: Check the appearance and behavior of elements in their default and disabled states, including any specific hover effects or lack thereof for disabled elements.
- **Text and Placeholders**:
  - Ensure all static text content matches the copy provided.
  - Verify that input fields have the correct placeholder text as specified in Figma.

**Figma is the source of truth for all design specifications. Always refer to the latest Figma designs before and during implementation and testing.**

## Performance & Caching

- Leverage Next.js **Static Generation** with `export const revalidate = <seconds>` in server components.

- Prefer **`next/image`** for automatic image optimization and responsive sizing.

- Use **dynamic imports** (`next/dynamic`) for code splitting large modules or heavy components.

- Analyze bundle size via `npx next build --profile`; address large dependencies promptly.

- Use Chrome DevTools and Lighthouse to profile performance and identify bottlenecks.

## SEO & Accessibility

- Utilize the Next.js **Metadata API** in `layout.tsx` for titles, descriptions, and OG tags.

- Use **semantic HTML** (nav, header, main, footer) and proper ARIA roles for accessibility.

- Provide meaningful `alt` text on all `<Image>` and `<img>` elements.

- Ensure **keyboard navigation** works across menus, dialogs, and interactive components.

## Logging & Monitoring

- Use `console.error` / `console.info` sparingly for local development; remove before production.

- Log errors and performance metrics in **Middleware** or **API routes** for auditing.

## Security Best Practices

- Sanitize all user inputs (forms, query params) to prevent XSS and injection attacks.

- Use secure HTTP headers via Next.js `headers()` middleware (HSTS, CSP, X-Frame-Options).

- Store secrets in environment variables and configure them in CI/CD or deployment platform.

- Use **HTTPS** in production and enforce `strictTransportSecurity` in responses.

- Keep dependencies up to date and monitor for vulnerabilities with `yarn audit` or Dependabot.

## Docker & Deployment

- **Dockerfile** builds a production image of Next.js app.

- `docker-compose.yml` orchestrates local development (database, services).

- Deployment on Vercel is supported; use `appspec.yml` for AWS CodeDeploy if needed.

## Git Workflow & Code Reviews

Follow this workflow to keep code consistent and avoid disrupting others:

1. Ensure you're on the main branch (if not, switch):

```bash

git checkout main

```

2. Pull the latest updates:

```bash

git pull origin main

```

3. Create and switch to a new feature branch (use a descriptive, consistent name):

```bash

git checkout -b feature/<ticket-number>-<short-desc>

```

4. Make your changes; after each logical chunk, run lint and build to catch issues early:

```bash
yarn lint
yarn build
```

5. Stage and commit your work using Conventional Commits, including the related ticket number:

```bash

git add .

git commit -m "feat(ABC-123): add user-profile component"

```

6. Push your branch to the remote:

```bash

git push -u origin feature/<ticket-number>-<short-desc>

```

7. Go to Bitbucket and open a Pull Request:

- Source: your feature branch

- Target: `main`

- Include ticket links, context, screenshots, and testing instructions in the PR description.

8. Review and collaboration:

- Link to the issue or ticket (e.g., Jira/GitHub Issue).

- Keep PRs small and focused; split large changes across multiple PRs.

- Ensure at least one approving review (two approvals for major or backend changes).

- Address any merge conflicts or build/linting failures from CI before merging.

9. Once approved and checks pass, merge into `main`.

10. Locally switch back to `main` and pull the latest merged code:

```bash

git checkout main

git pull origin main

```

**Branch Naming & Commit Messages**

- Feature branches: `feature/<ticket-number>-<short-desc>`

- Bugfix branches: `fix/<ticket-number>-<short-desc>`

- Release branches: `release/<version>`

- Commits should follow Conventional Commits (`feat:`, `fix:`, `chore:`, etc.) and reference the ticket.

**PR Best Practices**

- Include a clear title, summary, and testing steps.

- Tag relevant teammates for review.

- Add or update relevant Storybook stories and documentation when relevant.

- Include relevant documentation updates in your PR.

## Do's & Don'ts

### Do's

- Use Server Components by default; opt into Client Components only when necessary.

- Co-locate API calls in `src/api/*` and wrap them in React Query hooks.

- Build forms using React Hook Form with Zod schemas and resolvers.

- Use Tailwind CSS with cva & clsx for conditional styling.

- Leverage Radix UI primitives for accessible UI components.

- Always run `yarn lint` and `yarn build` locally before pushing code.

- Use the PR's description to include ticket links, context, screenshots, and testing instructions.

- Keep PRs small and focused; avoid large diffs by splitting work into multiple PRs.

- Link PRs to their issue/ticket in the tracker (e.g., Jira, GitHub Issues).

- Write or update Storybook stories for new or updated components to document usage.

- Sync with design/UX teams for UI changes and update design tokens or theme variables.

- Update localization files when adding or modifying user-facing text in any language.

- Document significant architectural or configuration changes in the README or project docs.

- When updating shared or common components, always discuss changes with teammates to avoid regressions.

- Use descriptive variable and function names; prefer explicit over implicit.

- Write type annotations on function signatures for readability.

- Refactor code for maintainability; avoid deeply nested ternary expressions.

- Use dynamic imports for large modules to optimize bundle size.

- Pair with QA to define testing scenarios for complex features.

- Keep component props minimal and explicit; avoid passing large generic `props` objects.

- Perform performance profiling for UI components using React DevTools and Lighthouse.

- Use memoization (`React.memo`, `useMemo`, `useCallback`) for expensive components and derived computations.

- Follow consistent file and folder naming conventions (PascalCase for components, camelCase for hooks, kebab-case for folders).

- Always adhere to React Hooks rules: only call hooks at the top level of React function components or custom hooks.

- Leverage TypeScript interfaces/types for component props and avoid excessive `any` or `unknown`.

- Validate external API responses before consumption; handle unexpected data shapes gracefully.

- Clean up side effects and listeners in `useEffect` hooks to prevent memory leaks.

### Don'ts

- Do not disable ESLint or TypeScript checks except for known Next.js exceptions.

- Do not use the `any` type unless required for Next.js dynamic params.

- Avoid mixing global CSS with Tailwind to prevent specificity issues.

- Do not bypass Next.js routing conventions or manipulate file-system routes directly.

- Do not fetch data in Client Components without caching; use server or React Query.

- Do not commit secrets or environment variables to the repository.

- Do not mutate state directly; always use React Query or setState properly.

- Do not modify shared or common components without informing your team to prevent breaking others' work.

- Don't leave `console.log`, `debugger`, or commented-out code in production.

- Don't push directly to `main` or `production` branches; always use feature branches.

- Don't bypass CI/CD checks; address any build/linting failures before merging.

- Don't merge PRs without at least one approving review (two required for major or backend changes).

- Don't add new dependencies without team consensus and a clear justification.

- Don't ignore failing lint or type-check errors; fix them before submitting your PR.

- Don't commit secrets, environment files, or large binary assets to source control.

- Don't skip updating Storybook or documentation when modifying UI components or APIs.

- Don't override ESLint or Prettier settings without team agreement.

- Don't leave TODOs or FIXMEs in committed code; resolve them or create tickets.

- Don't use `eval` or dynamic code generation.

- Don't swallow errors silently; always handle exceptions or surface them to users/developers.

- Don't introduce deep component trees without memoization or virtualization; watch for performance regressions.

- Don't hardcode API endpoints; use environment variables and config files.

- Don't rely on local state when global shared state or context is more appropriate.

- Don't modify `node_modules` or commit updated dependencies without lockfile updates.

- Don't ignore server-side rendering constraints (e.g., avoid using `window`/`document` in Server Components).

- Don't introduce heavy dependencies for trivial tasks; prefer lightweight, tree-shakable libraries.

- Don't use magic numbers or unexplained hardcoded values; define constants with clear names.

- Don't rely on default exports for components; prefer named exports for consistent imports.

- Don't leave unhandled promises or swallow errors; always `catch` and log or rethrow as needed.

- Don't overlook performance implications of deep component trees; use virtualization or pagination for large lists.

- Don't bypass TypeScript strict mode settings; adhere to `strict` compiler flags to catch errors early.

## Code Examples

### Server vs Client Component

_Example 1: A Server Component that fetches data on the server before rendering._

```tsx
// app/[locale]/dashboard/page.tsx

import { getDashboardData } from "@/api/dashboard";

export default async function DashboardPage() {
  const data = await getDashboardData();

  return (
    <div>
            <h1>Dashboard</h1>      <pre>{JSON.stringify(data, null, 2)}</pre> 
       {" "}
    </div>
  );
}
```

_Example 2: A Client Component with `useState` for interactive UI; note the `'use client'` directive._

```tsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return <button onClick={() => setCount((c) => c + 1)}>Count: {count}</button>;
}
```

### Data Fetching with React Query

_Custom hook using React Query to fetch and cache a list of users from `/api/users`._

```ts
// src/hooks/queries/users/useUsers.ts

import { useQuery } from "@tanstack/react-query";

import axios from "axios";

export function useUsers() {
  return useQuery(["users"], async () => {
    const { data } = await axios.get("/api/users");

    return data;
  });
}
```

### Form Example with React Hook Form & Zod

_A simple form component demonstrating form state management with React Hook Form and schema-based validation using Zod._

```tsx
// src/components/UserForm.tsx

"use client";

import { useForm } from "react-hook-form";

import { zodResolver } from "@hookform/resolvers/zod";

import * as z from "zod";

const userSchema = z.object({
  name: z.string().min(1, "Name is required"),

  email: z.string().email("Invalid email"),
});

type UserFormValues = z.infer<typeof userSchema>;

export function UserForm() {
  const {
    register,

    handleSubmit,

    formState: { errors },
  } = useForm<UserFormValues>({
    resolver: zodResolver(userSchema),
  });

  const onSubmit = (values: UserFormValues) => console.log(values);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
            <input {...register("name")} placeholder="Name" />     {" "}
      {errors.name && <p>{errors.name.message}</p>}
            <input {...register("email")} placeholder="Email" />      {errors.email && (
        <p>{errors.email.message}</p>
      )}      <button type="submit">Submit</button>   {" "}
    </form>
  );
}
```

### Styling with Tailwind, clsx & cva

_Defining a variant-driven Button component using CVA for styling variants and clsx for conditional classes._

```tsx
// src/components/Button.tsx

import { cva, type VariantProps } from "class-variance-authority";

import clsx from "clsx";

const buttonStyles = cva("px-4 py-2 rounded font-semibold", {
  variants: {
    intent: {
      primary: "bg-blue-600 text-white hover:bg-blue-700",

      secondary: "bg-gray-200 text-gray-800 hover:bg-gray-300",
    },

    size: {
      sm: "text-sm",

      md: "text-base",

      lg: "text-lg",
    },
  },

  defaultVariants: {
    intent: "primary",

    size: "md",
  },
});

export function Button({
  intent,

  size,

  className,

  ...props
}: VariantProps<typeof buttonStyles> &
  React.ButtonHTMLAttributes<HTMLButtonElement>) {
  return (
    <button
      className={clsx(buttonStyles({ intent, size }), className)}
      {...props}
    />
  );
}
```

### Localization Setup

_Wrapping the app locale-specific layout with NextIntlProvider and dynamically loading translation messages._

```tsx
// src/app/[locale]/layout.tsx

import { NextIntlProvider } from "next-intl";

import { ReactNode } from "react";

interface LayoutProps {
  children: ReactNode;

  params: { locale: string };
}

export default async function LocaleLayout({
  children,

  params: { locale },
}: LayoutProps) {
  const messages = (await import(`../../../i18n/${locale}.json`)).default;

  return (
    <html lang={locale}>
           {" "}
      <body>
               {" "}
        <NextIntlProvider locale={locale} messages={messages}>
                    {children}       {" "}
        </NextIntlProvider>
             {" "}
      </body>
         {" "}
    </html>
  );
}
```

## Additional Resources

- Next.js Docs: https://nextjs.org/docs

- Tailwind CSS: https://tailwindcss.com/docs

- React Query: https://tanstack.com/query/v5

- React Hook Form: https://react-hook-form.com

- Zod: https://github.com/colinhacks/zod

_This document will evolve—please contribute improvements!_
