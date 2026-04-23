# 2nd Brain - Codex System Guide

## Purpose
This is a personal knowledge and tracking system managed via the Codex app or Codex CLI. All canonical data lives in `.md` and `.csv` files. Codex can generate artifacts (Word docs, Excel sheets, HTML reports) from that data on demand.

## Repository
- Setup source: https://github.com/CJROYCE4311/codexbrain.git
- End-user GitHub use: clone/pull this starter repository only; no GitHub account is required if the repository is public
- End-user data storage: local files on the user's Mac; do not commit, push, or treat GitHub as the backup destination unless the maintainer explicitly requests it

## Directory Structure

```
2nd_Brain_Codex/
├── AGENTS.md               # System instructions (this file)
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

## Working with Codex

Codex reads `AGENTS.md` files before doing work, so this repository guide is the canonical set of project instructions. Start Codex from the repository root whenever possible so it loads these rules.

### End-User GitHub Model
The end user uses GitHub only to download the starter folder structure and this `AGENTS.md` file. After setup, their 2nd Brain lives locally on their Mac.

- Do not ask the end user to create a GitHub account.
- Do not ask the end user to configure SSH keys.
- Do not push the end user's personal 2nd Brain data to GitHub.
- Use HTTPS clone commands for setup.
- If the starter repository is private, the maintainer should either make it public or provide a ZIP export instead.

### Installing the Codex App
Use the Codex app for the easiest day-to-day experience with this system. Official setup docs live at `https://developers.openai.com/codex/app`.

1. Confirm you have a ChatGPT plan with Codex access and sign in with that same account.
2. Download the Codex app for macOS or Windows. If this is an Intel Mac, choose the Intel macOS build.
3. Open the installer, move Codex into Applications if prompted, then launch Codex.
4. Sign in with your ChatGPT account. If you use an API key instead, some cloud-thread features may not be available.
5. Select this project folder: `/Users/chrisroyce/2nd_Brain_Codex`.
6. Keep `Local` selected when you want Codex to edit the files on this Mac.
7. Send a first prompt such as: "Summarize this 2nd Brain system and list the active instructions."

### Optional Terminal Setup
If you prefer Terminal or need an alternate local interface, install the Codex CLI from the official docs at `https://developers.openai.com/codex/cli`.

```bash
npm i -g @openai/codex
cd /Users/chrisroyce/2nd_Brain_Codex
codex
```

To upgrade the CLI later:

```bash
npm i -g @openai/codex@latest
```

### Adding Content
Tell Codex what to add and to which category. Codex will:
1. Identify the correct file (or create it from a template)
2. Append or update the entry
3. Keep formatting consistent with existing content

Example prompts:
- "Add a repair log entry: replaced kitchen faucet on April 20, cost $340, did it myself"
- "Log an oil change for the 2021 Tacoma, today, 45,200 miles, Jiffy Lube, $89"
- "Update my budget — increase groceries target to $800/month"
- "Add Dr. Smith, cardiologist, St. Mary's Hospital, 555-1234"

### Generating Artifacts
Codex can generate exports from the canonical `.md`/`.csv` files.

Example prompts:
- "Generate an HTML report of all home repairs this year"
- "Create an Excel-formatted CSV of my 2025 expenses by category"
- "Make a maintenance schedule summary as a formatted markdown table"

Exports go in `exports/` with a datestamped filename: `exports/home_repairs_YYYY-MM-DD.html`

### Querying Data
- "What home repairs have I done in 2025?"
- "Show all maintenance due in the next 30 days"
- "What did I spend on auto expenses last quarter?"
- "List all medications currently active"

### Adding a New Category
Tell Codex: "Add a new category called [name]". Codex will:
1. Create the folder
2. Add a `README.md` inside describing the category
3. Update the directory tree in this file

## GitHub Setup Procedures

### End-user first-time setup
```bash
cd ~
git clone https://github.com/CJROYCE4311/codexbrain.git 2nd_Brain_Codex
```

After cloning, the end user works in the local folder. Their personal data stays on their Mac.

### Updating the starter files later
If the maintainer updates only the starter instructions/templates and the end user wants those updates, Codex may pull them down carefully:

```bash
cd ~/2nd_Brain_Codex
git pull
```

Only do this when the user requests it, and check for conflicts before overwriting any local personal data.

### Maintainer publishing
The maintainer may commit and push changes to this starter repository. This is not an end-user backup workflow.

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
Update AGENTS.md when:
- A new category is added
- A file naming convention changes
- A new procedure is established
- The remote repo URL changes
