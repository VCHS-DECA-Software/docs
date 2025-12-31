+++
title = "Roster Registration Checker"
description = "Check who, from the official year DECA roster, registered for a certain conference"
weight = 10
draft = false
toc = true
bref = "Check who, from the official year DECA roster, registered for a certain conference"
+++

### [GitHub Repository](https://github.com/VCHS-DECA-Software/Roster-Registration-Checker)

## Overview

Roster Registration Checker is a **Python** tool that compares the official DECA member roster against conference registration lists. It quickly identifies which members haven't registered for a specific conference, making follow-up outreach easy.

## Tech Stack

- **Language:** Python
- **Environment:** Jupyter Notebook for interactive analysis
- **Libraries:** Pandas, openpyxl (for Excel file handling)
- **Input/Output:** Excel files (.xlsx)

## How It Works

The tool uses a simple but effective comparison process:

### Step 1: Load Data Files
The program reads two Excel files:
1. **Master Roster** - The official DECA membership list (e.g., "2021-22 Final DECA Roster.xlsx")
2. **Registration Responses** - Conference registration form responses (e.g., "2022 SCDC Registration Form responses.xlsx")

### Step 2: Extract Email Addresses
Email addresses are extracted from both files:
- From the roster: Uses the "Email" column
- From registration: Uses the "Email Address" column

### Step 3: Normalize and Compare
1. All email addresses are converted to lowercase (to avoid case-sensitivity issues)
2. Both lists are sorted alphabetically
3. The program checks each roster email against the registration list

### Step 4: Identify Non-Registrants
Any roster member whose email doesn't appear in the registration list is flagged as "not registered."

### Step 5: Generate Output
The program creates:
- **Console output** - Prints the list of unregistered emails and a count
- **Excel file** - `names_not_registered.xlsx` with a formatted list for easy follow-up

## File Structure

```
Roster-Registration-Checker/
├── check_names.ipynb         # Main Jupyter notebook
├── reg_checker_test.py       # Python script version
├── [Data files]              # Excel files with rosters and registrations
└── names_not_registered.xlsx # Output file
```

## Getting Started

### Prerequisites
- Python 3.x
- Jupyter Notebook (or JupyterLab)
- Required libraries: `pandas`, `openpyxl`

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/VCHS-DECA-Software/Roster-Registration-Checker.git
   cd Roster-Registration-Checker
   ```

2. Install dependencies:
   ```bash
   pip install pandas openpyxl jupyter
   ```

### Usage

#### Option 1: Jupyter Notebook (Recommended)
1. Open `check_names.ipynb` in Jupyter:
   ```bash
   jupyter notebook check_names.ipynb
   ```
2. Update the file paths to point to your roster and registration files
3. Run all cells

#### Option 2: Python Script
1. Open `reg_checker_test.py`
2. Update the file paths for your data files
3. Run the script:
   ```bash
   python reg_checker_test.py
   ```

### Customizing for Your Data

In the code, update these file names to match your files:

```python
# Master roster file
roster_file = "2021-22 Final DECA Roster.xlsx"

# Registration responses file
registration_file = "2022 SCDC Registration Form responses.xlsx"
```

Make sure your Excel files have:
- **Roster:** An "Email" column with member emails
- **Registration:** An "Email Address" column with registrant emails

## Output

### names_not_registered.xlsx
A formatted spreadsheet containing:
| # | | Email |
|---|---|-------|
| 1 | | student1@school.edu |
| 2 | | student2@school.edu |
| ... | | ... |

This file provides a simple checklist for tracking which members need registration reminders.

## Use Cases

- Check who hasn't registered for State Career Development Conference (SCDC)
- Verify registration for regional competitions
- Track attendance for chapter meetings or events
- Follow up with members who need to complete forms
