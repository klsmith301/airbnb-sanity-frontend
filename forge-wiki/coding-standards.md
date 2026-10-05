# Coding Standards

## Languages and Tooling

The project is built with **JavaScript (Node.js/React)** as the primary language, with no TypeScript. The core frameworks and tools are:

- **Framework**: Next.js 10.1.3 (`package.json`)
- **UI Library**: React 17.0.2 (`package.json`)
- **Package Manager**: npm (`package.json` scripts)
- **Build and Development**: Next.js built-in dev server (`npm run dev`), build (`npm run build`), and production start (`npm start`)

## Formatting and Linting

No explicit linting or formatting tools are configured in `package.json`. The code follows basic JavaScript conventions without a configured formatter like Prettier or ESLint.

## Testing

The repository contains **no test files or test frameworks** (Jest, Mocha, etc. are not in `package.json`). No test commands are configured.

## Naming Conventions

### Components

Components are named with PascalCase and stored in the `components/` directory:
- `NavBar.js` - Navigation component
- `Map.js` - Single property map component
- `DashboardMap.js` - Multi-property map component
- `Image.js` - Optimized image display component
- `Review.js` - Review display component

### Pages

Pages follow Next.js conventions in the `pages/` directory:
- `pages/index.js` - Home/dashboard page
- `pages/property/[slug].js` - Dynamic property detail page (slug-based routing)
- `pages/_app.js` - Global app wrapper (Next.js convention)
- `pages/api/hello.js` - Example API route

### Utility Functions

Utilities use camelCase:
- `isMultiple()` in `utils.js` - Pluralization helper

### Configuration Files

- `sanity.js` - Sanity client configuration and image URL builder

## Project Structure

```
.
├── components/          # React components (NavBar, Map, Image, Review, etc.)
├── pages/              # Next.js pages (home, property detail, API routes)
│   ├── api/            # API routes
│   └── property/       # Dynamic property page
├── styles/             # CSS files (globals.css)
├── public/             # Static assets (favicon, SVGs)
├── images/             # Image assets (logos)
├── utils.js            # Utility functions
├── sanity.js           # Sanity client initialization
└── package.json        # Dependencies and scripts
```

## Key Files Demonstrating Standards

- **Component structure**: `components/NavBar.js`, `components/Map.js` - functional components with hooks
- **Page structure**: `pages/index.js`, `pages/property/[slug].js` - getServerSideProps for data fetching
- **API routes**: `pages/api/hello.js` - basic API route pattern
- **Styling**: `styles/globals.css` - global CSS with CSS classes for component styling
- **Environment variables**: `sanity.js` - uses `process.env.NEXT_PUBLIC_*` for public config (Next.js convention)
