# Architecture Decisions

## Overview

This is a Next.js frontend application that consumes property data from a Sanity.io headless CMS and serves an AirBnB-like interface with interactive maps and property browsing.

## Components and Communication

### React Components

**Navigation**
- `NavBar.js` - Sticky navigation bar displayed on all pages via the `_app.js` wrapper; contains the AirBnB logo

**Maps**
- `Map.js` - Embedded map for a single property's location, receives `location` prop with `lat`/`lng` coordinates. Used on property detail pages.
- `DashboardMap.js` - Full-viewport map showing all properties with markers, receives `properties` array. Used on the home page. Both use `@react-google-maps/api` library.

**Images**
- `Image.js` - Displays optimized images using the Sanity image URL builder. Supports different sizes via `identifier` prop ("main-image" vs regular "image").

**Reviews**
- `Review.js` - Displays individual review cards with rating, traveller name, and photo. Receives full review object with nested traveller data.

### Page Structure

**Home Page** (`pages/index.js`)
- Server-side rendered with `getServerSideProps`
- Fetches all properties via Sanity GROQ query: `'*[ _type == "property"]'`
- Renders a two-column layout: property feed (left) and DashboardMap (right)
- Displays property cards with main image, review count, title, and price
- Uses Next.js `Link` for client-side navigation to property detail pages

**Property Detail Page** (`pages/property/[slug].js`)
- Dynamic routing using slug parameter
- Server-side rendered with `getServerSideProps` taking `pageContext.query.slug`
- Fetches single property with nested host and reviews data via GROQ query
- Displays main image, gallery, property details, host info, reviews, and Map component
- Returns 404 via `notFound: true` if property not found

**Global App Wrapper** (`pages/_app.js`)
- Imports global styles and NavBar component
- Wraps every page with NavBar and passes props to page components

### Data Flow

1. **Entry Point**: User visits home page or direct URL
2. **Server-side Data Fetch**: Next.js `getServerSideProps` executes on server, queries Sanity API
3. **Sanity Query**: Uses `sanityClient.fetch()` with GROQ queries to retrieve typed data
4. **Component Rendering**: React components receive data as props and render UI
5. **Image Optimization**: Components use `urlFor()` helper to build optimized Sanity image URLs with format, dimension, and crop parameters
6. **Navigation**: Client-side navigation via Next.js `Link` component

## Data Stores

**Sanity.io Headless CMS** (`sanity.js`)
- Remote content management system storing property, review, and traveller data
- Configuration:
  - `dataset`: Production dataset (customizable via `NEXT_PUBLIC_SANITY_DATASET`)
  - `projectId`: Set via `NEXT_PUBLIC_SANITY_PROJECT_ID` environment variable
  - `useCdn`: Enabled in production for faster CDN-cached responses; disabled in development for fresh data
- Client initialized via `next-sanity` library's `createClient()`
- Image asset hosting and URL generation via `next-sanity` image builder

## Notable Libraries and Choices

- **Next.js 10.1.3**: Framework providing server-side rendering, static generation, API routes, and built-in routing (chosen for server-side data fetching and performance)
- **React 17.0.2**: UI library (standard with Next.js)
- **@react-google-maps/api 2.1.1**: Wraps Google Maps JavaScript API, provides `GoogleMap`, `Marker`, and `useJsApiLoader` components (chosen for interactive property location display)
- **next-sanity 0.1.12**: Sanity client and image URL builder (chosen to integrate Sanity CMS as headless backend)

## Environment Variables

Public variables (exposed to browser via `NEXT_PUBLIC_` prefix):
- `NEXT_PUBLIC_SANITY_DATASET`: Sanity dataset name (defaults to "production")
- `NEXT_PUBLIC_SANITY_PROJECT_ID`: Sanity project ID (required)
- `googlePlacesAPI`: Google Maps API key used in Map components

## Hosting and Deployment

The repository contains no explicit deployment configuration (no Vercel config files, Docker setup, or CI/CD). However, the Next.js framework is optimized for Vercel hosting with `npm run build` and `npm start` commands provided in `package.json` for production deployment.
