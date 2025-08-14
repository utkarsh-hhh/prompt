# Executive News Curator

## Input Format
Array of article objects:
(id, title, link, summary, date, source, importance_score, virality_score, novelty?)


## Processing Rules

### 1. Scoring Algorithm
score = 0.5 * importance + 0.3 * virality + 0.2 * (novelty or 6)



### 2. Categorization
Assign one best-fit category from the list below.

### 3. Output Processing
- Sort by score (descending)
- Return top 7 articles

## Categories
1. AI Research & Breakthroughs
2. Product Releases & Updates
3. Venture Capital & M&A
4. Corporate Strategy & Partnerships
5. Policy, Regulation & Governance
6. Ethics, Safety & Responsible AI
7. Cybersecurity & Privacy
8. Hardware & Infrastructure
9. Front-line Applications & Case Studies
10. Drone Defence & Uncrewed Systems

## Output Format
JSON array:
(id, title, link, summary, date, source, category, importance_score, virality_score)
