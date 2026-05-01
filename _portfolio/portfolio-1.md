---
title: "Constraint Satisfaction Problem Solver: Sudoku as a Model of Mathematical Computing Implemented from First Principles"
excerpt: "A Sudoku solver implemented from first principles using recursive backtracking, later identified as an equivalent to the standard Depth-First Search based solutions.<br/><br><img src='/images/sudoku_solver_sample.PNG'>"
collection: mathematics-portfolio
tags: [mathematics-portfolio]
---

This is an item in your portfolio. It can be have images or nice text. If you name the file .md, it will be parsed as markdown. If you name the file .html, it will be parsed as HTML. 

## Overview 

This project explores several principles of mathematical computing, specifically Constraint Satisfaction Problems (CSPs), algorithm design, and computational complexity. CSPs define specific conditions (constraints) that must be met in order for a mathematical solution to be valid. 

Sudoku was the problem that was chosen to model a CSP, as I was already familiar with its rules, which allowed me focus specifically on the mathematical aspects of solving it. In addition, Sudoku is a well-known problem that can be explored from a computational perspective as it has clearly defined rules, forming the constraints to be met, as well as demonstrating the principles of algorithm design through specific steps or techniques followed to solve the puzzle. The goal of the project was to explore mathematical computing in an open-ended environment by simply choosing a mathematical problem of interest and producing a working solution written in Python without having any prior knowledge of existing algorithms or commonly-implemented solutions. 

The resulting implementation, developed from first principles, performs recursive backtracking over a 9x9 Sudoku grid. After completion, I independently performed research to learn why Sudoku falls within the NP-complete domain which directed me towards the standard approaches used to solve Sudoku. As a result, I found that the method I implemented aligns with the Depth-First Search (DFS) backtracking principle, which is a common and standardized technique used for solving CSPs. 

## Problem Context

This project falls within three specific pillars of mathematical computing:

### 1. Constraint Satisfaction Problems (CSPs)

An unsolved Sudoku puzzle can be used to model a CSP with the following conditions:

- Variables: defined as each empty square within the grid. Given that Sudoku puzzles contain several starting numbers, this grid represents the initial condition in which the variables only correspond to the empty squares. 

- Domains: correspond to the set of values {1-9} that can be assigned to each variable.

- Constraints: correspond to the clearly defined rules of Sudoku that state each row and column must be unique with no conflicts (meaning repeated values) and that each row, column, and 3x3 grid must contain the numbers 1 through 9. 

### 2. Algorithm Design

The object of the chosen problem was to implement a working set of steps (the algorithm) in Python that systematically explores valid number placement, avoids number conflicts and then outputs the solved Sudoku puzzle. 

### 3. Computational Complexity

Sudoku is an NP-complete problem, which means that a solution can be verified very quickly (in polynomial time), but as complexity of the puzzles increase, a solution cannot be found in polynomial time using any known techniques. 

## Methodology

The solver was implemented from first principle reasoning applied to structured experimentation on partial board configurations. The resulting approach demonstrates recursive backtracking over the 9x9 grid:

1. Identify the next empty square in the grid.
2. Iterate through the possible values that can be assigned to this square {1-9}.
3. Determine whether an assignment meets the required conditions.
4. Recursively apply this process to the 9x9 grid for each new assignment made to an empty square.
5. Backtrack when either a conflict or a dead-end occurs. 

## Implementation Process

The implementation performs recursive exploration over a given 9x9 Sudoku grid. In addition to recursion, the algorithm explicitly uses a stack data structure to manage variable assignments and control the search order. 

Key components include:

- A recursive structure that demonstrates DFS exploration of possible solutions.
- A stack used to store and manage cell coordinates for backtracking and traversal steps. 
- Updates to the Sudoku grid with either a value between 1 and 9 for a cell assignment or a 0 for reversal steps. 
- A state-management mechanism that ensures previous board configurations can be revisited during backtracking. 

## Post-Implementation Analysis

After completing the implementation, I investigated standard approaches and solutions to Sudoku solvers more broadly. This led to the observation that most of the effective Sudoku solvers utilize DFS backtracking techniques. 

Since this project was implemented from first principles, I had no prior knowledge of the DFS algorithm or that it was a standard solution for Sudoku problems. Therefore, this project is best classified as an independently derived DFS-based backtracking solver that differs from typical implementations, but still aligns with standard DFS techniques. 

## Results 

- Successfully solves 9x9 Sudoku puzzles.
- Correctly performs backtracking techniques to correct conflicts or dead-ends.
- Produces the complete solution that satisfies all required conditions.

[View Project Repo](https://github.com/kaitlinw-dev/sudoku_solver)