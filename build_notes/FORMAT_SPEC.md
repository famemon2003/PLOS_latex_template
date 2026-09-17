# Format specification: compact reading draft and submission copy (M14, D-0080)

*This note is a record of the manuscript's preparation. It names files in the manuscript's own working tree, which is not part of this repository; only the LaTeX sources, figures, bibliography, compiled PDFs and these notes are distributed here.*


**Governs:** `scripts/m11_build_latex.py` (build) and `scripts/m11_verify_latex.py` (checks). Supersedes the M13
specification (`staging/plos2_compact_revision/FORMAT_SPEC.md`); M14 changes are marked.
**Rules source:**
- the official PLOS LaTeX template v3.8 (Apr 2026) in `submission/PLOS_latex_template.zip`;
- the PLOS Water pages checked live on 2026-09-17 (`OFFICIAL_ROUTES_2026-09-17.md`);
- the corpus layout measurements (`CORPUS_LAYOUT_MEASUREMENTS.md`), which describe the published layout, not a
  submission rule.

One Markdown source, one converter and one placement function produce both files. The text, numbers, display order,
captions, tables and bibliography are identical. The files differ only in the lines listed under "Mode differences",
and the verifier checks that nothing else differs.

**The reading copy is not the journal's typeset article.** It is an author-prepared layout for reading and review:
- no PLOS logo, DOI, dates, editor or copyright lines;
- placeholders stay "TO BE FILLED LATER".

## Common typography (both builds)

| Element | Setting | Source |
|---|---|---|
| Class and size | `article`, 10 pt, US Letter | template |
| Body alignment | ragged right, paragraph indent 0.5 cm | template |
| Abstract | justified in a local group | author request |
| Headings | `\section*` for PLOS top-level sections; `\subsection*` in sentence case; no third level | template; PLOS |
| Figure label | "Fig N.", numbered by first citation; caption title in bold | template |
| Tables | cell-based, `\footnotesize` (8 pt), 3 pt column separation, column widths as fractions of `\linewidth` so one table file fits both measures; Tables 1 and 4 as `longtable` with the header repeated | template; PLOS |
| Table notes | numbered notes; en dash = not available; "n/a" = not applicable | M6 |
| References | `plos2025.bst` output embedded as `thebibliography`; URLs in the text font; no line break after a URL scheme's colon (`\UrlNoBreaks` adds ":") | template; M13 reference QA |
| Font encoding | T1; Type 1 fonts embedded | M12 |
| Display placement | `flafter` (never before the citing paragraph); `\FloatBarrier` before each section, before subsections 4.1 and 4.2, and before Acknowledgments (M14 sweep of ten configurations) | M14 sweep (`R3_PAGE_LAYOUT_AUDIT.md`) |
| Float parameters | top 0.9, bottom 0.8, text 0.07, float page 0.8 (M14); up to 3 top, 2 bottom, 4 total | M14 sweep |
| End matter | submission: Acknowledgments → References → Supporting information captions (PLOS order); reading draft: see Mode differences | PLOS submission guidelines |
| PDF metadata | neutral title; empty author, subject, keywords and creator; no dates; links without coloured boxes | M12 privacy |
| Placeholders | "Title: TO BE FILLED LATER", "Authors: …", "Affiliations: …", "Corresponding author email: …", "Further acknowledgments: TO BE FILLED LATER" | author request |

## Mode differences

