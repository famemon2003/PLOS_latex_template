# R2 — Table, figure and SI caption counts, and the relocation matrix (M14, D-0080)

*This note is a record of the manuscript's preparation. It names files in the manuscript's own working tree, which is not part of this repository; only the LaTeX sources, figures, bibliography, compiled PDFs and these notes are distributed here.*


The author's request (package files 03 and 12): shorten all four table captions **and** their lengthy notes, keeping
every fact that a reader needs to interpret the table. Nothing was deleted: each clause that left a caption or note
is now in one named destination, and a script checks the destination string exists.

Measured by `staging/plos3_final_refinement/scripts/caption_register.py`, which reuses the M13 register against tag
`pre-plos3-refinement-20260917` and writes `CAPTION_AND_NOTE_REVISION_REGISTER.csv` (one row per caption and per note
block). Word counts from `text_counts.py`.

## 1. Totals

| Apparatus | Baseline | Now | Change |
|---|---:|---:|---:|
| Table titles and legends (4 tables) | 120 | 39 | −81 |
| Table notes (4 blocks) | 804 | 491 | −313 |
| Figure captions (17) | 930 | 893 | −37 |
| SI catalogue entries (12) | 278 | 186 | −92 |
| **Total** | **2,132** | **1,609** | **−523** |

## 2. Table by table

| Table | Title words | Legend words | Note words | Notes |
|---|---:|---:|---:|---:|
| Table 1. Monitoring actions and reassessment evidence across 26 contexts | 7 → 8 | 16 → 0 | 188 → 120 | 5 → 4 |
| Table 2. Indian monitoring records and decision-relevant cells by parameter | 8 → 8 | 16 → 0 | 191 → 111 | 4 → 3 |
| Table 3. Model performance by validation design and information channel | 8 → 8 | 24 → 0 | 266 → 125 | 5 → 3 |
| Table 4. Monitoring evidence and actions across application settings | 7 → 7 | 26 → 0 | 138 → 123 | 5 → 2 |

The legend sentence is gone from all four: in each case the column headers already carried it. Titles stay within
6–15 words. Table 4's note count fell furthest (5 → 2) because its notes had repeated scope statements that Table 1
and the Results already make; its word count barely moved, because the review returned three caveats to it (§4).

PLOS requires the title above the table and the notes below it, which both builds do; the notes are table footnotes,
which PLOS permits, and must not be stripped when body footnotes are removed at copy-edit.

## 3. Relocation matrix

Each row: what left the caption or notes, where it is now, and the string the register checks.

Reproduced from `CAPTION_AND_NOTE_REVISION_REGISTER.csv`, which is generated, not written by hand. Captions and SI
entries not listed had nothing to move.

