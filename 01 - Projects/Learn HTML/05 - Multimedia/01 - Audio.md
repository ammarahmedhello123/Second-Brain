```html
<!-- Basic audio player with controls -->
<audio controls>
  <source src="podcast.mp3"  type="audio/mpeg" />
  <source src="podcast.ogg"  type="audio/ogg" />
  <source src="podcast.webm" type="audio/webm" />
  <p>Your browser does not support the audio element. <a href="podcast.mp3">Download it instead.</a></p>
</audio>

<!-- Autoplay background audio (must be muted to autoplay) -->
<audio src="ambient.mp3" autoplay loop muted></audio>

<!-- All available attributes -->
<audio
  src="track.mp3"
  controls
  autoplay
  loop
  muted
  preload="metadata"
  controlslist="nodownload"
>
</audio>

<!-- Programmatic control via JavaScript -->
<audio id="player" src="music.mp3"></audio>
<button onclick="document.getElementById('player').play()">Play</button>
<button onclick="document.getElementById('player').pause()">Pause</button>
<button onclick="document.getElementById('player').volume = 0.5">Half Volume</button>
```

# Explanation

The `<audio>` element embeds sound content directly in the page without any plugin. It can display a native browser player with controls, or be driven entirely by JavaScript. Multiple `<source>` formats ensure the widest browser compatibility.

## Breakdown

- **`controls`**  
  Renders the browser's built-in audio player UI — play/pause button, progress bar, volume, and sometimes a download button. Without `controls`, the element is invisible and can only be controlled via JavaScript.

- **`<source>`**  
  Provides alternative audio files in different formats. The browser picks the first one it can play. Order matters — put your preferred format first. Providing `type` lets the browser skip formats it can't play without downloading the file to check.

- **Fallback content**  
  Text or links between the `<audio>` tags are shown only if the browser doesn't support the element at all. A download link is a good fallback for older browsers.

- **`autoplay`**  
  Starts playback immediately on page load. Most browsers block `autoplay` with sound — the user must have interacted with the page first, or the audio must be `muted`. Never autoplay audio with sound — it's jarring and disrespectful UX.

- **`loop`**  
  Restarts audio from the beginning when it ends. Useful for background music or ambient sound.

- **`muted`**  
  Starts playback silenced. Required for `autoplay` to work reliably. The user can unmute manually.

- **`preload`**  
  Hints to the browser how much to load before playback:  
  - `"none"` — don't load until the user plays.  
  - `"metadata"` — load only duration, size, and first frame.  
  - `"auto"` — browser decides (may load the whole file).  
  Default varies by browser.

- **`controlslist="nodownload"`**  
  Removes the download option from the native controls in Chromium browsers. Non-standard but widely supported.

- **JavaScript API**  
  The `<audio>` element exposes a full JS API — `.play()`, `.pause()`, `.volume`, `.currentTime`, `.duration`, `.muted`, `.playbackRate`, and events like `timeupdate`, `ended`, `error`.

## Key Points / Notes

- Audio format compatibility: **MP3** works everywhere. **OGG Vorbis** was the Firefox alternative. **WebM/Opus** has excellent quality at smaller sizes. For maximum compatibility, supply MP3 + one modern format.
- `autoplay` with sound is blocked by all major browsers by default and is considered hostile UX. Don't do it.
- The browser's default audio player UI cannot be fully styled with CSS. For custom-styled players, hide the controls and build your own UI using the JavaScript API.
- `preload="metadata"` is the best default for most use cases — it loads just enough to show duration without wasting bandwidth on files the user may never play.
- CORS restrictions apply to audio files loaded from a different domain. If JavaScript needs to analyse the audio (e.g., Web Audio API), the server must send the correct `Access-Control-Allow-Origin` header.
