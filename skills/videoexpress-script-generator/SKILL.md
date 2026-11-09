---
name: videoexpress-script-generator
description: Generate production-ready AI video scripts in the VideoExpress multi-clip format with keyframe image prompts, 5-second video/audio prompts, character consistency bibles, and generation checklists. Use when a user shares a YouTube or Instagram link, uploads a video file, or provides a video concept and asks to create a video script, replicate a video style, write prompt-by-prompt AI video generation scripts, or build scripts for VideoExpress, Kling, Runway, Luma, or Sora.
---

# VideoExpress Script Generator

Generate modular, production-ready AI video scripts tailored for clip-based generative video tools (such as VideoExpress, Kling AI, Runway Gen-3, Luma Dream Machine, Hailuo Minimax, and OpenAI Sora). Each script translates reference videos (YouTube links, Instagram Reels, uploaded video files) or original story premises into standardized multi-clip sequences with paired keyframe image prompts, motion/audio prompts, a character consistency bible, and generation parameter checklists.

## When to Use

- The user shares a YouTube link, Instagram URL, or uploaded video file and wants a video script structured like the reference.

- The user asks for a prompt-by-prompt AI video script with starting image prompts and video/audio prompts.

- The user specifies the VideoExpress script format, or requests short-form comedy, drama, sketch, or ad scripts for vertical 9:16 video generation.

- The user wants a character consistency bible and shot-by-shot prompt breakdown for consistent character AI video generation.

## Reference Architecture

Consult the bundled reference assets for exact formatting:

- `references/template-example.md` -- Real-world complete production script (Maharashtrian family comedy scenario).
- `assets/script-template.md` -- Structural skeleton template for new scripts.

## Workflow

### Step 1: Ingest and Analyze the Input

Determine the input format and extract the narrative skeleton:

1. **YouTube URL**: Inspect video metadata, description, and transcript. Identify total runtime, core hook, narrative tension, dialogue pacing, and punchline.

2. **Instagram Link or Web Video**: Review caption, visual pacing, audio track, camera angles, and character dynamics.

3. **Uploaded Video File**: Inspect video duration, visual blocking, shot transitions, speech/dialogue, and resolution.

4. **Text Concept or Topic**: Deconstruct the user premise into a 30 to 45 second comedic or dramatic arc with a clear premise, escalation, turning point, and twist.

Analyze the visible pattern of the reference: note the rhythm of shot alternation (e.g. alternating two-shots and single close-ups), total duration, camera framing, and soundscape.

### Step 2: Define Project Metadata and Synopsis

Open every script with a standardized header:

- **Document Title**: `# [Descriptive Scenario or Concept Title]`
- **On-screen Title**: `**On-screen [Language] title** -- [Native Script Title]`
- **Project Name**: `**Project name** -- [Series/Channel Name] -- [Episode Slug] -- [Version]`
- **Runtime**: `**Runtime** -- [Total seconds] seconds, [N] [duration]-second clips` (default: 30-40 seconds, six to eight 5-second clips).
- **Format**: `**Format** -- Vertical 9:16, [art style, e.g. photorealistic live-action], [language, dialect, and vocal tone]`.

Follow immediately with two concise paragraphs:

1. **Narrative Premise**: Character motivation, inciting action, escalation, and the specific unresolved twist or punchline.
2. **Reference Analysis Note**: Runtime of reference, visual alternation pattern observed, adaptation choices, dialogue treatment, and audio verification note.

### Step 3: Establish the Consistency Bible

Under `## Fixed cast, room and voices`, specify unchanging constraints across three categories:

1. **Cast Specifications**:
   - Provide for every visible actor: name, exact age, ethnic/regional background, physical build, hair style/color, facial hair state, exact wardrobe (garment type, pattern, fabric, color, rolled sleeves, pants, shoes).
   - Vocal profile: pitch (low, mid, high), dialect/accent (e.g. Pune Marathi, urban Hindi, neutral English), delivery tone (dry, warm, hesitant, deadpan).
   - Physical staging: default screen position (screen-left, screen-centre, screen-right), distance from other actors (e.g. half a metre), posture, and default hand positions.
   - For silent actors: specify that lips remain closed and acting occurs through gaze, eyebrow movements, and posture.

2. **Room and Location**:
   - Describe architectural boundaries, doorframes, wall textures and colors, cultural decor (e.g. toran, art, plants), and primary daylight or key light direction.
   - Specify adjacent visible zones (e.g. hallway, sofa corner, dining table) with matching palette.
   - Set strict prop rules: specify that lighting, costumes, and props remain fixed, and identify any prop introduced only in later clips (e.g. garlands, wedding cards, food items).

3. **Camera and Sound Conventions**:
   - Framing style: eye-level smartphone camera framing, subtle handheld movement, natural skin texture.
   - Execution rule: each generated shot is a single continuous take.
   - Safe zone enforcement: keep faces and hands clear of platform interface zones (top 15 percent for app headers, bottom 20 percent and right 15 percent for captions and engagement buttons).
   - Audio conventions: faint indoor room tone, clean speech, quiet pause before punchlines, watermark placement, and cover title handling.

