# 🕵️ Packet Whisperer – CTF Write-Up

**Category:** Network Forensics  
**Points:** 75  
**Challenge Prompt:**  
> Our blue team intercepted a network capture file. It contains unencrypted HTTP traffic. While skimming through it, analysts believe someone accidentally exposed their login credentials in plain text. Review the PCAP to find the password that the user logged in with.

---

## 🔍 Objective

Analyze a `.pcap` network capture to identify credentials (specifically the password) that were exposed in plain text via unencrypted HTTP traffic.

---

## 🧰 Tools Used

- `Python` (file parsing)
- Raw byte analysis
- Regex pattern matching
- URL decoding

---

## 🧪 Steps to Solve

1. **Initial Inspection**  
   The `.pcap` file was loaded and searched for any HTTP traffic or strings related to login attempts, such as `username`, `password`, or `POST`.

2. **Manual Byte Search**  
   Due to lack of advanced libraries (`scapy`, `pyshark`, `tshark`) in the environment, we searched the PCAP byte stream directly using Python's `open()` and `read()`.

3. **Regex Credential Discovery**  
   We ran regex to find patterns matching typical HTTP POST bodies such as:
   ```
   username=...&password=...
   ```
   This pattern was found inside the PCAP byte stream.

4. **Captured POST Data**
   ```
   username=ironpotatoadmin&password=C1%7Bmaybe_TLS_would_be_nice%7Dzn<h~B
   ```

5. **URL Decode the Password**
   The password field was URL-encoded:
   ```
   C1%7Bmaybe_TLS_would_be_nice%7D → C1{maybe_TLS_would_be_nice}
   ```

---

## 🏁 Final Answer

```
C1{maybe_TLS_would_be_nice}
```

---

## 💡 Takeaways

- Unencrypted HTTP traffic is highly insecure for transmitting credentials.
- PCAP analysis is a powerful method for digital forensics when interception is possible.
- Even basic byte and regex searches can reveal sensitive data in network captures.

---
