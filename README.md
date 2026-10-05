# financials.txt

An agreed, plain-text way to hand financial results to a language model.

Annual reports are written to persuade, and everyone knows it: a front section that
makes the case, then the financial statements. The figures are all there. They are also
complex, and the narrative in front of them is written to be read first.

A growing share of readers no longer read it first. They give the report to a language
model and say: *analyse this.* The model reads past the narrative to the statements, and
it will do that whatever the company publishes.

`financials.txt` is a small Markdown file a company publishes alongside its results. It
sets out what the document is, where its figures are, what they are, and what the
company's people say about them, in a way that cannot tilt the reading. It gives the
analysis a straight start without doing the analysis itself.

```
https://example.com/.well-known/financials.txt
```

- [The specification](SPEC.md): the jurisdiction-neutral core
- [The template](template.txt): a blank file to fill in
- [Profiles](profiles/): market-specific requirements
- [Examples](examples/)
- [Contributing](CONTRIBUTING.md)
- [Governance](GOVERNANCE.md): who decides, and what would change that

## The problem with the obvious version

A format that lets a company publish a flattering summary, which a language model then
treats as authoritative, is worse than having no standard at all. It is spin wearing a
credibility badge, and it would be adopted enthusiastically for exactly that reason. A
file written to be given to a model is also the obvious place to try to steer one.

So the integrity rules are the specification. The central one:

> **Materiality must be applied symmetrically.** If a favourable movement of a given
> size is reported, an adverse movement of that size or larger must also be reported,
> and the threshold must be stated.

Omission is how a self-published summary misleads without lying. A stated, symmetric
threshold makes omission checkable, and that is the only thing that makes the rest of
the file worth trusting.

The others: every figure and every quote traceable to the filed accounts, no new metrics
introduced, statutory figures before adjusted ones, forward-looking statements marked,
causation never asserted beyond what the source says, a hash tying the file to the
document it summarises, and nothing in the file that instructs, flatters or hides.
Quotes from the company's people are welcome, attributed and verbatim. They are the only
place a judgement may appear.

## Status

Draft 0.1, October 2026. Nothing is settled. The integrity rules in §5 are the part most
worth arguing about before anyone implements against them, and the open questions in §9
are genuinely open.

## Who runs this

**`financials.txt` is stewarded and funded by [EM04](https://em04.com)**, which builds
financial reporting software and implements this specification. This is stated up front
because finding it out later is what destroys a standard's credibility.

A `.org` does not make a specification neutral, and today EM04 decides what goes in.
[GOVERNANCE.md](GOVERNANCE.md) sets out what that means, what EM04 gets out of it, and
the stated trigger at which it stops: once three other organisations have published a
conforming file or shipped an implementation, EM04 holds at most one vote.

Trusting it does not require trusting EM04, because walking away is cheap. The licence
is CC0, the format has no vendor fields, and there is no signup. A standard that only
its author can implement is a proprietary format with better marketing, so this one is
deliberately boring to implement: Markdown with required headings and eight rules. A
spreadsheet and an afternoon will produce a conforming file. Any vendor, any in-house IR
team, any accountant can emit one, and a checker can validate anyone's.

Profiles are the part that most needs people who are not us. A UK profile written by
someone who files under the Companies Act beats one written by someone who read about
it, and we have no standing at all on SEC, ASX or TSX. Those are open.

## Prior art, and why this is not it

| | |
|---|---|
| **[llms.txt](https://llmstxt.org)** | Jeremy Howard, 2024. The right idea at site level; this extends the pattern to results. |
| **XBRL / iXBRL** | Mandatory in several markets and better than this at structured data. Built for regulators parsing by rule, not for reading, which makes it a poor prompt. |
| **The annual report** | The authoritative document. Designed for print, which is the whole problem. |

`financials.txt` replaces none of them. It points at the filing and is checkable
against it.

## Licence

The specification is CC0. Use it, fork it, implement it, ignore it. A standard nobody
can adopt without permission is not a standard.
