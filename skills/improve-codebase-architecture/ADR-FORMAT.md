# ADR Format

ADRs live in `docs/adr/` and use sequential numbering:
`0001-slug.md`, `0002-slug.md`, etc.

Create the `docs/adr/` directory lazily, only when the first ADR is needed.

## Template

```md
# {Short title of the decision}

{1-3 sentences: what's the context, what did we decide, and why.}
```

That is enough for most ADRs. The value is recording that a decision was made
and why, not filling out sections.

## Optional sections

Only include these when they add genuine value:

- **Status** frontmatter (`proposed | accepted | deprecated | superseded by ADR-NNNN`)
- **Considered Options**
- **Consequences**

## Numbering

Scan `docs/adr/` for the highest existing number and increment by one.

## When to offer an ADR

All three of these must be true:

1. **Hard to reverse**: the cost of changing your mind later is meaningful.
2. **Surprising without context**: a future reader will wonder why the code is
   shaped this way.
3. **The result of a real trade-off**: there were genuine alternatives and one
   was chosen for specific reasons.

If a decision is easy to reverse, unsurprising, or had no real alternative, skip
the ADR.

### What qualifies

- Architectural shape.
- Integration patterns between contexts.
- Technology choices that carry lock-in.
- Seam and scope decisions.
- Deliberate deviations from the obvious path.
- Constraints not visible in the code.
- Rejected alternatives when the rejection is non-obvious.
