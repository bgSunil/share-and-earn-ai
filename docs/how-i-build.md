# How I Build

A short summary of how Share & Earn Lite is built with AI coding tools. This describes the approach. The agent definitions and scripts are not published here.

## The short version

I use Claude Code as my main development tool and put structure around it, so I stay in charge of decisions and the tool does the repetitive work.

## Spec first

Every feature starts as a written spec. A design document covers the product, the data model, and every screen. A short set of engineering rules covers privacy, consent, and how the code is organized. Work is planned against these before anything is built.

## A small team of agents

Specialized agents each handle one job.

- **Plan.** One turns a feature idea into a spec, a plan, and a task list, and stops for my approval.
- **Build.** One implements the plan phase by phase.
- **Review and close.** One reviews the work, writes up what changed, and prepares it for merge.
- **Fix.** One handles bug fixes where the cause is already known.
- **Check.** Others walk through the live staging app as a customer, a merchant, and an admin, and report anything that does not match the design.

I approve plans and review results. The agents do not merge or deploy on their own.

## Guardrails

- A commit is blocked if the build fails.
- Risky git actions such as force pushing, merging, and deploying are blocked unless I do them.
- Tests run in layers. Quick checks run as I edit, a wider set runs between phases, and the full set runs before anything is merged.
- The tests include unit tests, end to end browser tests, and tests for the database security rules.

## My role

I am the product owner and reviewer. I make the product decisions, approve every plan, and check what comes back. I am not claiming to hand-write the code.

## What I learned

- Written specs and hard guardrails matter more than clever prompting.
- Anything important should be enforced by a check, not left to memory.
- A person still needs to read the plan before the work starts.

These are the same ideas behind the Llama features: the AI drafts, and a person decides.
