# SNAP Department Feedback & Improvement Survey

**How are we doing?** is an anonymous internal survey for SNAP Insurance Service, LLC. Employees share what is working, what is getting in the way, and how leadership can better support them.

**Live survey:** https://piperintech.github.io/snap-feedback/

## What it asks

Six required 1–5 ratings (1 = Very dissatisfied, 5 = Very satisfied), each with an optional comment, plus two optional open-ended questions.

| # | Area | Rating question (required) | Follow-up (optional) |
|---|------|----------------------------|----------------------|
| 1 | Overall satisfaction | Overall, how satisfied are you with your experience working for the company? | What contributes most to your satisfaction? |
| 2 | Leadership | How satisfied are you with your department's communication and leadership? | What could be improved? |
| 3 | Team effectiveness | How satisfied are you with the level of teamwork and accountability in your department? | What would make your team stronger? |
| 4 | Resources & support | How satisfied are you with the resources and support you need to be productive and effective in your position? | What would help you be more successful? |
| 5 | Recognition | How satisfied are you with the recognition and appreciation you receive? | How could we show more appreciation? |
| 6 | Employee voice | How satisfied are you with the opportunities to share your ideas and concerns with leadership? | What would encourage more open communication? |
| 7 | Open-ended (optional) | What is one thing we do well that you would like to see continue? | |
| 8 | Open-ended (optional) | What is one thing we could change to make this a better place to work? | |

Questions cover four focus areas: **People** (management, leadership, teamwork, accountability), **Processes** (inefficiencies, unnecessary steps, communication breakdowns), **Resources** (staffing, training, technology, workload), and **Culture** (recognition, appreciation, trust, employee involvement). The ratings give a quantitative baseline to compare against future surveys.

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
  "surveyId": "how-are-we-doing-v2",
  "submittedAt": "2026-11-13T15:00:00.000Z",
  "overallRating": 4,      "overallComment": "",
  "leadershipRating": 4,   "leadershipComment": "",
  "teamworkRating": 4,     "teamworkComment": "",
  "resourcesRating": 4,    "resourcesComment": "",
  "recognitionRating": 4,  "recognitionComment": "",
  "voiceRating": 4,        "voiceComment": "",
  "continueDoing": "",
  "oneChange": ""
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
