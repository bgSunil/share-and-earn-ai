# Share & Earn AI

AI features for **Share & Earn Lite**, a referral platform that helps neighbourhood businesses grow through trusted, personal word of mouth. This repository holds the Meta AI integration built for the Meta Global AI Developer Hackathon (Theme 1, Build for your world).

The main product is a private codebase. This repo shows the AI layer, its prompts, its privacy design, and how it plugs in.

> Status: planned. The AI features are designed but not yet built. Sections marked *planned* describe the intended build.

## The product in one minute

A customer scans a QR code at a business, rates the visit, and can recommend the place to named friends on WhatsApp. Never a broadcast, never an open link. When the friend visits, both people earn a reward. Customers who give a low rating send private feedback to the owner instead.

Stack: React, TypeScript, Firebase (Firestore, Cloud Functions on Node 22), WhatsApp deep links.

## What Meta's models add

### 1. Say it in your own words (planned)
Many happy customers want to recommend a place but freeze at the blank message box. One tap drafts three short, personal messages from what the customer said about their visit, in their chosen language. They pick one, edit it, and send it themselves.

### 2. Feedback assistant (planned)
Owners of small shops rarely have time or support staff to answer unhappy customers. The assistant drafts a kind, specific reply for each private feedback item, which the owner edits and sends. Grouping feedback into common problems is a planned bonus.

## Design principles

- **A person always reviews and sends.** Nothing goes out automatically.
- **Minimal data to the model.** No phone numbers, user IDs, or friends' names. A friend's name is filled in on the device after the draft comes back.
- **Legal text stays in code.** The reward disclosure and the referral link are added by the app, never written by the model.
- **Server side only.** The model is called from a Cloud Function. The API key never reaches the browser.
- **Fails safe.** If the model is slow or unavailable, the app behaves exactly as it did before.
- **Checked output.** Model responses are validated against a schema, with links and phone like patterns rejected.

## Documentation

- [Architecture](docs/architecture.md) shows how the AI layer fits into the app.
- [Privacy and safety](docs/privacy-and-safety.md) lists what goes to the model, what never does, and the checks on its output.

More will be added as the features are built.

## About

Built by Sunil Balabadra in Bothell, Washington. Share & Earn Lite is a bootstrapped, early stage product, currently in MVP and not yet piloted with real merchants.
