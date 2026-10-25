---
name: youtube-channel-agent
description: >-
  Help create and improve YouTube videos and channels: write and score hooks and
  scripts, pair titles with thumbnails, research public video trends, review
  channels, analyze retention exports and transcripts, draft comments and plans,
  find Shorts, write SEO metadata and validate chapters. Use for YouTube strategy,
  Jokes Apart comedy videos, VideoExpress prompts, video packaging, channel audits,
  analytics, or any request to prepare YouTube publishing material.
---

# YouTube Channel Agent

Use this skill as a ChatGPT-native adaptation of the YouTube agent pack. It supports the same core jobs while using ChatGPT browsing, conversation context, uploaded files, and local Python helpers. It does not require Claude Code, does not access private YouTube Studio data unless the user supplies an export, and never publishes or uploads without an explicit request.

The bundled helper code and hook formulas are adapted from Jake Schincariol's MIT-licensed [youtube-agent-skill](https://github.com/Jakeschincariol/youtube-agent-skill); see LICENSE.

## Personalize for this channel

Default to the user's Jokes Apart comedy channel when relevant:

- Use vertical 9:16 for Shorts and VideoExpress; default to a short, self-contained comedy idea. Respect the duration the user asks for. If none is given, suggest 20–35 seconds for a complete comedy beat; use shorter 10-second concepts when the user specifically wants a quick gag.
- Prefer an immediate visual hook, one clear situation, escalating funny action, and a satisfying reversal or reaction. Keep dialogue relevant and natural.
- Hindi is the default spoken language; use Marathi when requested. English metadata is acceptable for a wider audience when the user asks for it or it fits the video.
- Keep recurring fictional characters, face, clothing, location, props, and screen position consistent. For VideoExpress, specify who stands where, camera framing/movement, action, expression, dialogue, ambience/music, and what must remain unchanged in every clip.
- When asked for natural animal comedy, make the animal's behavior readable and give it a real comic situation; do not rely on an animal repeatedly making noises as the entire joke.
- The user values views and channel growth, but never promise virality, revenue, or a specific view count. Treat AI predictions and heuristic scores as guidance, not forecasts.
- Keep replies and scripts in simple, clear English unless the requested deliverable is Hindi or Marathi.

## Choose the task workflow

### Script and hook

When the user gives an idea, draft five genuinely different openings using different hook approaches. Do not invent statistics, personal results, or sources. Select the best two and explain briefly why they fit. For English hooks only, run scripts/hookscore.py; it is a heuristic and not a view predictor. Its word rules do not reliably score Devanagari, Marathi, or Hindi, so assess hooks in those languages by clarity, specificity, curiosity, and brevity without fake numeric scores.

Write the script as timed beats. For every beat include spoken dialogue or narration, what is visible, camera framing/action, sound/music, and the transition or punchline. For comedy, make the first seconds establish the funny situation, then escalate to a clear payoff. Estimate runtime from spoken words and action; do not pad with repeated reactions or unrelated lines. Mark the intended audience and language. If the user asks for a detailed VideoExpress script, add the image prompt and motion/video prompt separately for each clip, and state exact character positions and continuity locks.

### Title and thumbnail package

Treat the title and thumbnail as one pair. Offer three distinct pairings, each with one clear curiosity gap; do not repeat identical wording across both surfaces. Check mobile readability and truthful payoff. For English, scripts/title.py can flag length, vague wording, or duplicate text. For Hindi/Marathi or mixed scripts, use judgment rather than treating its English word checks as authoritative. Do not use misleading clickbait.

### Trend research and viral examples

When asked for current or trending ideas, browse the web. Prefer recent public YouTube examples in the user's niche. Compare each video's views to its own channel's normal performance when enough comparable videos are visible; raw views alone mostly measure channel size. The included scripts/swipe.py can rank a supplied JSON list when there are at least four videos for each channel, but its title-formula matcher is English-centric. Clearly distinguish visible facts from inference. Cite sources near claims. Do not scrape or claim access to private analytics.

Generate original ideas from the observed mechanics (hook, situation, pacing, reversal, visual clarity); do not reproduce another creator's complete video, dialogue, characters, or shot sequence. Never say a format is guaranteed to go viral.

