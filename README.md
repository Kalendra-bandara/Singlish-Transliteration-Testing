# Singlish to Sinhala Transliteration — Automated Test Suite

Automated **Playwright** test suite that evaluates the accuracy of the **Chat Sinhala** transliteration function at [pixelssuite.com/chat-translator](https://www.pixelssuite.com/chat-translator).

The script reads test cases from an Excel file, types each Singlish input into the website, captures the Sinhala output, compares it with the expected output, and writes the result back to the Excel file.


## Author

|------------|--------------------------------|
| Name       | Bandara A.M.T.K                |
| Student ID | IT23829756                     |
| Module     | IT3040 — IT Project Management |
| Assignment | Assignment 1 — Option 1        |
|------------|--------------------------------|

## Project Files

```
singlish-transliteration-testing/
├── test_automation.py              Playwright automation script
├── Assignment 1 - Test cases.xlsx  Test cases (input + expected output)
└── README.md                       This file
```

## Prerequisites

Install these once before running the suite:

1. **Python 3.11 or 3.12** — https://www.python.org/downloads/
2. **Google Chrome** (recommended) — https://www.google.com/chrome/

---

## Installation

Open **Command Prompt** in the project folder (`D:\singlish-transliteration-testing`) and run:

```bash
pip install -U pip
pip install playwright openpyxl
playwright install
```

> `playwright install` downloads the browser binaries and may take a few minutes.

---

## How to Run

From inside `D:\singlish-transliteration-testing`, run:

```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --url "https://www.pixelssuite.com/chat-translator" --wait-ms 5000 --type-delay-ms 80 --slow-mo-ms 200 --save-every 1 --keep-open
```

### What happens

1. Chrome opens automatically and loads the Chat Translator page.
2. The script types each Singlish input from the Excel file one by one.
3. It waits for the Sinhala output and reads it.
4. It writes the result into the **Actual output** and **Status** columns of the Excel file.
5. The Excel file is saved after every test case.


## Command-Line Options

| Option            | Default                          | Description                                  |
|-------------------|----------------------------------|----------------------------------------------|
| `--excel`         | `Assignment 1 - Test cases.xlsx` | Path to the Excel test cases file            |
| `--url`           | pixelssuite chat-translator      | URL of the application under test            |
| `--wait-ms`       | `5000`                           | Time to wait for the translation output (ms) |
| `--type-delay-ms` | `80`                             | Delay between keystrokes when typing (ms)    |
| `--slow-mo-ms`    | `200`                            | Slow-motion delay for browser actions (ms)   |
| `--save-every`    | `1`                              | Save Excel file after every N test cases     |
| `--keep-open`     | off                              | Keep the browser open after the run finishes |

---

## Excel File Format

The Excel file `Assignment 1 - Test cases.xlsx` has 8 columns:

| Col | Header                       | Filled by | Description                                  |
|-----|------------------------------|-----------|----------------------------------------------|
| A   | TC ID                        | You       | `Neg_0001` to `Neg_0050`                     |
| B   | Input length type            | You       | `S` (≤30 chars), `M` (31–299), `L` (300–450) |
| C   | Input                        | You       | Chat-style Singlish input                    |
| D   | Expected output              | You       | Correct Sinhala translation                  |
| E   | Actual output                | Script    | Output captured from the website             |
| F   | Status                       | Script    | `Pass` or `Fail`                             |
| G   | Singlish input types covered | You       | Which input types apply                      |
| H   | Evidence or rationale        | You       | Justification for each type                  |

> Only fill columns **A–D** before running the script. Columns **E** and **F** are auto-filled. Columns **G** and **H** are filled in manually after the run.

---

## Test Case Coverage

The suite contains **50 negative test cases** (`Neg_0001`–`Neg_0050`) — cases where the system **fails** to correctly transliterate. At least two cases are included for each of the 24 Singlish input types defined in the assignment:

| #  | Input Type                       | #  | Input Type                       |
|----|----------------------------------|----|----------------------------------|
| 1  | Question forms                   | 13 | English Abbreviations / Acronyms |
| 2  | Command forms                    | 14 | English Clipped Forms            |
| 3  | Greetings                        | 15 | Place Names                      |
| 4  | Requests                         | 16 | Person Names                     |
| 5  | Responses                        | 17 | Numbers & Numeric Suffixes       |
| 6  | Repeated Words                   | 18 | Currency                         |
| 7  | Punctuation Marks                | 19 | Time Formats                     |
| 8  | Romanization / Spelling Variants | 20 | Dates                            |
| 9  | Isolated English Word Insertions | 21 | Units of Measurement             |
| 10 | Multi-Word English Phrases       | 22 | Slang & Casual Phrasing          |
| 11 | English Digital Terms            | 23 | Online Identifiers               |
| 12 | Platform / App Names             | 24 | Emojis                           |

---

## Scope

**In scope:** the **Chat Sinhala** transliteration function only.

**Out of scope:** Standard Sinhala transliteration, backend APIs, performance, scalability, and security testing.

---

## Troubleshooting

| Problem                         | Fix                                                        |
|---------------------------------|------------------------------------------------------------|
| `playwright: command not found` | Re-run `pip install playwright`, then `playwright install` |
| Browser doesn't open            | Run `playwright install` to download Chromium              |
| Excel file is locked            | Close the file in Excel before running the script          |
| Output is empty / timing out    | Increase `--wait-ms` (e.g. `--wait-ms 8000`)               |
| Typing is too fast              | Increase `--type-delay-ms` and `--slow-mo-ms`              |
