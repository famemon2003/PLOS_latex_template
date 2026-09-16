# Quality checks on this LaTeX manuscript

**Status:** technically built and PLOS-template compliant, pending the author decisions listed with the manuscript.
It is not ready to submit until those are settled.

## Automated checks (at the build recorded in COMPILE.md)

| Check | Result |
|---|---|
| Template compliance, compile log, float and citation order, reference order, SI labels, number-by-number comparison with the source text, upload figures (`m11_verify_latex.py`) | 97 of 97 pass |
| Claim ledger (`m4_verify_claims.py`) | 13 verified, 3 partial, 1 refuted; each worded to its status in the text |
| Tables against their source data (`m6_verify_tables.py`) | 76 of 76 pass |
| Figures against their source data (`m7_verify_figures.py`) | 151 of 151 pass; PLOS technical checks pass for all six figures |
| Drafting and coherence rules | 0 failures |
| Bibliography rendered by `plos2025.bst` against the verified reference list | 52 references: 12 identical, 40 with the same content in the style's punctuation or order, 0 different |
| Retraction and correction notices (Crossref) | 36 DOIs checked, 0 notices |

## Reviews

Nine report-only reviews were run by AI agents and triaged one finding at a time: the abstract (scientific accuracy,
handling editor and plain-language reading, journal conventions), template compliance, tables, citations and
bibliography, figures, Supporting Information, and a claim-and-number regression against the pre-conversion text.
Accepted findings were applied and every check above was re-run afterwards.

## Not done by these checks

- No citation has yet been confirmed by the author against its source.
- The title, author list, affiliations, corresponding email and acknowledgments are placeholders.
- The model runs behind the validation and transfer results were not re-run; their result tables were verified
  against retained exports.
- PLOS's own conversion of the two page-spanning tables (Tables 1 and 4, set with `longtable`) is untested.
