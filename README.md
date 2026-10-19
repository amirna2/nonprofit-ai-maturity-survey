# Nonprofit AI Maturity Survey

A 19-question self-assessment that helps a nonprofit describe where it stands with AI and produces an explained maturity report with practical next steps.

**Live:** https://amirna2.github.io/nonprofit-ai-maturity-survey/

The whole thing is one static page (`index.html`). There is no build step, no dependencies, no backend, and no analytics. Answers never leave the browser tab.

## What it does

The survey takes about 10 minutes. It walks through five sections:

| Section | Questions | Scored? |
|---|---|---|
| About your organization | 1–3 (budget, focus area, paid staff) | No |
| Strategy and Governance | 4–7 | Yes |
| Data and Infrastructure | 8–10 (Q9, data tools in use, is informational) | Q8, Q10 |
| Culture and Literacy | 11–14 | Yes |
| Application and Impact | 15–19 (Q15 uses, Q16 adoption stage, Q19 main barrier) | Q17, Q18 |

Each scored question offers four practice statements that describe increasing maturity, plus **Not sure**. Respondents are asked to pick the last statement that fully describes established practice, and to choose Not sure rather than guess.

The report shows:

- An assessed maturity level: **Early**, **Developing**, **Established**, or **Advanced**.
- A short explanation of why, including the lowest-scoring section.
- How the scored practices compare with the adoption stage the respondent described (no use, informal use, piloting, integrated use).
- A per-section table with score, band, and the lowest reported practice.
- Up to three priority next steps, plus advice tied to the main barrier if one was given.
- Up to three questions to use in a follow-up conversation.

The report can be printed or saved as PDF from the browser, or downloaded as a standalone HTML file.

## How scoring works

- Each scored answer maps to a score of 1–4. **Not sure** is treated as unknown, not as a low score.
- A section score is the mean of its answered questions. A four-question section needs at least three answers to be scored, a two-question section needs both.
- The overall score is the mean of the four section scores. Every section has equal weight.
- Bands: below 1.75 is Early, below 2.5 is Developing, below 3.25 is Established, otherwise Advanced.
- If any scored question is Not sure, the result is **provisional**. The page shows the range of levels that could result once the unknowns are confirmed. That range is not a confidence interval.
- The result is also marked provisional when answers contradict each other, for example reporting no AI use alongside measured results. The report lists what to clarify.
- Next steps are chosen from the practices scored below 4. Responsible-use rules, accountability, security, and output checking come first, then strategy and operational measurement, then the rest.

## Running it locally

Open `index.html` in a browser. If you prefer a local server:

```
python3 -m http.server 8000
```

Then visit http://localhost:8000/.

## Deployment

GitHub Pages serves the root of the `main` branch. Pushing to `main` publishes the change.

## Agent integration

If the browser exposes the WebMCP `document.modelContext` API, the page registers three tools so an AI agent can drive the survey on the respondent's behalf:

- `get_survey_state` reads the questions, current answers, and visible section.
- `set_survey_answers` sets one or more answers and updates the form.
- `generate_maturity_report` generates the report once all 19 questions are answered.

Browsers without that API ignore this and the page works as a normal form.

## Status

This is a pilot framework. The levels describe the maturity of the practices a respondent reports. They are not a benchmark against other nonprofits and have not been validated as one. Treat the result as a starting point for a conversation, not a verdict.

## License

This work is licensed under the [Creative Commons Attribution 4.0 International License](LICENSE) (CC BY 4.0). You may share and adapt it, including commercially, as long as you give appropriate credit.
