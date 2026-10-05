# Profile: `uk`

United Kingdom · Companies Act 2006 · draft 0.1 · 4 October 2026

This profile extends [the core specification](../SPEC.md) and is declared as:

```markdown
- Profiles: core, uk
```

## Scope

This profile applies to companies incorporated in the United Kingdom and required to
prepare a strategic report under the Companies Act 2006. That means all companies other
than those that are small, or that would be small were they not part of an ineligible
group.

Small companies may use the core on its own.

## What the core does not already cover

The Companies Act requires a strategic report containing, for every company in scope:

- a fair review of the company's business;
- a description of the principal risks and uncertainties facing the company;
- to the extent necessary for an understanding of the business, the main trends and
  factors likely to affect its future development, performance and position.

Supplementary requirements apply to larger companies, to public interest entities, to
quoted companies and to AIM companies.

Source: [BDO, *Strategic Report: A Practical Guide*, June 2026](https://www.bdo.co.uk/getmedia/0d4accce-f7d2-44c2-a41e-052c8d6972a5/Strategic-Report-A-Practical-Guide-(June-2026).pdf)
and the FRC's [*Guidance on the Strategic Report*](https://media.frc.org.uk/documents/Guidance_on_the_Strategic_Report__Appendix_II_and_Appendix_III.pdf).

## Requirements added by this profile

### U1: `## Risks` becomes required

`## Risks` is optional in the core. The Act requires principal risks and uncertainties,
so a UK summary that omits them is summarising something the filing was obliged to
contain.

Each entry **SHOULD** be a principal risk as described in the strategic report, not a
general statement about trading conditions.

### U2: `## Outlook` becomes required where the filing contains trends and factors

Where the strategic report discusses main trends and factors likely to affect future
development, the summary **MUST** carry `## Outlook` reflecting them, under the core's
forward-looking marker (SPEC §5.5).

Where the filing genuinely contains none, state that:

```markdown
## Outlook
*Forward-looking. Not a forecast and not a guarantee.*
- The strategic report does not discuss expected future trends.
```

### U3: Companies House identifiers

`## Identity` **MUST** carry the registered company number. Where the entity is
registered in Scotland or Northern Ireland, the prefix is part of the number (`SC`,
`NI`).

### U4: Filing reference in `## Source`

`## Source` **MUST** name Companies House and the filing date where the accounts have
been filed, and **SHOULD** link the Companies House record:

```markdown
## Source
- Document: https://example.com/reports/2026-annual.pdf
- Published: 2026-10-04
- SHA-256: 3f786850e387550fdab836ed7e6dc881de23001b7a4f0c9b2e5d8a6c1f3b9e02
- Filed: Companies House, 2026-10-04
- Register: https://find-and-update.company-information.service.gov.uk/company/09847213
```

### U5: Framework must be named

`## Basis` **MUST** state the framework: `UK-adopted IFRS`, `FRS 102`, `FRS 102
Section 1A` or `FRS 105`. The same figure means different things under FRS 105 and
UK-adopted IFRS, and a model cannot infer which applies.

### U6: Section 172 statement

Where the company is required to publish a section 172(1) statement, the summary
**SHOULD** link to it. It **MUST NOT** be paraphrased: a summary of a statement about
how directors had regard to stakeholder interests is a new claim, and the core's
derivation rule (SPEC §5.3) does not permit one.

## Not yet established

Each of these gaps needs someone who files under the regime.

- **AIM.** AIM-listed companies carry obligations beyond the Companies Act. The `uk-aim`
  profile is not started, and the specific content requirements of **AIM Rule 19 have
  not been verified against the London Stock Exchange's AIM Rules for Companies**.
  Secondary sources discuss Rule 26 (corporate governance disclosure) far more often,
  and the two should not be conflated. Do not cite Rule 19 here until someone has read
  the rulebook.
- **Interim and half-year results.** Scope, and whether a lighter profile is warranted.
- **Structured digital reporting.** UK listed companies have iXBRL tagging obligations.
  Whether `## Source` should reference the tagged filing separately from the PDF is
  unresolved, though it probably should.
- **Charities, LLPs, community interest companies.** Different regimes, out of scope
  for now, and each would want its own profile rather than exceptions in this one.
- **Dormant and small companies.** Filing abridged or filleted accounts. Whether a
  meaningful summary is even possible is an open question.

## Worked example

See [`../examples/norwood-kite.txt`](../examples/norwood-kite.txt) for a fictional UK
limited company reporting under FRS 102 and declaring `core, uk`.
