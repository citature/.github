# Contributing to citature

Thanks for your interest. citature builds agent-native tools over public US
federal records — the product promise is that every answer ships with the
receipt behind it.

## Workflow

- `main` is protected; all changes land through a pull request. Direct pushes
  are blocked for everyone, including maintainers.
- Keep PRs focused. The commit message is the record — explain *why*, not just
  *what* (the diff shows what). Structured messages are welcome for large
  changes.
- CI must be green before merge.
- Merges are squash-merges that preserve the authored commit message.

## The bar for anything that touches data

citature's contract is provenance, so changes to retrieval, joins, or output
carry an extra requirement:

- **Every claim keeps its locator.** A record must stay re-fetchable from the
  upstream government source it came from. A change that drops, weakens, or
  guesses a citation is a correctness bug, not a cosmetic one.
- **Cite the source of record, never an aggregator.** If a figure cannot be
  traced to FEC, USASpending, SAM.gov, or Grants.gov, it does not ship.
- **Date anything that rots.** Coverage counts, cycle ranges, and refresh
  cadences go out with an as-of date or a link to a page that carries one.
- **Caveats are content, not footnotes.** Coverage gaps and match uncertainty on
  cross-source joins belong in the output, not in a README nobody reads.

## Reporting bugs

Open an issue with the tool or query you ran, the output, and what you expected.
For anything involving provenance or personal data, follow
[SECURITY.md](./SECURITY.md) instead of filing publicly.

## Scope

citature reports what the public record says. It is not legal, financial, or
eligibility advice, it is entity-level only, and it does not render verdicts.
Contributions that push past that line will be declined regardless of quality.
