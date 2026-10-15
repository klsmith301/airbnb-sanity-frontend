## Goal
Add a single documentation file to the repository to verify that Forge can build with the recommended model. No runtime code, configuration, dependencies, or existing files are modified.

---

## Tasks

### 1. Create `docs/forge-model-matching.md`
- Create the `docs/` directory (it does not currently exist).
- Create `docs/forge-model-matching.md` with **exactly** the following content:

```markdown
# Forge matching-model verification

This documentation-only change verifies that Forge can build with the recommended model.
```

That is: one H1 heading and one paragraph, nothing else.

---

## Acceptance Criteria
1. The file `docs/forge-model-matching.md` exists in the repository.
2. The file's first line is `# Forge matching-model verification`.
3. The file's body paragraph is exactly `This documentation-only change verifies that Forge can build with the recommended model.`
4. No other file in the repository is created, deleted, or modified.
