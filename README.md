# rathodkaransinh.github.io

Personal site — https://rathodkaransinh.github.io/

| File | What it is |
|---|---|
| `index.html` | The portfolio. Single file: inline CSS, ~40 lines of vanilla JS, inline SVG diagram. No build step. |
| `resume.html` / `resume.pdf` | A4 résumé **with photo** — the India-facing version, linked from the site. |
| `resume-intl.html` / `resume-intl.pdf` | Same résumé **without photo**, for US/UK/EU applications. Not linked publicly; send the URL directly. |
| `og.png` | 1200×630 link-preview card. |
| `.nojekyll` | Serve files as-is; skip GitHub's Jekyll pass. |

## Regenerating the PDF

The résumé uses `@page { margin: 0 }`, so the print dialog's margin and scale
settings matter. Headless Chrome bypasses the dialog and cannot get them wrong:

```sh
for v in resume resume-intl; do
  google-chrome --headless=new --no-pdf-header-footer \
    --print-to-pdf=$v.pdf $v.html
done
```

Both use strict A4 page boxes: content past 297 mm is clipped, not reflowed.
Opening either `.html` in a browser shows a red badge on any sheet that
overflows, so a bad edit is visible immediately. The badge never prints.

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
