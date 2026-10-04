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
- avoid obvious AI-tailoring phrases such as "strong match with the JD", "aligned with the job description", or "matching keywords"; write as a natural resume, not as commentary about the posting
- don't translate to English if the job posting is in German

## Resume Rules

- never invent metrics
- never invent technologies
- optimize wording for ATS compatibility
- Treat `resumes/master_resume.md` and `resumes/master_resume.tex` as read-only source resumes unless the user explicitly asks to edit the master resume.
- For each tailored application, create new tailored LaTeX and PDF files instead of editing the master resume.
- Use filenames based on the target role and company, for example:
  - `resumes/tailored/<Company> - <Role> - resume.tex`
- Do not create tailored Markdown resume files unless the user explicitly asks for one.
- Tailor only by selecting, reordering, or rephrasing truthful content from the master resume and the user's confirmed project/work history.
- Match the tailored resume language to the job description language: use German for German job descriptions and English for English job descriptions.
- When translating resume content into German, keep technical keywords recognizable and do not exaggerate language fluency or work experience.
- Prioritize the job posting's required skills, ATS keywords, and most relevant experience, but integrate them naturally through role titles, skills lists, project descriptions, and truthful bullet wording.
- Do not write tailored-resume bullets that explicitly say the resume or candidate is a "strong match" for the JD, "aligned with requirements", "matched to keywords", or similar. The tailoring should be visible through relevant evidence and terminology, not through meta-language.
- Keep ATS alignment natural: reuse exact technical terms from the JD when they truthfully apply, place important tools in the skills section, and rewrite bullets around concrete work performed, systems built, tools used, and outcomes supported.
- When appropriate for the timeline, add a concise current-focus entry before professional experience using this wording as the base:
  - `Independent AI Projects, German B2, and AI Agent Coursework | 2025 - Present`
  - `Developing independent AI/software projects focused on backend automation, LLM workflows, and practical AI-assisted applications.`
  - `Reached German B2 level through structured study for German-speaking engineering environments.`
  - `Continuing Coursera coursework in AI agents, RAG, tool use, and LLM application workflows.`
- Tailor the current-focus entry to the JD without changing the master resume:
  - For AI-related roles, emphasize independent AI projects, LLM workflows, RAG, tool use, and AI-assisted applications.
  - For backend roles, emphasize FastAPI, backend automation, APIs, and Python service development.
  - For full-stack roles, emphasize FastAPI plus React frontend work and end-to-end application development.
- Keep tailored resumes concise and targeted; remove less relevant bullets instead of adding unsupported content.
- If a tailored LaTeX resume is created, compile it to PDF with `xelatex` when available.
- If PDF compilation succeeds, update the job note's `Resume::` field with the PDF path and mention the LaTeX source path in the response.
- If PDF compilation fails because the PDF is open or locked, ask the user to close the PDF viewer and rerun compilation.
- If a tailored cover letter is created, update the job note's `CoverLetter::` field with the tailored cover letter path.

## Cover Letter Rules

- Treat `coverletters/master_coverletter.md` and `coverletters/master_coverletter.tex` as read-only source cover letters unless the user explicitly asks to edit the master cover letter.
- When preparing a promising job for application, create both a tailored resume and a tailored cover letter by default. Only skip the cover letter when the user explicitly asks for resume-only, the job application explicitly does not accept a cover letter, or the user asks to postpone cover letters.
- For each tailored application, create new tailored LaTeX and PDF cover letter files instead of editing the master cover letter.
- Use filenames based on the target role and company, for example:
  - `coverletters/tailored/<Company> - <Role> - coverletter.tex`
- Do not create tailored Markdown cover letter files unless the user explicitly asks for one.
- Match the tailored cover letter language to the job description language: use German for German job descriptions and English for English job descriptions.
- Tailor by selecting, reordering, and rephrasing truthful content from the master cover letter, master resume, job description, and user's confirmed project/work history.
- Focus the cover letter on why the user's background fits the specific role; avoid repeating the full resume.
- Do not overemphasize MMRI/manufacturing experience unless the job is research, ML, engineering, or manufacturing related.
- Do not invent metrics, technologies, clients, responsibilities, language fluency, or motivation.
- Keep the tailored cover letter concise, ideally one page.
- If a tailored LaTeX cover letter is created, compile it to PDF with `xelatex` when available.
- If PDF compilation succeeds, update the job note's `CoverLetter::` field with the PDF path and mention the LaTeX source path in the response.
- If PDF compilation fails because the PDF is open or locked, ask the user to close the PDF viewer and rerun compilation.

## File Management rules

Always do a file-management sweep after processing jobs, including existing files already in `jobs/`:
- Check every job note you touched.
- Check all files currently in `jobs/` for `Applied: Yes`.
- A job with `Applied: Yes` must not remain in `jobs/`; move it to `applied/`.

## Application Export Rules

After creating and compiling both a tailored resume PDF and tailored cover letter PDF for an application, also export copies to:

```text
D:\Job seeking and offers\2026\<Company>\
```

Use one folder per company. Create the company folder if it does not exist.

Export filenames must depend on the job description language:
- English applications:
  - `Sophia_Deng_{role}.pdf`
  - `Sophia-Deng-Cover-Letter.pdf`
- German applications:
  - `Sophia_Deng_{role}.pdf`
  - `Sophia-Deng-Motivationsschreiben.pdf`

For resume export filenames, make `{role}` the most concise JD-matched role title in PascalCase, with no spaces, brackets, separators, company names, seniority unless essential, or other extra information. Example: `Sophia_Deng_PythonBackendEngineer.pdf`.

Keep the canonical tailored source files under `resumes/tailored/` and `coverletters/tailored/`; the external folder is only an application-ready copy location.
If writing to `D:\Job seeking and offers\2026` requires permission, ask for approval before exporting.
Do not retroactively move or rename existing tailored files unless the user explicitly asks.

Routing rules:
- If `Applied` is `Yes`, move the file to `applied/`.
- Otherwise, if the chance is higher than 70%, move the file to `jobs/`.
- Otherwise, move the file to `trash/`.

Folder meanings:
- inbox/   = raw clipped jobs
- jobs/    = promising jobs that have not been applied to yet
- applied/ = jobs already applied to
- trash/   = rejected jobs, safer than delete