### Step 4: Construct the Clip-by-Clip Breakdown

Divide the narrative into sequential clips. Standard clip length is 5 seconds (e.g. `Clip 1 · 00-05 · Title`, `Clip 2 · 05-10 · Title`).

Each clip must contain two mandatory prompt blocks:

#### 1. Starting Image Prompt
Draft this as an independent prompt for text-to-image keyframe generation:

- Aspect ratio and style: `Vertical 9:16 photorealistic [style] [shot framing, e.g. medium two-shot / medium close-up / chest-up] at eye level.`
- Exact subject count: Always state `Exactly [N] adults` to prevent AI models from generating extra background figures.
- Repeat character descriptions: Reiterate name, age, build, hair, facial hair, and exact wardrobe verbatim so the image generator does not drift.
- Spatial blocking: State screen positions (`screen-left midground`, `screen-right foreground`, `half a metre away`).
- Eye-lines and posture: Specify where eyes look (`just off camera-right at Aai`, `eyes down toward phone screen`), shoulder tension, and hand positions (`hands rest low`, `holding phone at chest height`).
- Environment: Reiterate background architecture, lighting direction, and decor.

#### 2. Video/Audio Prompt
Draft this as an instruction block for image-to-video and audio generation engines:

- Duration and lock: Lead with `Exactly five seconds. POSITION LOCK THROUGHOUT.`
- Actor blocking: Reiterate position lock (`Omkar stays left and Aditya stays right, half a metre apart`).
- Micro-actions and timing: Specify exact timing for actions and dialogue (`Omkar takes a short breath and says... Start the line in the first second`).
- Spoken dialogue: Quote exact spoken dialogue in the intended language/script (e.g. Marathi, Hindi, English).
- Non-speaking actor directions: Explicitly state `[Name] listens silently with his lips closed` to prevent unwanted lip movement or hallucinations.
- Audio cues: End with background sound requirements (`Quiet room tone only beneath the dialogue`).
- Special cases (phone calls or off-screen audio): Include fallback instructions (`If the model cannot assign an off-screen voice, generate the shot with both actors silent and add the separately recorded line in post-production`).
- Final clip punchline: Direct the delivery of the twist line within the first 1-2 seconds, trigger immediate physical reaction (e.g. pointing, dropped smile, widened eyes), and mandate holding the freeze/reaction pose for at least the final 2 seconds before cutting cleanly.

### Step 5: Specify Generation Setup and Assembly Guidelines

Conclude the document with a `## VideoExpress setup and final checks` section providing:

1. **AI Video Generator Parameters**:
   - Mode settings: Creative Mode and Advanced Mode ON.
   - Clip length: manual 5 seconds, aspect ratio 9:16.
   - Feature toggles: Consistent Character references enabled, prompt enhancement turned OFF to prevent models from altering spatial blocking and spoken lines.
   - Reference slot handling: if character reference slots are limited, use an approved multi-person keyframe as the starting image for group scenes.

2. **Audio and Lip-Sync Verification**:
   - Pilot test: generate Clip 1 first to verify voice timbre, accent, pronunciation, and lip-sync before batch-generating the remaining clips.
   - Voice continuity: use identical voice model assignments for returning speakers.
   - Check silent actors: verify that non-speaking actors do not move their mouths during other characters' lines or off-screen audio.

3. **Timeline Assembly and Export**:
   - Edit style: hard cuts between clips with a single continuous ambient room-tone bed.
   - Reaction hold: verify the final comedic/dramatic reaction holds for at least two full seconds.
   - Export specifications: 9:16 vertical MP4 at 1080 x 1920, checking for black frames, repeat clips, and safe-zone clearance.

## Gotchas and Edge Cases

- **Character Drift**: Never use shorthand descriptions like "Omkar in his shirt" in later clips. Always repeat the full physical and wardrobe description in every single Starting Image Prompt.

- **Unwanted Lip Movement**: If an actor is not speaking, explicitly state in the video prompt that their lips remain closed.

- **Platform Interface Collisions**: Ensure hands holding props, gestures, and faces do not sit in the bottom 20 percent of the vertical frame where TikTok, Instagram, and YouTube Shorts place captions, usernames, and action buttons.

- **Prompt Enhancer Interference**: Always specify turning off automatic AI prompt expanders. Prompt expanders invent camera moves, extra characters, and decorative details that break continuity.

- **Dialogue Overflow**: A 5-second clip can realistically accommodate 6 to 10 words of dialogue. Keep lines short, punchy, and timed to allow at least 1 second of reaction time.

- **Off-Screen Voices**: When a character speaks over a phone speaker or off-camera, explicitly instruct the video engine that on-screen actors keep their mouths shut, and provide a post-production audio fallback.
