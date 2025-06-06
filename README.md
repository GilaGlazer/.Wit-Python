"# .Wit-Python-MongoDB" 
# CodeGuard – Code Analysis System for `wit push`

## Overview

CodeGuard is a backend system designed to automatically analyze Python code every time the user runs the `wit push` command. It acts as a lightweight Continuous Integration (CI) tool focused on code quality by detecting common issues in code and providing visual insights through graphs.

The system uses Python's Abstract Syntax Tree (AST) to inspect code, identifies issues such as long functions, unused variables, missing docstrings, and large files, and then generates informative graphs with Matplotlib to help developers maintain clean and efficient code.

Now includes support for **MongoDB** to track historical analysis results over time and generate trends.

---

## Installation and Execution

### Prerequisites

Make sure you have Python 3.7+ installed.

### Required Packages

Install the necessary Python packages using pip:

```bash
pip install fastapi uvicorn python-multipart matplotlib requests pymongo
 ```

### Running the Server

Start the FastAPI server with:

```bash
uvicorn app:app --reload

---

## Project Folder Structure

```
### 📁 Backend Server 
/server
│
├── analyzer.py              # AST-based code analysis logic
├── app.py                   # FastAPI server with API endpoints
├── matplotlibFunc.py        # Graph generation using matplotlib
├── db.py                    # MongoDB integration (new)
└── .venv/                   # Virtual environment

### 📁 wit Client 
/client
│
├── commit.py # Handles commit logic
├── displayImage.py # Displays analysis graphs locally
├── func_files.py # Utility functions for file handling
├── main.py # Main entry point for the wit CLI
├── repository.py # Basic version control logic
├── wit.bat # Batch file for CLI execution
└── .venv/ # Virtual environment
```

---

## API Endpoints

| Endpoint          | Method | Description                                                              |
|-------------------|--------|--------------------------------------------------------------------------|
| `/analyze`        | POST   | Accepts Python files and returns code analysis graphs as images.         |
| `/alert`         | POST   | Accepts Python files and returns JSON warnings for code issues detected. |
| `/graph/image`    | GET    | Returns a specific image (PNG) of a generated graph by file path query.  |

Example usage:
```
GET /graph/image?path=graphs/function_lengths.png
```

---


## Code Quality Checks

The server performs the following checks on each pushed file:

- **Function Length:** Warns if any function exceeds 20 lines.
- **File Length:** Warns if the entire file exceeds 200 lines.
- **Unused Variables:** Warns if variables are assigned but never used.
- **Missing Docstrings:** Warns if functions lack documentation strings.
- **Bonus:** Detects variables written in non-English letters and issues warnings.

---

## Visual Graphs Provided

- **Histogram:** Distribution of function lengths across the codebase.
- **Pie Chart:** Breakdown of issues by type.
- **Bar Chart:** Number of issues per file.
- **Line Chart:** Number of total issues over time, powered by MongoDB.

---
## MongoDB Integration

CodeGuard now saves each analysis result to MongoDB when using the /alert endpoint. This allows tracking historical trends and generating time-based visualizations like the line chart.

Make sure to configure MongoDB connection in db.py.

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.


---
If you want to contribute or have questions, feel free to open an issue or pull request!

---

© 2025 CodeGuard Team
