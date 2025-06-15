
# 🎧 CTF Challenge Write-up: Listening Post (150 Points)

## 🧠 Challenge Summary

> _"We've intercepted a radio broadcast being bounced off a satellite likely intended for the North Torbian cells located around the world. Do you think you can unravel what they are transmitting?"_

Two files were provided:
- `radio.wav`
- `radio.mp3`

The files were audibly identical, just in different formats.

---

## 🔍 Initial Analysis

Listening to the audio revealed a familiar sequence of **beeping tones**, reminiscent of old telephone dial tones. These are known as **DTMF** (Dual-tone multi-frequency) signals, commonly used in telecommunication systems to encode digits and characters.

---

## 🛠️ Tools Used

- [DTMF Decoder Web Tool](https://unframework.github.io/dtmf-detect/#/)
- CyberChef (for binary-to-text decoding)

---

## 🧪 Step-by-Step Solution

### 1. Upload and Decode DTMF

Using the tool linked above, I uploaded the `.mp3` file. It automatically decoded the beeps into a binary string:

```
0100001100110001011110110111001000110100011001000011000101101111010111110110101100110001011011000110110000110011011001000101111101110100011010000011001101011111011101000011000001110010011000100011000101100001010111110111001101110100001101000111001001111101
```

### 2. Convert Binary to ASCII

Pasting the binary into [CyberChef](https://gchq.github.io/CyberChef/) and running “From Binary” yielded:

```
C1{r4d1o_k1ll3d_th3_t0rb1a_st4r}
```

---

## 🏁 Final Flag

```
C1{r4d1o_k1ll3d_th3_t0rb1a_st4r}
```

---

## ✅ Takeaways

- Recognizing **DTMF tones** by ear was critical to solving this challenge.
- Online tools like the DTMF Decoder are invaluable for niche signal decoding.
- Binary decoding is often the final step in converting machine-encoded messages into human-readable flags.

---