| Aspect | Compact reading copy (`main.tex`) | Submission copy (`PLOS_Water_manuscript_submission.tex`) | Rule |
|---|---|---|---|
| Output | `PLOS_Water_REFINED_READING.pdf` | `PLOS_Water_REFINED_SUBMISSION.pdf` | M14 (D-0080) |
| Page geometry | one grid from page 1: 19 mm left, right and top, 23 mm bottom, footskip 10 mm (M14; 8 mm left 0.4 mm between a descender and the footer rule); text width 7.0 in; footer offset reset from page 1 | template title page (left 2.75 in) | M13, M14 |
| Leading | `\linespread{1.04}` (about 12.5 pt on 10 pt) for the longer line | double spacing (`setspace`) | PLOS: double-spaced |
| Captions | 9 pt (`\captionsetup{font=small}`, also for long tables), skip 4 pt | template size (10 pt) | — |
| References | 9 pt, 1 pt between entries | template size | — |
| Float spacing | text–float 10 pt, float–float 8 pt, in-text 8 pt | template | — |
| Figures | vector PDF from `figures/<id>.pdf` at print size (`\includegraphics` without scaling); Malawi map (4.2 in) set beside its caption in two minipages | none: caption and label only; figures uploaded as `figures/upload/FigN.tif` | PLOS: "Do not include figures in your PDF" (submission) |
| Figure float option | `[!htbp]` | `[!ht]` | — |
| Line numbers | none | continuous from the Introduction; off for references (template convention); on for the SI captions | PLOS: continuous line numbers |
| Long tables | one `longtable`, header row repeated, continuation pages labelled "Table *n*. (continued)" (M14) | — | M14 |
| Value and unit | tied in prose and captions so neither breaks across a line; table cells keep breakable spaces, their columns being fixed and narrow (M14) | — | M14 |
| Reference breaks | `\interlinepenalty` in `thebibliography`, so no entry and no URL is split across a page (M14) | — | M14 |
| Float pages | top-packed: `\@fptop` 0 pt, `\@fpsep` 10 pt plus 2 pt minus 2 pt, `\@fpbot` 0 pt plus 1fil, so spare space falls at the foot and never between floats (M14) | template defaults | — |
| Figure placement | `[!htbp]`; Fig 1 (workflow) `[!tb]`, so it is set at a page top with text below rather than alone on a float page (M14); Malawi map and caption in top-aligned minipages (M14) | `[!ht]` | — |
| End matter | Acknowledgments → **Supporting information** → References (M14, author request) | Acknowledgments → References → Supporting information captions | PLOS submission guidelines (submission) |
| Where the settings live | one delimited block `% >>> READING PROFILE … % <<< READING PROFILE` before `\begin{document}` | — | M13 |

The reading-profile block may contain only:
- `\usepackage{etoolbox}`;
- `\geometry{…}` and `\linespread{…}`;
- `\fancyhfoffset[L]{0pt}`;
- the three float-separation lengths;
- `\captionsetup` (including for long tables);
- `\AtBeginEnvironment{thebibliography}{\small}` and `\apptocmd{\thebibliography}{…}`;
- one `\makeatletter … \makeatother` line setting `\@fptop`, `\@fpsep` and `\@fpbot` (M14).

The verifier checks the block's position and its commands. Every other line of the two files is identical.

## Figure canvases (reading copy)

All main figures are drawn for a 7.0 in measure at print size. Lettering is 8–12 pt; the smallest span in any figure
PDF is 8.0 pt. Heights are budgeted so that a figure and its caption fit at the top of a page, and so that the two-figure
pages in the Indian and transfer results fit together. Values are unchanged. Canvases and printed placement are listed
in `FIGURE_LAYOUT_REGISTER.csv`.

## Checks that enforce this specification

`scripts/m11_verify_latex.py`, 415 checks across both modes (M14). Among others:
- **Structure:** template packages verbatim; the reading-profile block, its position and its allowed commands; the
  submission geometry string.
- **Pages:** the footer rule inside each mode's margins on every page; page n/N.
- **Line numbers:** continuous and increasing in the submission PDF; absent from the reading PDF.
- **Type sizes as printed:** reading body 10 pt, captions 9 pt, references 9 pt; submission 10/10/10 pt.
- **Figures:** lettering at least 7.95 pt as printed; 17 figures embedded in the reading copy and none in the submission
  copy.
- **Displays:** each on its citing paragraph's page or at most 2 pages later in the reading copy, at most 1 in the
  submission copy, never before.
- **URLs:** no line ending with "http:" or "https:"; every link's printed text equal to its target.
- **Across modes:** identical bibliographies; every submission word present in the reading PDF, independent of line
  breaks and hyphenation.
- **Text:** protected qualifications present in both, including the AI-disclosure review status; superseded wording
  absent; "retrospective(ly)" absent outside Materials and methods and at most once there (M14).
- **End matter:** order checked per mode; the SI block is compared across modes at one position (M14).

## Deviations from the template, each with its reason

1. `longtable`, `flafter`, `placeins`, `fontenc` (T1) and, in the reading copy only, `etoolbox` are added. The template
   permits added packages, and none is removed.
2. `\urlstyle{same}` and a colon added to `\UrlNoBreaks`, so references never break after "https:".
3. `\hypersetup{hidelinks,…}` and PDF metadata suppression, for privacy and a clean copy.
4. Submission body pages use 1 in margins with the footer offset reset (M11, M12).
5. The reading copy uses its own compact geometry and type sizes (this specification), for reading and review only.
6. End matter follows the journal's submission guidelines in the submission form; the reading draft lists the Supporting information before the References at the author's request (M14).
7. The abstract is justified locally (author request); the body stays ragged right.
