# Damage Ticket Solver
<img width="1031" height="503" alt="image" src="https://github.com/user-attachments/assets/fae6de71-9667-4df5-8f03-0384a7ca3677" />

## 1. Problem Description

This project solves a damage ticket problem on a grid using logical constraints.

We are given:
- A grid of `n` rows and `m` columns
- Each cell contains:
  - `*` : potentially damaged
  - `-` : confirmed damaged
- Two lists of integers:
  - `total_line[i]`: number of damaged cells expected in row `i`
  - `total_col[j]`: number of damaged cells expected in column `j`

### Objective

Determine which `*` cells must be replaced by `-` so that:
- Each row contains exactly `total_line[i]` damaged cells
- Each column contains exactly `total_col[j]` damaged cells

If the solution cannot be uniquely determined using logic only, the program outputs: **NON**

---

## 2. Algorithm Steps

### 2.1 Input Reading

- Read integers `n` and `m`
- Read the grid
- Read row totals and column totals

---

### 2.2 Remaining Damage Calculation

For each row and column, the algorithm computes how many damaged cells are still missing:

- `n_manquant[i]`: missing damaged cells in row `i`
- `m_manquant[j]`: missing damaged cells in column `j`

---

### 2.3 Trivial Case Elimination

If:
- `total_line[i] == m`, then all cells in row `i` must be damaged
- `total_col[j] == n`, then all cells in column `j` must be damaged

All corresponding `*` cells are immediately replaced by `-`.

---

### 2.4 Possible Damage Positions

A cell `(i, j)` is considered a possible damage position if:
- The cell is not already `-`
- Row `i` still needs damaged cells
- Column `j` still needs damaged cells

All such positions are stored in a list of possibilities.

---

### 2.5 Forced Placement Logic

The algorithm repeatedly applies the following rule:

If the number of remaining damaged cells in a row (or column) is equal to the number of possible positions in that row (or column), then all those positions must be damaged.

For each forced placement:
- The grid is updated
- Row and column counters are updated
- Invalid possibilities are removed

This process continues until no further deduction is possible.

---

### 2.6 Termination Conditions

- If all required damaged cells are placed, the final grid is printed
- If no forced placement is possible while damage is still missing, the program prints `NON`

---

## 3. Presentation

A presentation is provided with this project and explains:
- The problem constraints
- The reasoning behind the algorithm
- Step-by-step examples
- How forced placements are deduced
- Why the algorithm stops when ambiguity remains

The presentation follows the same logic as the implementation.

<img width="1278" height="716" alt="image" src="https://github.com/user-attachments/assets/2272fc93-9e75-4508-a4fb-921583df8fc0" />

---

## 4. Input Format

The input must be provided via standard input.

Example:
```
5 6
- * * * - *
* * * - * *
* - * * * *
* * * * * *
* * * * * *
4 2 2 3 6
3 2 1 3 3 5
```

---

## 5. How to Run

### Requirements

- Python 3.x

### Execution

Run the script and provide the input: `python damage_ticket.py`  
Or using an input file: `python damage_ticket.py < input.txt`


## 6. Output

- The resolved grid is printed if the solution is uniquely determined
- `NON` is printed if the solution is ambiguous or cannot be deduced logically

---
