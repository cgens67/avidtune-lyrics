# AvidLyrics

AvidLyrics is the official custom lyrics repository for **AvidTune**. It serves as a fast and free database of synchronized `.lrc` files mapped to specific tracks using their unique Song IDs or formatted Song Titles.

To ensure that newly added or edited lyrics are available instantly to users, AvidTune fetches these files directly from GitHub Raw, intelligently bypassing cache delays.

---

## 📂 Repository Structure

The repository is structured into two main directories to allow flexible querying:

```text
avidtune-lyrics/
├── lyrics/
│   ├── dQw4w9WgXcQ.lrc      <-- Named using exact YouTube Video IDs
│   └── sorted/
│       ├── billie_jean.lrc  <-- Fallbacks named using formatted song titles
│       └── yourockmyworld.lrc
└── README.md
```

---

## 🚀 How It Works in AvidTune

When a song plays, AvidTune queries this repository directly from GitHub Raw. To ensure maximum compatibility, it attempts to find the lyrics in a specific priority order:

1. **Exact Video ID**: `lyrics/pAyKJAtD5O4.lrc`
2. **Cleaned Title (Underscores)**: `lyrics/sorted/you_are_not_alone.lrc` *(Parentheses like "(Official Video)" are stripped)*
3. **Cleaned Title (No Spaces)**: `lyrics/sorted/youarenotalone.lrc`
4. **Raw Exact Title**: `lyrics/sorted/You_Are_Not_Alone_(Official_Video).lrc`

The URL requested looks like this:
```text
https://raw.githubusercontent.com/cgens67/avidtune-lyrics/main/[PATH]?t=[TIMESTAMP]
```
It stops and loads the lyrics as soon as one of the paths returns a successful match.

---

## ✍️ How to Add or Contribute Lyrics

If you want to add new synchronized lyrics or correct existing ones:

1. **Identify the Song**: Find the exact Video ID or the Song Title.
2. **Create the Lyric File**: Create a text file containing the synchronized lines.
3. **Format the File**: Ensure standard LRC timestamp formats are used (details below).
4. **Save the File**: 
   - If using the **Video ID**: Save it in the `lyrics/` directory (e.g., `lyrics/dQw4w9WgXcQ.lrc`).
   - If using the **Song Title**: Save it in the `lyrics/sorted/` directory (e.g., `lyrics/sorted/never_gonna_give_you_up.lrc`).
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

**No More Caching Delays!** 
Previously, AvidLyrics used a CDN which caused up to 12 hours of caching delay for edits. AvidTune now queries GitHub Raw directly and appends a dynamic timestamp (`?t=[CURRENT_TIME_MS]`) to every request. 

This completely bypasses GitHub's 5-minute cache, meaning any committed `.lrc` file will be **instantly available** in the AvidTune app the moment the repository is updated.
