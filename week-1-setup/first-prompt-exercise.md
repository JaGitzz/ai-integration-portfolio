# Week 1 — First Prompt Exercise

**Date:** 6 June 2026
**AI Tool:** Claude (free)
**Opportunity Log Reference:** Row #2 — Define field order rules for merged tables

## Prompt Used

I am merging two source tables into one target table for a data migration project.
I need to document the correct field ordering rules so the target table preserves
the original sequence.

Here are the two source tables:

Table A: Policy_Details
Fields (in order):
1. policy_number
2. insured_name
3. coverage_type
4. start_date
5. end_date
6. premium_amount

Table B: Claims_History
Fields (in order):
1. claim_id
2. policy_number
3. claim_date
4. claim_amount
5. claim_status
6. adjuster_name

Please:
1. Generate the complete ordered field list for the merged target table
2. Flag any field names that appear in both tables (potential duplicates)
3. Explain the merging rule you applied so someone else could repeat this

Output the result as a markdown table with columns: Position, Field Name,
Source Table, Notes.

## Claude's Response

Here is the complete merged field list with all rules documented:

---

**Merging Rule Applied — "Table A First, Then Table B (Deduplication on Overlap)":**
All fields from Table A are listed in their original order first. Fields from
Table B are then appended in their original order, **skipping any field that
already exists in Table A** (case-insensitive exact match). Shared fields are
sourced from Table A and flagged in the Notes column.

---

| Position | Field Name | Source Table | Notes |
|----------|--------------|--------------|-------|
| 1 | policy_number | Table A (Policy_Details) | ⚠️ **Duplicate** — also exists in Table B. Retained from Table A; Table B's copy omitted. |
| 2 | insured_name | Table A (Policy_Details) | |
| 3 | coverage_type | Table A (Policy_Details) | |
| 4 | start_date | Table A (Policy_Details) | |
| 5 | end_date | Table A (Policy_Details) | |
| 6 | premium_amount | Table A (Policy_Details) | |
| 7 | claim_id | Table B (Claims_History) | |
| 8 | claim_date | Table B (Claims_History) | |
| 9 | claim_amount | Table B (Claims_History) | |
| 10 | claim_status | Table B (Claims_History) | |
| 11 | adjuster_name | Table B (Claims_History) | |

---

**Summary**

- **Total fields in target table:** 11
- **Duplicate fields detected:** 1 — `policy_number` (present in both tables;
  retained from Table A at position 1, omitted from Table B's sequence)
- **Fields from Table A:** 6 (positions 1–6, original order preserved)
- **Fields from Table B:** 5 of 6 (positions 7–11, original order preserved
  minus the duplicate)

**Repeatability note:** To apply this same rule to any future merge, follow
these steps: (1) write out all fields from the primary table in order,
(2) iterate through the secondary table's fields in order, and (3) append each
field only if its name has not already appeared in the list. The primary table
always "wins" ownership of any shared field name.

## My Observations

### What worked well
- Claude correctly identified `policy_number` as a field appearing in both
  tables.
- The merge order was preserved correctly: Table A fields first, then Table B.
- The merging rule was stated clearly at the top under the heading "Merging Rule
  Applied," directly answering my third request.

### What surprised me
- The table was output in plain text (spaced columns), not standard markdown
  format as I requested. This would require manual reformatting before copying
  into GitHub. (Note: I have since reformatted it to markdown above for this
  file.)
- Claude stated the merging rule twice — once at the top as "Merging Rule
  Applied" and again at the bottom as "Repeatability note." The top heading
  clearly answers my third request. The bottom version is a practical how-to
  guide. Having both is useful, but the different labelling could confuse a
  reader looking for a single clearly named section.
- The Notes column only contained content for the duplicate field
  (`policy_number`). All other rows were left blank. I would have preferred
  consistent entries for every row.

### What I'd change next time
1. Add explicit instructions for how to handle duplicate columns (e.g., "keep
   the first occurrence and note duplicates in the Notes column").
2. Specify what content I expect in each column — particularly the Notes column,
   to prevent Claude from leaving cells empty for non-duplicate fields.
3. Ask Claude to review the column order and suggest alternatives to my column
   headers, turning a generation task into a validation task.
4. Add: "Output the table in standard markdown format so I can copy it directly
   into GitHub."
5. Add: "Present the merging rule once under a single heading called 'Merging
   Rule.' Do not repeat it elsewhere."

## Status
✅ Complete
