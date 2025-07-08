# 50‑Step Implementation Plan

## Phase 0 — Project Setup

1. Initialize Git repository with **Next.js 14 (App Router)** and TypeScript template.
2. Configure **ESLint**, **Prettier**, and **Husky** pre‑commit hooks.
3. Add **Tailwind CSS** and set up shadcn/ui components.
4. Create **Vercel** project; add Preview & Production environments.
5. Define runtime environment variable schema (e.g., `env.mjs`).
6. Set up **GitHub Actions** CI: lint, type‑check, test, and build.

## Phase 1 — Auth & Database Foundation

7. Install and configure **Clerk** SDK; add `<ClerkProvider>` and auth middleware.
8. Implement protected API and route groups (`/dashboard`, `/api/protected`).
9. Add **Prisma** ORM & **Data Proxy**; generate initial schema.
10. Provision **Vercel Postgres** database; store connection string in secrets.
11. Create entities: `User`, `Question`, `Response`, `Recommendation`.
12. Write seed script for default questions (with industry tags).
13. Run first migration and verify schema in Vercel UI.

## Phase 2 — Questionnaire Engine

14. Scaffold wizard UI with **App Router** pages and progress bar.
15. Implement *Industry* pre‑question and dynamic branching helper.
16. Build **Likert/MCQ** components with shadcn/ui `<RadioGroup>`.
17. Create **Calculator** component (hours × wage × frequency).
18. Persist draft responses in **local storage** for auto‑save/offline.
19. Add Zod schema validation for each question type.

## Phase 3 — LLM Integration

20. Define **OpenAI Assistant** with function calling for calculations.
21. Create server action `analyzeResponses()` using **streaming** mode.
22. Serialize user answers + calc inputs into structured JSON.
23. Parse streamed `function_call` chunks and update UI in real time.
24. Persist `Recommendation` rows in Postgres.

## Phase 4 — Voice Input/Output

25. Integrate **Whisper** STT endpoint via edge function.
26. Build mic button with waveform animation (framer‑motion).
27. Implement fallback text input when mic unavailable.
28. Add **OpenAI TTS** endpoint; cache mp3 in KV store.
29. Add speaker icon for playback on question and results screens.

## Phase 5 — Results & Sharing

30. Design results page with recommendation cards & savings summary.
31. Implement **copy‑to‑clipboard** for summary text.
32. Add Resend email endpoint and React email template.
33. Trigger email on button click; show toast on success/error.
34. Log email events back to Postgres (`EmailLog`).

## Phase 6 — Admin & Analytics

35. Build `/admin` dashboard secured by Clerk role = `admin`.
36. Display aggregated metrics: avg. time saved, top 5 recs.
37. Add **CSV export** using Next.js `export` route.
38. Install **PostHog**; track questionnaire drop‑off and completion.
39. Enable **Vercel Analytics** for performance monitoring.

## Phase 7 — Testing & QA

40. Write **Vitest** unit tests for utility functions & Zod schemas.
41. Create **Playwright** e2e tests covering full assessment flow.
42. Conduct accessibility audit with **axe‑core** and Lighthouse.
43. Run load test on LLM analysis endpoint using **k6**.
44. Fix any performance or accessibility issues (>90 scores).

## Phase 8 — Deployment & Monitoring

45. Configure **Vercel** preview URLs via GitHub PR comments.
46. Add **Sentry** for error tracking (frontend + API).
47. Set up CRON job to prune old drafts and audio files.
48. Enable **Edge Config** for runtime feature flags.

## Phase 9 — Launch

49. Roll out **beta** to select SMBs; collect feedback via in‑app NPS.
50. Iterate on feedback, then run full marketing launch with blog, email sequence, and social promo.
