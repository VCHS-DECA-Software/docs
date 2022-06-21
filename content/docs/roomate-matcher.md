+++
title = "Roommate Matcher"
description = "Automatically create roommate groups for DECA trips"
weight = 10
draft = false
toc = true
bref = "Automatically create roommate groups for DECA trips"
+++

### How to Use

Follow the directions [here](https://github.com/VCHS-DECA-Software/Roommate-Matcher/blob/1467d7250a9ff51ab5eebb111f0a5a21aa56bd37/README.md) to get started.

### How it works

1. The program converts the CSV file into a Pandas DataFrame.

2. The program uses the dataframe to create a square matrix with the number of rows and columns equal to the number of students.

3. The program then separates the students into cohorts. There are 4 cohorts: underclassmen boys, underclassmen girls, upperclassmen boys, and upperclassmen girls. This is to comply with the school policies for creating rooms. 

4. Iterating through each DataFrame, the program assigns a score/weight to the preferences (First preference: 10, Second preference: 7, Third preference: 4). The program checks for missing preferences and students assigning themselves as a preference. If this happens, the program will print out the error. 

5. The program uses a modified version of Irving's Algorithm to create rooms. However at this point, the output is ID's of the student from the original DataFrame. 

6. The program then converts the ID's into the actual data of each student in a group. 

7. The program outputs `rooms.csv`. This file contains the room allocations and can be imported into Google Sheets or Microsoft Excel.
