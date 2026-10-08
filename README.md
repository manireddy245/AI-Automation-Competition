# AI Event-to-Google-Forms Automation

Turn an event description in Google Sheets into a complete, shareable Google Form. The workflow uses Gemini to interpret the description, Make.com to coordinate the steps, and Google Forms to create and populate the form. It then writes the form results back to the tracking sheet.

## Workflow

![Make.com workflow: Google Sheets, Gemini, Google Forms, Iterator, and Router](assets/make-workflow.png)

*The Make.com scenario that reads event rows, generates forms, records form details, and routes each question to the matching Google Forms action.*

1. **Watch for an event description.** Google Sheets — Watch New Rows checks the input sheet for a new row containing an event description.
2. **Generate a form specification.** Gemini 3.5 Flash turns the description into structured form data: a title, description, questions, required settings, answer choices, assumptions, warnings, and preflight information.
3. **Create the form.** Google Forms — Create a Form creates the form using the generated title and description.
4. **Record the result.** Google Sheets update-cell steps write the generated form information to the tracking sheet.
5. **Add the questions.** An Iterator processes the questions array one item at a time. A Router sends each item to the Google Forms module configured for its question type.
6. **Keep the intended question order.** The prompt returns questions in reverse order because each item is inserted at index `0`. The final form therefore displays questions in the intended order.

## Spreadsheet columns

The sheet uses one row per event request:

| Column | Purpose |
| --- | --- |
| Event Description | The organizer's plain-language request; this is the workflow input. |
| Status | Indicates the request's processing state. |
| Form Title | The title generated for the Google Form. |
| Question Count | The number of questions generated for the form. |
| Responder Link | The link people use to open and submit the form. |

Enter a new request in a new row under **Event Description**. The other columns are reserved for the workflow's results.

## Supported question types

- Short text
- Long text / paragraph
- Multiple choice
- Checkboxes
- Dropdown
- Date
- Time

The Router uses a separate Google Forms update route for each supported type. Question titles, help text, required settings, and choice options are mapped from Gemini's generated specification.

## Tools and services

- **Make.com** — runs the scenario, watches the sheet, iterates over questions, and routes each question to the right action.
- **Google Gemini AI (Gemini 3.5 Flash)** — converts the event description into a structured form specification.
- **Google Sheets** — supplies event descriptions and stores the generated form details.
- **Google Forms** — creates the form and its questions, and provides the responder link.

## Current limitations

This version does not create file-upload questions, conditional questions, section branching, or Google's special write-in “Other” option. The Gemini specification includes preflight information so unsupported requests can be identified rather than silently treated as supported.

## Run the demo

1. Authorize the Google Sheets, Gemini, and Google Forms connections in Make.com.
2. Add an event description to a new row in the connected sheet.
3. Run the scenario once, or wait for its configured schedule to check for new rows.
4. Confirm that the tracking columns are filled and open the responder link to review the generated form.

## Project links

- **Live demo:** Add the public demo link here.
- **Demo video:** Add the recording link here.
