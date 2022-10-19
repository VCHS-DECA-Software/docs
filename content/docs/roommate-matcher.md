+++
title = "Roommate Matcher"
description = "Automatically create roommate groups for DECA trips"
weight = 10
draft = false
toc = true
bref = "Automatically create roommate groups for DECA trips"
+++

### [GitHub Repository](https://github.com/VCHS-DECA-Software/Roommate-Matcher)

### How to Use

Follow the directions [here](https://github.com/VCHS-DECA-Software/Roommate-Matcher/README.md) to get started.

### How it Works

1. The program converts the CSV file into a Pandas DataFrame.

2. The program uses the dataframe to create a square matrix with the number of rows and columns equal to the number of students.

3. The program then runs a series of checks for each of the student's preferences to make sure that:
- The student's preference has filled out the form
- The student has not entered themselves as a preference 
- The student and their preference are not more than one grade level apart (VCHS DECA policy)

4. Iterating through each DataFrame, the program assigns a score/weight to the preferences (First preference: 10, Second preference: 7, Third preference: 4). The program checks for missing preferences and students assigning themselves as a preference. If this happens, the program will print out the error. 

5. The program uses a modified version of Irving's Algorithm to create rooms. However at this point, the output is ID's of the student from the original DataFrame. 

6. The program then converts the ID's into the actual data of each student in a group. 

7. The program outputs `rooms.csv`. This file contains the room allocations and can be imported into Google Sheets or Microsoft Excel.
