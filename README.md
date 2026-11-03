# SNAP Department Feedback & Improvement Survey

**How are we doing?** is an anonymous internal survey for SNAP Insurance Service, LLC. Employees share what is working, what is getting in the way, and how leadership can better support them.

**Live survey:** https://piperintech.github.io/snap-feedback/

## What it asks

| # | Question | Type |
|---|----------|------|
| 1 | Overall, how satisfied are you working in this department? | Rating 1–5 (required) |
| 2 | What is one thing the department is doing well that you'd like to see more of? | Open text (required) |
| 3 | What is something the department does that we could do less of? | Open text (required) |
| 4 | What gets in the way of you being as productive as possible? | Open text (required) |
| 5 | Do you feel you have the support you need to succeed in your role? + What would make you feel more supported and valued? | Rating 1–5 + open text (both required) |
| 6 | What one change would make the biggest difference in building a stronger, more accountable team? | Open text (required) |
| 7 | How can leadership better support you? | Open text (required) |
| – | Anything else you'd like to share? | Open text (optional extra) |

## How it works

```
index.html  ──POST JSON──▶  Power Automate (HTTP trigger)  ──▶  Send an email (V2)  ──▶  Response 200
```

1. The employee fills out the form and clicks **Submit feedback**.
2. The page sends the answers as JSON to a Power Automate flow (*When an HTTP request is received*).
3. The flow emails a formatted question-and-answer summary to the configured recipient.
4. The flow returns `200`, and the page shows the thank-you screen.

## Anonymity

- No name, email, or login is collected.
- The flow trigger is set to **Anyone**, so no user identity is passed.
- Emails are sent from the flow owner's account, not the respondent's.

## Payload

```json
{
  "surveyId": "how-are-we-doing",
  "submittedAt": "2026-11-03T15:00:00.000Z",
  "satisfaction": 4,
  "doingWell": "",
  "doLess": "",
  "blockers": "",
  "supportRating": 3,
  "supportedValued": "",
  "biggestChange": "",
  "leadership": "",
  "anythingElse": ""
}
```

## Updating

- **Flow URL:** edit `FLOW_URL` near the top of the `<script>` in `index.html`.
- **Questions:** edit the question blocks in `index.html`. If you add or rename a field, update the payload in the script, the trigger schema, and the email body in Power Automate.
- **Logo:** embedded as base64 in the header. Height is fixed and width is auto, so the aspect ratio stays locked.

## Design

Built on the SNAP / CLADIS design system: navy `#051c2b`, gray `#f5f5f5`, Arsenal headings, Inter body text.

## Troubleshooting

| Symptom | Fix |
|---|---|
| Red error banner, but the flow ran | Add a **Response** action (status 200) with header `Access-Control-Allow-Origin: *` |
| Flow never runs | Check that `FLOW_URL` includes the full `&sp=…&sv=1.0&sig=…` part |
| Spam submissions | Regenerate the trigger URL in Power Automate and update `FLOW_URL` |

---
Built by Manuela Gonzalez Piper, Project Manager, SNAP Insurance Service, LLC.
