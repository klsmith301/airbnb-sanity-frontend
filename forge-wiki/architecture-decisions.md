# Architecture decisions

## Stack

- **Framework**: Next.js 10 (React 17) – pages are server-side rendered via `getServerSideProps`.
- **CMS**: Sanity.io (`next-sanity`) – content (properties, reviews, travellers) is fetched at request time using GROQ queries through `sanityClient` (configured in `sanity.js`).
- **Maps**: `@react-google-maps/api` – interactive cluster map rendered in a React component.
- **Styling**: plain CSS (`styles/`).

## Environment variables

| Variable | Purpose |
|---|---|
| `NEXT_PUBLIC_SANITY_DATASET` | Sanity dataset name (defaults to `production`) |
| `NEXT_PUBLIC_SANITY_PROJECT_ID` | Sanity project ID (required) |
| `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY` | Google Maps API key (used in map component) |

## Project layout

```
pages/         Next.js page routes (_app.js, index.js, property/[slug].js)
components/    Shared React components (NavBar, map, property card, etc.)
styles/        CSS files
images/        Static images
public/        Next.js public assets
sanity.js      Sanity client + image URL builder
utils.js       Shared utility helpers
```
