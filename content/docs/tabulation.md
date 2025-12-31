+++
title = "Tabulation"
description = "Algorithm to tabulate student scores and create a leaderboard"
weight = 10
draft = false
toc = true
bref = "Algorithm to tabulate student scores and create a leaderboard"
+++

### [GitHub Repository](https://github.com/VCHS-DECA-Software/Tabulation)

## Overview

Tabulation is a **Python** tool that calculates final scores for DECA competition events and generates ranked leaderboards. It handles the complex scoring formulas for different event types (role-plays, written events, exams) and outputs results to Excel for easy distribution.

## Tech Stack

- **Language:** Python
- **Libraries:** Pandas (data manipulation), openpyxl (Excel export)
- **Data Source:** Google Sheets
- **Output:** Excel file (.xlsx) and console output

## How It Works

### Data Flow Overview

```
Google Sheets → Python Processing → Weighted Calculations → Ranked Results → Excel Export
```

### Step 1: Load Data from Google Sheets

The program reads from three Google Sheets:

1. **Main Scoring Sheet** - Contains team numbers, student IDs, and individual event scores
2. **Group Information Sheet** - Team rosters with captain and partner names
3. **Exam Scores Sheet** - Student exam results by ID

### Step 2: Build Team Rosters

The `creategroupdictionary()` function builds a dictionary of teams, linking:
- Team numbers
- Captain names
- Partner names
- Member IDs

### Step 3: Calculate Event Scores

Different DECA events use different scoring formulas:

| Event Type | Formula |
|------------|---------|
| **Role-Play Events** | 67% Role-Play + 33% Exam |
| **Professional Selling & Consulting** | 30% Exam + 70% Presentation |
| **Individual Series** | Average of Two Role-Plays + Exam |
| **Business Operations Research (BORE)** | 60% Written + 40% Presentation |
| **Entrepreneurship Events (EE)** | Weighted Written + Presentation scores |
| **Integrated Marketing Campaign** | Custom marketing scoring |

### Step 4: Rank Participants

The `rankevent()` function sorts all groups by their final calculated score in descending order (highest score = 1st place).

### Step 5: Export Results

Results are formatted and exported to:
- **Console** - Plaintext rankings with scores
- **Excel file** - `foo.xlsx` with columns for rank, event, names, and scores

## File Structure

```
Tabulation/
├── tabulateit.py        # Main script - orchestrates all processing
├── BOREandEE.py         # Business Operations Research & Entrepreneurship scoring
├── IMC.py               # Integrated Marketing Campaign scoring
├── ISR.py               # Individual Series Role-play scoring
├── exam.py              # Exam score processing
├── dupeeventchecker.py  # Validates for duplicate entries
├── extradata.py         # Supplementary data handling
├── pandastesting.py     # Testing utilities
└── README.md            # Project documentation
```

## Key Functions

| Function | Purpose |
|----------|---------|
| `creategroupdictionary()` | Builds team roster from group sheet |
| `getAllEvents()` | Retrieves events and scores for each team member |
| `examAndRolePlayEvents()` | Calculates exam-weighted role-play scores |
| `professionalSellingAndConsulting()` | Applies 30/70 exam/presentation weighting |
| `IndividualSeriesRoleplay()` | Processes dual role-play format |
| `calcBOREfinal()` | Business operations weighted calculation |
| `calcEEfinal()` | Entrepreneurship event-specific formulas |
| `Integratedmarketing()` | Marketing campaign scoring |
| `rankevent()` | Sorts groups by final score |
| `processallevents()` | Orchestrates all event processing |
| `writeToExcel()` | Exports results to spreadsheet |

## Getting Started

### Prerequisites
- Python 3.x
- Required libraries: `pandas`, `openpyxl`
- Access to competition scoring Google Sheets

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/VCHS-DECA-Software/Tabulation.git
   cd Tabulation
   ```

2. Install dependencies:
   ```bash
   pip install pandas openpyxl
   ```

### Configuration

Before running, update the Google Sheets URLs in the code to point to your competition data:

```python
# Main scoring data
scoring_sheet_url = "YOUR_SCORING_SHEET_URL"

# Group information
groups_sheet_url = "YOUR_GROUPS_SHEET_URL"

# Exam scores
exam_sheet_url = "YOUR_EXAM_SHEET_URL"
```

### Usage

Run the main tabulation script:
```bash
python tabulateit.py
```

The program will:
1. Fetch data from Google Sheets
2. Process all event types
3. Calculate final scores
4. Print rankings to console
5. Export results to `foo.xlsx`

## Output

### Console Output
```
Event: Principles of Marketing
1. Team 42 - John Smith, Jane Doe - Score: 94.5
2. Team 17 - Alex Johnson, Sam Brown - Score: 91.2
3. Team 8 - Chris Lee, Pat Wilson - Score: 88.7
...
```

### Excel Output (foo.xlsx)
| Rank | Event | Captain | Partner(s) | Final Score |
|------|-------|---------|------------|-------------|
| 1 | Principles of Marketing | John Smith | Jane Doe | 94.5 |
| 2 | Principles of Marketing | Alex Johnson | Sam Brown | 91.2 |

## Supported DECA Events

The system handles scoring for major DECA event categories:

- **Role-Play Events** - Principles events, individual decision-making
- **Team Decision Making** - Business situations requiring team solutions
- **Written Events** - Business plans, research papers
- **Entrepreneurship Events** - Start-up, franchise, business growth
- **Integrated Marketing Campaign** - Multi-component marketing projects
- **Professional Selling & Consulting** - Sales presentations and business consulting
