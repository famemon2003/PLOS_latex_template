# R3 — Page layout audit for the reading draft (M14, D-0080)

*This note is a record of the manuscript's preparation. It names files in the manuscript's own working tree, which is not part of this repository; only the LaTeX sources, figures, bibliography, compiled PDFs and these notes are distributed here.*


The author's request (package file 05): fix the figure-page gaps without shrinking labels. Nothing in this stage
changes the text, the figures' plotted values or the type size. Body 10 pt, captions 9 pt, references 9 pt, and the
smallest lettering inside any figure is 8.0 pt — the same as the baseline, measured by
`scripts/figure_placement_register.py`. `figures/source/` is byte-identical to tag `pre-plos3-refinement-20260917`.

The submission build is untouched: it keeps the PLOS template's geometry, double spacing and continuous line
numbers, and PLOS typesets from the source in any case.

## 1. The baseline faults, and the cause of each

| Baseline page | Fault | Cause found in `submission/latex/main.tex` |
|---|---|---|
| p 3 | Fig 1 alone on a float page, splitting the sentence "…requires the model to / generalise" | `\floatpagefraction` 0.65 with Fig 1 at 71% of the text height: LaTeX tries a float page before a top float |
| p 10 | Table 1's notes stranded after its last row | the notes ran to 188 words, longer than the space the long table left |
| p 11 | a band of empty space above the section heading | the `\FloatBarrier` before §4.2 flushed Figs 6 and 7 early |
| p 12, p 14 | a gap *between* two figures on one float page | `\@fpsep` left at the article default, 8 pt plus 2fil, which out-stretched `\@fpbot` (1fil), so the spare space opened between the floats rather than at the foot |
| p 19 | the Malawi caption dangling below the map | the two minipages were `[b]`-aligned |

## 2. What was changed

| Setting | Baseline | Now | Effect |
|---|---|---|---|
| `\@fptop` / `\@fpsep` / `\@fpbot` | 0 pt / unset / 1fil | 0 pt / 10 pt plus 2 pt minus 2 pt / 0 pt plus 1fil | float pages pack from the top with the spare space at the foot; the inter-figure gaps close |
| `\floatpagefraction` | 0.65 | 0.8 | a float must fill 80% of a page before it may have one to itself |
| Fig 1 placement | `!htbp` | `!tb` (`FIGURE_PLACEMENT` override) | Fig 1 sets at the top of its page with Methods text below it |
| `\FloatBarrier` positions | every section and subsection heading | section headings plus §4.1 and §4.2 only | the barrier no longer flushes a queue mid-section; Table 3 sets on its callout page |
| Malawi minipages | `[b]` | `[t]` with `\vspace{0pt}` | artwork and caption top-align |
| India figure canvases | 4.8 in, 3.9 in | 4.4 in, 3.5 in | Figs 5 and 6 share one float page (plotted values unchanged) |
| Long tables | header repeated | header repeated under a "Table *n*. (continued)" label | a continuation page says what it continues |

The barrier choice was re-swept after the text and notes were final, because the shorter notes moved the break
points. Ten configurations were built by the real builder and measured
(`staging/plos2_compact_revision/scripts/layout_sweep.py`, new `grid` stage; results in `layout_sweep/grid.json`):

- **barriers at section headings** (M13's choice), float-page fraction 0.8, 0.85 or 0.9, table placement `!ht` or
  `!htp` — six configurations, all rejected. Table 3 fell three pages from its callout in every one, and the table
  placement specifier made no difference at all, because what holds Table 3 back is the figure queue ahead of it,
  not its own permitted positions. At 0.9 the draft fits 26 pages, but the gap sum rises from 15 to 22.
- **barriers at every heading**, fraction 0.8 or 0.9 — rejected: 28 pages with three under-filled float pages.
- **barriers at §4.1 and §4.2**, fraction 0.8 or 0.9 — both accepted, and identical on every measure (27 pages,
  largest gap 2, 20 of 21 displays at gap 0 or 1, gap sum 13, no under-filled float page). 0.8 was chosen as the
  lower of two equal results, being the closer to the class default.

## 3. The reading draft now, page by page

27 pages (28 at the baseline). "Band" is the largest empty vertical run inside the text block, as a fraction of the
text height; the footer zone is excluded.

| Page | Displays | Band | Notes |
|---|---|---:|---|
| 1–2 | — | 5%, 3% | title block, abstract, Introduction |
| 3 | Fig 1 | 4% | Fig 1 at the page top with 17 lines of text below it; no sentence split |
| 4 | — | 3% | |
| 5 | Fig 2 | 9% | |
| 6 | Fig 3 | 3% | |
| 7 | — | 3% | |
| 8–9 | Fig 4, Table 1 (spans both) | 3%, 3% | Table 1's notes sit directly under its last row on p 9, with §4.1 following |
| 10 | Table 2 | 3% | |
| 11 | Fig 5, Fig 6 | 4% | two figures, one page, no gap between them |
| 12 | Fig 7, Table 3 | 3% | Table 3 on its callout page |
| 13 | Fig 8, Fig 9 | 3% | |
| 14 | Fig 10, Fig 11 | 4% | |
| 15 | Fig 12 | 3% | |
| 16 | Fig 13, Fig 14 | 6% | |
| 17 | — | 3% | |
| 18 | Fig 15 | 4% | |
| 19 | Fig 16 | 3% | |
| 20–21 | Fig 17, Table 4 (spans both) | 5%, 3% | Discussion begins under Table 4's notes |
| 22–24 | — | 3%, 3%, 3% | Discussion, Acknowledgments, Supporting information |
| 25–27 | — | 0% | References |

No page carries a band over 9%; the planning rule was 25%. Every display sets on or after its callout page, the
largest gap is 2 pages (Fig 7), and 20 of 21 displays are at a gap of 0 or 1. Three pages carry figures with only
6–12 lines of text; none is a bare float page, and none is filled below 70%.

Robustness: the chosen configuration was rebuilt with the body padded by −25, −12.5, +12.5 and +25 pt. All four
hold at 27 pages with no under-filled float page and a largest gap of 1 or 2, so a small copy-edit does not
reopen the faults above (`layout_sweep/robust.json`).

## 4. Not changed, and why

- **No global font change, no `[H]`, no blanket `\clearpage`.** The author asked for the gaps to be fixed without
  small labels; every fix above is a placement or glue setting.
- **The submission build's page 2 spills two lines.** The cause is the template's own title block
  (`\vspace*{0.2in}`) under double spacing. Removing it would alter the template geometry the verifier checks, and
  PLOS re-typesets the submission, so the spill is left and recorded here.
- **Table 3's column headings are long** and stack three lines deep. Each names a metric and the validation design
  it belongs to, and no other column carries that distinction, so they stay.

## 5. Cross-links

`R3_FIGURE_PLACEMENT_REGISTER.md` (per figure: canvas, share of the text height, lettering, callout and display
pages) · `FORMAT_SPEC.md` · `R5_REVIEW_TRIAGE.md` · renders in `renders/`
