# Format specification: reading and submission builds (M12, D-0078)

**Governs:** `scripts/m11_build_latex.py` (build) and `scripts/m11_verify_latex.py` (checks).
**Rules source:** `OFFICIAL_REQUIREMENTS_2026-09-17.md`, the PLOS Water pages checked live on 2026-09-17, and the
official PLOS LaTeX template v3.8 (Apr 2026) in `submission/PLOS_latex_template.zip`.

One Markdown source, one converter and one placement function produce both files. The text, the numbers, the display
order, the captions, the tables and the bibliography are identical. They differ only in the lines listed under
"Mode differences", and the verifier checks that nothing else differs.

## Common typography (both builds, from the template)

| Element | Setting | Source |
|---|---|---|
| Class and size | `article`, 10 pt, US letter | template |
| Title page | template geometry: top 0.85 in, left 2.75 in, text width 5.25 in; footer offset 2.25 in into the margin | template |
| Body pages | `\newgeometry{top=0.85in,left=1in,right=1in,footskip=0.75in}`, text width 6.5 in | M11 build |
| Footer | template rule (2 pt) and page `n/N`, date left. **After `\newgeometry` the left offset is reset with `\fancyhfoffset[L]{0pt}`** so the rule and date sit inside the 1 in margins (baseline defect R01: rule ran from x = −90 to 540 pt) | M12 fix at cause |
| Body alignment | ragged right, paragraph indent 0.5 cm | template |
| Abstract | **justified** in a local group (`\rightskip=0pt`, `\parfillskip=0pt plus 1fil`); the rest of the document keeps the template's ragged right | author request |
| Headings | `\section*` for PLOS top-level sections; `\subsection*` in sentence case; no third level | template; PLOS limit of 3 levels |
| Captions | template `caption` settings (bold label, period separator, ragged right); bold title sentence ending with a period, then the legend | template |
| Figure label | "Fig N.", numbered by first citation | template (`\figurename{Fig}`) |
| Tables | cell-based `tabular` in `\footnotesize` with 3 pt column separation; caption above at normal size; notes below in `flushleft`; Tables 1 and 4 as `longtable` with the header repeated on continuation pages | template; PLOS table rules |
| Table notes | numbered notes; en dash = not available; "n/a" = not applicable | M6 conventions |
| References | `plos2025.bst` output embedded as `thebibliography`; URLs in the text font (`\urlstyle{same}`) | template style; M12 |
| Font encoding | `\usepackage[T1]{fontenc}`, so accented names and URL underscores copy correctly from the PDF; fonts remain embedded Type 1 | M12 (reference review R-06) |
| Display placement | `flafter` (a display is never set before the paragraph that cites it); `placeins` `\FloatBarrier` before each section and subsection heading and before Acknowledgments. Six variants were compiled and measured; without subsection barriers Results displays moved up to 8 pages from their citation, so the barriers stay and float pages stay centred | M12 |
| Float parameters | top 0.9, bottom 0.8, text 0.07, float page 0.75; up to 3 top, 2 bottom, 4 total | M12 |
| Order of end matter | Acknowledgments → References → Supporting information captions | PLOS submission guidelines (overrides the template's order) |
| PDF metadata | title "Draft manuscript (title to be filled later)"; empty author, subject, keywords and creator; no dates; no pdfTeX installation keys; links without coloured boxes | M12 privacy |
| Placeholders | "Title: TO BE FILLED LATER", "Authors: TO BE FILLED LATER", "Affiliations: TO BE FILLED LATER", "Corresponding author email: TO BE FILLED LATER", "Further acknowledgments: TO BE FILLED LATER" | author request |

## Mode differences

| Aspect | Reading copy (`main.tex`) | Submission copy (`PLOS_Water_manuscript_submission.tex`) | Rule |
|---|---|---|---|
| Output | `PLOS_Water_manuscript_REVISED_READING.pdf` | `PLOS_Water_manuscript_REVISED_SUBMISSION.pdf` | — |
| Figures | vector PDF from `figures/<id>.pdf` at print size (`\includegraphics` without scaling); 7.3 in figures centred with `\makebox[\linewidth][c]` and extending 0.4 in into each 1 in margin, so figure text stays at 8–12 pt | none: caption and label only; figures uploaded as `figures/upload/FigN.tif` | PLOS: "Do not include figures in your PDF" (submission only) |
| Figure float option | `[!htbp]` | `[!ht]` | — |
| Line numbers | none (`\linenumbers` never called) | continuous from the Introduction to the end of the body, off for the references (template convention), on again for the Supporting information captions; off inside long tables, whose notes carry none as float tables' do not | PLOS: "Use continuous line numbers" |
| Spacing | single | `\usepackage{setspace}` and `\doublespacing` (the template's own commented lines, activated); long tables in `spacing{1}`; floats single-spaced by `setspace` | PLOS: "double-spaced" |
| Header comment | names the file as the reading copy and points to the submission file | names the file as the submission form and points to the reading copy | — |

Every other line of the two files is identical (`scripts/m11_verify_latex.py`, check "Modes").

## Checks that enforce this specification

`scripts/m11_verify_latex.py` (269 checks across both modes) verifies, among others: template packages verbatim; the
footer offset reset and the footer rule inside the margins on every page of both PDFs; line numbers continuous and
strictly increasing in the submission PDF and absent from the reading PDF; double spacing only in submission; 17
embedded figures in reading and none in submission; section order ending Acknowledgments, References, Supporting
information; each display on the page of its citing paragraph or at most 4 pages later in the reading copy (the Indian subsection
cites four large displays within about one page of text) and 1 in submission, never before; embedded fonts; no local path in either PDF; identical bibliographies; every word of the submission PDF also
present in the reading PDF.

## Deviations from the template, each with its reason

1. `longtable`, `flafter`, `placeins` and `fontenc` (T1) added (template permits added packages; none removed).
2. `\urlstyle{same}` so URLs in references are set in the text font rather than typewriter.
3. `\hypersetup{hidelinks,…}` and PDF metadata suppression (privacy and a clean reading copy).
4. Body pages use 1 in margins (M11, kept) with the footer offset reset (M12).
5. End-matter order follows the journal's submission guidelines, not the template sample.
6. Abstract justified locally (author request); body stays ragged right as in the template.
