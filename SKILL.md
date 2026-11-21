---
name: getc-content
description: Produce GETC's daily four Facebook drafts, one daily Reels/TikTok video script, scan Japan news for a qualifying optional Post 5, enforce anti-shadow comments, mandatory cross-promotion, and smart topic lifecycle via generate_posts.py, and display copy-ready blocks.
---

# GETC Daily Content Production — V1.2

You are running in Kai 9000 on Android with the Debian 12 Linux Sandbox. Use Kai's live web tools and shell tools. Complete the entire workflow autonomously; do not stop to ask the user to copy log lines manually.

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
1. Generate Posts 1–4 every day (150–250 words each for Posts 1–3, 80–150 words for Post 4, strict Facebook safety compliance).
2. Generate one 30–45 second vertical video script (for Facebook Reels & TikTok) based on the strongest post of the day, including 2 vertical (9:16) Gemini B-roll image prompts.
3. Perform the mandatory daily Japan news scan. Generate Post 5 ONLY if a genuinely urgent, time-critical update (announced within 24–72 hours) qualifies. Otherwise explicitly skip Post 5.
4. Never connect to Facebook or publish/schedule anything automatically.

## Required Execution Sequence

### 1. Read Project Files & Recent Logs
Use `execute_shell_command` to read:
- Full `master_prompt_template.md`, `sources.txt`, `categories.txt`, and `generate_posts.py`.
- Recent logs (to avoid repeating topics or URLs): run `tail -n 120 /root/GETC/Marketing/used_topics.txt`, `tail -n 120 /root/GETC/Marketing/used_sources.txt`, and `tail -n 15 /root/GETC/Marketing/news_monitoring_log.txt` (if they exist).
- Ensure `/root/GETC/Marketing/FB_Posts/` exists. Do not overwrite or delete existing log files.

### 2. Confirm Date & Timezone
Check the current local date/time in `Asia/Yangon` (or the timezone configured in `generate_posts.py`). Use one consistent `YYYY.MM.DD` date for filenames and `YYYY-MM-DD` for logs. Always include the current year in search queries to prevent outdated results.

### 3. Dynamic Hashtag Research & Smart Topic Planning
- Use `web_search` to find 2–4 currently trending, relevant Burmese/English/Japanese hashtags on Facebook and TikTok for Japan study, JLPT, or Japan life. Always pair them with mandatory `#GETC` and `#GakushinEikou` (total 4–6 hashtags per post).
- Review the last 120 lines of `used_topics.txt` and `used_sources.txt` BEFORE researching articles.
- **Anti-Repetition Rule:** Never select a topic whose core concept (`core_tags`) was already covered in `used_topics.txt` (within 180 days for `STATIC` topics, or within 90 days for `DYNAMIC` policy topics unless an official source published a newer update date). Never reuse an exact URL from `used_sources.txt`, and respect the 3-day domain cooldown for non-government sites.
- Drill into fresh, specific sub-topics from `sources.txt` rather than surface-level homepage guides.

### 4. Mandatory Japan News Scan (Post 5 Gate)
Search Japanese, English, and Burmese sources for urgent updates affecting Myanmar students, workers, or residents in Japan announced in the **past 24–72 hours** (or critical deadlines closing within days).
- Keep the boundary strict: routine educational/how-to guides belong in Posts 1–3, NOT Post 5.
- Open exact source pages; never rely on search snippets alone.
- Cross-check legal/immigration/policy updates across at least two authoritative sources where possible.
- If a qualifying urgent item exists, create Post 5 (for both pages), exclude that topic from Posts 1–4 today, and set `news_monitoring.status` to `POST_CREATED`.
- If none qualifies, omit Post 5 and set `news_monitoring.status` to `NO_QUALIFYING_NEWS`.

### 5. Write Content & Video Script
Follow every rule in `master_prompt_template.md`:
- **FB Safety Shield:** No external website URLs inside the post caption (put official source URLs inside Comment 1). No banned promise words, no Facebook polls, no "မမတို့", and always spell "comment" in English.
- **Mandatory Bidirectional Cross-Promotion:**
  - Posts 1 & 2 (`GETC - Hledan`) MUST include a natural cross-promotion link to `https://www.facebook.com/gakushineikou2`.
  - Posts 3 & 4 (`GETC - Kamayut`) MUST include a natural cross-promotion link to `https://www.facebook.com/gakushineikou`.
- **Zero-Shadow Comments (Information Gap):** Hold back 1–2 crucial exceptions, edge cases, or insider tips from the main caption and reveal them in Comment 2. NEVER repeat or paraphrase the main caption inside the comments.
- **Synthesized Burmese & Japanese Format:** Never translate a web article line-by-line. Always write Japanese as `Japanese Script (Romaji) — Burmese meaning`.
- **Image Prompts (No English Text + Logo Watermark):** Any text on the image MUST be in Japanese script and Burmese only (no English text unless strictly unavoidable). Instruct the AI to place the attached GETC school logo cleanly in the top-left or top-right corner (12–15% width) as a subtle, semi-transparent watermark blended naturally with the background without distorting the logo.
- **Video Script:** Create one 30–45 second Reels/TikTok script (Hook, 3 Quick Points, CTA) plus two 9:16 B-roll image prompts (following the exact same Japanese/Burmese-only text and logo watermark rules).

### 6. Build JSON Batch
Write valid UTF-8 JSON (no Markdown fences) to `/root/GETC/Marketing/.getc_batch_YYYY.MM.DD.json` matching this exact schema:

```json
{
  "news_monitoring": {
    "checked_at": "ISO 8601 timestamp with timezone",
    "status": "POST_CREATED or NO_QUALIFYING_NEWS",
    "summary": "Scan result and explanation",
    "search_coverage": ["search topics and languages"],
    "sources_checked": [
      {
        "title": "Exact page title",
        "url": "Exact page URL",
        "published_or_updated": "YYYY-MM-DD or Date not stated"
      }
    ]
  },
  "video_script": {
    "source_post_number": 1,
    "title": "Video topic title",
    "hook_0_3s": "Scroll-stopping Burmese spoken hook + [On-screen text]",
    "body_3_30s": "3 concise spoken Burmese points with visual cues",
    "cta_30_45s": "Closing Burmese CTA",
    "broll_image_prompts": [
      "9:16 vertical Gemini image prompt 1",
      "9:16 vertical Gemini image prompt 2"
    ]
  },
  "posts": [
    {
      "post_number": 1,
      "page": "GETC - Hledan ([https://www.facebook.com/gakushineikou](https://www.facebook.com/gakushineikou))",
      "role": "Assigned role",
      "category": "Selected category from categories.txt",
      "topic_type": "STATIC or DYNAMIC",
      "core_tags": ["japan", "standardized-tag-2", "standardized-tag-3"],
      "source_updated_date": "YYYY-MM-DD or Date not stated",
      "title": "Working title",
      "caption": "Complete Burmese Facebook caption (no external URLs, includes mandatory cross-promotion link + #GETC #GakushinEikou + 2-4 trending hashtags)",
      "image_prompt": "Complete image prompt (Japanese/Burmese text only + attached school logo corner watermark blending)",
      "comments": [
        "Comment 1: Official source title, date, exact URL + 1 specific fact omitted from caption",
        "Comment 2: Crucial exception, edge case, or insider tip NOT mentioned in the caption (Zero-Shadow)"
      ],
      "sources": [
        {
          "title": "Exact source title",
          "url": "Exact source sub-page URL",
          "published_or_updated": "YYYY-MM-DD or Date not stated",
          "claim_supported": "Specific supported claim"
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
