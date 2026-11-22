---
name: getc-content
description: Produce GETC's daily four value-first Facebook drafts with clean paragraph spacing across education, Japan life, and science/tech/medical categories (Post 4 strictly as a Japanese language lesson from language sub-pages in sources.txt), one 30-second Reels/TikTok video script, scan Japan news for a qualifying optional Post 5, enforce 'ဂျပန်စာ (Romaji - မြန်မာလို)' on first occurrence only while minimizing English, 2-3 informative Burmese Zero-Shadow comments, brief CTAs, Post 1 & 3 plain cross-promotion, and smart topic lifecycle via generate_posts.py, rendering copy-ready blocks directly inline in the chat UI without file links.
---

# GETC Daily Content Production — V1.8

You are running in Kai 9000 on Android with the Debian 12 Linux Sandbox. Use Kai's live web tools and shell tools. Complete the entire workflow autonomously; do not stop to ask the user to copy log lines manually.

## IMMUTABLE CORE FILES GUARDRAIL (DO NOT MODIFY)
- You are **STRICTLY FORBIDDEN** from editing, overwriting, or deleting any core files (`SKILL.md`, `master_prompt_template.md`, `generate_posts.py`, `sources.txt`, `categories.txt`, `README.md`).
- If `generate_posts.py` reports a validation error, fix ONLY your `.getc_batch_YYYY.MM.DD.json` draft file and re-run. Never alter the validator or prompt files.

## Project Paths
- Project root: `/root/GETC/Marketing`
- Master prompt: `/root/GETC/Marketing/master_prompt_template.md`
- Sources directory: `/root/GETC/Marketing/sources.txt`
- Categories list: `/root/GETC/Marketing/categories.txt`
- Source log: `/root/GETC/Marketing/used_sources.txt`
- Topic log: `/root/GETC/Marketing/used_topics.txt`
- News monitoring log: `/root/GETC/Marketing/news_monitoring_log.txt`
- Posts output directory: `/root/GETC/Marketing/FB_Posts/`
- Generator & Validator script: `/root/GETC/Marketing/generate_posts.py`

## Default Daily Run
1. Generate Posts 1–4 every day with clean blank-line paragraph spacing (`\n\n`):
   - **Posts 1–3:** 150–250 words of structured, zero-fluff Burmese educational/practical info researched from deep-dive sub-page articles in `sources.txt`, rotating across both core Japan education/life topics and expanded categories (`Science & Innovation`, `IT & Software Engineering`, `Advanced Tech & Robotics`, `Medical & Healthcare`, `Nuclear & Clean Energy`, `Aerospace & Engineering`, `Business & Economics`, `Environment & Disaster Prevention`, `Pop Culture & Modern Society`), enriched with at least 2 authentic Japanese vocabulary terms per post.
   - **Post 4 (`GETC - Kamayut`):** Strictly a **Daily Short Japanese Language Lesson** (`Japanese Grammar & Vocabulary` or `Daily Japanese` — 80–150 words) researched specifically from the **Japanese language learning sub-pages in `sources.txt`**.
2. Generate one **strictly 30-second** vertical video script (for Facebook Reels & TikTok) based on the strongest post of the day, including 2 vertical (`9:16`) Gemini B-roll image prompts.
3. Perform the mandatory daily Japan news scan. Generate Post 5 ONLY if a genuinely urgent, time-critical policy/visa/deadline update (announced within 24–72 hours) qualifies. Otherwise omit Post 5.
4. Never connect to Facebook or publish/schedule anything automatically.

## Required Execution Sequence

### 1. Read Project Files & Recent Logs
Use `execute_shell_command` to read:
- Full `master_prompt_template.md`, `sources.txt`, `categories.txt`, and `generate_posts.py`.
- Recent logs (to avoid repeating topics or URLs): run `tail -n 120 /root/GETC/Marketing/used_topics.txt`, `tail -n 120 /root/GETC/Marketing/used_sources.txt`, and `tail -n 15 /root/GETC/Marketing/news_monitoring_log.txt` (if they exist).
- Ensure `/root/GETC/Marketing/FB_Posts/` exists. Do not overwrite or delete existing log files.

### 2. Confirm Date & Timezone
Check the current local date/time in `Asia/Yangon` (`+06:30`). Use one consistent `YYYY.MM.DD` date for filenames and `YYYY-MM-DD` for logs. Always include the current year in search queries to prevent outdated results.

