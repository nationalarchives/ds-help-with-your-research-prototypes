# Catalogue hierarchy research

Notes from a dig into how The National Archives' catalogue is structured, done on 7 October 2026 using the beta catalogue (https://beta.nationalarchives.gov.uk/catalogue/). Focus: early modern collections — State Papers (SP), Chancery (C), Exchequer (E), Prerogative Court of Canterbury wills (PROB) and Star Chamber (STAC).

A condensed version is in `CLAUDE.md`.

## Limits

- Based on about 15 record pages and a handful of searches on beta, which is still in development. The existing Discovery catalogue was not checked.
- Counts are beta's totals for each collection across all dates, not just 1485 to 1714.
- Which levels are mandatory is The National Archives' cataloguing convention as the system understands it, consistent with the beta data but **not yet confirmed by collection experts (CEE)**.

## The seven levels

| Level | Mandatory? | Has its own reference? | What it is | Early modern example |
|---|---|---|---|---|
| Department | Yes | Yes (SP) | The body that created or collected the records, shown as a letter code | SP: records assembled by the State Paper Office, 1231 to c1888 |
| Division | No | No | A grouping of related series | State Papers Domestic, Edward VI to Charles I (8 series) |
| Series | Yes | Yes (SP 12) | The main "folder": one type of record from one source | SP 12: State Papers Domestic, Elizabeth I, 1558 to 1603 (290 volumes) |
| Sub-series | No | No | A grouping inside a series | In SP: "Papers relating to the Atterbury Plot" |
| Sub-sub-series | No | No | A grouping inside a sub-series | In C 2 (Chancery pleadings): "Z plaintiffs: originally 1 bundle" |
| Piece | Yes | Yes (SP 12/1) | The physical thing that can be ordered: a volume, bundle, roll or box | SP 12/1: letters and papers for November to December 1558 |
| Item | No | Yes (SP 12/1/69) | A single document inside a piece | SP 12/1/69: "Copy of SP 12/1 no 68" |

- Within The National Archives' own records nothing sits outside a series: every piece belongs to exactly one series, and every series to exactly one department.
- The reference spells out the path: SP 12/1/69 is department SP, series 12, piece 1, item 69. A reference always has at least three parts.
- Optional levels have no reference of their own. Beta labels them "Division within SP" or "Sub-sub-series within C 2".

## Counts by level on beta

| Collection | Divisions | Series | Sub-series | Sub-sub-series | Pieces | Items |
|---|---|---|---|---|---|---|
| SP (State Papers) | 10 | 127 | 321 | 82 | 14,060 | 195,992 |
| C (Chancery) | 20 | 251 | 582 | 159 | 771,636 | 739,262 |
| E (Exchequer) | 8 | 277 | 1,163 | 395 | 245,611 | 146,212 |
| PROB (wills) | 4 | 57 | 82 | 76 | 66,674 | 1,198,745 |
| STAC (Star Chamber) | 0 | 13 | 45 | 0 | 55,638 | 2,330 |

## What makes it hard to know where you are

- **The level a document is described at varies by collection.** A will is an item. A Star Chamber case is usually a piece. In C 2 a single case is a piece (for example C 2/ChasI/W121/54). "Piece" can mean a whole bound volume or one lawsuit.
- **Beta's "Catalogue hierarchy" leaves levels out.** SP 12/1/69 shows department, series, piece, item. The division "State Papers Domestic, Edward VI to Charles I" describes itself as series organised by reign, which should include SP 12, yet SP 12's hierarchy shows no division. The C 2 sub-sub-series shows only department and series above it.
- **There is no "search within this" link** on department, series or piece pages. The only route is the search filters (collection and level).
- **Searching a reference is not scoped.** Searching "SP 12" for pieces returns Ordnance Survey map sheets named "SP 12 NW" first, not State Papers.
- **The existing in-context help is generic.** Every record has a "What is this page?" tab, with the same text at every level: what the catalogue is, not what a series or piece is.
- **Counts are missing.** The hierarchy says "Unknown number of records" at each level.

