# AGENTS.md - Coding Guidelines for SiteWebPersonal

## Project Overview

This is a personal portfolio website built with **Astro** using TypeScript. The project uses pnpm as the package manager and follows strict TypeScript configuration.

---

## Build, Lint, and Test Commands

### Package Manager
This project uses **pnpm**. Do not use npm or yarn.

### Available Scripts

| Command | Description |
|---------|-------------|
| `pnpm dev` | Start development server with hot reload |
| `pnpm build` | Build for production (outputs to `dist/`) |
| `pnpm preview` | Preview production build locally |
| `pnpm astro` | Run Astro CLI commands |

### Running Single Commands

```bash
# Development
pnpm dev

# Production build
pnpm build

# Preview build
pnpm preview
```

### Adding Tests (Recommended)

This project currently has no test setup. If adding tests, use:
- **Testing Framework**: Vitest (Astro's recommended choice)
- **Single test file**: `pnpm vitest run src/components/MyComponent.test.ts`

Example test script to add to `package.json`:
```json
{
  "scripts": {
    "test": "vitest",
    "test:run": "vitest run",
    "test:ui": "vitest --ui"
  }
}
```

### Linting

Astro includes basic TypeScript checking via `astro check`:
```bash
pnpm astro check    # Type-check the project
pnpm astro sync     # Generate TypeScript types
```

For stricter linting, consider adding ESLint:
```bash
pnpm add -D eslint @astrojs/eslint-plugin
```

---

## Code Style Guidelines

### General Principles

1. **Keep it simple** - This is a portfolio site; prioritize readability over complexity
2. **Component-based** - Create reusable components in `src/components/`
3. **Layouts** - Use layouts in `src/layouts/` for consistent page structure
4. **Scoped styles** - Use Astro's scoped `<style>` blocks for component-specific CSS

### TypeScript

- **Strict mode**: Enabled via `astro/tsconfigs/strict`
- **Type inference**: Prefer implicit types for simple cases
- **Explicit types**: Use explicit types for function parameters and return types
- **No `any`**: Avoid `any`; use `unknown` if type is truly unknown

### Astro Components (.astro files)

**Frontmatter (between `---`):**
```astro
---
// Imports at top
import Layout from "../layouts/Layout.astro";
import MyComponent from "../components/MyComponent.astro";

// Constants and logic
const pageTitle = "About Me";
const items = ["item1", "item2"];
---
```

**Template:**
- Use 2-space indentation
- Self-closing tags for void elements: `<component />`
- Wrap attributes for readability:
  ```astro
  <MyComponent
    prop1="value"
    prop2={variable}
  />
  ```

**Styles:**
- Use CSS custom properties (variables) for theming
- Keep styles scoped to the component
- Use `:root` for global variables in Layout components

### Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Files (components) | PascalCase | `Header.astro`, `Footer.astro` |
| Files (utilities) | camelCase | `utils.ts`, `apiClient.ts` |
| Variables/Constants | camelCase | `const userName`, `const API_URL` |
| Constants (config) | UPPER_SNAKE_CASE | `const MAX_RETRIES = 3` |
| CSS classes | kebab-case | `class="social-links"` |
| Astro pages | kebab-case | `about.astro`, `contact-us.astro` |

### Import Order

1. Astro imports
2. React/Vue/Svelte imports (if any)
3. Local component imports
4. Local utility imports
5. Type imports (with `type` keyword)

```astro
---
import type { Props } from "../types";
import Layout from "../layouts/Layout.astro";
import Header from "../components/Header.astro";
import { formatDate } from "../utils/date";
---
```

### CSS Guidelines

- Use CSS variables for colors, spacing, fonts
- Prefer flexbox and grid for layout
- Use `rem` for font sizes, `px` for borders/shadows
- Keep selectors simple and specific
- Mobile-first media queries

```css
:root {
  --primary-color: #00bfff;
  --bg-color: #1a1a1a;
}

.card {
  padding: 1rem;
}

@media (min-width: 768px) {
  .card {
    padding: 2rem;
  }
}
```

### Error Handling

- Let Astro handle SSR errors with its built-in error pages
- For client-side code, use try/catch with console.error for debugging
- Validate props with TypeScript interfaces

### Git Conventions

- **Branch naming**: `feature/description`, `fix/description`, `docs/description`
- **Commits**: Use clear, concise messages (imperative mood)
- **No commits**: Only commit when explicitly requested by user

### VS Code Recommended Extensions

- `astro-build.astro-vscode` - Astro language support

### File Structure

```
src/
├── assets/          # Static assets (images, fonts)
├── components/     # Reusable Astro components
├── layouts/        # Page layouts
├── pages/          # File-based routing
├── styles/         # Global styles (optional)
└── utils/          # Utility functions (optional)
```

---

## Important Notes

1. **No existing tests** - This project has no test suite; consider adding Vitest if tests are needed
2. **No ESLint/Prettier** - Currently using Astro's built-in formatting; add if stricter control needed
3. **Sharp included** - Image optimization via Sharp is configured
4. **Dist folder** - Production builds go to `dist/`, which is git-ignored
