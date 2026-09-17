# Page layout QA: compact reading copy and submission copy (M13, D-0079)

**What this is.** A page-by-page quality record of the two PDFs built at M13, measured against the PLOS_2 baseline
(`PLOS_2.pdf`, the author's Overleaf compile of delivery commit `02b8f10`; 36 pages, SHA-256 `1fa3f5b0…5c0d9a`). It also records the scripted
float-layout sweep that chose the reading copy's float settings.

**How it was produced.**
- **Layout metrics.** `scripts/layout_metrics.py` reads ink from the PDF draw log and callout pages from the `.aux`
  labels.
- **Page renders.** `scripts/page_qa.py` writes:
  - contact sheets of every page;
  - 150 dpi renders of nine reading pages;
  - before-and-after pairs for every under-filled PLOS_2 float page;
  - `page_qa.json`.
  All of these are in `page_qa/`.
- **Sweep.** `scripts/layout_sweep.py`, with results in `layout_sweep/*.json` and `layout_sweep_*.log`.
- **Visual inspection.** The assistant viewed every page of both PDFs from the contact sheets (reading copy at 75 dpi,
  four pages per sheet).

**Status.** Built and inspected by the assistant. The author's own reading of the PDF remains open (M10 item C7).

## 1. Result against the baseline

| Measure | PLOS_2 (baseline) | Compact reading copy | Submission copy |
|---|---:|---:|---:|
| Pages | 36 | **28** | 34 |
| Text grid | page 1: 5.25 in, offset 2.75 in; body: 6.5 in, 1 in margins | one 7.0 in grid from page 1 (19 mm sides, 19 mm top, 23 mm bottom) | template: page 1 offset, then 6.5 in |
| Body / captions / references (pt, measured) | 10 / 10 / 10 | 10 / **9** / **9** | 10 / 10 / 10 |
| Table text (pt) | 8 | 8 | 8 |
| Smallest figure lettering, as printed | 5.6 (Fig 1 subscript) | **8.0** (all 17 figures) | no figures (captions only) |
| Float-only pages | 11 | 6 (p 9 holds Table 1; p 15 holds Table 3 and Fig 11) | 1 |
| Float-only pages filled below 70% | 6 (pp 12, 13, 14, 15, 20, 21) | **1** (p 14, 66%) | 0 |
| Text pages with an empty band over 25% of text height | 1 (p 19) | **0** | 1 (p 2, see §4) |
| Largest callout-to-display gap (pages) | 4 | **2** | 1 |
| Displays at gap 0 or 1 | 13 of 21 | 18 of 21 | 21 of 21 |
| Line numbers | none | none | continuous |
| Compile log issues (overfull ≥ 2 pt, float or reference warnings) | — | 0 | 0 |
| `m11_verify_latex.py` | 269/269 (M12) | 325/325 (both modes) | |

## 2. What changed, and why it works

| Cause in PLOS_2 (from `BASELINE_LAYOUT_AUDIT.md`) | M13 change | Effect |
|---|---|---|
| Template title page (2.75 in offset) then `\clearpage` and new geometry | Reading copy: one 19 mm grid from page 1 in a `READING PROFILE` block; no page break after the abstract | Introduction starts on page 1 |
| 6.5 in measure with 7.3 in figures pushed into the margins | 7.0 in measure; all figures redrawn at 7.0 in (Kwale 4.9 in, Malawi 4.2 in), at print size | lettering 8–12 pt as printed; nothing in the margins |
| Tall canvases that could not share a page (for example Figs 12 and 13 at 4.75 in; workflow 6.15 in) | Heights redrawn to page budgets (`FIGURE_LAYOUT_REGISTER.csv`); plotted values unchanged (`figures/source/` identical to the baseline tag) | two-figure pages full (pp 12, 17); Figs 12 and 13 share pages with text |
| Body-size captions and references | 9 pt captions (bold label and title) and 9 pt references with 1 pt item spacing | captions distinct from body text; the 52 references set compactly |
| Captions and notes long | Captions 1,249 → 930 words; table notes 1,010 → 804; SI captions 791 → 278 | `CAPTION_AND_NOTE_REVISION_REGISTER.csv` |
| A `\FloatBarrier` before every subsection (placeins flushes pending floats with `\newpage`, then `\clearpage`) | Barriers before each section and before subsections 4.1 and 4.2 only (sweep, §3); float pages at least 65% full and top-aligned | under-filled float pages 6 → 1; gaps ≤ 2 |
| Malawi map alone in a text-width band | Map (4.2 in) with its caption beside it | p 19 shares the page with text |

## 3. Float-layout sweep (R6a)

**What was held fixed.** The text, figures and captions. Only page-composition settings varied, and every
configuration was compiled from the real builder three times.

**Stages.**
1. **Stage 1, 36 configurations:**
   - barriers at every heading, at sections only, or at sections plus 4.1 and 4.2;
   - `placeins` default or `[below]`;
   - float-page fraction 0.5, 0.65 or 0.8;
   - figure placement `[!htbp]` or `[!tbp]`.
2. **Stage 2, 24 configurations.** The top three from stage 1, crossed with top fraction 0.85 or 0.9, float pages
   centred or top-aligned, and 3 or 4 floats per page.
3. **Stage 3, 4 configurations.** Barriers before 4.1 only, 4.2 only, 4.2 and 4.3, or 4.1 and 4.2.
4. **Stage 4, 4 configurations.** Reading-copy tables allowed on float pages (`[!htbp]`, `[!htp]`), with barriers at
   sections or at 4.1.
5. **Robustness.** The chosen configuration with ±12.5 pt and ±25 pt of vertical space inserted at the start of Results
   and of Discussion.

**Findings.**
- **Barrier placement and float-page fraction decide the layout.** The `placeins` option, `[!htbp]` against `[!tbp]`,
  top fraction, floats per page and table placement changed nothing measurable.
- **Every subsection barrier (PLOS_2 setting, fraction 0.75).** 29 pages, a 28% band on p 17 and an under-filled float
  page.
- **Sections only (fraction 0.65).** No bands and no under-filled float page, but Table 3 falls 3 pages after its
  callout. This is outside the verifier's limit, and table placement options do not change it (stage 4).
- **Chosen: sections plus 4.1 and 4.2 (fraction 0.65, top-aligned float pages).**
  - 28 pages, no band over 25%, one float page under 70% (p 14, 66%);
  - largest gap 2, with 18 of 21 displays at gap 0 or 1;
  - zero log issues.
- **Robustness.** Identical metrics at −12.5, +12.5 and +25 pt. At −25 pt one band appears (p 11), within the limit
  of one.

**Acceptance as planned.**

| Criterion | Planned | Chosen configuration | Note |
|---|---|---|---|
| Bands over 25% | ≤ 1 | 0 | |
| Float-only pages under 70% full | ≤ 2 | 1 | |
| Float-only pages | ≤ 4 | 6 (5 hold a figure) | The planned count did not allow for the long tables: Table 1 fills p 9 and Table 3 shares p 15 with Fig 11. The five figure pages are Fig 1 (5.9 in with caption, 70% of the text height) and the paired pages 12, 14 and 17; all but p 14 are more than 90% full. Recorded as a deviation from the plan |
| Largest gap | ≤ 2, ≥ 80% at ≤ 1 | 2; 86% | |
| Pages | target ≤ 27 | 28 | The body is 8,871 words after the scientific review restored qualifications (TRIAGE.md) |

## 4. Residual defects, each with its cause

| Page | Observation | Cause | Disposition |
|---|---|---|---|
| Reading p 11 | Blank band below the text: 23% of the text height (below the 25% threshold) | The barrier before 4.2 flushes Figs 6 and 7, which cannot follow Fig 5 on p 11 (order is kept) | Accepted. Removing that barrier moves Table 3 three pages from its callout (§3) |
| Reading p 14 | Float page with Figs 9 and 10, 66% full, top-aligned | Both figures are cited in one paragraph on p 13, and together they are too tall to share p 13 with Fig 8 | Accepted |
| Reading p 6 | Band of about 6% at the foot of the page | The heading "External transfer assessment" is kept with its first lines | Normal heading behaviour |
| Reading p 28 | Last page 31% used | End of the Supporting information list | Normal |
| Submission p 2 | Last two lines of the abstract, then the page break into body geometry | Template title-page geometry (5.25 in measure, double spacing) followed by the body `\newgeometry`. PLOS_2's submission copy had the same spill. A filled author block will lengthen page 1 anyway | Accepted; template-compliant |

## 5. Figures and captions as printed (reading copy)

One row per figure is in `FIGURE_LAYOUT_REGISTER.csv`: canvas, lettering range, caption words before and after,
callout and display pages, and page kind. In summary:
- all 17 figures are drawn at print size with lettering 8.0 pt or more;
- 11 share a page with text, and the other six stand on full float pages (pp 3, 12, 14, 17);
- every display follows its first callout on the same page or within two pages.

`m11_verify_latex.py` also confirms, in the reading PDF:
- every Arial span is at least 7.95 pt;
- captions are set at 9 pt and references at 9 pt;
- no URL line ends after its scheme colon;
- every link's printed text equals its target.

## 6. Before and after (images in `page_qa/`)

| PLOS_2 page, content | Compact page |
|---|---|
| p 12: Table 2, float page 51% full | p 10: Table 2 shares the page with Table 1's notes and the start of 4.1 |
| p 13: Fig 5 alone, 66% | p 11: Fig 5 with text |
| p 14 and p 15: Figs 6 and 7, each alone (57%, 60%) | p 12: both on one page, 99% full |
| p 20: Fig 12 alone, 62% | p 16: Fig 12 with text |
| p 21: Fig 13 alone, 60% | p 17: Figs 13 and 14 together, 92% full |

## 7. Robustness of the delivered layout on Overleaf

Overleaf compiles with a different TeX distribution (the PLOS_2 baseline was pdfTeX 1.40.29 on Overleaf against 1.40.28
locally, with identical text and the same figures on the same pages). A different TeX release can move a float by a
line. The sweep shows the chosen settings keep the gaps within 2 when the text shifts by up to 25 pt. The figures-per-page
signature of the local build, for comparison with the author's Overleaf PDF:

`p3 Fig1 · p5 Fig2 · p7 Fig3 · p8 Fig4 · p9 Table1 · p10 Table2 · p11 Fig5 · p12 Figs6–7 · p13 Fig8 · p14 Figs9–10 ·
p15 Table3, Fig11 · p16 Fig12 · p17 Figs13–14 · p19 Fig15 · p20 Fig16 · p21 Fig17, Table4 (continues p22)`
