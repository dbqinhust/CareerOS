# CareerOS

CareerOS is a local-first job application workflow built around Markdown, Obsidian, and AI-assisted review. It helps you capture job postings, clean them up, evaluate fit, track active applications, and keep tailored resumes and cover letters organized without pushing private application files to GitHub.

## What This Vault Does

This vault is organized as a simple pipeline:

1. Capture a job posting into `inbox/`.
2. Clean the note so it contains only the real job description.
3. Analyze the role for fit, missing skills, ATS keywords, and interview focus.
4. Move promising jobs into `jobs/`.
5. Move rejected jobs into `trash/` instead of deleting them.
6. Create tailored resumes in `resumes/` and cover letters in `coverletters/`.
7. Track active applications from `Jobs Dashboard.md`.

The private working folders are intentionally ignored by Git. GitHub keeps the folder structure through `.gitkeep` files, but your actual job notes, resumes, and cover letters stay local.

## Folder Structure

```text
CareerOS/
+-- Jobs Dashboard.md
+-- inbox/           # Raw clipped job postings
+-- jobs/            # Promising applications
+-- trash/           # Rejected jobs kept for reference
+-- resumes/         # Master and tailored resumes
+-- coverletters/    # Tailored cover letters
+-- templates/       # Obsidian templates
+-- prompts/         # AI workflow instructions
+-- analysis/        # Extra research or notes
```

## Setup

Download Obsidian from the official site:

https://obsidian.md/download

Then open this repository as an Obsidian vault:

1. Open Obsidian.
2. Choose **Open folder as vault**.
3. Select the `CareerOS` folder.
4. Enable community plugins if Obsidian asks.

This vault expects these Obsidian plugins:

- **Dataview**: powers the active applications dashboard.
- **Templater**: fills dynamic fields in job templates.
- **Obsidian Web Clipper**: saves job postings from the browser into the vault.

## Web Clipper

Install Obsidian Web Clipper from Obsidian's official page:

https://obsidian.md/clipper


Recommended Web Clipper setup for this vault:

- Set the target vault to `CareerOS`.
![alt text](image.png)
- Create a new template note name something like: Job Application, then add Note Location and Vault, Content properties
	![[Pasted image 20260513165917.png]]
	
- In the Note content, paste below
	
		# {{title}}

        ## Job Description

        {{content}}

        ---

        # AI Analysis
        Company:
        Role:
        Location:
        WorkMode:
        TechStack:
        Salary:
        VisaSponsorship:

        ## Match Strengths

        ## Weaknesses

        ## Resume Improvements

        ## ATS Keywords

        ## Interview Focus

        ---

        # Tailored Documents

        Resume::
        CoverLetter::

        ---

        # Notes

Those settings can be modified based on use cases.

## Job Note Workflow

Create or clean each job note using `templates/job_template.md`.

Each job note should contain fields like:

```markdown
Company::
Role::
Location::
Salary::
URL::
Captured::
Status::
Priority::
Applied::
InterviewStage::
Chance::
```

Then keep the job description under `# Job Description` and add AI review under `# AI Analysis`.



## Dashboard

`Jobs Dashboard.md` uses Dataview to show active applications from the `jobs/` folder:

```dataview
table Status, Chance, Priority, Applied
from "jobs"
sort file.name asc
```

Update the fields inside each job note and the dashboard updates automatically.

Useful status values:

- `Wishlist`
- `Ready to Apply`
- `Applied`
- `Interview`
- `Rejected`
- `Offer`

## Resume And Cover Letter Workflow

Keep one source resume in `resumes/master_resume.md`.

if a tailored resume or cover letter needs to be created, update [[AGENTS]]

## Git Privacy

The repository tracks structure and workflow files, but ignores private application content in:

- `inbox/`
- `jobs/`
- `trash/`
- `resumes/`
- `coverletters/`

Only the `.gitkeep` placeholders are committed inside those folders. This keeps the workflow portable while protecting job postings, resumes, and cover letters.
