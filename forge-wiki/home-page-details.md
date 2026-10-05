# Home Page Details

## File: `pages/index.js`

### State
The component is currently **stateless** — it receives `properties` as a prop from `getServerSideProps` and renders them directly. No `useState` or `useEffect` hooks are used.

### Rendering
- Wraps everything in a conditional `{properties && (...)}` guard
- Two-column layout via `.main` CSS class:
  - Left (`.feed-container`, `width: 50%`): heading `"Places to stay near you"`, then a `.feed` flex-wrap grid of property cards
  - Right (`.map`, `width: 50%`): `<DashboardMap properties={properties} />`
- Each card is a `<Link>` → `<div className="card">` containing: image, review count, title, price per night

### Data Shape (from Sanity)
Each property object has at minimum:
- `_id` — unique identifier
- `slug.current` — URL slug
- `mainImage` — Sanity image asset ref (passed to `urlFor()`)
- `title` — string (the property name used for display)
- `reviews` — array (length used for review count)
- `pricePerNight` — number
- `location.lat` / `location.lng` — coordinates for map markers

### Server-Side Fetch
`getServerSideProps` fetches `'*[ _type == "property"]'` — all properties, no filtering. Filter would need to be client-side (on the already-fetched array) or via a parameterised GROQ query.

## CSS Classes Relevant to Home Page (in `styles/globals.css`)
- `.main` — flex row container
- `.feed-container` — 50% wide, 100vh, background `#f8f8f8`, padding 20px
- `.feed` — flex-wrap row
- `.card` / `.card img` — individual property card styles
- `.map` — 50% wide right column

No existing search-related styles are present.
