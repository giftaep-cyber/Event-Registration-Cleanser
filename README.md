# Event Registration Cleaner

**CIT AI-Native Engineering Programme - Semester 1 - Assessment 5**  
**Domain:** Events  
**Application type:** Console-based Python program

## 1. What this project does

The program reads a CSV containing event-registration messages in different formats. The LLM copies five fields (`name`, `phone`, `email`, `year`, and `branch`) into JSON. Python then checks that the returned phone digits and email text really occur in the original entry, cleans the allowed formatting, validates every field, identifies duplicates after cleaning, and writes three reports.

The LLM does not correct contact details. The event team must review `problems.csv` and contact every person whose registration needs fixing or is a duplicate.

## 2. Project files

| File | Purpose |
|---|---|
| `main.py` | Main console program, Gemini API call, fallback, cleaning, checking, duplicate detection, and report writing |
| `registrations.csv` | Sample input with 24 registration entries |
| `SYSTEM_PROMPT.txt` | Five-role system prompt with two examples |
| `eval_harness.py` | Five-case evaluation harness |
| `eval_results.txt` | Saved evaluation result |
| `red_team_checks.py` | Three deterministic red-team checks |
| `red_team_results.md` | Saved red-team result and interpretation |
| `clean_list.csv` | Sample output: valid registrations only |
| `problems.csv` | Sample output: entries needing fixes or marked duplicate |
| `summary.txt` | Sample counts by status, branch, and year |
| `SPECIFICATION.md` / `specification.pdf` | One-page project specification |
| `JUDGMENT_FRAMEWORK.md` | Responsibility, risk, and human-checkpoint table |
| `COST_AND_LATENCY.md` | API call, timing, and cost estimate |
| `AI_DECISION_JOURNAL.md` | Record of important AI-assisted decisions |
| `REFLECTION.md` | 400-word project reflection |

## 3. Requirements

- Python 3.10 or later is recommended.
- No third-party Python package is required. The program uses Python's standard library only.
- Internet access and a Gemini API key are needed for live LLM extraction.

## 4. Set up the Gemini API key on Windows

1. Open this project folder in File Explorer.
2. Make a copy of `.env.example` and rename the copy to `.env`.
3. Open `.env` in Notepad and paste your own key after `GEMINI_API_KEY=`.
4. Save the file. Do not share `.env` or upload it to GitHub.
5. The default model is `gemini-3.6-flash`. To use another model available to your API key, set `GEMINI_MODEL` in `.env` too.

Example `.env` format (use your own key; never paste a real key into a public document):

```text
GEMINI_API_KEY=PASTE_YOUR_OWN_KEY_HERE
GEMINI_MODEL=gemini-3.6-flash
```

Create a key through [Google AI Studio](https://aistudio.google.com/). The program sends the key in the `x-goog-api-key` request header; it is not hard-coded in `main.py`.

## 5. Run the program

Open PowerShell in this folder. One easy method is to open the folder in File Explorer, click the address bar, type `powershell`, and press Enter.

Run with the LLM (requires a valid `.env` key):

```powershell
python main.py
```

Run without an API call, using the local fallback extractor:

```powershell
python main.py --offline
```

Use a different input file or output folder:

```powershell
python main.py --input registrations.csv --output-dir reports
```

The program creates or replaces `clean_list.csv`, `problems.csv`, and `summary.txt` in the chosen output folder.

## 6. Run the tests

```powershell
python eval_harness.py
python red_team_checks.py
```

The evaluation harness checks five fixed parser outputs against expected status and cleaned phone values. The red-team script supplies intentionally unsafe mock LLM outputs to test the Python fact-check and duplicate logic. These tests do **not** claim that a live model has passed the tests. Before the showcase, run the same inputs with your real API key, inspect the returned JSON, and record the actual outputs.

## 7. Important rules and human checkpoint

- The LLM copies. Python checks, cleans, counts, and writes the reports.
- A phone must contain ten digits after removing one leading `91` or `0`, and it must start with 6, 7, 8, or 9.
- An email is lowercased only when it has exactly one `@`, no spaces, and a dot after the `@`. Missing suffixes are never completed.
- Duplicates are detected using valid cleaned phone or email values. The first registration is retained; later matching registrations go to `problems.csv`.
- The event team reviews all rows in `problems.csv` and contacts the affected people. The program never decides or edits someone's correct contact details.

**Privacy note:** Registration names, phone numbers, and emails are personal data. Use dummy/sample data for practice. Before sending real registrations to an external API, obtain the required faculty/participant approval and follow the institution's data-handling rules. Check the provider's current data-use terms for the account tier you use.

## 8. Suggested GitHub commit sequence

See `GITHUB_STEPS.md` for the three meaningful commits and the steps to create and share your own repository. Confirm `.gitignore` before the first commit.
