# R3 — Figure placement register (M14, D-0080)

*This note is a record of the manuscript's preparation. It names files in the manuscript's own working tree, which is not part of this repository; only the LaTeX sources, figures, bibliography, compiled PDFs and these notes are distributed here.*


Reading draft `PLOS_Water_REFINED_READING.pdf` (27 pages); baseline `PLOS_3_BASELINE.pdf` (28 pages).
Lettering is measured in the figure's own PDF and printed at scale 1 (no `\includegraphics` option scales a figure).
Text height is 673 pt; 'share' is the canvas height as a fraction of it, before the caption.

| Figure | Id | Canvas | Share | Lettering | Caption words | Callout page | Display page | Gap | Page | Placement | Baseline page |
|---|---|---|---:|---|---:|---:|---:|---:|---|---|---:|
| Fig 1 | `workflow` | 7.0 × 5.9 in | 63% | 8.0–9.0 pt | 54 | 2 | 3 | 1 | shares the page with text | page top, [!tb] | 3 |
| Fig 2 | `evidence-map` | 7.0 × 3.9 in | 42% | 8.0–8.0 pt | 50 | 4 | 5 | 1 | shares the page with text | full width | 5 |
| Fig 3 | `validation-designs` | 7.0 × 1.75 in | 19% | 8.0–9.0 pt | 39 | 6 | 6 | 0 | shares the page with text | full width | 7 |
| Fig 4 | `action-distribution` | 7.0 × 2.5 in | 27% | 8.0–8.5 pt | 36 | 8 | 8 | 0 | shares the page with text | full width | 8 |
| Fig 5 | `india-map` | 7.0 × 4.4 in | 47% | 8.0–8.0 pt | 58 | 10 | 11 | 1 | float page | full width | 11 |
| Fig 6 | `india-intervals` | 7.0 × 3.5 in | 37% | 8.0–8.5 pt | 55 | 10 | 11 | 1 | float page | full width | 12 |
| Fig 7 | `india-support-cadence` | 7.0 × 2.6 in | 28% | 8.0–11.0 pt | 62 | 10 | 12 | 2 | shares the page with text | full width | 12 |
| Fig 8 | `design-discrimination` | 7.0 × 3.9 in | 42% | 8.0–9.0 pt | 44 | 12 | 13 | 1 | shares the page with text | full width | 13 |
| Fig 9 | `prevalence-prauc` | 7.0 × 2.6 in | 28% | 8.0–8.5 pt | 40 | 13 | 13 | 0 | shares the page with text | full width | 14 |
| Fig 10 | `channel-comparison` | 7.0 × 2.5 in | 27% | 8.0–8.5 pt | 51 | 13 | 14 | 1 | shares the page with text | full width | 14 |
| Fig 11 | `transfer-verdicts` | 7.0 × 2.6 in | 28% | 8.0–8.5 pt | 62 | 14 | 14 | 0 | shares the page with text | full width | 15 |
| Fig 12 | `transfer-ordering` | 7.0 × 3.6 in | 39% | 8.0–11.0 pt | 67 | 14 | 15 | 1 | shares the page with text | full width | 16 |
| Fig 13 | `transfer-calibration` | 7.0 × 3.6 in | 39% | 8.0–11.0 pt | 58 | 15 | 16 | 1 | float page | full width | 17 |
| Fig 14 | `kwale-map` | 4.9 × 3.9 in | 42% | 8.0–8.5 pt | 61 | 15 | 16 | 1 | float page | full width | 17 |
| Fig 15 | `malawi-map` | 4.2 × 4.8 in | 51% | 8.0–8.5 pt | 43 | 17 | 18 | 1 | shares the page with text | beside its caption | 19 |
| Fig 16 | `product-evidence` | 7.0 × 5.85 in | 63% | 8.0–8.5 pt | 64 | 19 | 19 | 0 | shares the page with text | full width | 20 |
| Fig 17 | `documentation-threshold` | 7.0 × 2.9 in | 31% | 8.0–8.5 pt | 47 | 20 | 20 | 0 | shares the page with text | full width | 21 |

- Smallest printed lettering in any figure: 8.0 pt.
- Figures sharing a page with text: 13 of 17.
- Largest callout-to-display gap: 2 page(s).
- Open item (M14 R5, production review MINOR-10): Fig 1 sets "NO3" without a subscript, where the body text and the table notes write NO₃. Correcting it means regenerating the figure's lettering, which this stage's rule against redrawing figures excludes; it is carried to the author items.
- Canvas changes at M14: `india-map` 4.8 → 4.4 in and `india-intervals` 3.9 → 3.5 in, so that Figs 5 and 6 share one float page and the queue clears a page earlier. Plotted values are unchanged (`figures/source/` is identical to tag `pre-plos3-refinement-20260917`).
