---
name: generate-round-icons
description: "Generate round Android launcher icons (ic_launcher_round.png) from existing launcher icons for all mipmap densities (ldpi, mdpi, hdpi, xhdpi, xxhdpi, xxxhdpi). Uses ImageMagick to create perfect circular masks. Trigger keywords: generate round icons, create round icons, 生成圆形图标, 圆形图标."
---

# Generate Android Round Icons

Generate round launcher icons (ic_launcher_round.png) from existing launcher icons for all Android mipmap densities.

## Prerequisites

Check if ImageMagick is installed:

```bash
magick --version
```

If ImageMagick is not installed, install it based on user's OS:

**macOS:**
```bash
brew install imagemagick
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install imagemagick
```

**Windows:**
```powershell
choco install imagemagick
```

---

## Instructions

When the user requests to generate round icons, follow this workflow:

**IMPORTANT: This skill will automatically regenerate ALL round icons and overwrite existing ic_launcher_round.png files without confirmation.**

### Step 1: Verify Environment

1. Check if ImageMagick is installed:
   ```bash
   magick --version
   ```

2. If not installed, provide installation instructions based on the OS (see Prerequisites above).

3. Verify the Android project structure exists:
   ```bash
   ls -la android/app/src/main/res/mipmap-*
   ```

### Step 2: Process Each Mipmap Directory

For each mipmap directory (mipmap-ldpi, mipmap-mdpi, mipmap-hdpi, mipmap-xhdpi, mipmap-xxhdpi, mipmap-xxxhdpi):

1. Check if `ic_launcher.png` exists in the directory.

2. If exists, generate/regenerate the round version (will overwrite existing):
   ```bash
   # Navigate to the mipmap directory and generate round icon
   cd /path/to/project/android/app/src/main/res/[mipmap-directory] && \
   size=$(magick identify -format "%w" ic_launcher.png) && \
   radius=$((size/2)) && \
   magick ic_launcher.png \
       \( +clone -alpha extract \
          -draw "fill black rectangle 0,0 $size,$size fill white circle $radius,$radius $radius,0" \
          -alpha off \
       \) \
       -compose copy_opacity -composite \
       ic_launcher_round.png && \
   magick identify -format "✓ Created: [mipmap-directory]/ic_launcher_round.png (%wx%h)\n" ic_launcher_round.png
   ```

   **Note:** Use absolute paths to avoid directory navigation issues. Replace `/path/to/project` with the actual working directory.

3. Process all directories in parallel for faster execution.

### Step 3: Summary Report

After processing all directories, provide a summary:

```
✓ All round icons generated successfully!
  - mipmap-mdpi: 48x48
  - mipmap-hdpi: 72x72
  - mipmap-xhdpi: 96x96
  - mipmap-xxhdpi: 144x144
  - mipmap-xxxhdpi: 192x192

Total: 5 icons created
```

---

## Error Handling

- **ImageMagick not installed**: Provide installation command for user's OS
- **Not in Android project**: Ask user to navigate to the correct directory
- **Missing source icons**: List which directories are missing `ic_launcher.png`
- **Command fails**: Show the error message and suggest checking file permissions

---

## Technical Details

The ImageMagick command works by:
1. Reading the source `ic_launcher.png`
2. Creating a circular mask using the `draw` command
3. Applying the mask to the source image using `copy_opacity`
4. Outputting the result as `ic_launcher_round.png`

The circular mask ensures perfect round corners for all icon sizes across different Android device densities.
