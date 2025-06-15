# 📁 `message.mp3` Challenge Write-Up  
**Challenge Concept:** Some messages aren’t meant to be _heard_ — they're meant to be _read_.

---

## 🕵️ Challenge Overview

In this challenge, we are presented with an audio file named `message.mp3`. The initial intuition might be to analyze the audio waveform, listen for hidden messages, or attempt steganographic decoding via spectrum analysis (e.g., using Audacity). However, this turns out to be a misdirection.

---

## 🔧 Tool Used: `ffprobe`

Instead of focusing on the audio content itself, the real trick is to inspect the **metadata** of the file. This can be done using `ffprobe`, a command-line tool that comes with FFmpeg and is used to retrieve information from media files.

---

## 🧪 Analysis with `ffprobe`

Command used:

```bash
ffprobe message.mp3
```

### Output:

```
Input #0, mp3, from 'message.mp3':
  Metadata:
    encoded_by      : C1{metadata_tells_more}
    encoder         : Lavf61.7.100
  Duration: 00:00:30.04, start: 0.025057, bitrate: 64 kb/s
  Stream #0:0: Audio: mp3, 44100 Hz, mono, fltp, 64 kb/s
```

The **flag** is hidden in the metadata under the `encoded_by` field:

```
C1{metadata_tells_more}
```

---

## ❌ Why Audacity or WAV Conversion Would Not Help

Audacity and WAV conversion tools focus on the *audible content* and visual waveform/spectrogram analysis. While they are excellent tools for uncovering:

- Hidden Morse code in frequency shifts
- Reversed audio
- Spliced voice data
- Subsonic messages

They do **not** show or preserve metadata like `encoded_by`, `artist`, or `comment` unless explicitly programmed to extract it. Converting the file to `.wav` would strip out MP3-specific metadata, and opening it in Audacity would just yield a 30-second empty/ambiguous waveform.

---

## ✅ Takeaway

This CTF challenge cleverly plays on the idea that _"not all messages are meant to be heard."_ Instead of following the obvious path (listening to or editing audio), it rewards lateral thinking and knowing your tools.

**The correct solve path was:**

```bash
ffprobe message.mp3
# or for more detail:
ffprobe -v quiet -show_format -show_streams message.mp3
```

**Flag:**

```
C1{metadata_tells_more}
```

---

## 🧠 Lessons Learned

- **Metadata is often overlooked** — check it in forensic investigations and CTFs.
- `ffprobe` can be more powerful than `strings` for media files.
- Sometimes, **less is more**: don’t overcomplicate with stego tools when a simple metadata check solves the challenge.
