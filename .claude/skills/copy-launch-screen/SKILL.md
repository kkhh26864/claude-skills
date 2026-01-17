---
name: copy-launch-screen
description: "Copy Android launch screen images to iOS with proper density mapping. Automatically maps Android mipmap densities (mdpi, xhdpi, xxhdpi) to iOS scales (1x, 2x, 3x). Trigger keywords: copy launch screen, sync launch images, update iOS launch screen, 复制启动屏幕, 同步启动图片."
---

# Copy Android Launch Screen to iOS

Automatically copy launch screen images from Android mipmap directories to iOS imageset with proper density mapping.

## Overview

This skill copies `launch_screen.png` files from Android to iOS, mapping the densities correctly:

- **Android mipmap-mdpi** (1x) → iOS **launch_screen.png** (1x)
- **Android mipmap-xhdpi** (2x) → iOS **launch_screen@2x.png** (2x)
- **Android mipmap-xxhdpi** (3x) → iOS **launch_screen@3x.png** (3x)

---

## Instructions

When the user requests to copy or sync launch screen images, follow this workflow:

**IMPORTANT: This skill will automatically copy launch screen images from Android to iOS without confirmation.**

### Step 1: Verify Directories

1. Check if Android source directory exists:
   ```bash
   ls -la android/app/src/main/res/mipmap-*/launch_screen.png
   ```

2. Check if iOS imageset directory exists:
   ```bash
   ls -la ios/*/Images.xcassets/LaunchImage.imageset/
   ```

### Step 2: Copy Images

Copy the launch screen images from Android to iOS with proper naming:

1. **Copy 1x (from mdpi to iOS 1x)**:
   ```bash
   cp android/app/src/main/res/mipmap-mdpi/launch_screen.png ios/[ProjectName]/Images.xcassets/LaunchImage.imageset/launch_screen.png
   ```

2. **Copy 2x (from xhdpi to iOS 2x)**:
   ```bash
   cp android/app/src/main/res/mipmap-xhdpi/launch_screen.png ios/[ProjectName]/Images.xcassets/LaunchImage.imageset/launch_screen@2x.png
   ```

3. **Copy 3x (from xxhdpi to iOS 3x)**:
   ```bash
   cp android/app/src/main/res/mipmap-xxhdpi/launch_screen.png ios/[ProjectName]/Images.xcassets/LaunchImage.imageset/launch_screen@3x.png
   ```

**Note:** Replace `[ProjectName]` with the actual iOS project name found in the `ios/` directory.

### Step 3: Summary Report

After copying all images, provide a summary:

```
✓ Launch screen images copied successfully!
  - 1x: mipmap-mdpi → launch_screen.png
  - 2x: mipmap-xhdpi → launch_screen@2x.png
  - 3x: mipmap-xxhdpi → launch_screen@3x.png

Next steps:
  1. Rebuild your iOS app to see the changes
  2. Run: cd ios && bundle exec pod install && cd ..
  3. Run: yarn ios
```

---

## Error Handling

- **Android source directory not found**: Report which Android res directory is missing
- **iOS imageset directory not found**: Report the expected iOS path and ask user to verify
- **Missing source images**: List which density files are missing (mdpi, xhdpi, xxhdpi)
- **Copy fails**: Show the error message and suggest checking file permissions

---

## Technical Details

**Density Mapping:**
- Android uses density-independent pixels (dp) with different mipmap folders for different screen densities
- iOS uses point-based system with @1x, @2x, @3x suffixes for different scales
- The mapping ensures images display correctly on both platforms:
  - mdpi = 160 dpi = 1x baseline
  - xhdpi = 320 dpi = 2x
  - xxhdpi = 480 dpi = 3x

**File Locations:**
- Android: `android/app/src/main/res/mipmap-{density}/launch_screen.png`
- iOS: `ios/{ProjectName}/Images.xcassets/LaunchImage.imageset/launch_screen{@scale}.png`

**React Native Build:**
After copying images, iOS requires a rebuild to pick up the new assets. CocoaPods installation is not strictly required unless dependencies changed, but rebuilding the app is necessary.