### 3. Pre-Flight Log Check & Deep-Dive Source Research
- **Pre-Flight Check (Zero First-Run Errors):** Inspect `used_sources.txt` and `used_topics.txt` BEFORE selecting any topic or URL so you never pick an already-logged URL or overlapping `core_tags`.
- Use `web_search` to find 2–4 currently trending, relevant Burmese/English/Japanese hashtags on Facebook and TikTok for Japan study, JLPT, science/tech, or Japan life. Always pair them with mandatory `#GETC` and `#GakushinEikou` (total 4–6 hashtags per post).
- **Anti-Repetition Rule:** Never select a topic whose core concept (`core_tags`) was already covered in `used_topics.txt` (within 180 days for `STATIC` topics, or within 90 days for `DYNAMIC` policy topics unless an official `.go.jp` source published a newer update date). Never reuse an exact URL from `used_sources.txt`, and respect the 3-day domain cooldown for non-government sites.
- **Mandatory Deep-Dive Reading (NO Guessing from Titles):**
  - Pick specific deep-dive sub-pages from `sources.txt` (for **Post 4**, specifically pick a Japanese language teaching sub-page from `sources.txt`).
  - Navigate to and fetch **specific deep-dive article or lesson sub-page URLs** (NEVER cite bare homepages). Read the full page content and extract concrete facts, rules, or grammar patterns.

### 4. Mandatory Japan News Scan (Post 5 Gate)
Search Japanese, English, and Burmese sources for urgent updates affecting Myanmar students, workers, or residents in Japan announced in the **past 24–72 hours** (or critical deadlines closing within days).
- Keep the boundary strict: routine educational/how-to guides or generic student stories belong in Posts 1–3, NEVER Post 5.
- Open exact source pages; never rely on search snippets alone.
- Cross-check legal/immigration/policy updates across at least two authoritative sources where possible.
- If a qualifying urgent item exists, create Post 5 (for both pages), exclude that topic from Posts 1–4 today, and set `news_monitoring.status` to `POST_CREATED`.
- If none qualifies, omit Post 5 and set `news_monitoring.status` to `NO_QUALIFYING_NEWS`.

### 5. Write Content & 30-Second Video Script
Follow every rule in `master_prompt_template.md`:
- **Clean Paragraph Spacing (Mobile UX):** Always separate Hook, intro, every `📌` point, comment teaser, CTA, cross-promo, and hashtags with explicit blank lines (`\n\n`). Never produce a single dense block of text.
- **Value-First, Zero Bragging (18–35 Youth & Guardians):** Write like a trusted mentor—structured (`📌 ၁။ ...`, `📌 ၂။ ...`), crisp, and memorable so readers want to Like & Share. Never include boastful brochure sections bragging about GETC.
- **Varied Hooks:** Rotate across fact, warning/mistake, relatable scenario, actionable tip, and question hooks. At most 1 post among Posts 1–4 may open with a question hook.
- **Japanese-First Vocabulary & Minimize English:**
  - Replace English terms with authentic Japanese terms (e.g., use `出入国在留管理庁 (Shutsunyūkoku Zairyū Kanrichō - လူဝင်မှုကြီးကြပ်ရေးဌာန)` instead of `Immigration (လူဝင်မှုကြီးကြပ်ရေး)`). Include at least 2 distinct Japanese terms in each of Posts 1–3, and avoid unnecessary English parenthetical translations.
  - On the **first occurrence** of any Japanese term in a post, ALWAYS put Japanese script first: `ဂျပန်စာ (Romaji - မြန်မာလို)` — e.g., `件名 (Kenmei - ခေါင်းစဉ်)`. NEVER put Romaji first (`Keigo (敬語)` is forbidden) and NEVER put English inside the parentheses.
  - On **every subsequent occurrence** of that term in the post or comments, write **ONLY the Japanese script** (`件名`) so readers build visual familiarity with Japanese characters.
- **Comment Teaser + 2–3 Informative Burmese Comments (NO URLs):**
  - End every caption body with a natural teaser inviting readers to check the comments (always spelling `comment` in English).
  - Write **2 to 3 substantial comments** per post strictly in **Burmese** in the exact same informative mentor tone as the post—revealing omitted rules, exceptions, or insider tips from the source article using Japanese-Burmese terminology (no URLs, no empty Messenger-only filler).
- **Brief CTA & Post 1 & 3 Cross-Promotion (Plain URLs Only):**
  - End with a brief, natural 1–2 line CTA inviting readers to inquire/enroll/register at GETC.
  - Include cross-promotion ONLY on **Post 1** (`GETC - Kamayut` + plain URL `[https://www.facebook.com/gakushineikou2](https://www.facebook.com/gakushineikou2)`) and **Post 3** (`GETC - Hledan` + plain URL `[https://www.facebook.com/gakushineikou](https://www.facebook.com/gakushineikou)`). Write plain URLs directly (NEVER `[url](url)` Markdown link brackets).
- **Rich Image Prompts (Pure Japanese + Burmese Overlay Only):** Describe a clear visual scene + **pure Japanese script ONLY** (e.g., `Japanese text '日本語学校'`, NO Romaji/English inside the image text quote) + **pure Burmese title overlay** + single attached GETC school logo corner watermark (`top-left` or `top-right`) blended naturally with the background. Use `1:1` square or `4:5` portrait for Posts 1–4, and `9:16` vertical for the 2 video B-roll prompts.
- **30-Second Video Script:** Write a crisp 30-second Reels/TikTok script (`title`, `hook_0_3s`, `body_3_24s`, `cta_24_30s`) plus two `9:16` B-roll image prompts.

