# Workflow 2 - n8n Automation Documentation

## Overview
This n8n workflow is an automated news curation and digest system that processes news articles from a database, uses AI to curate content, and sends formatted email digests.

## Workflow Structure

### Trigger Node
- **Type**: Schedule Trigger
- **Schedule**: Daily at 5:00 AM
- **Purpose**: Initiates the workflow automatically

### Conditional Logic
- **Node**: If
- **Condition**: Current day equals 5 (Friday)
- **Logic**: Routes to weekly or daily processing based on the day

### Database Operations

#### Daily Query
``` SELECT * FROM news WHERE keep = true AND date = CURRENT_DATE;```


#### Weekly Query  
```SELECT * FROM news WHERE keep = true AND date >= CURRENT_DATE - INTERVAL '7 days';```


### AI Processing Pipeline

#### Executive News Curator
- **System Message**: Processes article arrays with scoring algorithm
- **Scoring Formula**: `0.5 * importance + 0.3 * virality + 0.2 * (novelty or 6)`
- **Output**: Top 7 articles sorted by score

#### Tech Journalist
- **Prompt**: Creates structured JSON output
- **Fields**: headline (≤90 chars), digest (≤280 chars), source_line, insights
- **Format**: 3 insights starting with 💡 in italic

#### AI Components
- **LLM**: Groq Chat Model
- **Parser**: Structured Output Parser with JSON schema
- **Agent**: Langchain AI Agent for content processing

### Content Enhancement
- **HTTP Request**: Fetches source URLs for metadata
- **Code Node**: Extracts og:image URLs using regex
- **Pattern**: `/<meta content="([^"]+)" property="og:image"/`

### Email Generation
- **Processing**: JavaScript code node that compiles HTML email
- **Features**: 
  - Responsive email template
  - Article cards with images
  - Key insights formatting
  - Dynamic subject lines
- **Delivery**: Gmail integration for email sending

## Node Configuration

| Node Name | Type | Purpose |
|-----------|------|---------|
| workflow 2 | Schedule Trigger | Daily automation trigger |
| If | If Node | Day-based routing logic |
| Execute a SQL query | Postgres | Daily news retrieval |
| Execute a SQL query | Postgres | Weekly news retrieval |
| daily/weekly | Set Node | Data assignment |
| AI Agent | Langchain Agent | News curation |
| Groq Chat Model | LLM | AI processing |
| Structured Output Parser | Parser | JSON formatting |
| HTTP Request | HTTP | Source URL fetching |
| Code | JavaScript | Image URL extraction |
| Code | JavaScript | Email HTML generation |
| Send a message | Gmail | Email delivery |

## Data Flow
1. **Trigger**: Daily at 5 AM
2. **Condition**: Check if Friday (day 5)
3. **Query**: Fetch daily or weekly news articles
4. **AI Curation**: Score and categorize articles
5. **Enhancement**: Extract source images
6. **Compilation**: Generate HTML email template
7. **Delivery**: Send digest via Gmail

## Categories Supported
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

## Email Configuration
- **Recipient**: email for the recipient
- **Subject**: Dynamic based on article count

