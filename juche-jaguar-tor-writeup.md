# 🧅 TOR Challenge: "Problems in North TORbia" – CTF Write-up

**Challenge Name**: Problems in North TORbia  
**Category**: Web / OSINT / TOR  
**Points**: 150  
**Description**:  
> We were given a ransom note but none of our files were encrypted. Regardless, could you run it back and see what information could be gleaned from it?

---

## 🕵️ Step 1: Review the Ransom Note

We were provided with a `note.txt` file, which contained a threatening message supposedly from a hacker group called **JUCHE JAGUAR**.

### Contents of `note.txt` (snippet):

```
...
SEND PAYMENT TO:
http://jjpwn5u6ozdmxjurfitt42hns3qovikeyhocx5b2byoxgupnuzd2vkid.onion/
...
```

This `.onion` link is the main clue provided in the challenge.

---

## 🌐 Step 2: Access the .onion Website

Using the [Tor Browser](https://www.torproject.org/) or `torsocks` and `curl`, we accessed the provided link:

```
http://jjpwn5u6ozdmxjurfitt42hns3qovikeyhocx5b2byoxgupnuzd2vkid.onion/
```

The hosted page contained the following HTML structure:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>JUCHE JAGUAR</title>
    <link rel="stylesheet" href="styles.css">
<!-- MESS WITH US AND YOU GOT THE CLAUSE! -->
  </head>
  <body>
    <h1 class="typewriter">> You've been pwned by JUCHE JAGUAR</h1><br>
    <form class="hacker-form">
    <h2>SUBMIT YOUR RANSOM INFO</h2>
      <label for="first_name">First Name:</label><br>
      <input type="text" id="first_name" name="first_name"><br>
      <label for="surname">Last Name:</label><br>
      <input type="text" id="surname" name="surname"><br>
      <label for="email">Email:</label><br>
      <input type="text" id="email" name="email"><br>
      <label for="ransom_code">Ransom Code:</label><br>
      <input type="text" id="ransom_code" name="ransom_code"><br>
      <input type="hidden" id="send" name="ransom_code" value="ransom@ethtrader-ai.com">
      <input type="hidden" id="send_data" value="C1{h1dd3n_f13lds_0f_0n10ns}">
      <input type="submit" value="Submit">
    </form>
  </body>
</html>

```
---

## 🔐 Step 3: Locate the Flag

The flag was cleverly hidden in a `hidden` input field inside the HTML page source:

```html
<input type="hidden" id="send_data" value="C1{h1dd3n_f13lds_0f_0n10ns}">
```

---

## 🏁 Final Flag

```
C1{h1dd3n_f13lds_0f_0n10ns}
```

---

## ✅ Lessons Learned

- Always inspect the source code of onion services — flags are often hidden in plain sight.
- Look for `<input type="hidden">`, HTML comments, or JavaScript variables when doing static analysis.
- .onion links often serve as puzzles in themselves, even without full backend functionality.
- Check the challenge for clues, TORbia was a TOR browser giveaway.

---