## What doesn't fit the pattern

There are no orphan items, but there are four kinds of misfit:

- **Records held elsewhere.** The catalogue also lists records at other UK archives (about 480,000 results for "wills" alone). These don't follow the department, series, piece structure.
- **Mixed series.** SP 12 is one series but holds every kind of government paper. Guidance can explain the collection, not the document.
- **Artificial series.** Some series were assembled by archivists, not by the original office: PROB 1 (famous people's wills pulled out of the main files). "Miscellanea" series are the same problem. Their contents share a shelf, not a type.
- **One record type across many series.** Wills are in PROB 11, PROB 10 and PROB 1; State Papers Domestic are split into a series per reign. Guidance belongs to the record type, not to one series.

Series is the reliable anchor for *where* guidance attaches, but not always the right unit for *what* it says.

## Design idea: guidance inherited down the hierarchy

An assumption to test, not something beta does today.

Guidance attaches to a level of the catalogue, and every record below shows it automatically. Series is the natural place: everything in PROB 11 is a registered copy of a will proved in the Prerogative Court of Canterbury, so what "proved" means, why the date isn't the date of death and how the registers are arranged are true of all of it.

| Page the user is on | What the help panel shows |
|---|---|
| Series PROB 11 | The full series help: what these records are, how they are arranged, how to search within them |
| Piece PROB 11/337 | A short line on what this piece is (one register volume), plus the series help in brief |
| Item PROB 11/337/27 | A short line on what this item is (one will), the one or two series points most likely to confuse, and a link to the rest |

Help could attach at more than one level and stack, most specific first:

- **Department (PROB):** what the court was and who used it.
- **Series (PROB 11):** what a will register is and how to read an entry.
- **Subject (Wills and probate):** links to the long-form guide.

The user's question changes by level:

- **Department or division:** "What is this body and which series should I look in?"
- **Series:** "What kind of records are these, how are they arranged, and how do I search inside?"
- **Piece:** "Is this one document or a volume of many, and can I order or view it?"
- **Item:** "What does this document tell me, and what do the terms mean?"

What it gives the project:

- **Coverage:** 57 series in PROB against roughly 1.2 million items. Help for a few dozen series covers nearly every record.
- **Maintenance:** one fix to a block updates every page that shows it (hypothesis 3 in the brief).
- **Orientation:** the panel can say "This will is part of PROB 11", which helps with "what folder am I in".

## For the people writing the guidance

Experts write a guide as a whole piece; this model shows it in fragments. Three things would make it workable:

- **They write about record types, not catalogue levels.** An expert writes "PCC wills" once and tags it to the series it covers (PROB 11, PROB 10, PROB 1). The split by level is done for them.
- **They can see where each block appears** — on a series page, a piece page and an item page — before publishing.
- **Each block has a named owner**, which the brief already asks for.

## Maintenance and exceptions

- **Default plus override:** records inherit from their series unless a record or piece has its own note. Shakespeare's will (PROB 1/4) would carry an override, because PROB 11's help would be wrong for it.
- **A fallback:** where no series guidance exists yet, show department-level or generic help, so coverage can grow gradually, starting with the most used series.
- **A flag for misfits:** mixed and artificial series are marked so they get lighter, collection-level help.
- **Uneven levels:** the short "what this is" line has to be written per series, not per level, because a piece is a volume in PROB 11 but a lawsuit in C 2.

## Open questions

- Do collection experts confirm that department, series and piece are always present?
- How many early modern series are "clean" enough for series-level guidance? If most are mixed or artificial, tagging guidance to record type and subject may matter more than tagging to series.
- Does series-level help shown on an item page read as relevant, or as generic text the user skips?
- Does the in-context panel get noticed and trusted on a record page?
- Does "short answer first" satisfy troubleshooting users without hiding what first-time users need to learn?
