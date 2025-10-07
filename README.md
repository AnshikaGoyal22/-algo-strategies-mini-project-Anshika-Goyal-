# -algo-strategies-mini-project-Anshika-Goyal-
## Problem 1: Scheduling TV Commercials to Maximize Impact

### Problem Description
This problem involves scheduling a set of TV commercials, each with a specified deadline and profit value, to maximize the total profit earned. The commercials must be scheduled in such a way that each commercial is aired before its deadline without overlapping time slots.

### Algorithm Strategy
The problem is solved using a Greedy algorithm approach. First, the commercials are sorted in decreasing order of profit. Then, each commercial is assigned to the latest available time slot before its deadline. This ensures that the most profitable commercials are given priority and scheduled optimally.

### Code Snippet
Sort ads in descending order by profit
sorted_ads = sorted(ads, key=lambda x: x['profit'], reverse=True)

Find maximum deadline to know number of slots
max_deadline = max(ad['deadline'] for ad in ads)

Initialize slots: -1 means free slot
slots = [-1] * max_deadline

Result list to hold scheduled ads
scheduled_ads = [None] * max_deadline

for ad in sorted_ads:
for slot in range(ad['deadline'] - 1, -1, -1):
if slots[slot] == -1:
slots[slot] = 1
scheduled_ads[slot] = ad['id']
break

print("Scheduled commercials in slots:", scheduled_ads)

### Profiling Visualization
The profiling shows the efficiency of the greedy scheduling algorithm in terms of time and memory usage.

## Problem 2: Maximizing Profit with Limited Budget (Knapsack Problem)

### Problem Description
This problem involves selecting items with given weights and values to maximize total profit without exceeding a specified budget. The goal is to find the best combination of items to achieve maximum value within the budget constraints.

### Algorithm Strategy
The Bottom-Up 0/1 Knapsack dynamic programming algorithm is used. It builds a 2D table where each cell represents the maximum value achievable with a given number of items and budget capacity. The algorithm determines whether to include or exclude each item to maximize profit.

### Code Snippet
def knapsack(items, capacity):
n = len(items)
dp = [[0 for _ in range(capacity + 1)] for _ in range(n + 1)]

text
for i in range(1, n + 1):
    for w in range(1, capacity + 1):
        if items[i-1]['weight'] <= w:
            dp[i][w] = max(
                items[i-1]['value'] + dp[i-1][w - items[i-1]['weight']],
                dp[i-1][w]
            )
        else:
            dp[i][w] = dp[i-1][w]

w = capacity
selected_items = []
for i in range(n, 0, -1):
    if dp[i][w] != dp[i-1][w]:
        selected_items.append(items[i-1]['id'])
        w -= items[i-1]['weight']

selected_items.reverse()
return dp[n][capacity], selected_items
max_profit, selected = knapsack(items, total_budget)
print(f"Maximum profit: {max_profit}")
print(f"Selected items: {selected}")

### Profiling Results
- Execution time: 0.076543 seconds
- Memory usage: 111.097656 MiB


## Problem 3: Solving Sudoku Puzzle Using Backtracking

### Problem Description
The problem is to solve a partially filled Sudoku puzzle by filling empty cells so that each number from 1 to 9 appears exactly once in each row, column, and 3x3 subgrid. Empty cells are denoted by 0.

### Algorithm Strategy
A backtracking algorithm is used. The algorithm tries numbers 1 to 9 in empty cells, checks if the placement is valid, and recursively solves the puzzle. If a contradiction is found, it backtracks to previous cells and tries different numbers until the solution is found.

### Code Snippet
def is_valid(board, row, col, num):
for i in range(9):
if board[row][i] == num or board[i][col] == num:
return False

text
start_row, start_col = 3 * (row // 3), 3 * (col // 3)
for i in range(start_row, start_row + 3):
    for j in range(start_col, start_col + 3):
        if board[i][j] == num:
            return False
return True
def solve_sudoku(board):
for row in range(9):
for col in range(9):
if board[row][col] == 0:
for num in range(1, 10):
if is_valid(board, row, col, num):
board[row][col] = num
if solve_sudoku(board):
return True
board[row][col] = 0
return False
return True

if solve_sudoku(sudoku_grid):
for row in sudoku_grid:
print(row)
else:
print("No solution exists")

### Profiling Results
- Execution time: 0.091826 seconds
- Memory usage: 111.097656 MiB


## Problem 4: Password Cracking Using Brute-Force Algorithm

### Problem Description
The problem requires cracking a password by generating all possible combinations of characters from a given charset. The goal is to find the target password by brute force, trying all possible character sequences up to a specified maximum length.

### Algorithm Strategy
A brute-force algorithm is used, which tries every possible combination of characters starting from length 1 up to a maximum length. The algorithm stops when the target password is found.

### Code Snippet
import itertools
import time

def brute_force_password(target, charset, max_length=4):
attempt_count = 0
start_time = time.time()

for length in range(1, max_length + 1):
    for guess in itertools.product(charset, repeat=length):
        attempt_count += 1
        guess_str = ''.join(guess)
        if guess_str == target:
            end_time = time.time()
            print(f"Password found: {guess_str}")
            print(f"Total attempts: {attempt_count}")
            print(f"Time taken: {end_time - start_time:.6f} seconds")
            return guess_str, attempt_count, end_time - start_time

print("Password not found within max length")
return None, attempt_count, time.time() - start_time
result, attempts, duration = brute_force_password(target_password, charset)