| From | Content | Destination, and the string checked |
|---|---|---|
| Table 1 notes | local archives are not national estimates | `tables/final/T-04.md`: "local, not national, samples" |
| Table 1 notes | one determination over the 23-product catalogue | Results: "one determination over the 23-product catalogue" |
| Table 1 notes | no reference method named for a traceable reference workflow | Results: "a reference method the rule does not name" |
| Table 2 notes | the interval describes the archive as held | Results: "describes the archive as held rather than the programme as now designed" |
| Table 2 notes | not a ranking of severity | `tables/final/T-02.md`: "not a ranking of severity" |
| Table 2 notes | a cell is not a well or a person | Table 4 note 2 (see below) |
| Table 2 notes | nitrate figures are not carried between analyses | Methods: "no nitrate figure is carried between the two analyses" |
| Table 2 notes | revisit cadence detail | S3 Table legend; Table 2 keeps the pointer "revisit cadence: S3 Table" |
| Table 3 notes | none of the designs is a claim about transfer to an unmonitored country | Methods: "is not carried to the transferred scores" |
| Table 3 notes | the Model B minus A column is the quantity to read | Results: "by 0.0215 to 0.0643 in ROC-AUC" |
| Table 3 notes | runs not re-run; no prediction-level file retained | S1 Text: "no prediction-level file was retained, and no fitted model object is recorded" |
| Table 3 notes | Model A and Model B calibration slopes (all twelve values) and the DeLong paired-observation sizes | S1 Text, verbatim; `m6_verify_tables.py` checks each pair, as "0.7608 against 0.8883" |
| Table 4 notes | definition of ordering | Framework §2: "ordering locations so that confirmatory sampling is sequenced" |
| Table 4 notes | a cell is not a well or a person, from the Table 2 notes | `tables/final/T-04.md`: "not prevalence, and a cell is not a well or a person" |
| Table 4 notes | the thermal-spring and surface-water caveat | Results: "come from one thermal spring" |
| Fig 1 | step-by-step description of strands, harmonisation and documentation | Methods: "Five populations are kept separate" |
| Fig 2 | why station locations are not drawn (redistribution terms unconfirmed) | `submission/DATA_AVAILABILITY_STATEMENT.md`: "No GEMStat record is redistributed or mapped in this article" |
| Fig 5 | nitrate basis 50 mg/L as NO₃ | `tables/final/T-02.md`: "Nitrate is classified at 50 mg/L as NO₃" |
| Fig 8 | pointer to the retained result tables | `tables/final/T-03.md`: "Values are from retained result tables (S1 Text)" |
| Fig 9 | prevalence is not population prevalence | Methods: "not population prevalence" |
| Fig 10 | the comparison is not evidence of spatial generalisation | Results: "is not evidence of spatial generalisation" |
| Fig 12 | the CGWB portal pH interval lies wholly below 0.5 | Results: "the CGWB portal pH interval, 0.4784 to 0.4964, lies wholly below 0.5" |
| Fig 13 | calibration-in-the-large not assessed; no local recalibration; fitting archive surface water against groundwater | Results: "Calibration-in-the-large was not assessed"; Methods: "crosses water-body type as well as geography" |
| Fig 14, Fig 15 | the archives are local and support no national statement | Methods: "bounded local archives, not national samples" |
| Fig 17 | the abstention is about the evidence base, not a ranking | Discussion §5.2: "its abstention describes the evidence base" |
| S1 Text, S6 Fig, S11 Table entries | contents inventory, design counts and window, interval and TDS-scale explanation | `manuscript/SI_FULL_CAPTIONS.md`, each with its own checked string |

`caption_register.py` exits non-zero if any checked string is absent, if a figure title exceeds 15 words, or if a
figure caption falls outside 35–65 words (50–85 for a two-panel figure). It passes with no failures.

## 4. Facts returned to the notes by the R5 reviews

Shortening removed five things a reader does need. They are back, and `m6_verify_tables.py` now checks each:

| Table | Returned | Finding |
|---|---|---|
| T-01 note 4 | the three further exclusions: not the action it would change to, who supplies it, or its frequency | R5-M07 |
| T-02 note 2, T-04 note 2 | "operational **project** convention" — the convention is this project's, not an external standard | R5-M06 |
| T-03 note 3 | which population violates the DeLong independence assumption ("which revisited stations violate") | R5-M05 |
| T-04 note 2 | thresholds as in Methods, arsenic 0.010 mg/L is 10 µg/L; the Kwale exclusions and the thermal spring | R5-M09 |
| S1 Text | that the channel difference was not estimated under station-grouped or spatial-block splitting | R5-M08 |

One relocation had to be rebuilt rather than re-pointed: the S12 sheet takes its notes from Table 4 and dropped any
note containing "S12 Table", so moving the pointer into a note removed that whole note from the sheet. The builder
now drops only the sentence that points at itself (`scripts/m7_build_si.py`), and the S12 workbook carries both
Table 4 notes in full — verified by reading the built file.

## 5. Cross-links

`R1_ARGUMENT_AND_READER_AUDIT.md` · `R3_FIGURE_PLACEMENT_REGISTER.md` · `R5_REVIEW_TRIAGE.md` ·
`CAPTION_AND_NOTE_REVISION_REGISTER.csv` · `manuscript/TABLE_CAPTIONS.md`