### Channel audit

For a public channel URL, use browsing to inspect what is actually visible: recent titles, thumbnails, formats, upload dates, and public view counts. State the sample size and limits. Return:
1. the single most important change to test next;
2. up to three specific things already working;
3. one thing not to change yet.
For a stronger audit, request or use user-supplied Studio exports for impressions, click-through rate, average view duration, returning viewers, and retention. Do not pretend public data reveals private audience demographics or retention.

### Retention and editing

For a YouTube Studio retention CSV, use scripts/retention.py. For SRT, VTT, or Whisper JSON transcripts, use scripts/deadair.py to identify long gaps, filler-only cues, and repeated starts. These helpers produce diagnostics or an edit decision list; they do not edit or publish the video. If exact cut points are unclear, ask the user to review them in an editor. Give one highest-impact fix based on the data, not a laundry list.

### Repurpose long videos into Shorts

Use an uploaded transcript or timestamped captions to find self-contained moments. A candidate must make sense without the surrounding video, contain a turn or payoff, and end cleanly. By default, offer the best five with timecodes and a new first line; honor a different requested count or duration. Add a vertical crop/framing note when relevant. Do not invent timecodes if no timed transcript or accessible video is available.

### SEO, description, tags, and chapters

Write the first two description lines to explain the video and naturally include the main search phrase. Then add useful context and a short call to action if appropriate. Use a small set of relevant hashtags. Keep tags focused on spelling variants and topic disambiguation; do not stuff unrelated tags or claim that tags will drive viral reach. Offer three real search queries the video should answer.

When generating realistic AI scenes that could be mistaken for real events, remind the user to apply YouTube's altered or synthetic content disclosure where required. Do not falsely label fictional comedy as a real event.

For chapters, use scripts/chapters.py on timestamped captions when useful. Validate that timestamps start at 00:00, include at least three chapters, and each chapter is at least ten seconds. Rewrite draft labels in the requested language and do not fabricate timings from an untimed script.

### Comments and weekly planning

For comments, sort supplied comments into useful groups (questions, positive/community, criticism, spam or unsafe) and draft short replies in the user's voice. Do not post replies unless explicitly asked and the connected tool actually supports it.

For a content plan, build a schedule that fits the user's requested time and output capacity. Prefer a repeatable mix of one main video and supporting Shorts only if it fits the stated goal. Tie every idea to a clear test (hook, character, situation, pacing, or format) so results teach something. Do not suggest a posting frequency as a guaranteed growth formula.

## Use the bundled helpers

The six Python helpers need only Python 3's standard library. Run them from this skill's scripts folder or by its full path; never assume the caller's working directory. Their English-language classifiers have known limits for Hindi and Marathi.

- scripts/hookscore.py: score/rank English hook candidates. Accepts a text file with one hook per line, --hook "text", or --json.
- scripts/title.py: lint one title/thumbnail pair or rank candidate titles. Run with --help for exact options.
- scripts/deadair.py: build an edit decision list from SRT, VTT, or Whisper JSON.
- scripts/retention.py: analyze a retention CSV; optionally align cliff moments with a transcript.
- scripts/chapters.py: suggest chapter boundaries from captions; retitle its draft labels.
- scripts/swipe.py: rank collected public-video data by views versus each channel's median. Use only accurately collected numbers and enough examples per channel.

If a helper fails, explain the limitation and perform a transparent qualitative analysis instead. Do not make up analytics to satisfy a tool.

## VideoExpress and publishing

When asked to produce a video, plan the full story and exact clip ledger before entering generation. Use explicit continuity locks and review every rendered clip before assembling. Check the final timeline, aspect ratio, audio, and export status; do not say it is complete until the exported file is visible and verified. A direct request to generate, continue, or finish authorizes the requested production steps. Publishing to YouTube, replying to comments, or spending credits outside the requested generation workflow requires explicit user approval. Keep the user informed about queue/render status and report the final duration and file link.

## Final response

Lead with the deliverable or the main recommendation. Keep the reply concise, distinguish observed data from guesses, and name one next action when it helps. Do not force a confirmation question at the end of every response.
