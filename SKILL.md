---
name: getc-content
description: Produce GETC's daily four Facebook drafts, one daily Reels/TikTok video script, scan Japan news for a qualifying optional Post 5, verify dates and sources, save files and logs via generate_posts.py, and show every draft in copy-ready code blocks.
---

# GETC Daily Content Production — V1.1

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
3. Perform the mandatory daily Japan news scan. Generate Post 5 only if a genuinely important, current, and verified update qualifies (intended for both GETC pages). Otherwise explicitly skip Post 5.
4. Never connect to Facebook or publish/schedule anything automatically.

## Required Execution Sequence

### 1. Read Project Files & Recent Logs
Use `execute_shell_command` to read:
- Full `master_prompt_template.md`, `sources.txt`, `categories.txt`, and `generate_posts.py`.
- Recent logs only (to prevent context window bloat): run `tail -n 80 /root/GETC/Marketing/used_topics.txt`, `tail -n 80 /root/GETC/Marketing/used_sources.txt`, and `tail -n 15 /root/GETC/Marketing/news_monitoring_log.txt` (if they exist).
- Ensure `/root/GETC/Marketing/FB_Posts/` exists. Do not overwrite or delete existing log files.

### 2. Confirm Date & Timezone
Check the current local date/time in `Asia/Yangon` (or the timezone configured in `generate_posts.py`). Use one consistent `YYYY.MM.DD` date for filenames and `YYYY-MM-DD` for logs. Use the current year in all search queries to prevent outdated results.

### 3. Dynamic Hashtag Research & Topic Planning
- Use `web_search` to find 2–4 currently trending, relevant Burmese/English/Japanese hashtags on Facebook and TikTok for Japan study, JLPT, or Japan life. Always pair them with mandatory `#GETC` and `#GakushinEikou` (total 4–6 hashtags per post).
- Plan Posts 1–4 together, assigning distinct categories from `categories.txt`.
- Check recent topics, core keywords, and domains in `used_topics.txt` and `used_sources.txt`. Do not repeat recent concepts, angles, or non-government website domains used within the last 3 days.

### 4. Mandatory Japan News Scan (Post 5 Gate)
Search Japanese, English, and Burmese sources for important updates affecting Myanmar students, workers, or residents in Japan (past 24–72 hours, newly updated official rules, or upcoming effective dates/deadlines).
- Open exact source pages; never rely on search snippets alone.
- Cross-check legal/immigration/policy updates across at least two authoritative sources (Tier 1 official + Tier 2 news) where possible.
- If a qualifying item exists, create Post 5 (for both pages) and set `news_monitoring.status` to `POST_CREATED`.
- If none qualifies, omit Post 5 and set `news_monitoring.status` to `NO_QUALIFYING_NEWS`.

### 5. Write Content & Video Script
Follow every rule in `master_prompt_template.md`:
- **FB Safety Shield:** No external website URLs inside the post caption (put official source URLs inside Comment 1 instead; GETC Facebook Page URLs are allowed for cross-promotion). No banned promise words, no Facebook polls, no "မမတို့", and always spell "comment" in English.
- **Synthesized Burmese & Japanese Format:** Never translate a web article line-by-line. Synthesize into Problem -> Official Fact -> Actionable Tip + Interactive Comment Invitation. Always write Japanese as `Japanese Script (Romaji) — Burmese meaning`.
- **Image Prompts (No English Text + Logo Watermark):** Any text on the image MUST be in Japanese script and Burmese only (no English text unless strictly unavoidable). Instruct the AI to place the attached GETC school logo cleanly in the top-left or top-right corner as a subtle, semi-transparent watermark blended naturally with the background without distorting the logo.
- **Video Script:** Create one 30–45 second Reels/TikTok script (Hook, 3 Quick Points, CTA) plus two 9:16 B-roll image prompts (following the same Japanese/Burmese-only text and logo watermark rules) for Gemini + CapCut workflow.

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
        "published_or_updated": "Date or Date not stated"
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
      "title": "Working title",
      "caption": "Complete Burmese Facebook caption (no external URLs, includes #GETC #GakushinEikou + 2-4 trending hashtags)",
      "image_prompt": "Complete image prompt (Japanese/Burmese text only + attached school logo corner watermark blending)",
      "comments": [
        "Comment 1: Official source link + brief verification note",
        "Comment 2: Practical extra tip or follow-up insight"
      ],
      "sources": [
        {
          "title": "Exact source title",
          "url": "Exact source sub-page URL",
          "published_or_updated": "Date or Date not stated",
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
