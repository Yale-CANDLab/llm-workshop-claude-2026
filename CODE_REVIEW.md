## Review Scope

- **What to review**: All `.R` scripts in `scripts/`
- **Focus areas**: Scoring algorithm correctness, data cleaning logic, missing data handling, statistical model specification
- **Out of scope**: Code style (covered by the Coding Standards section of `CLAUDE.md`), visualization aesthetics, documentation completeness

## Review Priorities

Review in this order; earlier items are more consequential than later ones:

1. **Scoring correctness** — reverse-coding, subscale composition, clinical cutoff application
2. **Data integrity** — missing data handling, subject ID matching across time points, duplicate detection
3. **Statistical assumptions** — normality checks, model specification, multiple comparison handling
4. **Reproducibility** — random seeds, hardcoded values, environment dependencies

## Domain-Specific Checks

- **CBCL**: Verify reverse-coded items match the published Achenbach manual (items 2, 4, and 7 are commonly miscoded as reverse-scored despite their wording — confirm against the manual, not intuition). Verify subscale item groupings against the manual. Verify T-score norming uses age- and gender-appropriate norm tables.
- **SDQ**: Verify the 5-subscale structure (Emotional, Conduct, Hyperactivity, Peer, Prosocial). Verify that Total Difficulties excludes the Prosocial subscale. Verify reverse-coded items (items 7, 11, 14, 21, 25).
- **Longitudinal alignment**: Verify the same scoring algorithm is applied identically across all three time points. Flag any time-point-specific exclusion criteria that differ without documented justification.
- **Score range validation**: CBCL raw subscale scores and SDQ subscale scores (each 0-10) and SDQ Total Difficulties (0-40) should fall within their valid ranges; flag any out-of-range computed value.

## Statistical Standards

- **Growth-curve models**: Verify the random-effects structure is justified by the design (not simply maximal by default); check for convergence warnings; verify the time variable is coded correctly (e.g., 0, 0.5, 1.0 for baseline, 6-month, 12-month).
- **Descriptive statistics**: Verify N is reported at each level of analysis; verify missingness rates are reported alongside descriptives.
- **Group comparisons** (if present): Verify assumption checks precede each test; verify effect sizes accompany test statistics.
- **Power**: Flag any analysis where N per cell or group falls below 20 for the planned statistical test.

## Common Pitfalls

- Silently dropped NA rows during scoring that inflate effect sizes or reduce N without documentation
- Subscale scores computed on incomplete item sets without prorating or an explicit missingness policy
- Off-by-one errors in reverse coding (e.g., `max_value - response` instead of `max_value - response + min_value`)
- Joining data frames across time points with `left_join()` without checking for unexpected duplicates or mismatches
- Hardcoded age or gender norm lookups that silently fail or return NA when a participant falls outside the expected range
- Applying significance testing to descriptive or demographic tables (a common methodological objection in developmental journals)

## Output Format

- Organize findings by severity: **Critical** (scoring errors, data integrity issues), **Warning** (statistical assumption violations, reproducibility gaps), **Note** (suggestions for improvement)
- For each finding: state the file and line number, describe the issue, explain the consequence if left unfixed, and provide a concrete fix
- Group findings by script, not by severity, so each script's issues are read together

## Report Generation

After completing the review, compile all findings into a single structured `.docx` report, written to `output/code_review_report.docx`.

Report structure:

1. **Executive Summary** — a 2-3 sentence overview of the review's scope and overall assessment
2. **Critical Findings** — if any
3. **Warnings**
4. **Notes**
5. **Summary Table** — columns: File, Line, Severity, Issue, Fix

The report should be human-interpretable without requiring reading the underlying code. Use clear section headers and consistent formatting throughout.
