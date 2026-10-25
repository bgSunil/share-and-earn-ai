# Architecture

A high level view of how the AI features fit into Share & Earn Lite. Status: planned for the hackathon build.

## Overview

The app is a React and TypeScript web app on Firebase. The AI layer is one server function plus a thin service in the app. The model is called only from the server.

```
  App (React)
     |  user taps "Help me write" or "Draft reply"
     v
  AI service (in app)          small module, no model code in screens
     |
     v
  Cloud Function (server)
     |  1. require a signed in user
     |  2. enforce a daily limit per user
     |  3. build the prompt from an allowed list of fields
     |  4. call the Meta Model API using a managed secret
     |  5. validate and clean the response
     v
  Drafts returned to the app
     |
     v
  User reads, edits, and sends (through WhatsApp)
```

If any step fails, the app shows its normal behavior with no AI help.

## Feature 1: Share composer

1. After a customer rates a visit highly and chooses to recommend the place, they can tap "Help me write".
2. The app sends the business name and type, their rating, tags, note, and a language choice.
3. The model returns three short drafts with different tones.
4. The customer picks one and edits it. The app fills in the friend's name on the device.
5. The app adds the reward disclosure and the referral link, then shows the exact final message in a preview.
6. The customer taps Send, and WhatsApp opens to that friend.

The AI step happens before the Send tap, in its own button. This keeps Send immediate, which matters because WhatsApp must open directly from a tap.

## Feature 2: Feedback assistant

1. A business owner opens a private feedback item from a low rating.
2. The app asks for a reply draft, sending only the rating, tags, written note, and age of the item.
3. The model returns a kind, specific reply that makes no promises about refunds or discounts.
4. The owner edits the draft and sends it through the existing contact flow. The server looks up the customer's contact details itself, so they never reach the model or the owner's browser.

Grouping feedback into common problems is a possible addition.

## Feature 3: Setup assistant (stretch)

Drafts a short business description, reward ideas, and a staff script from one sentence about the business. Descriptions pass the same content checks as ones written by hand. Reward ideas are advice only and never create a reward by themselves.

## Design choices

- **One server function, one service in the app.** Screens never talk to the model.
- **Allowed list of fields.** Each feature defines what it may send.
- **Structured output.** Responses are checked against an expected shape before use.
- **Code owns the legal text.** The disclosure and the link are added after the draft, not written by the model.
- **Graceful fallback.** The product works the same without AI.

See [privacy-and-safety.md](privacy-and-safety.md) for the data rules.
