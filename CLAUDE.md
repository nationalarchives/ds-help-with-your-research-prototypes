# Help with your research prototypes

A prototype built with the GOV.UK Prototype Kit (Node), with The National Archives Design System (`@nationalarchives/frontend`) installed as a kit plugin. Pages are National Archives (TNA) branded via `app/views/layouts/main.html`.

These are throwaway prototypes for user research. Content in them is placeholder.

## Running it

- `npm install`, then `npm run dev`. The kit serves on http://localhost:3000.

## Reference resources

- **TNA Design System:** https://design-system.nationalarchives.gov.uk/ — the documented components, styles and patterns. `@nationalarchives/frontend` in `node_modules` is its code; check `nationalarchives/components/<name>/macro-options.json` and `fixtures.json` there for component options.
- **GOV.UK Prototype Kit:** https://prototype-kit.service.gov.uk/docs/

## Prototypes

- Each prototype lives in its own folder under `app/views/`, and is listed on the index page (`app/views/index.html`).
- Do not use `pageTitle` for long on-page headings: the TNA layout truncates it for the browser tab title. Use a separate variable for the `<h1>`.

## Components

- Reach for existing components first: National Archives frontend (`@nationalarchives/frontend`), then GOV.UK Frontend and the installed kit plugins.
- Isolate every custom component or pattern so it can be reviewed on its own:
  - markup in `app/views/components/<name>/` (a Nunjucks macro), never pasted inline across pages;
  - styles in `app/assets/sass/components/_<name>.scss`, imported from `app/assets/sass/prototype-components.scss` (not `application.scss`: the kit bundles all of GOV.UK Frontend into `application.css`, and the TNA layout does not load it);
  - class names prefixed `proto-` so they are never mistaken for TNA (`tna-`) or GOV.UK (`govuk-`) components.
- Add every custom component to the register in `docs/custom-components.md`.
- Do not modify or override the TNA or GOV.UK components themselves without raising it.
