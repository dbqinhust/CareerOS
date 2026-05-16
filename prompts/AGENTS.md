# CareerOS Agent Instructions

## Purpose

This repository is an AI-assisted job application management system.

## First thing
Clean this job note.

Tasks:
- remove unrelated sections
- remove "More jobs"
- remove navigation/footer/ads
- preserve only the actual job posting

## Markdown Rules

- All job notes use YAML frontmatter
- Preserve existing markdown structure
- Never remove Dataview fields
- Never rewrite the original job description
- Append analysis under "# AI Analysis"

## YAML Schema

Every job note should contain:

```yaml
---
Company:
Role:
Location:
TechStack: []
Status:
Chance:
Priority:
Applied:
InterviewStage:
URL:
Captured:
---
```

## Analysis Rules

When analyzing job postings:
- estimate fit probability
- identify missing skills
- suggest resume modifications
- identify ATS keywords
- never hallucinate experience
- prefer concise professional wording

## Resume Rules

- never invent metrics
- never invent technologies
- optimize wording for ATS compatibility

## File Management rules

After finishing all above work:
- If `Applied` is `Yes`, move the file to `applied/`.
- Otherwise, if the chance is higher than 70%, move the file to `jobs/`.
- Otherwise, move the file to `trash/`.

Folder meanings:
- inbox/   = raw clipped jobs
- jobs/    = promising jobs that have not been applied to yet
- applied/ = jobs already applied to
- trash/   = rejected jobs, safer than delete
