# Known Issues

## TODO and FIXME Notes

No TODO or FIXME comments were found in the codebase.

## Test Coverage

The repository contains **no test files or test frameworks**. No tests are configured in `package.json` and no test commands are available (`npm test` is not defined).

## Failing or Skipped Tests

Not applicable; no tests exist in the repository.

## Documented Limitations and Issues

### Map Component Issues

**Duplicate console logs** in `components/Map.js` (lines 10-11):
```javascript
console.log("location.lat", location.lat)
console.log("location.lat", location.lat)  // duplicate
```

**Duplicate console logs** in `components/DashboardMap.js` (lines 9-10):
```javascript
console.log(properties[0].location?.lat)
console.log(properties[0].location?.lat)  // duplicate
```

These are debug statements left in the code that should be removed.

### Property Detail Page

**Typo in house rules text** in `pages/property/[slug].js` (line 58):
```javascript
"This place isn't suitable for pets andthe host does not allow"
```
Missing space between "and" and "the" ("andthe").

### API Routes

An example/placeholder API route exists at `pages/api/hello.js` that returns sample JSON and may not be used in production.

## No Documented Environment Limits

The codebase contains no documented limits or constraints on:
- Number of properties that can be displayed
- API rate limits
- Map marker limits
- Image loading constraints
