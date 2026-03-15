---
name: video-publish-workflow
description: "Three-phase workflow for short video creation and multi-platform publishing. Phase 0: user describes video content → Claude recommends which platforms to publish to (YouTube/抖音/TikTok) based on content type. Phase 1: user describes raw footage → Claude provides CapCut editing suggestions (structure, pacing, titles, captions, music). Phase 2: user provides the finished video file path → Claude uses Playwright browser automation to publish to YouTube Shorts, 抖音 (Douyin), and TikTok automatically. Use when user asks which platform to publish to, wants editing guidance for short videos, or wants to publish a finished video to one or more of these platforms."
---

# Video Publish Workflow

Three-phase workflow: platform selection → editing guidance → multi-platform automated publishing.

## Phase 0: Platform Selection

When user describes a video or asks which platform(s) to publish to, recommend based on content type.

Read [references/platform-selection.md](references/platform-selection.md) for the full decision table.

**Quick rules:**
- 东南亚旅行 / 骑行 / 实用干货 → TikTok + 抖音 + YouTube 生活频道
- 长沙 / 国内内容 → 抖音 + YouTube 生活频道（TikTok 可选）
- 技术内容（工具/开发）→ YouTube 技术频道"自由码农" **独发**
- 视频 >3 min → YouTube 主发，剪 60s 竖屏版给 TikTok + 抖音

Always confirm the YouTube channel (生活频道 vs 技术频道) before uploading there.

## Phase 1: Editing Guidance

When user describes raw footage, provide CapCut editing suggestions covering:

1. **Structure** — recommended clip order, pacing, total duration (YouTube Shorts/TikTok/Douyin: ≤60s ideal)
2. **Opening hook** — first 3 seconds must grab attention; suggest text overlay or action cut
3. **Titles & captions** — specific suggested text, font style (bold/contrasting), placement
4. **Transitions** — which transition type fits the content (cut/dissolve/zoom)
5. **Music** — mood, tempo, whether to use CapCut's built-in library or upload
6. **Ending** — call-to-action text or subscribe reminder

Ask clarifying questions only if essential (e.g., target platform aspect ratio, duration constraint).

After giving suggestions, tell user: "剪辑好之后告诉我输出目录，我来帮你发布到各平台。"

## Phase 2: Multi-Platform Publishing

When user provides a video file path, publish to all three platforms using Playwright browser automation.

### Pre-flight

1. Confirm the file exists: `ls -lh <path>`
2. Ask user for title and description if not provided (or auto-generate from Phase 1 context)
3. Open browser tabs and check login state for each platform before uploading

### Publishing Order

Publish in this order (most reliable → most quirky):
1. **TikTok** — `tiktok.com/tiktokstudio/upload`
2. **YouTube Shorts** — `studio.youtube.com`
3. **抖音 (Douyin)** — `creator.douyin.com/creator-micro/content/upload`

For platform-specific quirks, selectors, and workarounds → see [references/platforms.md](references/platforms.md)

### File Upload Pattern (all platforms)

Never use `browser_file_upload` directly — the visible upload area is an overlay that blocks the hidden `<input type="file">`. Always use:

```javascript
// via browser_run_code
async (page) => {
  await page.locator('input[type="file"]').setInputFiles('/path/to/video.mp4');
}
```

### Status Reporting

After each platform attempt, report:
- ✅ Published successfully
- ⚠️ Uploaded but requires manual action (e.g., SMS verification)
- ❌ Failed — reason

## Key Reminders

- Keep user informed of progress — each platform takes 1–3 minutes to process
- If a platform requires login, ask user to log in then confirm before proceeding
- Douyin often triggers SMS verification on first publish of the day — warn user upfront
- Always set video to **Public** visibility unless user specifies otherwise
