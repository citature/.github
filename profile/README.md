<!-- The h1 sits below the brand lockup by design: the mark leads the hero.
     The a11y requirement MD041 protects — a top-level heading naming the
     document — is satisfied at "# Answers with receipts" below. MD041 stays
     enforced for every other file in the repo. -->
<!-- markdownlint-disable-next-line MD041 -->
<div align="center">

<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="https://raw.githubusercontent.com/citature/.github/main/profile/assets/mark-dark.svg">
  <img
    alt="citature"
    src="https://raw.githubusercontent.com/citature/.github/main/profile/assets/mark.svg"
    width="112"
    height="112">
</picture>

# Answers with receipts

**Agent-native tools over public US federal records.**

Every citature answer ships with the receipt behind it — citations to the exact
upstream government source, retrieval timestamps, coverage caveats, and match
provenance on every cross-source join. Nothing is asserted without a locator you
can re-fetch yourself.

[citature.com](https://citature.com) · [Apify Store](https://apify.com/citature)

</div>

---

## The data

Primary sources only. Public-domain US federal records, ingested nightly from the
source of record — never an aggregator. What each nightly run *finds* depends on
the upstream's own cadence, so coverage is stated per source rather than as one
number:

- **FEC** — campaign finance: 217M+ itemized contribution records across the
  2020–2026 cycles, plus committees and candidates. FEC publishes bulk files on
  the two-year election cycle, so the ingest advances when new files land rather
  than daily.
- **USASpending** — federal awards and contracts, keyed on recipient UEI. New
  records land daily.
- **SAM.gov** — contract opportunities and solicitations. New records land daily.
- **Grants.gov** — grant opportunities. Advances when the upstream publishes.

No date is printed here on purpose. Every answer carries its own `retrieved_at`
(when citature fetched the record) alongside the source's own `as_of` date, which
is a separate field — a receipt on the answer beats an as-of line on a page that
nobody regenerates.

## The tools

Fourteen tools in two families, all live. Each is callable from the MCP server or
as a standalone [Apify actor](https://apify.com/citature). The mapping is not
one-to-one — several tools share an actor, and `opportunity_search` spans both
SAM.gov and Grants.gov.

Descriptions below are the tool descriptions as registered, so an agent reading
this page and an agent reading the server see the same contract.

### Money

| Tool | Contract |
| --- | --- |
| `contributions_by_state` | Individual FEC contribution dollars for an election cycle, totaled by the contributor's state of origin, largest first. |
| `contributions_by_committee_type` | Individual FEC contribution dollars for an election cycle, totaled by the recipient committee's type, largest first. |
| `awards_by_agency` | Federal contract-award dollars for a fiscal year, ranked by the awarding agency. Declares the exact agency crosswalk in the receipt. |
| `awards_by_state` | Federal contract-award dollars for a fiscal year, ranked by place-of-performance state (a native award field, no join). |
| `awards_by_recipient` | Federal contract-award dollars for a fiscal year, ranked by recipient keyed on the universal federal awardee UEI. Declares the UEI crosswalk. |
| `follow_the_money` | Itemized contribution dollars flowing into an FEC committee, aggregated by the contributor's state of origin. Entity-level only; declares the committee-id crosswalk. |
| `committee_lookup` | Look up one FEC committee by its committee id. Returns the committee or a null answer with a citation when none is found. |
| `candidate_lookup` | Look up one FEC candidate by its candidate id. Returns the candidate or a null answer with a citation when none is found. |
| `committee_search` | Prefix-search FEC committees by name (case-insensitive, bounded). Each result carries the citature entity id next to the FEC id. |
| `candidate_search` | Prefix-search FEC candidates by name (case-insensitive, bounded). Each result carries the citature entity id next to the FEC id. |

### GovCon

| Tool | Contract |
| --- | --- |
| `recompetes_expiring` | Federal contracts whose period of performance ends within a YYYY-MM month window, soonest first, each with the incumbent (by UEI) and its obligation. Optional NAICS (prefix) and awarding-agency (name) filters. Declares the exact UEI and agency-code crosswalks. |
| `incumbent_history` | A federal contractor's contract lineage per agency and NAICS, by exact UEI or recipient-name prefix (at least one required): contract count, total obligated, fiscal-year span, latest period-of-performance end. Declares the exact UEI and agency-code crosswalks. |
| `agency_buying` | Federal contract obligations, contract counts, and distinct-contractor counts by awarding agency, NAICS, and fiscal year. All filters optional. Declares the exact agency-code crosswalk and the UEI behind the distinct-contractor count. |
| `opportunity_search` | Open and forecasted procurement opportunities across SAM.gov and Grants.gov, newest first, filterable by NAICS, agency, posted-date window, and active state. Single-source native records, so no cross-source join; cites each contributing source. |

### Actors

| Actor | Family |
| --- | --- |
| [`funding-entity-lookup`](https://apify.com/citature/funding-entity-lookup) | money |
| [`fec-contributions`](https://apify.com/citature/fec-contributions) | money |
| [`federal-awards`](https://apify.com/citature/federal-awards) | money |
| [`follow-the-money`](https://apify.com/citature/follow-the-money) | money |
| [`govcon-recompetes`](https://apify.com/citature/govcon-recompetes) | govcon |
| [`incumbent-history`](https://apify.com/citature/incumbent-history) | govcon |
| [`agency-buying-patterns`](https://apify.com/citature/agency-buying-patterns) | govcon |
| [`citature-mcp`](https://apify.com/citature/citature-mcp) | mcp |

Every tool above is delivered as agent-native calls from one MCP server,
published as the [`citature-mcp`](https://apify.com/citature/citature-mcp) actor
and served over Streamable HTTP on the `/mcp` path.

The connection host is assigned by the Apify platform when the actor starts in
Standby mode, so it is not a fixed address this page can quote — take it from the
actor's listing. Nothing here states an endpoint it cannot cite.

## The rules

The standing caveats, quoted from the literals every receipt and every tool
description ships:

- Research over public-domain federal records — not legal, financial, or
  eligibility advice.
- citature reports what the record says. It never renders a compliance verdict,
  a screening pass/fail, or a recommendation.
- Entity-level records only (committees, candidates, recipients, agencies,
  contracts). No individual-person data.

Money is integer cents.

---

<div align="center">
  <sub>
    <b><a href="https://citature.com">citature.com</a></b>
    · answers with receipts, from primary sources
  </sub>
</div>
