---
name: getc-content
description: Produce GETC's daily four Facebook drafts, one 30-second Reels/TikTok video script, scan Japan news for a qualifying optional Post 5, enforce Burmese Zero-Shadow comments, varied hooks, contextual soft-sell CTAs, Post 1 & 3 cross-promotion, and smart topic lifecycle via generate_posts.py, and display copy-ready blocks in chat.
---

# GETC Daily Content Production — V1.3

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
1. Generate Posts 1–4 every day (150–250 words of rich Burmese substance for Posts 1–3; 80–150 words for Post 4; strict Facebook safety compliance).
2. Generate one **strictly 30-second** vertical video script (for Facebook Reels & TikTok) based on the strongest post of the day, including 2 vertical (`9:16`) Gemini B-roll image prompts.
3. Perform the mandatory daily Japan news scan. Generate Post 5 ONLY if a genuinely urgent, time-critical update (announced within 24–72 hours) qualifies. Otherwise omit Post 5.
4. Never connect to Facebook or publish/schedule anything automatically.

## Required Execution Sequence

### 1. Read Project Files & Recent Logs
Use `execute_shell_command` to read:
- Full `master_prompt_template.md`, `sources.txt`, `categories.txt`, and `generate_posts.py`.
- Recent logs (to avoid repeating topics or URLs): run `tail -n 120 /root/GETC/Marketing/used_topics.txt`, `tail -n 120 /root/GETC/Marketing/used_sources.txt`, and `tail -n 15 /root/GETC/Marketing/news_monitoring_log.txt` (if they exist).
- Ensure `/root/GETC/Marketing/FB_Posts/` exists. Do not overwrite or delete existing log files.

### 2. Confirm Date & Timezone
Check the current local date/time in `Asia/Yangon` (`+06:30`). Use one consistent `YYYY.MM.DD` date for filenames and `YYYY-MM-DD` for logs. Always include the current year in search queries to prevent outdated results.

### 3. Dynamic Hashtag Research & Smart Topic Planning
- Use `web_search` to find 2–4 currently trending, relevant Burmese/English/Japanese hashtags on Facebook and TikTok for Japan study, JLPT, or Japan life. Always pair them with mandatory `#GETC` and `#GakushinEikou` (total 4–6 hashtags per post).
- Review the last 120 lines of `used_topics.txt` and `used_sources.txt` BEFORE researching articles.
- **Anti-Repetition Rule:** Never select a topic whose core concept (`core_tags`) was already covered in `used_topics.txt` (within 180 days for `STATIC` topics, or within 90 days for `DYNAMIC` policy topics unless an official source published a newer update date). Never reuse an exact URL from `used_sources.txt`, and respect the 3-day domain cooldown for non-government sites.
- Open and read full specific sub-page articles from `sources.txt` rather than generic landing pages.

### 4. Mandatory Japan News Scan (Post 5 Gate)
Search Japanese, English, and Burmese sources for urgent updates affecting Myanmar students, workers, or residents in Japan announced in the **past 24–72 hours** (or critical deadlines closing within days).
- Keep the boundary strict: routine educational/how-to guides belong in Posts 1–3, NOT Post 5.
- Open exact source pages; never rely on search snippets alone.
- Cross-check legal/immigration/policy updates across at least two authoritative sources where possible.
- If a qualifying urgent item exists, create Post 5 (for both pages), exclude that topic from Posts 1–4 today, and set `news_monitoring.status` to `POST_CREATED`.
- If none qualifies, omit Post 5 and set `news_monitoring.status` to `NO_QUALIFYING_NEWS`.

### 5. Write Content & 30-Second Video Script
Follow every rule in `master_prompt_template.md`:
- **Varied Hooks:** Rotate across fact, warning/mistake, relatable scenario, actionable tip, and question hooks. At most 1 post among Posts 1–4 may open with a question hook.
- **Pure Burmese Substance & Term-Only Japanese:**
  - Posts 1–3 MUST be written in rich, complete Burmese (150–250 words), using `Japanese Script (Romaji) — Burmese meaning` ONLY for specific vocabulary terms or short phrases (NEVER full Japanese sentences in Posts 1–3).
  - Reserve full example sentences for Post 4 (Daily Short Japanese Lesson, 80–150 words).
  - Never use standalone Burmese phonetic approximations.
- **Comment Teaser + Zero-Shadow Burmese Comments (1–3 Comments, NO URLs):**
  - End every caption body with a natural teaser inviting readers to check the comments (always spelling `comment` in English) for the omitted exceptions/details.
  - Write **1 to 3 comments** per post strictly in **Burmese**, revealing the specific facts, exceptions, or tips deliberately held back from the source article. NEVER put website URLs in comments.
- **Contextual Soft-Sell CTA & Post 1 & 3 Cross-Promotion:**
  - Include a rotating, topic-matched soft-sell CTA in every post.
  - Include cross-promotion links ONLY on **Post 1** (`[https://www.facebook.com/gakushineikou2](https://www.facebook.com/gakushineikou2)`) and **Post 3** (`[https://www.facebook.com/gakushineikou](https://www.facebook.com/gakushineikou)`). Do NOT include cross-promotion links on Post 2 or Post 4.
- **FB Safety Shield:** Zero external URLs in captions, no banned guarantee words, no polls, no `"မမတို့"`.
- **Image Prompts:** Japanese and Burmese text only (no English text on image) + single attached GETC school logo watermark in top-left or top-right corner. Use **`1:1` square or `4:5` portrait** for Posts 1–4, and **`9:16` vertical** for the 2 video B-roll prompts.
- **30-Second Video Script:** Write a crisp 30-second Reels/TikTok script (`hook_0_3s`, `body_3_24s`, `cta_24_30s`) plus two `9:16` B-roll image prompts.

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
        "url": "Exact page URL",
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
      "caption": "Complete Burmese Facebook caption (varied hook, rich Burmese body, term-only Japanese in Posts 1-3, natural 'comment' teaser, contextual soft-sell CTA, cross-promo URL on Post 1 & 3 only, 4-6 hashtags)",
      "image_prompt": "1:1 square or 4:5 portrait image prompt (Japanese/Burmese text only + single attached school logo corner watermark)",
      "comments": [
        "Comment 1 in Burmese: Specific detail or exception omitted from the caption (NO URLs)",
        "Comment 2 in Burmese: Additional insider tip or edge case from the source article (NO URLs)"
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
```

### 7. Validate & Save via `generate_posts.py`
Run:
`python3 /root/GETC/Marketing/generate_posts.py --input /root/GETC/Marketing/.getc_batch_YYYY.MM.DD.json`
*(If a `--date YYYY.MM.DD` override was requested by the user, pass `--date YYYY.MM.DD` to `generate_posts.py` as well).*

If `generate_posts.py` exits with a validation error, fix every listed issue in the JSON immediately and re-run until `GETC SAVE SUCCESS` appears. Once succeeded, remove the temporary `.getc_batch_YYYY.MM.DD.json` file so the directory stays clean.

### 8. Final Chat Output Format
Read the generated `/root/GETC/Marketing/FB_Posts/YYYY.MM.DD-chat-ready.md` and present the entire **PART 1: COPY-READY CONTENT** (Posts 1–4/5 captions, image prompts, Burmese comments, and the 30-second Reels/TikTok script + B-roll prompts) directly in the chat using clean individual code blocks so the user can tap-to-copy immediately on mobile, followed by a concise summary of **PART 2: AUDIT & NEWS SCAN STATUS**.
