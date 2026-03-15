```html
<!-- Basic video player -->
<video controls width="800" height="450" poster="thumbnail.jpg">
  <source src="video.mp4"  type="video/mp4" />
  <source src="video.webm" type="video/webm" />
  <p>Your browser doesn't support video. <a href="video.mp4">Download it.</a></p>
</video>

<!-- Background video (autoplay, no sound, loops) -->
<video autoplay loop muted playsinline>
  <source src="hero-bg.mp4"  type="video/mp4" />
  <source src="hero-bg.webm" type="video/webm" />
</video>

<!-- Video with subtitles / captions -->
<video controls width="800">
  <source src="lecture.mp4" type="video/mp4" />

  <!-- Subtitles: translation of spoken words -->
  <track kind="subtitles" src="subs-en.vtt" srclang="en" label="English" default />
  <track kind="subtitles" src="subs-ur.vtt" srclang="ur" label="Urdu" />

  <!-- Captions: includes sound effects for deaf users -->
  <track kind="captions" src="captions-en.vtt" srclang="en" label="English Captions" />

  <!-- Chapters: enables navigation in some browsers -->
  <track kind="chapters" src="chapters.vtt" srclang="en" />
</video>

<!-- All common attributes -->
<video
  src="video.mp4"
  controls
  autoplay
  loop
  muted
  playsinline
  preload="metadata"
  poster="cover.jpg"
  width="1280"
  height="720"
  controlslist="nodownload nofullscreen"
>
</video>
```

# Explanation

The `<video>` element embeds a video player natively in the page. Like `<audio>`, it uses `<source>` for format fallbacks. The big addition over audio is visual — `poster`, `width`/`height`, and the `<track>` element for accessibility captions.

## Breakdown

- **`controls`**  
  Shows the browser's built-in video player controls — play/pause, seek bar, volume, fullscreen. Appearance varies by browser and OS.

- **`width` and `height`**  
  Set the dimensions in pixels. Setting both prevents layout shift while the video loads, just like with `<img>`. Scale with CSS, but always provide the intrinsic dimensions.

- **`poster`**  
  A still image shown before the video plays (or if it can't play). Use a representative, high-quality frame from the video. If omitted, the browser shows a blank or grey box.

- **`<source>`**  
  Multiple format options. **MP4/H.264** works everywhere. **WebM/VP9** offers better compression at the same quality. Provide both for maximum compatibility and efficiency.

- **`playsinline`**  
  Critical for iOS/Safari. Without it, Safari plays the video in a fullscreen native player rather than inline in the page. Always include on background and hero videos.

- **`<track kind="subtitles">`**  
  Links a WebVTT (`.vtt`) file containing timed text. Subtitles are a translation or transcription of spoken dialogue for users who don't understand the language.

- **`<track kind="captions">`**  
  Like subtitles but also includes descriptions of important sound effects, speaker identification, and non-speech audio — specifically for deaf or hard-of-hearing users.

- **`<track kind="chapters">`**  
  Provides named chapter points. Chromium-based browsers render these as navigable segments on the seek bar.

- **`srclang`**  
  The language of the track content as a BCP 47 language tag (`"en"`, `"ur"`, `"fr"`).

- **`default`**  
  Marks the track that should be shown by default (if the browser decides to show one at all, based on user preferences).

- **`controlslist`**  
  Removes specific controls in Chromium browsers: `nodownload`, `nofullscreen`, `noremoteplayback`.

## Key Points / Notes

- Always provide `<track kind="captions">` for any video with dialogue — it's required for WCAG 2.1 Level AA accessibility compliance.
- The `.vtt` (WebVTT) format is simple plain text. Each cue has a timestamp range and the text to display: `00:00:05.000 --> 00:00:10.000` on one line, then the caption text below.
- `autoplay loop muted playsinline` is the exact combination for background hero videos. All four attributes are needed for cross-browser reliability.
- Video format guide: **MP4/H.264** — universal support. **WebM/VP9** — smaller files, same quality. **AV1** — best compression, limited older browser support. Always offer at least MP4 as a fallback.
- For large videos, use adaptive bitrate streaming (HLS or DASH) via a library like `hls.js` rather than a plain `<source>` — it adjusts quality based on the user's connection speed.
