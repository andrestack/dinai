# App Flow

```mermaid
flowchart TD
  A[Landing / Hero] --> B[Sign Up / Log In (Clerk)]
  B --> C[Questionnaire Wizard]
  C --> C1{Select Industry}
  C1 -->|Trades| D[Trades‑Specific Questions]
  C1 -->|E‑commerce| E[E‑commerce Questions]
  C1 -->|Professional Services| F[Pro‑Services Questions]
  D & E & F --> G[Calculator Widgets (Time × Hourly Rate, etc.)]
  G --> H[Submit Answers]
  H --> I[LLM Analysis — Streaming Function Calls]
  I --> J[Recommendations & Savings Summary]
  J --> K[User Actions]
  K --> K1[Copy to Clipboard]
  K --> K2[Email via Resend]
  K --> K3[Return to Dashboard]
  J --> L[Store Results → DB]
  L --> M[Admin Dashboard]

  subgraph Voice Mode
    C --> V1[Whisper STT → Text]
    J --> V2[TTS Playback]
  end
```

## States & Key Events

| Step | State                | Trigger/Event                          |
| ---- | -------------------- | -------------------------------------- |
| 1    | `unauthenticated`    | User lands on page                     |
| 2    | `authenticating`     | Clerk social/email OAuth               |
| 3    | `in‑survey`          | Wizard mount                           |
| 4    | `survey‑answering`   | Each answer → local `zustand` store    |
| 5    | `survey‑calculating` | Calculator widget emits numeric values |
| 6    | `survey‑submitting`  | User hits                              |

| *Next* on final screen |                                   |                                    |
| ---------------------- | --------------------------------- | ---------------------------------- |
| 7                      | `analysis‑streaming`              | Server action pipes OpenAI stream  |
| 8                      | `results‑ready`                   | All tokens received                |
| 9                      | `results‑shared‑email` / `copied` | Email call success / clipboard API |

## Error / Edge Cases

* **Token expiration:** refresh via Clerk before any API call.
* **OpenAI latency > 10 s:** show skeleton loaders & retry button.
* **Voice permission denied:** fallback to keyboard.

## Admin Flow (condensed)

1. Admin signs in (role = `admin`).
2. Views dashboard: aggregate metrics & individual assessments.
3. Exports CSV and flags low‑quality answers.
4. Adjusts question wording via CMS table (phase 2).
