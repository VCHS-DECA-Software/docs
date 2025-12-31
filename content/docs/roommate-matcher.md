+++
title = "Roommate Matcher"
description = "Automatically create roommate groups for DECA trips"
weight = 10
draft = false
toc = true
bref = "Automatically create roommate groups for DECA trips"
+++

### [GitHub Repository](https://github.com/VCHS-DECA-Software/Roommate-Matcher)

## Overview

Roommate Matcher is a **Python** tool that automatically assigns students to hotel rooms for DECA trips based on their preferences. Using a weighted scoring system and a modified version of Irving's Algorithm, it creates optimal room groupings while enforcing chapter policies on gender and grade-level requirements.

## Tech Stack

- **Language:** Python
- **Libraries:** Pandas (data manipulation), NumPy (matrix operations)
- **Input:** CSV file from Google Forms
- **Output:** CSV files for room assignments and errors

## How It Works

The algorithm uses a **preference-weighted matrix approach** combined with Irving's Stable Roommates Algorithm to create fair and optimal room assignments.

### Step 1: Load and Parse Data

The program reads a CSV file (typically exported from Google Forms) containing:
- Student names and email addresses
- Grade level and gender
- First, second, and third roommate preferences

### Step 2: Build the Preference Matrix

A square matrix is created where:
- Rows and columns represent each student
- Cell values represent preference weights between students

### Step 3: Validate Preferences

For each student's preferences, the program validates:

| Check | Description |
|-------|-------------|
| **Form Completion** | The preferred roommate must have submitted the form |
| **Self-Reference** | Students cannot list themselves as a preference |
| **Gender Match** | Students must be the same gender (VCHS DECA policy) |
| **Grade Proximity** | Students cannot be more than one grade level apart |

Failed validations are logged to `errors.csv` for follow-up.

### Step 4: Assign Preference Weights

Each valid preference receives a weighted score:

| Preference | Weight |
|------------|--------|
| First Choice | 10 points |
| Second Choice | 7 points |
| Third Choice | 4 points |

### Step 5: Run Matching Algorithm

The program uses a **modified Irving's Algorithm** to find stable room assignments:
1. Each student "proposes" to their highest-weighted preference
2. Students tentatively accept or reject based on their own preferences
3. The algorithm eliminates impossible pairings and cycles
4. Final stable groupings are determined

### Step 6: Convert IDs to Student Data

The algorithm outputs are student IDs from the DataFrame. These are converted back to actual student information (names, emails, etc.).

### Step 7: Generate Output Files

Two CSV files are created:
- **rooms.csv** - Final room assignments
- **errors.csv** - Students with preference validation issues

## File Structure

```
Roommate-Matcher/
├── main.py              # Main entry point
├── matcher.py           # Core matching algorithm
├── validator.py         # Preference validation logic
├── [input].csv          # Input data from Google Forms
├── rooms.csv            # Output room assignments
├── errors.csv           # Validation errors log
└── README.md            # Setup instructions
```

## Getting Started

### Prerequisites
- Python 3.x
- Required libraries: `pandas`, `numpy`

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/VCHS-DECA-Software/Roommate-Matcher.git
   cd Roommate-Matcher
   ```

2. Install dependencies:
   ```bash
   pip install pandas numpy
   ```

### Usage

1. Export your Google Form responses as a CSV file
2. Place the CSV in the project directory
3. Update the input filename in the code if necessary
4. Run the program:
   ```bash
   python main.py
   ```

### Input Format

Your CSV file should include these columns:
- Student name
- Email address
- Grade level
- Gender
- First preference (name)
- Second preference (name)
- Third preference (name)

## Output

### rooms.csv

Contains the final room assignments:

| Room | Student 1 | Student 2 | Student 3 | Student 4 |
|------|-----------|-----------|-----------|-----------|
| 1 | John Smith | Alex Johnson | Chris Lee | Sam Brown |
| 2 | Jane Doe | Pat Wilson | Morgan Taylor | Jordan Davis |

This file can be directly imported into Google Sheets or Microsoft Excel for distribution.

### errors.csv

Lists students with preference validation issues:

| Student Name | Email | Error |
|--------------|-------|-------|
| Student A | a@school.edu | First preference did not fill out form |
| Student B | b@school.edu | Second preference is different gender |

Use this file to follow up with students who need to update their preferences.

## Algorithm Details

### Why Irving's Algorithm?

Irving's Stable Roommates Algorithm guarantees:
- **Stability** - No two students would both prefer each other over their assigned roommates
- **Fairness** - Preferences are weighted equally across all participants
- **Optimality** - The solution maximizes overall preference satisfaction

### Modifications for DECA

The standard algorithm is modified to:
- Handle groups of 3-4 students (not just pairs)
- Enforce policy constraints (gender, grade level)
- Weight preferences asymmetrically (first choice worth more than third)

## Use Cases

- State Career Development Conference (SCDC) hotel assignments
- International Career Development Conference (ICDC) room planning
- Regional competition overnight trips
- Any multi-day DECA event requiring room assignments
