# AI Event-to-Google-Form Generator

## What it does

This automation takes an event description written in plain language and creates a Google Form from it. It identifies the form title, description, questions, required fields, and answer choices, then adds the questions to the form according to their type.

## How it works

1. **Gemini analyzes the event description** and returns a structured form specification containing the title, description, questions, answer options, assumptions, warnings, and preflight status.
2. **Google Forms creates a new form** using the generated title and description.
3. **The Iterator processes the questions** one at a time.
4. **The Router sends each question to the matching route**, such as short text, long text, checkbox, multiple choice, dropdown, date, or time.
5. **Google Forms adds each question** to the new form. Questions are returned in reverse order because each one is inserted at position `0`; this makes them appear in the intended order in the finished form.
6. **Google Forms provides the responder link** for the completed form.

## Tools used

- **Make.com** — connects and runs the automation modules.
- **Google Gemini AI** — interprets the event description and generates the structured form specification.
- **Google Forms** — creates the form and its questions.

## Current limitations

File-upload questions, conditional questions, section branching, and special write-in “Other” options are not supported by this version. The generated preflight status, warnings, and assumptions help identify requests that may need attention.
