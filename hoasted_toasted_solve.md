# 🍞 Hoasted Toasted CTF Challenge Write-Up

## Challenge Overview

The task involved investigating a publicly available website that hinted at a hidden internal-only site:

```
https://not-torbian.ethtrader-ai.com
```

Hints suggested that unusual digital signatures or SSL certificates might be involved in revealing the hidden internal site.

---

## Step-by-Step Solution

### 1. Inspecting SSL Certificate

Using `openssl`, we inspected the website’s SSL certificate:

```bash
openssl s_client -connect not-torbian.ethtrader-ai.com:443 -showcerts
```

This revealed crucial details:

```plaintext
Subject Alternative Name:
definitelynotaflag.north.torbia
```

**Initial curl attempt (before hosts modification):**

```bash
curl https://definitelynotaflag.north.torbia -k
# curl: (6) Could not resolve host: definitelynotaflag.north.torbia
```

**Incorrect openssl command attempt:**

```bash
openssl s_client -connect https://definitelynotaflag.north.torbia -showcerts
# BIO_lookup_ex error due to incorrect usage
```

### 2. Resolving the Internal Domain

Since `north.torbia` isn't a publicly resolvable domain, we manually edited the system hosts file:

```bash
sudo nano /etc/hosts
```

And added:

```
34.86.60.228 definitelynotaflag.north.torbia
```

### 3. Accessing the Hidden Site

With the domain resolved locally, we successfully accessed the hidden site via `curl`:

```bash
curl https://definitelynotaflag.north.torbia -k
```

The `-k` flag bypassed certificate verification due to a self-signed certificate.

---

## 🚩 Flag Found

Upon accessing the hidden internal portal, the following flag was obtained:

```
C1{vH0st_S4n_M4g1c_R3ve4l3d}
```

---

## 🛠️ Tools & Techniques

- **SSL Certificate Inspection:** Using `openssl s_client`
- **Hosts File Modification:** Manual DNS resolution
- **Virtual Host Enumeration:** Leveraging certificate information for vHost discovery

---

## ✅ Conclusion

This challenge highlighted the importance of SSL certificate inspection and internal DNS manipulation in discovering hidden web resources.

