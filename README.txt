================================================================================
CONFERENCE PAPER MANAGEMENT SYSTEM - README

This archive contains the following files:

1. ER_Diagram.pdf
2. part_2.txt
3. project_1.db
4. part_3_1.txt
5. part_3_2.txt
6. part_3_3.txt
7. part_3_4.txt
8. project_1.db
9. README.txt


================================================================================
FILE DESCRIPTIONS
================================================================================

---

1. ER_Diagram.pdf

---

Peter Chen Entity-Relationship diagram for the conference paper management system.

Contents:

- Entities: PAPER, AUTHOR, RESEARCH_AREA
- Relationships: WRITES, REVIEWS, EXPERT_IN, ASSIGNED_TO
- Attributes: All entity and relationship attributes
- Primary keys: Underlined attributes (paper_id/pid, email, area_name)
- Derived attributes: Shown with dashed ellipses (acceptance status, avg_score)
- Cardinality constraints: Marked on all relationships
  - WRITES: many-to-many
  - REVIEWS: many-to-many
  - EXPERT_IN: many-to-many
  - ASSIGNED_TO: many-to-one

---

2. part_2.txt

---

Complete SQL script to create and populate the database.

Contents (in order):
a) DROP TABLE statements for clean database creation
b) CREATE TABLE statements for all 6 tables:

- Author (email as PK, name)
- Research_Area (area_name as PK)
- Paper (pid as PK, title, area_name as FK, status, avg_score)
- Writes (composite PK: email + pid, junction table for authorship)
- Expert_In (composite PK: email + area_name, junction table for Research_Area)
- Reviews (composite PK: email + pid, with originality, correctness, fitness scores)

c) Constraints included:

- PRIMARY KEY constraints on all tables
- FOREIGN KEY constraints with ON DELETE CASCADE
- CHECK constraints for status ('accepted', 'rejected', 'undecided')
- CHECK constraints for review scores (0-5 range)

d) Triggers

- prevent_self_review: Prevents an author from reviewing their own paper.
- update_avg_on_review_insert: Updates Paper.avg_score when review inserted
- update_avg_on_review_update: Updates Paper.avg_score when review modified
- update_avg_on_review_delete: Updates Paper.avg_score when review deleted
- update_acceptance_on_review_insert: Updates Paper.acceptance when review inserted
- update_acceptance_on_review_update: Updates Paper.acceptance when review modified
- update_acceptance_on_review_delete: Updates Paper.acceptance when review deleted

e) INSERT statements to populate all tables with test data:

- 6 Research Areas
- 5 Authors with varying expertise
- 7 Papers across different research areas
- 7 authorship relationships (1-3 authors per paper)
- 6 Expert_In relationships (authors with 1-2 expertise areas)
- Review data with varied scores to test all query scenarios



3. part_3

---

SQL queries for the four required tasks in Part 3.

part_3_1: Update Paper Status Based on Review Scores

- Updates avg_score for all papers with reviews
- Updates status to 'accepted' if avg_score >= 3.5
- Updates status to 'rejected' if avg_score < 3.5
- Only processes papers with at least 2 reviews
- Papers with < 2 reviews remain 'undecided'

part_3_2: List Accepted Papers by Research Area

- Displays: area_name, title, avg_score
- Filters: Only papers with status = 'accepted'
- Ordering: By avg_score descending

part_3_3: Count Papers by Status per Research Area

- Displays: area_name, accepted_papers, rejected_papers, undecided_papers
- Uses conditional aggregation (COUNT with CASE)
- Includes all research areas (even those with 0 papers)
- Groups by research area

part_3_4: Identify Reviewers with Inconsistent Reviews

- Calculates each reviewer's average score per paper
- Calculates overall paper average (average of all reviewers' averages)
- Identifies reviews where |reviewer_avg - paper_avg| / paper_avg > 0.33
- Displays: author_email, pid, reviewer_avg_score, paper_avg_score

---

4. project_1.db

---

SQLite database file with all tables created and populated with test data.

This is the actual working database used for testing all queries.
Can be opened with:

- SQLite command line: sqlite3 project_1.db
- DB Browser for SQLite (GUI tool)
- Any SQLite-compatible database management tool

Database includes:

- 6 tables (Research_Area, Author, Paper, Writes, Expert_In, Reviews)
- 7 active triggers

---

Authors:
Bishwajit Karki, Yi Xu, Linghe Zhou
