# Platform Publishing Reference

Platform-specific selectors, quirks, and step-by-step flows for automated video publishing.

## TikTok

**URL:** `https://www.tiktok.com/tiktokstudio/upload`

**Upload flow:**
1. Navigate to upload URL
2. Upload file via `input[type="file"]` using `setInputFiles`
3. Wait for processing bar to complete (~30–60s depending on file size)
4. Fill description: the field is a `div[contenteditable]` inside a `div[class*="editor"]` — click it then type
   - Hashtags are auto-parsed inline (type `#tag` directly in the description)
5. Set cover: click the cover thumbnail area if desired (optional)
6. Visibility: default is Public — verify the dropdown shows "Everyone"
7. Click "Post" button

**Content check:** TikTok may show a "Content Check" warning dialog after clicking Post. Click "Continue" to proceed.

**Key selectors:**
```
input[type="file"]                          — hidden file input
div[class*="DraftEditor-root"]              — description rich text editor
button[data-e2e="post-button"]              — Post button (or text match "Post")
```

**Known issues:**
- `browser_file_upload` tool fails — must use `setInputFiles` via `browser_run_code`
- Processing can take 60–120s for videos >50MB; wait for upload progress to reach 100%

---

## YouTube Shorts

**URL:** `https://studio.youtube.com`

**Upload flow:**
1. Navigate to YouTube Studio
2. Click "CREATE" → "Upload videos" button
3. Upload file via `input[type="file"]` using `setInputFiles`
4. Fill title in the title input (first field)
5. Fill description (optional)
6. In "Audience" section: select "No, it's not made for kids"
7. Click "NEXT" × 3 to advance through the wizard
8. On "Visibility" step: select "Public"
9. Click "PUBLISH"

**Shorts detection:** YouTube auto-detects vertical videos (9:16, ≤60s) as Shorts. No special action needed.

**Channel note:** The user has two channels:
- 自由码农的生活 — lifestyle/vlog content
- 自由码农 (tech channel) — tech tools, dev, networking content

Always confirm which channel to publish to before uploading.

**Key selectors:**
```
input[type="file"]                          — file input (in upload dialog)
#title-textarea ytcp-form-input-container   — title field
ytcp-button#next-button                     — NEXT button
ytcp-button#done-button                     — PUBLISH button
```

---

## 抖音 (Douyin)

**URL:** `https://creator.douyin.com/creator-micro/content/upload`

**Upload flow:**
1. Navigate to upload URL
2. Upload file via `input[type="file"]` using `setInputFiles`
   - The visible drop zone has a `.container-drag-info` overlay — must use `setInputFiles`, not `.click()`
3. Wait for video processing (progress bar)
4. Fill 标题 (title) and 简介 (description/caption)
5. **Set cover (REQUIRED before publish):**
   - Click "设置封面" or the cover thumbnail area
   - In cover editor, select a frame or keep default
   - Click "完成" to confirm
   - If prompted "设置横封面", click "暂不设置" to dismiss
6. Set visibility to "公开" (Public)
7. Click "发布" button

**SMS Verification:** Douyin frequently requires phone verification (SMS code to 155\*\*\*\*\*\*98) when publishing, especially the first publish of the day. If this dialog appears, warn user to check their phone and enter the code manually. The video stays staged — user can complete publish after entering the code.

**Key selectors:**
```
input[type="file"]                          — hidden file input (under .container-drag-info)
.zone-container input[type="file"]          — alternative selector
textarea[placeholder*="标题"]               — title field
textarea[placeholder*="简介"]               — description field
button:has-text("发布")                     — publish button
button:has-text("完成")                     — cover confirm button
button:has-text("暂不设置")                 — dismiss horizontal cover prompt
```

**Known issues:**
- Cover must be set before clicking 发布 — otherwise error "请设置封面后再发布"
- SMS verification blocks headless publish — user must complete manually
- File input is hidden under overlay; `setInputFiles` required

---

## Login State Check

Before starting uploads, verify login state:

```javascript
// TikTok: check for avatar or username
async (page) => {
  await page.goto('https://www.tiktok.com/tiktokstudio/upload');
  const loggedIn = await page.locator('[data-e2e="upload-icon"]').count() > 0;
  return loggedIn ? 'logged in' : 'need login';
}
```

If not logged in, ask user to log in manually and confirm before proceeding.

## Timing Guidelines

| Platform | Upload wait | Post-click wait |
|----------|------------|-----------------|
| TikTok   | 30–120s    | 5–10s           |
| YouTube  | 20–60s     | Instant         |
| Douyin   | 30–90s     | 5s (or SMS wait)|
