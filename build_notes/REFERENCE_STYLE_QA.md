# Reference style QA (M12, D-0078)

**Scope.** All 52 references in both LaTeX files, rendered by the official `plos2025.bst` from
`submission/latex/references.bib`, which `scripts/m11_build_bib.py` generates from `references/REFERENCE_LIST.csv`.
**Method.** An independent audit of every entry against PLOS/NLM (Vancouver) style and the saved source files
(`reviews/M12_REVIEW_REFERENCES.md`); fixes applied only where the correct value is in a saved source; no metadata
invented. **Status:** 0 MAJOR open; 14 MINOR open (style-file behaviour, author decisions or needing a source check).

## Checks that pass

| Check | Result | Evidence |
|---|---|---|
| Numbering follows first citation | 52 of 52 | audit; `m11_verify_latex.py` (order equals the Markdown build) |
| Every cited key has an entry and every entry is cited | yes | `m11_verify_latex.py` |
| Embedded bibliography equals a fresh BibTeX run | yes, identical in both files | audit; `m11_verify_latex.py` "embedded bibliographies identical" |
| Reference render check (bbl against the reference list) | 13 identical, 39 same content, **0 differ** | `build_notes/REFERENCE_RENDER_CHECK.md` |
| "et al." after six authors | correct in all long lists | audit |
| Corporate authors not split into initials | yes | audit |
| Accents and proper nouns | display correctly; copy correctly since T1 encoding was added | audit; PDF text extraction ("Wöllauer", "Ó Dochartaigh", URL underscores) |
| Duplicate works or DOIs | none | audit |
| URL typography | text font (`\urlstyle{same}`) | `FORMAT_SPEC.md` |
| Retraction or correction notices | none found at M11 | `references/RETRACTED_OR_CORRECTED_CHECK.md` |

## Findings and dispositions

| ID | Refs | Finding | Disposition |
|---|---|---|---|
| R-01 (MAJOR) | 22–24 | Year Book documents dated by data year; no printed date | **FIXED**: "[date unknown]" in the bib and the reference list; data year stays in the title |
| R-02 | 2 | GLAAS 2025 publisher omits UNICEF | **FIXED** from the report's copyright page (saved PDF p. 4) |
| R-03 | 2, 13 | Organisational authors separated by comma or semicolon | Open (style consistency); no data error |
| R-04 | 4, 13, 19, 25, 35 | "[cited]" prints after the URL for report and proceedings types | Open: `plos2025.bst` behaviour; changing entry types is possible for 4, 13, 25, 35 but not for 19 |
| R-05 | 19, 31 | URL breaks after "https:" | Open: typographic; PLOS re-typesets references |
| R-06 | 8, 13, 19, 24, 41, 45, 48 | Accents and URL underscores lost when copying from the PDF | **FIXED**: `\usepackage[T1]{fontenc}` (fonts remain embedded Type 1) |
| R-07 | 20, 21, 31 | No date element | **FIXED**: "[date unknown]"; ref 31 also "[updated 2026 Aug 31]" from the saved EPA page |
| R-08 | 20 | GEMStat has no publisher or place | Open: needs a source check against GEMStat's terms |
| R-09 | 26 | Water Quality Portal citation cannot identify the extract | Open: the query URLs are held by the author (M10 A19) |
| R-10 | 13, 26, 31 | EPA named in several forms | Open (style consistency); ref 26 follows the provider's wording |
| R-11 | 4, 21–25, 35 | CGWB publisher and place vary; ref 4 place not printed | Open: needs a source check |
| R-12 | 4, 35 | "[date unknown]" could become a probable date | Open: needs a source check |
| R-13 | 8 | Preprint DOI and version; a published version exists | Open: author decision already logged in the reference list |
| R-14 | 10, 19, 41 | No place of publication | Open: needs a source check |
| R-15 | 27 | Version position; possible missing initial | Open: needs a source check against the Zenodo record |
| R-16 | 28, 29 | Concept DOIs do not identify the version used | Open: needs a source check |
| R-17 | 21–25, 27–29, 38 | Title case mixed across dataset titles | Open (style consistency) |
| R-18 | 38 | Hyphen in a year range | **FIXED** (en dash) |
| R-19 | 33 | No access date for the JMLR landing page | Open: author decision (the recorded retrieval was of the PDF) |
| R-20 | all DOIs | DOI links use the legacy dx.doi.org resolver | Open: `plos2025.bst` constant; PLOS re-links DOIs |

No author has yet verified any citation (0 of 53 citation debts `support_verified=YES`); that confirmation remains an
author item and is independent of this style audit.
