+++
draft= false
title = "FAQ"
description = "Asked and answered"
+++

## General

### How do I get started?

Download the code on [GitHub](https://github.com/VCHS-DECA-Software). Each repository includes a README with setup instructions specific to that tool.

### What programming languages are used?

- **Roommate Matcher** - Python (with Pandas, NumPy)
- **Roster Registration Checker** - Python (with Pandas, openpyxl)
- **Tabulation** - Python (with Pandas, openpyxl)
- **Event Scheduler** - Go

### Do I need programming experience to use these tools?

Basic familiarity with running scripts is helpful, but most tools are designed to be straightforward. You'll need to install dependencies and update file paths in the code, but detailed instructions are provided in each tool's documentation.

## Data & Input

### What file formats are supported?

Most tools use CSV or Excel (.xlsx) files as input. Data is typically exported from Google Forms or Google Sheets.

### How should I structure my Google Form for Roommate Matcher?

Your form should collect: student name, email address, grade level, gender, and three roommate preferences (by email). See the [Roommate Matcher documentation](/docs/roommate-matcher/) for example screenshots.

### Why are email addresses used for matching instead of names?

Email addresses are unique identifiers that avoid issues with duplicate names, nicknames, or spelling variations.

## Troubleshooting

### What happens if a student lists an invalid roommate preference?

Invalid preferences (wrong gender, grade gap too large, unlisted student) are logged to `errors.csv` for follow-up. The algorithm continues matching with valid preferences only.

### The Roommate Matcher isn't finding matches for some students. Why?

This usually happens when:
- A preferred roommate didn't submit the form
- Preferences violate gender or grade policies
- Students only listed each other, creating isolated pairs

Check `errors.csv` for specific issues.

### How do I update file paths in the code?

Look for variables like `roster_file`, `registration_file`, or `scoring_sheet_url` near the top of each script. Update these strings to match your actual file names.

## Contributing

### Can I contribute to these projects?

Yes! Visit the [GitHub organization](https://github.com/VCHS-DECA-Software) to view open issues or submit pull requests.

### I found a bug. How do I report it?

Open an issue on the relevant GitHub repository with a description of the problem and steps to reproduce it.