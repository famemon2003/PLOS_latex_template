# PLOS Water manuscript (LaTeX)

This repository holds the LaTeX source of a PLOS Water research article, built on the official PLOS LaTeX template
(v3.8, April 2026). It is linked to Overleaf.

**Status:** built; not cleared for submission; placeholders and author items remain (title, authors, affiliations,
corresponding author email, further acknowledgments, and the author's verification of every citation).

## Two entry points, one text

| File | What it is | Output |
|---|---|---|
| `main.tex` | **Clean reading copy.** Figures embedded after the paragraph that first cites them, no line numbers, single spacing, justified abstract. Compiles by default on Overleaf. | `pdf/PLOS_Water_manuscript_REVISED_READING.pdf` |
| `PLOS_Water_manuscript_submission.tex` | **PLOS submission form.** Captions only (PLOS asks for figures as separate files), continuous line numbers, double spacing, Supporting information captions after the references. | `pdf/PLOS_Water_manuscript_REVISED_SUBMISSION.pdf` |

Both files are generated from the same source and differ only in the lines listed in `build_notes/FORMAT_SPEC.md`.

## Other files

| Path | What it is |
|---|---|
| `figures/<id>.pdf` | The 17 figures as vector PDFs, drawn into `main.tex`. |
| `figures/upload/Fig1.tif` to `Fig17.tif` | The figure files for separate upload to PLOS, numbered by first citation. |
| `references.bib`, `plos2025.bst` | The bibliography source and the template's style, needed only to regenerate the embedded references. |
| `build_notes/` | Compile record, format specification, caption audit, figure numbering map and QA summaries. |
| `official_template/` | The PLOS template files as downloaded, for reference. |

## Compiling

On Overleaf, `main.tex` is the main document (compiler pdfLaTeX). To compile the submission form, choose
Menu > Main document > `PLOS_Water_manuscript_submission.tex`. Locally, run pdflatex three times on either file:

```
pdflatex main.tex
pdflatex main.tex
pdflatex main.tex
```

No BibTeX run is needed, because the references are embedded. Supporting Information files are uploaded to PLOS
separately and are not in this repository.

## Provenance

The `.tex` files, `references.bib`, the figures and the notes are generated from the article's source files by scripts
in the author's project repository; edit the source there and regenerate rather than editing the `.tex` files by hand,
or record any hand edit so it can be carried back.
