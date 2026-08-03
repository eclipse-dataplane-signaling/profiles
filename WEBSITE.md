## Static Rendering and Web Deployment

This repository contains the set of artifacts that make up the normative and non-normative sections of the Data Plane
Signaling Profiles. All artifacts are bundled by the [respec framework](https://www.respec.org) which takes care of
rendering a static website.

### Conventions

The following extensions to the basic markdown syntax are used in this specification project. Keep them handy and
navigating the document will be easy.

- Referencing an external specification document. [Respec Docs](https://respec.org/docs/#references-0)
    - with identifier inline `[[foreign-spec-id]]`
    - with the foreign spec's display name inline `[[[foreign-spec-id]]]`
    - referencing a particular section in a remote document works via ordinary markdown links. The reference has to be
      added to the `References` section manually (if it's not already there).
- Defining terminology: A term is defined by wrapping it in
  `<dfn>Defineable</dfn>`. [Respec Docs](https://respec.org/docs/#definitions-and-linking)
- Custom section IDs: If various sections have the same heading, they must be given a unique id manually via
  `{#my-custom-section-id}` that can then be used for referencing
  it. [Respec Docs](https://respec.org/docs/#example-specifying-a-custom-id-for-a-heading)
- Referencing within the document. Please note that despite separation in multiple markdown files, there is only one
  html document. References to sections must be flat `(#section)` instead of path-based
  `../specifications/profile.md#some-section`.
    - with the sections number and display name inline `[[[#my-section-id]]]`
    - If that's not desired, ordinary links work as well. `[my custom link](#my-section-id)`
    - referencing terminology: `[=Defineable=]`. This will work out of the box with Plurals such that `[=Definables=]`
      refers to the definition of `<dfn>Defineable</dfn>`.
- Code blocks work natively like in markdown.

### Previewing locally

The spec content lives in markdown files that `index.html` pulls in via `data-include`, which the browser loads with
`fetch()`. Browsers block `fetch()` over the `file://` protocol, so **opening `index.html` directly will not work** —
serve the folder over HTTP instead:

```bash
python3 -m http.server 8000   # then open http://localhost:8000/
```

Alternatives: `npx serve` (or `npx http-server`) from the repo root, or an IDE preview that serves over HTTP —
IntelliJ's built-in "Open in Browser" and VS Code's *Live Server* extension both work. ReSpec loads its engine and the
mermaid plugin from a CDN, so an internet connection is required. Edit a markdown file and refresh to see changes.

Once schema files or additional versioned artifacts are added, locally execute the commands from the
[autopublish](.github/workflows/autopublish.yaml) workflow's "Copy files for correct web access" step to reproduce the
published folder layout. All resulting folders and files are duplicates, gitignored and don't break anything.

### Publishing

The [autopublish](.github/workflows/autopublish.yaml) workflow renders and deploys the site to GitHub Pages on every
push to `main`, publishing the current branch under the `HEAD` path and every git tag under its own version path. The
root redirects to `HEAD`.
