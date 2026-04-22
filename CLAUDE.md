# 2nd Brain - Claude Code System Guide

## Purpose
This is a personal knowledge and tracking system managed via Claude Code in the terminal. All canonical data lives in `.md` and `.csv` files. Claude can generate artifacts (Word docs, Excel sheets, HTML reports) from that data on demand.

## Repository
- Remote: https://github.com/CJROYCE4311/brain.git
- Sync: push after every session or when explicitly requested

## Directory Structure

```
2nd_Brain_Claude/
├── CLAUDE.md               # System instructions (this file)
├── README.md               # Human-readable overview
├── home/                   # Home repair, maintenance, remodel
├── auto/                   # Vehicles, maintenance logs, insurance
├── financial/              # Budget, investments, accounts, expenses
├── health/                 # Medical records, medications, providers, fitness
├── hobbies/                # User-defined hobby tracking
├── templates/              # Reusable file templates
└── exports/                # Generated artifacts (Word, Excel, HTML)
```

## Core File Formats

### Markdown (.md) - Narrative / Reference Data
Use for: notes, procedures, logs with context, reference info, provider contacts.

Standard frontmatter block at the top of every `.md` file:
```
---
category: home
subcategory: repairs
last_updated: YYYY-MM-DD
---
```

### CSV (.csv) - Structured / Tabular Data
Use for: logs with repeated entries, financial transactions, maintenance schedules, medication lists.

Always include a header row. Dates in ISO format: `YYYY-MM-DD`.

## Category Guidelines

### home/
| File | Purpose |
|------|---------|
| `repairs_log.csv` | Date, item, description, cost, contractor, status |
| `maintenance_schedule.md` | Recurring tasks, frequencies, last completed |
| `remodel_projects.md` | Project name, scope, budget, status, notes |
| `appliances.csv` | Item, brand, model, serial, purchase date, warranty expiry |
| `contacts.md` | Contractors, vendors, HOA contacts |

### auto/
| File | Purpose |
|------|---------|
| `vehicles.md` | Each vehicle: year/make/model, VIN, purchase date, insurance info |
| `maintenance_log.csv` | Date, vehicle, service type, mileage, cost, shop |
| `insurance.md` | Policy details, renewal dates, coverage summary |

### financial/
| File | Purpose |
|------|---------|
| `accounts.md` | Account names, institutions, types (checking/savings/brokerage) |
| `budget.md` | Monthly category targets, notes on adjustments |
| `expenses.csv` | Date, category, description, amount, account, notes |
| `investments.md` | Holdings, strategy notes, rebalancing schedule |
| `net_worth.csv` | Date, asset/liability snapshots for tracking over time |

### health/
| File | Purpose |
|------|---------|
| `providers.md` | Doctors, dentists, specialists — name, practice, phone, address |
| `records.md` | Key diagnoses, procedures, hospitalizations (summary only) |
| `medications.csv` | Medication, dose, frequency, prescriber, start date, end date |
| `fitness.md` | Goals, routines, benchmarks |

### hobbies/
One subfolder per hobby (e.g., `hobbies/woodworking/`). No fixed schema — user defines structure as needed.

## Working with Claude Code

### Adding Content
Tell Claude what to add and to which category. Claude will:
1. Identify the correct file (or create it from a template)
2. Append or update the entry
3. Keep formatting consistent with existing content

Example prompts:
- "Add a repair log entry: replaced kitchen faucet on April 20, cost $340, did it myself"
- "Log an oil change for the 2021 Tacoma, today, 45,200 miles, Jiffy Lube, $89"
- "Update my budget — increase groceries target to $800/month"
- "Add Dr. Smith, cardiologist, St. Mary's Hospital, 555-1234"

### Generating Artifacts
Claude can generate exports from the canonical `.md`/`.csv` files.

Example prompts:
- "Generate an HTML report of all home repairs this year"
- "Create an Excel-formatted CSV of my 2025 expenses by category"
- "Make a maintenance schedule summary as a formatted markdown table"

Exports go in `exports/` with a datestamped filename: `exports/home_repairs_2025-04-22.html`

### Querying Data
- "What home repairs have I done in 2025?"
- "Show all maintenance due in the next 30 days"
- "What did I spend on auto expenses last quarter?"
- "List all medications currently active"

### Adding a New Category
Tell Claude: "Add a new category called [name]". Claude will:
1. Create the folder
2. Add a `README.md` inside describing the category
3. Update the directory tree in this file

## Git Sync Procedures

### After each session
```bash
git add -A
git commit -m "YYYY-MM-DD: brief description of changes"
git push origin main
```

Or tell Claude: "sync changes" and Claude will stage, commit with today's date, and push.

### First-time setup (if repo not yet initialized)
```bash
git init
git remote add origin https://github.com/CJROYCE4311/brain.git
git branch -M main
git add -A
git commit -m "Initial 2nd Brain setup"
git push -u origin main
```

## Sensitive Data Policy
- Do NOT store full account numbers, SSNs, passwords, or credentials in any file.
- Insurance/financial files store policy names and institutions only — not full policy numbers unless last 4 digits.
- Health files store summary info — not full medical records or lab results.

## Naming Conventions
- Files: `snake_case.md` or `snake_case.csv`
- Folders: `snake_case/` (lowercase, underscores)
- Dates: always ISO 8601 — `YYYY-MM-DD`
- No spaces in filenames

## Templates
Starter templates live in `templates/`. When creating a new file in a category, copy the relevant template and customize.

## Maintenance of This File
Update CLAUDE.md when:
- A new category is added
- A file naming convention changes
- A new procedure is established
- The remote repo URL changes
