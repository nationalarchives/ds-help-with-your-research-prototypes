# Box prototype

GOV.UK Prototype Kit project (Node) with `@nationalarchives/frontend` installed as a kit plugin. Pages are National Archives (TNA) branded via `app/views/layouts/main.html`.

## Project context

Alpha-phase prototyping for TNA research guidance. Full brief: [docs/brief.md](docs/brief.md) — read it when a design or content decision needs more than this summary.

**Who the system is working with:** Joe, the interaction designer on this project. The prototype work here serves the interaction designer deliverables in the brief: rapid low-fi prototypes, refined prototypes using the component library, and user journeys.

**Goal:** support users to teach themselves how to find and understand records, step by step, from wherever they start.

**Background:** TNA has nearly 400 research guides in varied styles. Discovery (March 2026) found guidance is distant from the point of need, hard to parse, and inconsistently written, marked up and maintained — which also feeds misleading AI summaries. A standing principle is that staff and users share the same view of the same content.

**Two patterns alpha is exploring:**

1. In-context support and signposting.
2. Long-form, progressively detailed support, for users and machines (agents) alike. This is the senior interaction designer's delivery focus.

**Hypotheses:**

1. Support content at the point of need helps users adapt and refine their research tactics.
2. A consistent, predictable template with progressive detail lets users and agents find the level of detail they need for their next step.
3. Reusable content support components make content easier to maintain.

**Design considerations:**

- Two user groups: "quick answer" and "investigative". Modes of use include troubleshooting and first-time introduction (three modes in total).
- Content should be progressive, not repetitive or laborious, and users should move freely between support and functionality or services.
- Content must work for agents as well as people.

**Out of scope:** the catalogue, the website homepage, Explore the Collection and guided search. Scope creep is the biggest named risk.

**Phases:**

- Phase 1, ice sculpting (5 weeks): throwaway, rapid, low-fi interactive prototypes; one focus area per week (for example the early modern period). Grounded in the possible but not constrained by existing solutions.
- Phase 2, prioritisation and refinement (5 weeks): a few ideas refined using the component library, with new design components as needed and rules for their use.

## Reference resources

- **TNA Design System:** https://design-system.nationalarchives.gov.uk/ — the documented components, styles and patterns. `@nationalarchives/frontend` in `node_modules` is its code; check `nationalarchives/components/<name>/macro-options.json` and `fixtures.json` there for component options.
- **TNA beta catalogue:** https://beta.nationalarchives.gov.uk/catalogue/ — TNA's redesigned catalogue UI and UX, still in development. Use it as the reference for how catalogue search, results and record pages look and read.
- The beta site uses components and patterns that are not in the design system (class names without the `tna-` prefix, for example `etna-accordion`, `record-details`, `record-hierarchy`, `related-records`, `etna-results`). Where a prototype needs one of these, first try to get close with design system components. If that is not enough, recreate it as a custom component under the component rules below and note in the register that it mirrors the beta site.
- The catalogue itself is out of scope for the alpha. Catalogue pages in prototypes are context for testing support content, not designs for the catalogue.

## Catalogue hierarchy

Research notes: [docs/catalogue-hierarchy.md](docs/catalogue-hierarchy.md) — read it before designing in-context help for any catalogue level. Findings are from the beta catalogue (7 October 2026) and the mandatory levels are not yet confirmed by collection experts.

- Seven levels: department, division, series, sub-series, sub-sub-series, piece, item.
- **Mandatory: department, series, piece.** The rest are optional. Every piece is in exactly one series; nothing in TNA's own records sits outside a series.
- The reference is the path: SP 12/1/69 is department SP, series 12, piece 1, item 69. Divisions and sub-series have no reference of their own.
- What a level means varies by collection: a will is an item, a Star Chamber or Chancery case is usually a piece. A piece can be a bound volume or a single lawsuit.
- Beta's "Catalogue hierarchy" omits some levels, has no "search within this" link, and its "What is this page?" help is the same generic text at every level.
- Working design idea (untested): guidance attaches at series level and is inherited by pieces and items beneath it, with stacking (department, series, subject), per-record overrides and a fallback where no guidance exists.
- Misfits to design for: records held at other archives, mixed series (SP 12), artificial series (PROB 1, "Miscellanea"), and record types spread across several series (wills in PROB 1, 10 and 11). Series is the anchor for where guidance attaches, not always for what it says.
- Authors (collection experts) should write about record types and tag them to series; they should not have to think in catalogue levels.

## Prototypes

- Each prototype lives in its own folder under `app/views/`, and is listed on the index page (`app/views/index.html`), which is the team's record of prototypes and versions and is not shown in research sessions.
- `app/views/test-journey/`: set-up journey — guide list, research guide, catalogue record.
- Do not use `pageTitle` for long on-page headings: the TNA layout truncates it for the browser tab title. Use a separate variable for the `<h1>`.

## Rules

### Communication

- Never use the first person ("I", "me", "my", "we") to refer to the assistant. Refer to it as "The system". This applies to replies, and to anything written into project files.
- Never praise Joe: no compliments on ideas, questions, decisions or work. State facts, findings and recommendations only.

### Components

- Reach for existing components first: National Archives frontend (`@nationalarchives/frontend`), then GOV.UK Frontend and the installed kit plugins.
- When mocking up ideas, it is fine to create simple new components and patterns without asking first. Keep them simple.
- Isolate every custom component or pattern so it can be reviewed on its own:
  - markup in `app/views/components/<name>/` (a Nunjucks macro), never pasted inline across pages;
  - styles in `app/assets/sass/components/_<name>.scss`, imported from `app/assets/sass/prototype-components.scss` (not `application.scss`: the kit bundles all of GOV.UK Frontend into `application.css`, and the TNA layout does not load it);
  - class names prefixed `proto-` so they are never mistaken for TNA (`tna-`) or GOV.UK (`govuk-`) components.
- Raise every one: say in the reply that a custom component or pattern was created, what it is for, and which existing components were considered. Add it to the register in `docs/custom-components.md`.
- Do not modify or override the TNA or GOV.UK components themselves without raising it.
