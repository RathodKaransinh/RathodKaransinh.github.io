# rathodkaransinh.github.io

Personal site — https://rathodkaransinh.github.io/

| File | What it is |
|---|---|
| `index.html` | The portfolio. Single file: inline CSS, ~40 lines of vanilla JS, inline SVG diagram. No build step. |
| `resume.html` | A4 résumé. Strict WYSIWYG page boxes — screen matches PDF exactly. |
| `resume.pdf` | Generated from `resume.html` (see below). |
| `og.png` | 1200×630 link-preview card. |
| `.nojekyll` | Serve files as-is; skip GitHub's Jekyll pass. |

## Regenerating the PDF

The résumé uses `@page { margin: 0 }`, so the print dialog's margin and scale
settings matter. Headless Chrome bypasses the dialog and cannot get them wrong:

```sh
google-chrome --headless=new --no-pdf-header-footer \
  --print-to-pdf=resume.pdf resume.html
```

## Regenerating the OG card

`og.png` is a screenshot of a 1200×630 HTML page:

```sh
google-chrome --headless=new --window-size=1200,630 \
  --screenshot=og.png og.html
```

## Editing

Everything is static — edit the HTML and push. GitHub Pages redeploys in
under a minute. Hard-refresh to beat the CDN cache.

If this ever outgrows a single file, Astro is the natural next step: it ships
zero JS by default and keeps React available for the parts that need it.
