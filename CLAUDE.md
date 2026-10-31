# CLAUDE.md --- SYNC BUILD

This file contains mandatory project instructions. Read
`docs/MVP_SPEC.md` before implementing features. The MVP specification
is the product and technical source of truth.

## Product objective

Build Sync Build: a student collaboration and project-execution
platform. A student describes an idea; Gemma 4 turns it into a
structured brief, identifies needed roles/skills, and generates
actionable tasks. The app recommends collaborators from stored profile
data, creates a workspace, and provides an advisory review of submitted
work.

The product is not a job board, job scraper, general chatbot, or
autonomous code-deployment agent.

## Mandatory behavior

1.  Follow `docs/MVP_SPEC.md`. Do not invent features, requirements,
    integrations, or product decisions.
2.  Build the smallest complete end-to-end demo. Four-hour scope is
    strict.
3.  Do not add paid AI APIs or other AI providers. Gemma 4 is the only
    model.
4.  Do not add job-board integrations, scraping, LinkedIn/Indeed
    integrations, email/SMS, GitHub OAuth, payments, or unnecessary
    services.
5.  Use the selected Gemma 4 model through the configured local
    inference runtime. Verify the actual model tag and connectivity; do
    not guess.
6.  Never fake AI output. If Gemma is unavailable, show a clear error or
    an explicitly labeled demo fixture. Never present a fixture as live
    model output.
7.  Treat all model output as untrusted. Parse and validate it with
    schemas before use.
8.  Never let model output execute arbitrary SQL, shell commands,
    JavaScript, filesystem access, or arbitrary URLs.
9.  The model may propose structured content. Application code validates
    and performs actions.
10. Do not automatically invite real people, accept submissions, or make
    consequential changes. Require explicit user action.
11. Collaborator matching must be calculated in application code from
    actual profile fields. Do not invent candidates, skills,
    availability, personality, reliability, or compatibility.
12. AI submission review is advisory. It must never automatically mark
    work accepted.
13. Label fictional profiles as demo profiles and AI estimates/reviews
    as AI-generated or advisory.
14. Never claim that the model browsed, researched, verified, contacted,
    tested, or executed something unless the application actually did so
    and has evidence.
15. Do not store or display hidden chain-of-thought. Provide concise
    explanations and evidence only.

## Anti-hallucination rules

-   Use only supplied user/project/profile/task data for each AI
    operation.
-   Missing information must be represented as unknown, an assumption,
    or an open question.
-   Do not invent statistics, citations, market research, competitors,
    external facts, or user demand.
-   Delimit user-provided content and treat it as data, not
    instructions.
-   Keep system instructions separate from user content.
-   Require JSON outputs matching the schemas in `docs/MVP_SPEC.md`.
-   Validate required keys, types, allowed enum values, array lengths,
    and relationships.
-   If JSON is invalid, retry at most once for formatting correction. If
    still invalid, show an error; do not silently fabricate missing
    fields.
-   For task review, compare each original acceptance criterion exactly
    once. Mark insufficient evidence as unclear.
-   The user, not the model, decides whether submitted work is accepted.

## Technical constraints

-   Next.js App Router + TypeScript.
-   Tailwind CSS; shadcn/ui if useful.
-   Supabase for persistence/auth if it does not jeopardize the core
    demo.
-   Gemma 4 via a configured local inference runtime such as Ollama,
    only after verifying support for the chosen model.
-   Keep model calls server-side.
-   Use environment variables. Never expose service-role keys to the
    browser.
-   No unnecessary backend service, Redis, multi-agent framework, or
    orchestration framework.
-   Prefer simple, readable code and a small dependency set.
-   Do not create abstractions before they are needed.

## Working process

Before coding: 1. Inspect the existing repository and package manager.
2. Read `docs/MVP_SPEC.md`. 3. Report the current structure and any
blocking conflicts with the spec. 4. Verify Gemma 4 connectivity early.
Do not build around an unverified model tag. 5. If a required decision
is missing or a change would violate the spec, ask the user instead of
guessing.

While coding: - Implement one vertical slice at a time. - Run type
checks and relevant tests after meaningful changes. - Keep existing
working code unless there is a clear reason to change it. - Do not
rewrite the whole project just to impose a preferred architecture. - Do
not install a package if native platform functionality or an existing
dependency is sufficient. - Keep `.env.local`, secrets, and credentials
out of Git.

Before declaring completion: - Run the app and test the main flow. -
Test Gemma unavailable and invalid JSON states. - Test the project
creation confirmation step. - Test deterministic collaborator
matching. - Test submission review and explicit user acceptance. -
Report what works, what is incomplete, commands run, and any
assumptions. - Never claim a test passed if it was not run.

## Required main demo

1.  Enter a student project idea.
2.  Gemma generates a structured project brief.
3.  User edits/reviews and confirms it.
4.  App recommends fictional demo collaborators based on deterministic
    skill overlap.
5.  User selects collaborators.
6.  App creates a workspace and tasks.
7.  User submits text for a task.
8.  Gemma reviews the submission against the exact acceptance criteria.
9.  User explicitly accepts or requests changes.

## Scope protection

Do not add internships, job scraping, external application flows,
messaging integrations, GitHub integration, code execution,
notifications, or complex social features in this MVP. These may be
future roadmap items, not current requirements.

If a feature is not required for the main demo, leave it out unless the
user explicitly approves it.
