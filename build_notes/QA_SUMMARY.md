# QA summary (M12 presentation revision, 2026-09-17)

**Status:** built; not cleared for submission; placeholders and author items remain.

## What changed from the previous build

- A clean reading copy (`main.tex`) with the 17 figures embedded after the paragraphs that cite them, no line
  numbers, a justified abstract and the footer fixed at its cause (the template's left footer offset is reset after
  the body page geometry changes).
- A separate PLOS submission copy (`PLOS_Water_manuscript_submission.tex`): captions only, continuous line numbers,
  double spacing, Acknowledgments, References and then Supporting information captions.
- The six composite figures split into 17 standalone figures, numbered by first citation; captions shortened (figure
  titles at most 15 words; mean caption length per figure 213 → 73 words); table captions 341 → 180 words and table
  notes 1,833 → 1,010 words, with every removed definition traced to its new place.
- The abstract and all sections rewritten as an application-led article; the standalone Limitations subsection
  removed, with each of its 30 points relocated beside the result or method it qualifies.
- Neutral placeholders: Title, Authors, Affiliations, Corresponding author email, Further acknowledgments — all
  "TO BE FILLED LATER".
- Reference list audited entry by entry; three undated government data documents now carry "[date unknown]".

## Checks

| Check | Result |
|---|---|
| LaTeX verifier, both copies (structure, compile log, display placement, references, SI, content, PDF) | 269/269 |
| Figures (values, PLOS image limits, embedded fonts) | 366/366 |
| Tables | 76/76 |
| Clean compile of each entry point (pdfLaTeX, three runs) | 0 errors, 0 undefined references, 0 overfull boxes of 2 pt or more |
| Footer rule inside the page margins, page n/N | every page of both PDFs |
| Line numbers | none in the reading copy; continuous and strictly increasing in the submission copy |
| Display placement | never before the citing paragraph; at most 4 pages after in the reading copy, 1 in the submission copy |
| Reference rendering against the verified reference list | 0 content differences |
| Independent reviews (scientific claims, editorial and layout, references) | 0 critical; all major findings fixed or recorded with a reason |

## Known limits

- In the reading copy, the Indian results subsection cites four large displays within about one page of text, so
  those figures stand on their own pages with white space below.
- Minor reference-style points that depend on the official style file or on source checks remain listed in
  `REFERENCE_STYLE_QA.md`.
- No citation has yet been confirmed by the author.
