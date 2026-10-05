# Governance

Draft 0.1 · 4 October 2026

## Who runs this

**This specification is stewarded and funded by [EM04](https://em04.com), which builds
financial reporting software and implements it.**

That is stated first because discovering it later is what destroys a standard's
credibility, and because it is true. EM04 pays for the domain, the hosting and the time,
and today EM04 decides what goes in.

A `.org` domain does not make a specification neutral. A specification that one company
controls is a vendor format with a better URL, and calling it something else would be
the dishonest version of this document.

## Why trust it anyway

The protection is that walking away costs almost nothing:

- **CC0.** No permission is needed, now or ever. Fork it the day we disappoint you.
- **No vendor fields.** Nothing in the format exists because EM04 wanted it there, and
  nothing ever will: no `generator`, no attribution, no branding.
- **Boring to implement.** It is Markdown with required headings and eight rules, and a
  spreadsheet and an afternoon are enough. There is no moat in the format, and there is
  not meant to be one.
- **Mirrored.** The repository is public and designed to be cloned. If EM04 stops
  existing, the specification does not.

## What EM04 gets out of it

A standard that exists means EM04's output is conformant rather than idiosyncratic, and
it means an argument about whether a summary is honest has a reference to point at. We
think the symmetry rule in SPEC §5.1 is good for readers, and we also think a product
that enforces it looks better than one that does not.

We do not get a format only we can implement, lead capture, a signup wall, or any
preferential position in a checker. If any of those appear, that is the point to stop
trusting this.

## How decisions are made today

1. Anyone opens an issue or a pull request.
2. Discussion happens in public, on the issue.
3. EM04 merges or declines, and says why in writing.

Step 3 is what keeps this honest. A declined contribution with a stated reason is a
decision; a declined contribution that goes quiet is the behaviour this document exists
to make visible.

Changes to the integrity rules in SPEC §5 get a minimum **four-week comment period**,
because those rules are the specification and a quiet change to them is how a standard
rots.

## How that changes

Single-steward governance is a starting condition. It should end when anybody else has
standing, and the trigger is stated now so that it cannot be quietly deferred:

> **When three organisations other than EM04 have published a conforming file or
> shipped an implementation, governance moves to a group in which EM04 holds at most
> one vote.**

Until then, a committee would be theatre. After then, continuing to decide alone would
be indefensible.

## Profiles

Market profiles are governed by whoever writes them, not by us. EM04 has no standing on
SEC, ASX, TSX or JSE filing requirements and should not be the last word on any of
them.

A profile maintainer may merge changes to their own profile without our involvement.
The only constraint is the one in SPEC §6: **a profile may not weaken a core
requirement.** That exists so that "conforms to `financials.txt`" means the same thing
in every market, and it is the one thing not delegated.

## Versioning

Version numbers are semantic, and changed conservatively:

| Change | Version | Notes |
|---|---|---|
| Clarification, typo, example | patch | |
| New optional section, new profile | minor | |
| New requirement, changed integrity rule | major | Four-week comment period. |

Published files declare the version they target. A checker reports against the declared
version, never the latest. A file conforming in 2026 does not stop conforming because
the specification moved in 2028.

## What this document is not

It is not a constitution, a foundation or a legal entity, only a page saying who
decides, what they get out of it, and what would have to happen for that to change.
Anything more elaborate would be pretending at a scale this does not have.

If the specification acquires one implementer, this document was adequate. If it
acquires fifty, this document is the wrong one and should be replaced by people who have
joined by then.
