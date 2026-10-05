# Contributing

This specification is more useful the more people who file real accounts have argued
with it. There are four ways in, in rough order of how much they would help.

## 1. Write a profile

This is the most valuable contribution, and the one we are least able to make ourselves.

The core is jurisdiction-neutral. Disclosure obligations are not. A profile written by
someone who files under a regime will be better than one written by someone reading
about it, and on SEC, ASX, TSX, JSE and most others we have no standing at all.

A profile needs: what the market requires that the core does not cover, which optional
sections become required, any constraints on existing ones, and a citation to the rule
or statute behind each. See [`profiles/uk.md`](profiles/uk.md) for the shape, including
its own list of what remains unverified.

Open a pull request against `profiles/`. A partial profile with honest gaps is more
useful than no profile, and much more useful than a confident wrong one.

## 2. Attack the integrity rules

§5 is the part that decides whether this is a standard or a press-release format, and
it is where a bad decision does the most damage.

Particularly welcome:

- **A way to game the symmetry rule.** If a publisher can satisfy §5.1 while still
  misleading, the rule is not doing its job and we would rather know now.
- **A case where a rule is impossible to satisfy honestly.** A first-period company has
  no comparatives; a restating company has two versions of the same period. The rules
  must have an answer that is honest as well as strict.
- **A rule that is unenforceable.** Anything a checker cannot verify is advice, and
  should be labelled as advice rather than sitting among requirements.

Open an issue. These are worth discussing before anyone writes a patch.

## 3. Publish a file

Nothing will expose a flaw faster than one real company publishing one real file. If
you do, say so in an issue, and include what you could not make conform: that is the
more useful half.

## 4. Build a checker

Ours will be open and is not meant to be the only one. A second implementation
disagreeing with the first is how the specification's ambiguities get found.

## What we will push back on

**New sections.** The core is short on purpose. A section that only matters to one
market belongs in a profile; one that matters to one company belongs nowhere.

**A taxonomy.** XBRL exists, is mandatory in several markets, and is better at this
than we would be. This is a summary with a pointer to the filing, not a data model, and
attempts to make it one should be resisted.

**Scoring.** The specification says whether a file conforms. It does not say whether a
company is doing well, and it must never be read that way. A conforming file about a
terrible year is still conforming.

**Branding.** No vendor names in the format, including ours. The moment a field exists
because one company wanted it there, nobody else should adopt it.

## Decisions already taken, and why

So that settled ground is not re-litigated by accident:

| Decision | Reasoning |
|---|---|
| The name `financials.txt` | Descriptive, and the domain is held. It covers interim results and trading updates too; `results.txt` was narrower still. |
| Markdown, not JSON or YAML | It is read by people and by models. JSON is read well by neither, and the file's whole purpose is to be read. |
| `/.well-known/` | A conventional, discoverable, uncontested location. |
| Extends `llms.txt` rather than competing | That convention has adoption. Forking it would split a small audience for no gain. |
| Hash, not signature | A hash is checkable by anyone with the file and the source. Signing needs a key distribution story nobody has asked for yet. See SPEC §9. |
| No full statements | Reproducing a balance sheet in Markdown helps nobody. Link the filed one. |
| CC0 | A standard that needs permission is not a standard. |

Any of these can be reopened with an argument. None should be reopened with a
preference.
