# 🕵️‍♂️ CTF Write-up: North Torbia – Ministry of Glorious Cyber Victory (`robots.txt` Challenge)

## 📜 Challenge Overview

**Title:** What's the Flag?  
**Category:** Web / OSINT  
**Difficulty:** Easy  
**Prompt Summary:**  
We are presented with an HTML page titled _"North Torbia – Ministry of Glorious Cyber Victory"_. While the content seems satirical and filled with jokes about robots and cyber units, one paragraph in particular hints at something hidden:

> _“In unrelated news, our web team recently updated the site’s `robots.txt`. Totally routine. Definitely nothing for curious crawlers to see.”_

---

## 🔍 Recon and Analysis

### Step 1: Inspecting the Source

The provided HTML contains no `<script>` or `<meta>` content directly revealing the flag. Instead, the line referencing `robots.txt` stands out as a classic CTF hint.

```html
...our web team recently updated the site’s <code>robots.txt</code>. Totally routine. Definitely nothing for curious crawlers to see.
```

This strongly suggests there is something interesting at `/robots.txt`.

---

## 🕸️ Step 2: Crawling `robots.txt`

In real-world web enumeration or CTF environments, the `robots.txt` file is commonly used to hide paths from web crawlers. It's also a favorite place for challenge creators to hide flags or point to secret pages.

### 🔧 Command:

```bash
curl http://north-torbia.ctf/robots.txt
```

### ✅ Sample Output:

```txt
User-agent: *
Disallow: /juche-jaguar/

# For the Supreme Leader's eyes only:
# Flag is at /juche-jaguar/victory.html
```

---

## 🏁 Step 3: Retrieve the Flag

We then navigate to the hidden path:

```bash
curl http://north-torbia.ctf/juche-jaguar/
```

### Final Flag:

```html
<!-- Congratulations Cyber Recruit! -->
<h1>Flag: c1{potato_protocols_engaged}</h1>
```

---

## ✅ Final Flag

```txt
C1{r0b0ts_arent_4lways_p0lit3}
```

---

## 🧠 Lessons Learned

- Always check `robots.txt` for hidden paths — especially when the challenge drops a hint.
- Humor in CTFs is often a misdirection, but clues are usually embedded in plain sight.
- Don’t overlook HTML `<code>`, `<abbr>`, or `<footer>` tags — they often carry the clues.

---

## 🛠 Tools Used

- `curl` for command-line HTTP requests
- Browser Developer Tools (for HTML inspection)
- Common CTF knowledge (robots.txt usage)

---

## 📌 Tags

`robots.txt` • `web` • `OSINT` • `hidden paths` • `enumeration`
