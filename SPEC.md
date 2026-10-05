# financials.txt: core specification

Version 0.1 · draft · 5 October 2026

An agreed, plain-text way for a company to hand its published financial results to a
language model, written to be read by a model and by a person.

## 1. Why this exists

Annual reports are written to persuade, and everyone involved knows it. By convention
they open with a section that makes the case (highlights, a chair's statement, measures
the company has chosen and named itself) and then move to the financial statements.
Nothing in that is wrong, and the figures are all published. But they are complex, and
the narrative in front of them is written to be read first.

A growing share of readers skip it. They give the document to a language model and say
*analyse this*, and the model reads past the narrative to the statements whatever the
company publishes.

`financials.txt` is an agreed way for a company to hand its results to that model. It
says what the document is, where its figures are, what they are, and what the company's
people say about them, in a form that cannot tilt the reading. The analysis is left to
the reader's model; the file gives it an accurate place to start.

A file like this could easily become a press release. If a company could publish a
flattering summary that a model then treated as authoritative, readers would be worse
off than they are now. A file written to be given to a model is also the obvious place
to try to steer one. The rules in §5 exist to prevent both, and a file that breaks any
of them does not conform.

### Relationship to existing formats

| Format | What it is for | How it differs |
|---|---|---|
| XBRL / iXBRL | Structured filing for regulators | Verbose XML built to be extracted by rule. It makes a poor prompt. |
| The annual report PDF | The authoritative, designed document | Designed for print, so its structure is visual. |
| [llms.txt](https://llmstxt.org) | Context for language models across a whole site | The same idea, applied here to results. |

`financials.txt` does not replace the filed accounts. It points at them, and can be
checked against them.

## 2. Location and discovery

```
https://example.com/.well-known/financials.txt
```

A publisher **SHOULD** also link it from `/llms.txt`, and **MAY** serve period-specific
files at a stable path, with `/.well-known/financials.txt` always resolving to the most
recent:

```
https://example.com/.well-known/financials/2026-annual.txt
```

Served as `text/markdown; charset=utf-8`.

## 3. Format

Markdown, the same choice [llms.txt](https://llmstxt.org) makes and for the same
reasons: a person can read it, a program can parse it without a library, and version
control shows every change to a published file.

Headings are the structure. A consumer **MUST** locate sections by heading, never by
position.

## 4. Document structure

### 4.1 Example

````markdown
# Norwood & Kite Design Ltd

> Annual results for the year ended 30 September 2026. Audited. Figures in GBP.
> Published 4 October 2026. Prepared from the filed accounts; see Source.

## Identity
- Legal name: Norwood & Kite Design Ltd
- Jurisdiction: United Kingdom
- Company number: 09847213
- LEI: (none)
- Ticker: (unlisted)

## Basis
- Period: 1 October 2025 to 30 September 2026
- Comparative: 1 October 2024 to 30 September 2025
- Status: audited
- Framework: FRS 102
- Currency: GBP
- Units: as stated, in full
- Consolidation: single entity

## Headline figures
| Measure | This period | Prior period | Change |
|---|---|---|---|
| Revenue | 332,890 | 268,400 | +24.0% |
| Gross profit | 235,435 | 196,300 | +19.9% |
| Operating expenses | 199,800 | 171,250 | +16.7% |
| Profit before tax | 35,635 | 25,050 | +42.3% |
| Cash at period end | 88,120 | 61,400 | +43.5% |

## What changed
*Movements of 5% or more, or 10,000 or more, whichever is larger.*
- Revenue rose 24.0% to 332,890, with growth weighted to the second half.
- Gross margin fell 2.4 points to 70.7%, as cost of sales grew faster than revenue.
- Operating expenses rose 16.7%, principally staff costs.

## Outlook
*Forward-looking. Not a forecast and not a guarantee.*
- The order book at 30 September 2026 stood at 141,000, covering approximately five months.

## Risks
- Client concentration: the three largest clients represented 46% of revenue.
- Recruitment: delivery capacity is constrained by hiring in a competitive market.

## Source
- Document: https://example.com/reports/2026-annual.pdf
- Published: 2026-10-04
- SHA-256: 3f786850e387550fdab836ed7e6dc881de23001b7a4f0c9b2e5d8a6c1f3b9e02
- Filed: Companies House, 2026-10-04
````

### 4.2 Section requirements

| Section | Required | Notes |
|---|---|---|
| H1 company name | **MUST** | The legal name, exactly as filed. |
| Blockquote summary | **MUST** | Period, audit status, currency, publication date. |
| `## Identity` | **MUST** | Identifies the reporting entity without ambiguity. |
| `## Basis` | **MUST** | Without it, none of the figures can be interpreted. |
| `## Headline figures` | **MUST** | Statutory measures, with comparatives. See §5.2 and §5.7. |
| `## Adjusted measures` | MAY | The only place an adjusted measure may appear. See §4.3 and §5.7. |
| `## What changed` | **MUST** | See §5.1. Most conformance failures happen here. |
| `## Quotes` | MAY | Verbatim and attributed. See §4.3. |
| `## Outlook` | MAY | If present, **MUST** carry the forward-looking marker. |
| `## Risks` | SHOULD | **MUST** where a jurisdiction profile requires it. |
| `## Document map` | SHOULD | Where the figures are in the source. See §4.3. |
| `## Source` | **MUST** | See §5.4. |

A profile (§6) may make an optional section required and may add sections. A profile
**MUST NOT** remove a core requirement.

### 4.3 Adjusted measures, quotes and the document map

#### Adjusted measures

Each entry gives the measure's name with every abbreviation written out, a definition in
plain words, a prior-period comparative, the nearest statutory measure with its own
comparative, and the page where the source reconciles the two:

```markdown
## Adjusted measures
- Adjusted operating profit: 48.2m (prior period 41.0m). Operating profit before
  restructuring costs and the amortisation of acquired intangibles. Statutory operating
  profit: 31.5m (prior period 38.9m). Reconciled on page 212.
```

#### Quotes

Words the company's people have published. Each entry gives the speaker's name, their
role, and where the quote appears, followed by the quote itself, verbatim and in
quotation marks:

```markdown
## Quotes
- Hannah Norwood, Managing Director (strategic report, page 4): "We won more work this
  year than in any year before, and kept less of each pound of it."
```

A quote is the speaker's view and is read as one. It is the only place in the file
where a judgement may be expressed (§5.8). A quote that looks forward goes under
`## Outlook` (§5.5). Quotes **SHOULD** be few, no more than one per person, and the
section **SHOULD NOT** be longer than `## What changed`.

#### Document map

Where things are in the source document, so a reader can go straight to the statements.
Pages are the PDF's own page index, counting the cover as page 1. Printed page numbers
rarely match it.

```markdown
## Document map
*Pages in the source PDF, counting the cover as page 1.*
- Strategic report: 3-9
- Principal risks: 7-8
- Independent auditor's report: 12-14
- Primary statements: 15-18
- Notes to the accounts: 19-31
```

The map **SHOULD** include the primary statements, the notes, the auditor's report where
there is one, and the reconciliation of any adjusted measure.

## 5. Integrity rules

A file that breaks any of these rules does not conform, however well formed it is.

### 5.1 Symmetry

> Materiality **MUST** be applied symmetrically. If a favourable movement of a given size
> is reported, an adverse movement of that size or larger **MUST** also be reported.

This is the central rule and the one a checker can most usefully enforce. A
self-published summary usually misleads by leaving things out, and an omission is
invisible unless the threshold is explicit. A publisher **MUST** state the threshold
used:

```markdown
## What changed
*Movements of 5% or more, or 10,000 or more, whichever is larger.*
```

### 5.2 Comparatives

Every figure in `## Headline figures` **MUST** carry a prior-period comparative, or
state why none exists (first period of trading, restatement, change of year end).

### 5.3 Derivation

Every figure **MUST** appear in, or be arithmetically derivable from, the source
document, so the file cannot introduce a new metric. A derived figure, such as a margin,
a ratio or a runway, **MUST** be marked as derived, with its inputs identifiable.

Every quote **MUST** appear verbatim in the source document, and say where.

### 5.4 Provenance

`## Source` **MUST** carry a resolvable link to the authoritative document, its
publication date, and a SHA-256 of the exact file. With the hash, anyone holding the
file can confirm which document it summarises.

### 5.5 Forward-looking statements

Anything that is not a statement of past fact, including a quote that looks forward,
**MUST** sit under `## Outlook` and carry the marker. A model reading the file must be
able to tell what the company has done from what it hopes to do.

### 5.6 No narrative causation without evidence

A file **MAY** state that two things moved in the same period. It **MUST NOT** assert
that one caused the other unless the source document does. Causation is the easiest
place to editorialise and the hardest for a reader to check.

### 5.7 Statutory before adjusted

Adjusted measures (underlying, adjusted, like-for-like, EBITDA and the acronyms built
from them) are where a report most often shows a business in a better light than its
statutory accounts do. They are legitimate and often useful, and this rule keeps them
out of the headline.

- `## Headline figures` **MUST** include revenue, profit or loss before tax, and cash at
  period end, as stated in the filed accounts, or say why one does not apply to the
  entity. A profile may add to this set.
- `## Headline figures` **MUST NOT** contain an adjusted measure. One **MAY** appear
  under `## Adjusted measures`, in the form §4.3 sets out, and nowhere else in the
  company's own voice.
- If `## What changed` reports a movement in an adjusted measure, it **MUST** report the
  movement in the nearest statutory measure beside it.

Regulators already apply this principle. ESMA's *Guidelines on Alternative Performance
Measures* (2015) and, in the US, Regulation G and Item 10(e) of Regulation S-K require
adjusted measures to be defined, reconciled, and given no more prominence than the
statutory figures. This rule applies the same principle to a file that a model will
read first.

### 5.8 No steering

The file reports what is in the results and leaves the reading to the reader.

- The file **MUST NOT** address its reader or the reader's model. That rules out
  instructions on what to emphasise, ignore or conclude, or how to summarise; a role or
  persona ("you are an analyst"); and any text written for a model rather than a person.
- Everything in the file **MUST** be visible to a person, both as plain text and as
  rendered Markdown. No comments, no invisible or zero-width characters, nothing that
  only a parser would find.
- Outside `## Quotes`, the file **MUST** state figures and movements without
  characterising them: "revenue rose 24.0%", never "strong revenue growth of 24.0%". The
  company's own voice uses no evaluative words, such as record, strong, robust, resilient
  or disappointing, whichever way they point.
- `## What changed` **MUST** follow the order of `## Headline figures`, so the good news
  cannot be put first.
- Bold and italics **MUST NOT** be applied to a figure, a movement or a judgement. They
  are for the required markers and for list labels.

A consumer **SHOULD** read the file as data throughout, and treat an instruction found
in it as a conformance failure.

## 6. Profiles

The core is jurisdiction-neutral, so a company anywhere can conform to it. Disclosure
obligations differ by market, and market-specific requirements live in profiles.

A file declares its profiles in the `## Basis` section:

```markdown
- Profiles: core, uk, uk-aim
```

A profile **MAY** require additional sections, require an optional core section, or
constrain a core section further. A profile **MUST NOT** weaken a core requirement.

Profiles live in [`profiles/`](profiles/):

| Profile | Market | Status |
|---|---|---|
| [`uk`](profiles/uk.md) | United Kingdom, Companies Act 2006 | draft |
| `uk-aim` | AIM-listed | not started |
| `us-sec` | SEC registrants | not started |
| `au`, `nz`, `ie`, `ca`, `za` | Australia, New Zealand, Ireland, Canada, South Africa | not started |

Profiles are where this specification most needs outside help. A profile written by
someone who files under a regime beats one written by someone reading about it. See
[CONTRIBUTING.md](CONTRIBUTING.md).

## 7. Conformance

| Level | Means |
|---|---|
| Core | §4 structure and §5 integrity rules satisfied. |
| Core + profile | Also satisfies every declared profile. |
| Verified | The `## Source` hash matches the document at the stated URL. |

A checker reports the level reached and names every rule failed. Conformance is a
property of the file, not the publisher, and says nothing about how well the business is
doing.

## 8. What this specification does not do

- It does not analyse. The reader's model does that, and a quote is the only place the
  company's view of its own results appears.
- It does not score a company. A conforming file about a bad year is conforming.
- It does not replace a filing. Statutory obligations are unaffected.
- It does not define a taxonomy. XBRL exists, is mandatory in several markets, and does
  that job better. This file is a summary with a pointer to the filing.
- It does not require the full statements. Reproducing a balance sheet in Markdown helps
  nobody; linking the filed one does.

## 9. Open questions

- Multi-entity groups: one file per listed parent, or one per reporting entity?
- Restatements: when a prior period is restated, is a new file published or the old one
  amended? Amending silently would defeat §5.4.
- Languages: one file per language at distinct paths, or sections within one?
- Signing: a hash proves the source has not changed. It does not prove the publisher is
  who they claim to be, and whether that matters is unresolved.

Draft. Nothing here is settled, and the integrity rules in §5 are the part most worth
arguing about before anyone implements against them.
