Project Documentation Report
Exercise: Project Documentation

Option Selected: Task Manager System (Python 3.11 CLI)

Date: July 2026

1. Selected Project Information
Project Name: Task Manager CLI

Description: A lightweight, modular Python command-line application built to create, organize, filter, priority-score, and persist tasks without external library dependencies 
Key Features:

Interactive CLI for task creation, status updates, filtering, and tag management.

Weighted multi-factor priority scoring algorithm.

Local file persistence using JSON (tasks.json).

CSV export utility for external reporting.
Technologies Used: Python 3.11 Standard Library (argparse, json, datetime, unittest).

Code Structure:

cli.py — Command-line Interface and argument parser.

task_manager.py — Core business logic and task management queries.

repository.py — File I/O and JSON persistence layer.
models.py — Data entities (Task) and state definitions (TaskStatus, TaskPriority).

tests/ — Automated unit testing suite.

2. Prompt 1 Output: Comprehensive README.md
3. # Task Manager CLI

A lightweight, zero-dependency Python command-line interface for managing everyday tasks, tracking deadlines, and prioritizing work items.

---

## Features

- **Zero External Dependencies:** Runs natively on Python 3.11 standard library modules.
- **Dynamic Priority Scoring:** Automatically ranks tasks based on urgency, deadlines, status, and custom tags.
- **JSON File Persistence:** Stores state locally in `tasks.json` so your data persists across sessions.
- **CSV Data Export:** Export task lists to standard CSV format for external reporting.
- **Flexible Search & Filtering:** View tasks by status, priority level, or custom tag.

---

## Installation & Setup

### Prerequisites
- **Python 3.11** or higher.

### Quickstart
1. Clone your repository:
   ```bash
   git clone [https://github.com/YOUR-USERNAME/ai-code-exercises.git](https://github.com/YOUR-USERNAME/ai-code-exercises.git)
   cd ai-code-exercises
   python --version
   python cli.py --help
   Basic Usage Examples
1. Add a New Task
2. python cli.py add "Fix login bug" --priority HIGH --due 2026-08-05 --tags blocker critical
3. 2. List Top Priority Tasks
   3. python cli.py list --top 5
   4. 3. Update Task Status
      4. python cli.py update --id 1 --status IN_PROGRESS
      5. python cli.py export --output my_tasks.csv
     
      Project Structure
      ai-code-exercises/
├── cli.py             # Presentation layer & CLI entry point
├── task_manager.py    # Service layer housing business logic
├── repository.py      # Data access layer for JSON reading/writing
├── models.py          # Domain entities (Task, TaskStatus, TaskPriority)
├── tasks.json         # Local data store (generated on first run)
└── tests/             # Automated test suite
    └── test_task_manager.py
Configuration Options
Custom Storage File: By default, data is written to tasks.json in the root folder. You can override this location by setting the environment variable:
export TASK_STORAGE_PATH="/path/to/custom_tasks.json"
Troubleshooting:
Issue	Cause	Solution
FileNotFoundError: tasks.json	Running the app for the first time without write permissions in the directory.	Ensure write permissions in the folder, or run python cli.py add ... to auto-initialize tasks.json.
ValueError: Invalid date format	Dates must strictly follow YYYY-

Contributing Guidelines
Fork the repository.

Create a feature branch (git checkout -b feature/new-feature).

Ensure unit tests pass (python -m unittest discover tests).

Commit your changes and open a Pull Request.
License
This project is released under the MIT License.
---

## 3. Prompt 2 Output: Step-by-Step Feature Guide

# User Guide: Setting Up, Managing, and Exporting Tasks

**Target Audience:** Beginner to Intermediate Developers  
**Task Goal:** Create your first task, monitor its priority rank, update its progress, and export your task list to a CSV report.

---

### Prerequisites
Terminal or Command Prompt access.
* Python 3.11 installed.

---

### Step-by-Step Instructions

#### Step 1: Open Your Terminal & Navigate to the Folder
Open your terminal and change directory into your project repository:
```bash
cd path/to/ai-code-exercises
Step 2: Create a High-Priority Task
Add a new task with a deadline and tags:
python cli.py add "Prepare presentation for Friday" --priority URGENT --due 2026-07-31 --tags presentation blocker
Expected Output:

[SUCCESS] Task #1 created: 'Prepare presentation for Friday' (Score: 88)
Step 3: View Ranked Tasks
Display tasks ordered by calculated urgency:
python cli.py list
Expected Output:
ID  | Title                           | Status      | Priority | Score
----------------------------------------------------------------------
1   | Prepare presentation for Friday | TODO        | URGENT   | 88

Step 4: Advance Task Status
Move the task to IN_PROGRESS as you begin working on it:
python cli.py update --id 1 --status IN_PROGRESS

Step 5: Export to CSV
Export all tasks into a spreadsheet-compatible format:
python cli.py export --output report.csv
Expected Output:

[SUCCESS] Exported 1 task(s) to report.csv
Common Errors & Mistakes
💡 Warning — Date Formatting:

Always use YYYY-MM-DD. Entering 31-07-2026 or 07/31/2026 will trigger a date parsing error.

Guide Troubleshooting
Problem: CLI returns command not found: python.

Fix: Try using python3 cli.py ... instead.

Problem: CSV file contains strange characters or wrong column alignment.

Fix: Ensure task titles containing commas are enclosed in quotes when using the CLI.

4. Prompt 3 Output: FAQ Document
Task Manager CLI — Frequently Asked Questions (FAQ)

1. Getting Started
Q: Do I need to install any external libraries like requests or pandas?
A: No. The Task Manager is built strictly using standard Python standard library tools (argparse, json, datetime, csv).

Q: How is my task data stored?
A: Tasks are serialized and saved locally in a tasks.json file created in the project root directory.

2. Features & Functionality
Q: How does the priority scoring system work?
A: Scores combine base priority (LOW=10 to URGENT=60), deadline proximity (+35 points if overdue), recent modifications (+5 points), and urgent tags (blocker, critical, urgent add +8 points). Finished tasks (DONE) receive a -50 point deduction.

Q: Can I add multiple tags to a single task?
A: Yes. Space-separate your tags during creation:
python cli.py add "Task Name" --tags tag1 tag2 tag3

3. Troubleshooting Common Issues
Q: What happens if tasks.json gets corrupted or deleted?
A: If deleted, the application creates a fresh, empty tasks.json file on the next write operation. If corrupted, restore a backup or delete the file to re-initialize storage.

Q: Why did my URGENT task score drop lower than a LOW task?
A: Once a task is updated to DONE, it suffers a -50 point penalty so completed items naturally drop to the bottom of your active task lists.

5. Reflection & Learning Points
Which aspects were most challenging to document?
Explaining the priority scoring algorithm in plain, non-technical terms inside the FAQ and README was the trickiest balance. Translating code loops and dictionary weights into easy-to-understand rules required refining the language several times.

How were prompts adjusted for better results?
Explicitly instructing the prompt to "include concrete CLI command examples and sample terminal output" produced actionable documentation instead of generic summaries.

Insights on document structure and organization
Dividing documentation by audience function works best:

README.md: Serves as the technical overview for developers inspecting the repo on GitHub.

Step-by-Step Guides: Help end-users execute real tasks quickly.

FAQ: Addresses recurring edge-case questions without cluttering the main guide.

Incorporating this approach into future workflows
Drafting documentation prompts alongside writing unit tests makes writing docs part of the feature delivery pipeline rather than an afterthought left until deadline day.
