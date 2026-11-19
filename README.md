# Event Registration Cleaner

**CIT AI-Native Engineering Programme – Semester 1 – Assessment 5**
**Domain:** Event Registration
**Application Type:** Console-based Python Program

## 1. Project Overview

The Event Registration Cleaner processes CSV files containing event-registration messages in different formats.

Gemini extracts five fields: `name`, `phone`, `email`, `year`, and `branch` into JSON format.

Python performs fact-checking, data cleaning, validation, duplicate detection, and report generation.

The program generates three reports:

- `clean_list.csv` – Valid registrations.
- `problems.csv` – Registrations requiring correction or marked as duplicates.
- `summary.txt` – Registration statistics and counts.

## 2. Project Files

| File                     | Description                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------ |
| `main.py`                | Main program with Gemini API, fallback extraction, validation, and report generation |
| `registrations.csv`      | Sample input containing 24 registrations                                             |
| `SYSTEM_PROMPT.txt`      | System prompt with five roles and two examples                                       |
| `eval_harness.py`        | Evaluation testing program                                                           |
| `eval_results.txt`       | Evaluation results                                                                   |
| `red_team_checks.py`     | Red-team testing program                                                             |
| `red_team_results.md`    | Red-team test results                                                                |
| `clean_list.csv`         | Valid registration records                                                           |
| `problems.csv`           | Invalid and duplicate records                                                        |
| `summary.txt`            | Summary of registration statistics                                                   |
| `SPECIFICATION.md`       | Project specification                                                                |
| `specification.pdf`      | PDF version of the specification                                                     |
| `JUDGMENT_FRAMEWORK.md`  | Responsibility and decision framework                                                |
| `COST_AND_LATENCY.md`    | API cost and processing-time analysis                                                |
| `AI_DECISION_JOURNAL.md` | Record of AI-assisted decisions                                                      |
| `REFLECTION.md`          | Project reflection                                                                   |
| `GITHUB_STEPS.md`        | GitHub setup and commit instructions                                                 |

## 3. Requirements

- Python 3.10 or later
- Gemini API key
- Internet connection for live API extraction
- No third-party Python packages required

## 4. Gemini API Setup

1. Create an API key using [Google AI Studio](https://aistudio.google.com/).
2. Create a `.env` file in the project folder.
3. Add your API key:

```text
GEMINI_API_KEY=YOUR_API_KEY
GEMINI_MODEL=gemini-3.6-flash
```

4. Save the file.

The API key is loaded from `.env` and is not hard-coded in the Python program.

## 5. Running the Program

Open PowerShell in the project folder.

**Run with Gemini API:**

```powershell
python main.py
```

**Run in offline mode:**

```powershell
python main.py --offline
```

**Specify input and output folders:**

```powershell
python main.py --input registrations.csv --output-dir reports
```

The program generates `clean_list.csv`, `problems.csv`, and `summary.txt` in the selected output folder.

## 6. Running Tests

Run the evaluation harness:

```powershell
python eval_harness.py
```

Run the red-team checks:

```powershell
python red_team_checks.py
```

These scripts evaluate extraction accuracy, validation, fact-checking, and duplicate detection using predefined test cases.

## 7. Data Processing Rules

- The LLM extracts registration fields without correcting the original information.
- Python verifies extracted phone numbers and email addresses against the original entries.
- Phone numbers are cleaned by removing formatting, country code `91`, or a leading `0`.
- Valid phone numbers must contain ten digits and start with 6, 7, 8, or 9.
- Email addresses are converted to lowercase after validation.
- Missing email suffixes are not automatically completed.
- Year must be between 1 and 4.
- Branches are checked against the predefined allowed list.
- Duplicate registrations are identified using cleaned phone numbers or email addresses.
- The first occurrence is retained, and subsequent duplicates are included in `problems.csv`.

## 8. GitHub

Refer to `GITHUB_STEPS.md` for repository creation, commit sequence, and publishing instructions.


