# PLOS Water manuscript (LaTeX)

This repository holds the LaTeX version of a PLOS Water research article, built on the official PLOS LaTeX template
(v3.8, April 2026). It is linked to Overleaf.

**Status:** technically built and PLOS-template compliant, pending the author decisions listed with the manuscript
(the title, the author list and affiliations, the corresponding author's email, acknowledgments, and the
verification of every citation by the author). It is not ready to submit until those are settled.

## Files

| Path | What it is |
|---|---|
| `main.tex` | The manuscript: one file, bibliography embedded, no graphics (PLOS requirement). Compile this. |
| `references.bib`, `plos2025.bst` | The bibliography source and the template's style, needed only to regenerate the embedded references. |
| `figures/Fig1.tif` to `Fig6.tif` | Figure files, uploaded to PLOS separately from the manuscript. |
| `pdf/PLOS_Water_manuscript_submission.pdf` | `main.tex` compiled. |
| `review/` | A reading copy with the figures drawn in. **Not for PLOS submission.** |
| `build_notes/` | How the file was compiled and checked, and the reference-rendering check. |
| `official_template/` | The PLOS template files as downloaded, for reference. |

## Compiling

On Overleaf, set the main document to `main.tex` (Menu, Main document) and the compiler to pdfLaTeX. Locally:

```
pdflatex main.tex
pdflatex main.tex
```

No BibTeX run is needed. Supporting Information files are uploaded to PLOS separately and are not in this
repository.

## Provenance

`main.tex`, `references.bib`, the figures and the notes are generated from the article's source files by scripts in
the author's project repository; edit the source there and regenerate rather than editing `main.tex` by hand, or
record any hand edit so it can be carried back.
