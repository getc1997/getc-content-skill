---
name: getc-content
description: Produce GETC's daily four Facebook drafts, scan Japan news for a qualifying optional Post 5, verify dates and sources, save files and logs, and show every draft in copy-ready code blocks.
---

# GETC Daily Content Production — Kai 9000 V4

You are running in Kai 9000 on Android with the Debian 12 Linux Sandbox. Use Kai's live web tools and shell tools. Complete the work; do not stop at request files or ask the user to copy log lines manually.

## Project paths
- Project root: `/root/GETC/Marketing`
- Master prompt: `/root/GETC/Marketing/master_prompt_template.md`
- Sources: `/root/GETC/Marketing/sources.txt`
- Categories: `/root/GETC/Marketing/categories.txt`
- Hashtags: `/root/GETC/Marketing/hashtags.txt`
- Source log: `/root/GETC/Marketing/used_sources.txt`
- Topic log: `/root/GETC/Marketing/used_topics.txt`
- News monitoring log: `/root/GETC/Marketing/news_monitoring_log.txt`
- Posts: `/root/GETC/Marketing/FB_Posts/`
- Saver: `/root/GETC/Marketing/save_getc_batch.py`

## Default daily run
Generate Posts 1–4 every day. Every run must also perform the Japan-important-news scan described in the Master Prompt. Generate Post 5 only if a genuinely important, relevant, current, and verified update qualifies. Otherwise explicitly skip Post 5.

Do not connect to Facebook or publish/schedule anything on Facebook. The user personally reviews, creates images, publishes posts, and adds comments.

## Required sequence

### 1. Read project files
Use `execute_shell_command` to read the full Master Prompt, sources, categories, hashtags, used source log, used topic log, news monitoring log (if it exists), and saver script. Do not overwrite existing source/topic logs. Create `FB_Posts/` if missing. If a required file is missing, report it; do not invent its content.

### 2. Confirm date/time
Use Kai's local-time tool if available. Confirm the project timezone configured in the saver (currently `Asia/Yangon`). Use one consistent date for the output filenames and logs. Do not infer the date from old chat messages.

### 3. Plan Posts 1–4
Read all previous topic and source logs. Plan all four together, matching page/role in the Master Prompt. Prevent conceptual duplicates, including repeated audience question, example, lesson point, and angle. Exact-string matching alone is insufficient.

### 4. Mandatory news scan for Post 5
Search Japanese, English, and Burmese sources for important Japan updates affecting Myanmar students, workers, and residents. Check recent 24–72 hour developments, newly updated official notices, upcoming effective dates, and still-actionable deadlines. Open exact source pages; do not rely on snippets or social reposts. Apply the Master Prompt's source hierarchy, date checks, relevance test, and Post 5 qualification criteria.

- If a qualifying item exists, create exactly one Post 5 and set `news_monitoring.status` to `POST_CREATED`.
- If none qualifies, do not create Post 5; set status to `NO_QUALIFYING_NEWS` and explain the scan result.
- Never fabricate a search or claim to have checked a page that was not opened.
- Include `checked_at`, `search_coverage`, and `sources_checked` in the JSON.

### 5. Write the content
Follow every requirement in the Master Prompt:
- Natural, professional Burmese.
- Correct Japanese script + romaji + Burmese meaning where relevant.
- 1–3 useful comment drafts, each distinct.
- Tailored image prompt.
- Realistic marketing; no false urgency or promises.
- No invented student stories, school affiliations, prices, deadlines, outcomes, or statistics.
- For Post 5 include `news_announcement_date`, `effective_date`, `affected_audience`, and `action_required`.
- Keep high-risk legal/immigration/scholarship/labor/financial claims marked for human review where required.

### 6. Build the JSON batch
Create:
`/root/GETC/Marketing/.getc_batch_YYYY.MM.DD.json`

Use UTF-8, valid JSON, no Markdown fence. Structure:

{
  "news_monitoring": {
    "checked_at": "ISO 8601 timestamp with timezone",
    "status": "POST_CREATED or NO_QUALIFYING_NEWS",
    "summary": "Scan result and reason",
    "search_coverage": ["search topics/languages"],
    "sources_checked": [
      {
        "title": "Exact page title",
        "url": "Exact page URL",
        "published_or_updated": "Date or Date not stated"
      }
    ]
  },
  "posts": [
    {
      "post_number": 1,
      "page": "Exact target page and URL",
      "role": "Assigned role",
      "category": "Selected category",
      "title": "Working title",
      "caption": "Complete Burmese Facebook caption",
      "image_prompt": "Complete prompt",
      "comments": ["Comment one", "Comment two"],
      "sources": [
        {
          "title": "Exact source title",
          "url": "Exact source sub-page URL",
          "published_or_updated": "Date or Date not stated",
          "claim_supported": "Specific supported claim"
        }
      ],
      "topic": "Normalized topic",
      "angle": "Distinct angle",
      "audience_need": "Reader need",
      "verification_status": "VERIFIED or NEEDS HUMAN REVIEW or HOLD",
      "verification_checklist": [
        {"item": "Exact check", "status": "Verified or Needs human review or N/A"}
      ]
    }
  ]
}

The `posts` array must contain Posts 1–4 and Post 5 only when it qualifies. No duplicate post numbers. If no source was genuinely used for a general educational post, use `sources: []`. Post 5 must have at least one exact source URL.

### 7. Save and update automatically
Run:
`python3 /root/GETC/Marketing/save_getc_batch.py --input /root/GETC/Marketing/.getc_batch_YYYY.MM.DD.json`

The saver validates the full batch before writing, then:
- Saves/overwrites `FB_Posts/YYYY.MM.DD-pN.txt`.
- Creates `FB_Posts/YYYY.MM.DD-chat-ready.md` from the same JSON.
- Updates `used_sources.txt` and `used_topics.txt` with GENERATED entries.
- Updates one dated record in `news_monitoring_log.txt` (reruns replace that date's news scan record).

If the saver fails, fix the JSON and rerun. Never claim success until the command succeeds.

### 8. Verify files
List the saved post files and read the complete `YYYY.MM.DD-chat-ready.md`. Confirm the source/topic/news logs changed as expected. The chat-ready Markdown is the authoritative copy for the chat response.

### 9. Final chat response — mandatory full copy-ready output
Paste the COMPLETE contents of `YYYY.MM.DD-chat-ready.md` into the Kai chat. Do not merely summarize or provide paths. Preserve every code block and all wording exactly. It must include:
- Each post caption in its own code block.
- Each image prompt in its own code block.
- Each comment draft in its own separate code block.
- Source URLs, topic log, verification checklist, publication status.
- News scan result and clear Post 5 skipped note when applicable.

Then briefly state saved paths and counts. Do not omit the full post content. Do not publish or comment on Facebook.

## Daily schedule setup
If the user asks to schedule this workflow, create one recurring task using Kai's `schedule_task` tool with cron `0 8 * * *` (08:00 in Kai/device local timezone). The task prompt must explicitly say to read this skill and the Master Prompt from disk, run the complete daily workflow above, save the outputs, and paste the entire chat-ready Markdown into the scheduled-task response. Do not create duplicate recurring tasks; call `list_tasks` first and reuse/leave an existing matching task. Explain that Kai's scheduled task output may appear in the heartbeat/scheduled-task conversation surface, not necessarily the original chat thread.
