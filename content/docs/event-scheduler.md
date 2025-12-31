+++
title = "Event Scheduler"
description = "Full-stack platform to schedule mock DECA conferences"
weight = 10
draft = false
toc = true
bref = "Full-stack platform to schedule mock DECA conferences"
+++

### [GitHub Repository](https://github.com/VCHS-DECA-Software/Event-Scheduler)

## Overview

Event Scheduler is a tool built in **Go** that automatically generates schedules for mock DECA conferences. It handles the complex task of assigning students to events, judges to assignments, rooms to judgments, and exam times to students—all while avoiding conflicts.

## Tech Stack

- **Language:** Go (98.6%)
- **Build System:** Makefile
- **Data Format:** Protocol Buffers for data serialization
- **Output:** CSV files

## How It Works

The scheduling algorithm uses a **bottom-up approach** that prioritizes flexibility and minimizes student conflicts. Here's the step-by-step process:

### Step 1: Gather Inputs
The system needs:
- **Time parameters:** Starting time and time slot duration
- **Constraints:** Maximum group size and exam length
- **Resources:** List of students, judges, events, and available rooms
- **Requests:** Which students want to participate in which events

### Step 2: Process Enrollment Requests
All student enrollment requests are converted into formal assignments.

### Step 3: Sort Judges by Availability
Judges are sorted from least to greatest based on their event restrictions. This preserves judges with broader availability for more complex scheduling needs.

### Step 4: Prioritize Large Groups
Larger groups are processed first (greatest to least by group size). This reduces scheduling conflicts since large groups have fewer available time slots.

### Step 5: Match Assignments to Time Slots
For each request, the algorithm:
1. Identifies time slots already occupied by overlapping groups
2. Places the request in an available, non-adjacent slot
3. Ensures no conflicts across all judges' schedules

### Step 6: Schedule Exams
The system finds consecutive free time blocks that match the required exam duration and assigns students accordingly.

### Step 7: Allocate Rooms
Judges are distributed across rooms while matching event type compatibility.

If any requests cannot be assigned, the system alerts the user.

## File Structure

```
Event-Scheduler/
├── cmd/              # Command-line applications
│   └── real/         # Main executable
├── components/       # Reusable modules
├── scheduler/        # Core scheduling logic
├── proto/            # Protocol buffer definitions
├── tests/            # Test suite
├── docs/             # Documentation
│   ├── conventions.md    # Coding standards
│   └── scheduling.md     # Algorithm explanation
├── output/           # Generated CSV files
├── go.mod            # Go dependencies
├── go.sum            # Dependency checksums
├── goreleaser.yml    # Release configuration
└── makefile          # Build automation
```

## Getting Started

### Prerequisites
- Go installed on your system

### Running the Scheduler

1. Navigate to the command directory:
   ```bash
   cd cmd/real
   ```

2. Build and run:
   ```bash
   go build && ./real
   ```

3. Open the generated `output.csv` in a spreadsheet application (Excel, Google Sheets, LibreOffice)

## Output

The scheduler generates an `output.csv` file containing:
- Student event assignments
- Judge schedules
- Room allocations
- Exam times

This file can be directly imported into spreadsheet software for viewing and further customization.