### 6. Build JSON Batch
Write valid UTF-8 JSON (no Markdown fences) to `/root/GETC/Marketing/.getc_batch_YYYY.MM.DD.json` matching this exact schema:

```json
{
  "news_monitoring": {
    "checked_at": "ISO 8601 timestamp with +06:30 timezone",
    "status": "POST_CREATED or NO_QUALIFYING_NEWS",
    "summary": "Scan result and explanation",
    "search_coverage": ["search topics and languages"],
    "sources_checked": [
      {
        "title": "Exact page title",
        "url": "Exact deep-dive page URL",
        "published_or_updated": "YYYY-MM-DD or Date not stated"
      }
    ]
  },
  "video_script": {
    "source_post_number": 1,
    "title": "Video topic title",
    "hook_0_3s": "Scroll-stopping Burmese spoken hook + [On-screen text]",
    "body_3_24s": "3 concise Burmese spoken points + [Visual Cue]",
    "cta_24_30s": "Crisp Burmese closing CTA",
    "broll_image_prompts": [
      "9:16 vertical Gemini image prompt 1",
      "9:16 vertical Gemini image prompt 2"
    ]
  },
  "posts": [
    {
      "post_number": 1,
      "page": "GETC - Hledan (https://www.facebook.com/gakushineikou)",
      "role": "Assigned role",
      "category": "Selected category from categories.txt",
      "topic_type": "STATIC or DYNAMIC",
      "core_tags": ["japan", "standardized-tag-2", "standardized-tag-3"],
      "source_updated_date": "YYYY-MM-DD or Date not stated",
      "title": "Working title",
      "caption": "Multi-paragraph Burmese Facebook caption separated by \\n\\n (varied hook, structured 📌 info on separate lines, >=2 first-occurrence 'ဂျပန်စာ (Romaji - မြန်မာလို)' glosses then Japanese script only, natural 'comment' teaser, brief 1-2 line GETC CTA, full-name plain-URL cross-promo on Post 1 & 3 only, 4-6 hashtags on bottom line)",
      "image_prompt": "1:1 square or 4:5 portrait image prompt (rich scene + pure Japanese script text + pure Burmese title overlay + single attached school logo corner watermark blended with background)",
      "comments": [
        "Comment 1 in Burmese: Substantial omitted detail/rule from source article in the same informative tone (NO URLs)",
        "Comment 2 in Burmese: Additional practical tip/exception from source article (NO URLs)",
        "Comment 3 in Burmese: Further nuance or brief training connection (NO URLs)"
      ],
      "sources": [
        {
          "title": "Exact article/lesson sub-page title",
          "url": "Exact deep-dive sub-page URL from sources.txt",
          "published_or_updated": "YYYY-MM-DD or Date not stated",
          "claim_supported": "Concrete verified facts/grammar extracted from the page"
        }
      ],
      "topic": "Normalized topic",
      "keywords": ["keyword1", "keyword2", "keyword3"],
      "angle": "Distinct angle",
      "audience_need": "Reader need",
      "verification_status": "VERIFIED or NEEDS HUMAN REVIEW or HOLD",
      "verification_checklist": [
        {"item": "Exact check", "status": "Verified or Needs human review or N/A"}
      ]
    }
  ]
}
```

### 7. Validate & Save via `generate_posts.py`
Run:
`python3 /root/GETC/Marketing/generate_posts.py --input /root/GETC/Marketing/.getc_batch_YYYY.MM.DD.json`
*(If a `--date YYYY.MM.DD` override was requested by the user, pass `--date YYYY.MM.DD` to `generate_posts.py` as well).*

If `generate_posts.py` exits with a validation error, fix every listed issue silently in `.getc_batch_YYYY.MM.DD.json` and re-run until `GETC SAVE SUCCESS` appears. Once succeeded, remove the temporary `.getc_batch_YYYY.MM.DD.json` file so the directory stays clean.

### 8. Final Chat Output Format (Direct Inline Text — NEVER File Links)
Read `/root/GETC/Marketing/FB_Posts/YYYY.MM.DD-chat-ready.md` using `cat` in shell and paste its **PART 1: COPY-READY CONTENT** directly inside your final chat response message:
- **CRITICAL ANDROID UI RULE:** NEVER include any clickable markdown file link (`[...](...)`), `file://` URI, file attachment card, or full `/root/.../YYYY.MM.DD-chat-ready.md` path in your final reply (which triggers Android's "Open with..." external app chooser dialog).
- Render all Posts 1–4/5 captions, image prompts, 2–3 Burmese comments per post, and the 30-second Reels/TikTok script + B-roll prompts directly inside your response using individual ```text fenced code blocks so the user can tap-to-copy immediately inside the chat UI, followed by a concise plain-text summary of **PART 2: AUDIT & NEWS SCAN STATUS**.
