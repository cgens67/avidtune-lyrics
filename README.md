# AvidLyrics

AvidLyrics is the official custom lyrics repository for **AvidTune**. It serves as a decentralized, fast, and free database of synchronized `.lrc` files mapped to specific tracks using their unique Song IDs.

To deliver these lyrics efficiently and prevent API rate limits, AvidTune fetches files from this repository using the [jsDelivr CDN](https://www.jsdelivr.com/).

---

## 📂 Repository Structure

The repository is structured dynamically to ensure fast queries:

```text
avidtune-lyrics/
├── lyrics/
│   ├── dQw4w9WgXcQ.lrc      <-- Named using unique Song/Video IDs
│   └── [Another_ID].lrc
└── README.md
```

---

## 🚀 How It Works in AvidTune

When a song plays, AvidTune queries this repository via CDN using the unique identifier (`id`) of the active track:

```text
https://cdn.jsdelivr.net/gh/cgens67/avidtune-lyrics@main/lyrics/{id}.lrc
```

If a matching file is found, it is parsed instantly and synchronized with the music player UI.

---

## ✍️ How to Add or Contribute Lyrics

If you want to add new synchronized lyrics or correct existing ones:

1. **Find the Song ID**: Identify the unique ID of the track inside AvidTune (usually the YouTube Video ID from the track URL).
2. **Create the Lyric File**: Create a text file containing the synchronized lines.
3. **Format the File**: Ensure standard LRC timestamp formats are used (details below).
4. **Save the File**: Save the file in the `lyrics/` directory and name it exactly `{Song_ID}.lrc` (for example, `lyrics/dQw4w9WgXcQ.lrc`).
5. **Commit & Push**: Submit a pull request or push your changes to the `main` branch.

---

## 📝 Lyrics Formatting Guide

AvidLyrics supports both standard synchronized lyrics and advanced multi-voice layouts supported by AvidTune's advanced lyric renderer.

### 1. Standard Synchronized Lyrics
Lines should start with standard minutes, seconds, and centiseconds timestamps.

```text
[00:00.00]This is an instrumental intro
[00:15.30]We're no strangers to love
[00:19.40]You know the rules and so do I
```

### 2. Multi-Voice and Duets (`{agent:vX}`)
To assign specific lines to different parts of the screen (e.g. Left/Right alignment for duets), prefix the text with `{agent:v1}` or `{agent:v2}`:

```text
[00:30.20]{agent:v1}I believe in you
[00:32.40]{agent:v2}And I believe in us
```

### 3. Background Vocals (`{bg}`)
To format background vocals or overlapping voices differently (e.g., italics, lower opacity, or smaller text size in the UI), prefix the line with `{bg}`:

```text
[00:45.00]Gotta make you understand
[00:47.10]{bg}(Never gonna give you up)
```

---

## ⚡ Technical Details & Caching

Because lyrics are served via jsDelivr, there can be a brief delay (up to 24 hours) for CDN caches to update globally after a file is modified on GitHub. 

To force-clear the cache for a specific file during testing, you can access the jsDelivr purge API:
```text
https://purge.jsdelivr.net/gh/cgens67/avidtune-lyrics@main/lyrics/{id}.lrc
```
