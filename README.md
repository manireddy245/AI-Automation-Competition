# AI Event-to-Google-Form Automation

## What it does

This automation turns an event description entered in Google Sheets into a Google Form. It uses AI to identify the form title, description, questions, required fields, and answer choices, then creates the form and records its responder link and creation time in Google Sheets.

## How it works

1. **Google Sheets watches for new rows** containing event descriptions.
2. **Google Gemini AI analyzes the description** and returns a structured form specification. It includes the proposed questions, answer options, assumptions, warnings, and preflight information.
3. **Google Forms creates the form** using the generated title and description.
4. **Google Sheets adds a result row** with the form details, including the responder link and creation time.
5. **The Iterator processes the questions** one at a time.
6. **The Router sends each question to the matching route** based on its type. Separate Google Forms modules handle short text, long text, multiple choice, checkbox, dropdown, date, and time questions.
7. **Questions are inserted at position 0.** Gemini returns them in reverse of the desired display order, so the finished form displays them in the intended order.

## Tools used

- **Make.com** — connects the services and runs the workflow.
- **Google Sheets** — receives event descriptions and stores generated form details.
- **Google Gemini AI** — interprets event descriptions and generates the form specification.
- **Google Forms** — creates the form and its questions.

## Supported question types

Short text, long text, multiple choice, checkboxes, dropdowns, dates, and times.

## Current limitations

File uploads, conditional questions, section branching, and special write-in “Other” options are not supported in this version. Gemini’s preflight information can flag unsupported requests for review.
