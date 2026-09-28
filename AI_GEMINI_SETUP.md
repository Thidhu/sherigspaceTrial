# SherigSpace v15 AI Teaching Tools

v15 adds a teacher-only AI Teaching Assistant using the Gemini Developer API through a Supabase Edge Function.

## What is included

- Question Generator
- Competency-Based Question Generator
- Lesson Plan Generator
- Worksheet Generator
- Classroom Activity Generator
- Rubric Generator
- Simplify Explanation
- Save generated questions directly to the existing Question Bank
- 20 AI generations per teacher per rolling 24 hours by default
- Gemini API key stays server-side in Supabase Edge Function secrets

## Important: the website does NOT contain the Gemini API key

Never paste `GEMINI_API_KEY` into `teacher.html`, `student.html`, `config.js`, GitHub, or any browser JavaScript file.

## Setup

### 1. Get a Gemini API key

Create an API key in Google AI Studio. Use the Gemini API free tier if your account/model is eligible.

### 2. Create the usage table

Run:

`AI_GEMINI_SETUP.sql`

once in Supabase SQL Editor.

### 3. Deploy the Edge Function

In Supabase Dashboard:

1. Open your project.
2. Open **Edge Functions**.
3. Choose **Deploy a new function → Via Editor**.
4. Create a function named:
   `ai-teacher-assistant`
5. Paste the complete contents of:
   `supabase/functions/ai-teacher-assistant/index.ts`
6. Deploy the function.

Supabase also supports deploying Edge Functions with the CLI.

### 4. Add the Gemini secret

In Supabase Dashboard, open the Edge Function secrets area and add:

`GEMINI_API_KEY` = your Gemini API key

Optional:

`GEMINI_MODEL` = `gemini-3.7-flash`

`AI_DAILY_LIMIT` = `20`

Do not put these secrets in the website repository.

### 5. Replace teacher.html

Use the v15 `teacher.html` from this package.

Keep your existing working `config.js`, `theme.js`, `drive-upload.js`, `student.html`, `admin.html`, `index.html`, `assignment-utils.js`, `assignment-interactive.js`, and `interactive-video.js` unless you intentionally move to a newer consolidated version.

## How to test

Teacher Dashboard → **AI Teaching Tools** → choose a class → choose a tool → enter subject/topic → **Generate with AI**.

For question generation, review each question and use **Save to Question Bank**.

## Free tier note

Google's Gemini API pricing page currently lists a free tier for several Gemini models, but free-tier rate limits and model availability can change. Free does not mean unlimited.

## Security note

The Edge Function checks that the caller is authenticated and owns at least one SherigSpace class before calling Gemini. It also keeps a server-side rolling usage count. It does not store the prompts or generated teaching content in `ai_usage`.
