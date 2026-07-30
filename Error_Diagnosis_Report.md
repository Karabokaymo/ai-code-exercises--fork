Error Diagnosis Report
Exercise: Error Diagnosis Challenge

Selected Scenario: Python IndexError: list index out of range in stock_manager.py

Date: July 2026

1. Error Analysis & Root Cause
Error Description
Traceback (most recent call last):
  File "/home/user/projects/inventory/stock_manager.py", line 25, in <module>
    main()
  File "/home/user/projects/inventory/stock_manager.py", line 17, in main
    print_inventory_report(items)
  File "/home/user/projects/inventory/stock_manager.py", line 10, in print_inventory_report
    for i in range(len(items) + 1):
      print(f"Item {i+1}: {items[i]['name']} - Quantity: {items[i]['quantity']}")
IndexError: list index out of range

What it means: An IndexError occurs in Python whenever your code tries to access an element at a list position (index) that does not exist.

Root Cause: This is a classic off-by-one error.

Python lists use zero-based indexing. For a list with 3 items, valid position indices are 0, 1, and 2.

What it means: An IndexError occurs in Python whenever your code tries to access an element at a list position (index) that does not exist.

Root Cause: This is a classic off-by-one error.

Python lists use zero-based indexing. For a list with 3 items, valid position indices are 0, 1, and 2.

The function calculates len(items), which equals 3.
Adding + 1 makes the loop boundary range(4), producing the number sequence: 0, 1, 2, 3.

On the 4th iteration, the loop sets i = 3 and attempts to evaluate items[3]. Since index 3 does not exist, Python crashes with IndexError.


2. Suggested Solutions
Solution 1: Fix the Range Loop Boundary (Quick Fix)
Remove the + 1 addition inside the range() function so the loop stops at len(items) - 1.
def print_inventory_report(items):
    print("===== INVENTORY REPORT =====")
    # Corrected range boundary
    for i in range(len(items)):
        print(f"Item {i+1}: {items[i]['name']} - Quantity: {items[i]['quantity']}")
    print("============================")

Solution 2: Use Pythonic Iteration with enumerate() (Best Practice)
Instead of manually tracking list length and using index lookup brackets items[i], iterate over the list directly using Python's built-in enumerate() function.
def print_inventory_report(items):
    print("===== INVENTORY REPORT =====")
    # enumerate provides both the 1-based counter and item object directly
    for i, item in enumerate(items, start=1):
        print(f"Item {i}: {item['name']} - Quantity: {item['quantity']}")
    print("============================")

    3. Key Learning Points & Prevention Strategies
Avoid range(len(...)): Indexing into a list by position is error-prone. Iterating directly over items (for item in items) or using enumerate() eliminates boundary calculation errors entirely.
Remember Zero-Based Indexing: The highest valid index in any Python list is always len(list) - 1.

Input Validation: Ensure functions gracefully handle empty lists (items = []) before attempting loop processing.

4. Reflection Answers
How did the AI's explanation compare to online documentation?
Standard online documentation (like Python docs or Stack Overflow threads) explains IndexError in generic terms ("you accessed an index outside the list"). The AI trace analysis immediately pinpointed the exact line (line 10), highlighted the specific + 1 arithmetic mistake, and explained how len(items) = 3 conflicted with range(4).

What aspects of the error would have been difficult to diagnose manually?
In a small 20-line script, finding + 1 is quick. However, in large real-world applications where data is dynamically fetched from a database or external API, off-by-one errors can hide in edge cases (such as when lists are empty or contain only 1 item).

How would you modify your code to provide better error messages in the future?
Add defensive checks at the start of functions to handle unexpected inputs cleanly:
def print_inventory_report(items):
    if not items:
        print("Notice: Inventory report is empty.")
        return

    print("===== INVENTORY REPORT =====")
    for i, item in enumerate(items, start=1):
        print(f"Item {i}: {item.get('name', 'Unknown')} - Quantity: {item.get('quantity', 0)}")
    print("============================")


    Did the AI help you understand not just the fix, but the underlying concepts?
Yes. Rather than just giving a line replacement, it highlighted the core concept behind zero-based indexing arrays versus 1-based human count display (i + 1), showing why enumerate(items, start=1) is the cleaner overall pattern.
