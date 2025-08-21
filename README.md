
# Ess-a-Bagel Training — Single File App (Branded)

This ZIP contains a **self-contained HTML file** with your training content pre-filled and styled using your brand guide. It works offline and on any device.

## Files
- `ess-a-bagel-training-single.html` — the entire app (logos embedded in color)
- `README.md` — this guide
- `screenshots/` — desktop, tablet, and mobile previews with sample data

## Quick Start (Beginner)
1. Double-click the HTML file to open in your browser. If it doesn't navigate after registration, try Chrome/Edge/Firefox or run a tiny local server (`python -m http.server`) and open `http://localhost:8000/ess-a-bagel-training-single.html`.
2. Enter your name (and optional cohort code). You will be taken to **Chapters** automatically.
3. Complete lessons, flashcards, and quizzes (pass ≥ 70% to unlock next).

## Share with Trainees
- Host the single file on **any** web server/CDN (Netlify Drop, GitHub Pages, S3, Intranet).
- Share links like: `https://your.host/ess-a-bagel-training-single.html?invite=TeamA-Aug`

## Optional: Cloud Leaderboard (Supabase)
1. Create a project at supabase.com
2. In SQL Editor, run:
```
create table if not exists public.scores (
  id bigserial primary key,
  name text, email text, phone text, cohort text,
  chapter_id text, score_percent int check (score_percent between 0 and 100),
  created_at timestamptz default now()
);
alter table public.scores enable row level security;
drop policy if exists scores_select on public.scores;
drop policy if exists scores_insert on public.scores;
create policy scores_select on public.scores for select using (true);
create policy scores_insert on public.scores for insert with check (true);
```
3. In the HTML near the top, set `SUPABASE_URL` and `SUPABASE_ANON` (or pass via URL `?supabaseUrl=...&supabaseKey=...`).
4. Re-upload the file and test a quiz submit. Your score should appear on the **Leaderboard**.

## Editing Content
- Search within the HTML for `const CHAPTERS =` — it contains your condensed lesson bullets, flashcards, and quizzes per chapter (auto-generated from the manual).
- You can edit/add items directly in that block.

## Branding
- Colors match your guide: Ess-a-Green `#083915`, Artisanal Green `#062B0F`, Sage Green `#A3AB8D`, Sophistic Gray `#E4E3E3`, Cream White `#F6F6F6`, Blushing Bagel `#FFAB7F`.
- Logos are embedded (header, quiz intro, scoreboard, dashboard watermark, footer) in full color.
