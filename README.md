# MultiPowerAI YouTube Video Pipeline

Automated video asset pipeline for MultiPowerAI commercial content. Videos land here → OpenClaw grabs them → uploads to YouTube.

## Directory Structure

```
scripts/        → Commercial scripts (.md) with timing, dialogue, scene descriptions
audio/          → 11 Labs generated voiceover files (.mp3, .wav)
video/          → 11 Labs generated video clips (.mp4)
renders/        → Final composited videos ready for upload (.mp4)
thumbnails/     → YouTube thumbnails (.png, .jpg)
metadata/       → Upload metadata per video (title, description, tags) (.json)
```

## Workflow

1. **Script** → Write commercial script in `scripts/`
2. **Voice** → Generate voiceover via 11 Labs TTS → save to `audio/`
3. **Video** → Generate video clips via 11 Labs Image & Video → save to `video/`
4. **Compose** → Combine audio + video → save final render to `renders/`
5. **Metadata** → Create upload metadata JSON in `metadata/`
6. **Upload** → OpenClaw picks up new files in `renders/` + matching `metadata/` → uploads to YouTube

## Metadata Format

Each video in `renders/` needs a matching JSON in `metadata/`:

```json
{
  "filename": "commercial-001-agent-protection.mp4",
  "title": "Your AI Agent Is Spending Your Money Right Now",
  "description": "MultiPowerAI — the trust layer for the agent web...",
  "tags": ["AI agents", "trust", "MultiPowerAI", "agent safety"],
  "category": "Science & Technology",
  "privacy": "public",
  "shorts": true,
  "scheduled_publish": null
}
```

## OpenClaw Integration

OpenClaw watches for new `.mp4` files in `renders/` that have matching metadata.
When found, it uploads via YouTube Data API v3 using the channel's OAuth credentials.

## 11 Labs Settings

- **Plan:** Creator (427s video, 100K TTS credits)
- **Video:** Image & Video tool
- **Voice:** Female voice from Voice Library
- **Output:** 1080x1920 (vertical for Shorts) or 1920x1080 (landscape)
