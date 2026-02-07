Qualtrics integration and data mapping

This file documents how Twine choices are sent to Qualtrics via postMessage and how they are stored as Embedded Data for export.

Payload (sent from Twine iframe)
- Each choice is posted with the following JSON payload to the parent window via window.postMessage:
  - type: 'twine-click'
  - choice: string (link text shown to user)
  - passage: string|null (passage name if available)
  - time: ISO timestamp string when the click occurred

Qualtrics Embedded Data mapping (the recommended fields saved by the listener)
- twine_click_count: integer counter of choices recorded (1-based)
- twine_click_1, twine_click_2, ...: each choice's displayed text saved in order
- twine_click_json: full JSON array of recorded clicks with objects { choice, passage, time }

Exporting to CSV
- In Qualtrics Data & Analysis, use the Export Data function (CSV/TSV) to include Embedded Data fields.
- The fields twine_click_1..N will appear as individual columns; twine_click_json will appear as a single string column containing the JSON array.
- If you need a column per click but do not know max clicks, consider using Qualtrics to create a fixed number of embedded-data fields (e.g., twine_click_1 to twine_click_10) before the survey starts.

Notes
- The Qualtrics listener (provided in project docs) stores each click into these Embedded Data fields; adjust field names if your survey requires different naming.
- For security, restrict the message origin check in the Qualtrics listener to your Twine host origin in production.
