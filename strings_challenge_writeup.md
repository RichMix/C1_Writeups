# Hardcoded Config Challenge – Quick Write‑Up

## Overview  
The binary `hardcodedlies` contains a hard‑coded configuration string (flag) buried in its data section. The clue _“pull on some strings”_ suggests using the classic **`strings`** technique.

---

## Step‑by‑Step Solution (Terminal)

| Step | Command | Result / Notes |
|------|---------|----------------|
| 1 | `file hardcodedlies` | Confirms it is an executable (≈33 KB). |
| 2 | `strings -n 4 hardcodedlies \| less` | Dumps all printable sequences ≥ 4 bytes. |
| 3 | `/`<kbd>c1{</kbd> **inside _less_** <br>or:<br>`strings -n 4 hardcodedlies \| grep -i "c1{"` | Finds:<br>`C1{h4rdc0ded_but_0verlooked}` |
| 4 | Submit the flag | **Flag:** `C1{h4rdc0ded_but_0verlooked}` |

**One‑liner extraction**

```bash
strings -n 4 hardcodedlies | grep -o 'C1{[^}]*}'
```

---

## Strings Dump vs. CyberChef “Strings” Operation

| Terminal `strings` | CyberChef “Strings” recipe |
|--------------------|----------------------------|
| Runs locally, scriptable, no upload risk | Browser‑based GUI, easy for quick visual checks |
| Chainable with `grep`, `awk` for automation | Can build multi‑step pipelines visually |
| Ideal for large files & CTF speed runs | Good when you need interactive exploration |

Both methods reveal the **same content**:

```
Initializing network interface...
C1{h4rdc0ded_but_0verlooked}
```

---

## Key Take‑aways

* **Always try `strings` first** on unfamiliar binaries—flags, URLs, keys, and debug lines often sit in plain text.  
* Combine `strings` with Unix text filters for lightning‑fast triage.  
* CyberChef remains excellent for interactive, multi‑operation analysis, but the humble CLI often wins in time‑pressured CTF play.

Happy hacking! 🏴‍☠️
