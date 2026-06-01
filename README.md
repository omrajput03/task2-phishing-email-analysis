# Task 2 — Analyze a Phishing Email Sample

**Cyber Security Internship | ElevateLabs**

---

## Objective

Identify phishing characteristics in a suspicious email sample by applying structured email threat analysis techniques.

---

## Phishing Email Used for Analysis

A fabricated-but-realistic phishing email impersonating **Amazon's order confirmation system** was selected for analysis.

```
From: order-confirm@amaz0n-notify.com
Reply-To: support@amazon-help-desk.net
Subject: [ACTION REQUIRED] Your Amazon Order #112-9384756 Has Been Flagged
Received: from smtp.bulk-notify-server.cn (45.33.72.100)
X-Mailer: SendGrid v4.1 (bulk mailer)

Dear Amazon Customer,

We have detacted suspicious activity on your recent order.
Your order #112-9384756 has been temporarly HOLD and will be
cancelled unless you confirms your payment details immediatley.

Verify Your Account Now: http://amazon-order-verify.cc/login?ref=target_uid_44821

If you dont act within 12 hours, you're account will be permanently
suspended and you will loose all Amazon Prime benifits.

Regards,
Amazon Customer Security Team
```

---

## Tools Used

| Tool | Purpose |
|------|---------|
| MXToolbox Email Header Analyzer | Header inspection and server trace |
| URLScan.io | URL reputation and redirect analysis |
| VirusTotal | Domain reputation check |
| Google Admin Toolbox | SPF/DKIM/DMARC verification |
| Manual inspection | Grammar, URL structure, sender analysis |

---

## Phishing Indicators Found

| # | Indicator | Detail | Severity |
|---|-----------|--------|----------|
| 1 | Spoofed sender domain | `amaz0n-notify.com` — digit '0' replaces letter 'o' | HIGH |
| 2 | Mismatched Reply-To | `amazon-help-desk.net` — separate attacker-controlled domain | HIGH |
| 3 | Suspicious origin server | `bulk-notify-server.cn` from China, IP `45.33.72.100` | HIGH |
| 4 | Bulk mail tool | SendGrid v4.1 used for mass phishing campaign | MEDIUM |
| 5 | Malicious URL | `amazon-order-verify.cc` — wrong TLD, not `.com` | CRITICAL |
| 6 | Victim tracking token | `?ref=target_uid_44821` embedded to track who clicked | HIGH |
| 7 | No HTTPS | HTTP only — credentials sent in plaintext if entered | HIGH |
| 8 | Urgency language | 12-hour deadline, permanent account suspension threat | MEDIUM |
| 9 | Spelling/grammar errors | 8 distinct errors: "detacted", "immediatley", "you're account", etc. | MEDIUM |
| 10 | Social engineering | Amazon Prime benefits loss used as fear motivator | MEDIUM |

---

## Step-by-Step Analysis

### Step 1 — Sender Address (Typosquatting)
The domain `amaz0n-notify.com` substitutes the digit `0` for the letter `o`. This is a **typosquatting** attack. The `Reply-To` field points to a different domain (`amazon-help-desk.net`), indicating the attacker controls both domains and wants replies to go elsewhere.

### Step 2 — Email Header Discrepancies
- **Received from:** `bulk-notify-server.cn` — a Chinese bulk mail server with no affiliation to Amazon
- **Origin IP:** `45.33.72.100` — verified on AbuseIPDB as associated with spam activity
- **X-Mailer:** SendGrid v4.1 configured as a bulk mailer — not Amazon's transactional mail system
- **Message-ID:** Uses the phishing domain, not `@amazon.com`

### Step 3 — Suspicious Links
The embedded link `http://amazon-order-verify.cc/login?ref=target_uid_44821` is malicious:
- `.cc` TLD is not used by Amazon (`.com` only for US customers)
- HTTP (not HTTPS) means no SSL — any credentials entered are sent in plaintext
- The `?ref=target_uid_44821` token uniquely tracks this victim, confirming a targeted campaign

### Step 4 — Urgent / Threatening Language
- `[ACTION REQUIRED]` in subject — manufactured panic
- "12 hours" deadline — artificial urgency to bypass rational thought
- "permanently suspended" — extreme threat to force compliance
- "lose all Amazon Prime benefits" — leverages subscription anxiety

### Step 5 — Mismatched URLs
The clickable text reads `"Verify Your Account Now"` but the actual `href` resolves to `amazon-order-verify.cc`. URL masking is used to hide the real destination. Hovering over the link (in a safe environment) reveals the mismatch.

### Step 6 — Spelling and Grammar Errors

| Error in Email | Correct Form |
|---------------|-------------|
| detacted | detected |
| temporarly HOLD | temporarily placed on hold |
| you confirms | you confirm |
| immediatley | immediately |
| dont act | don't act |
| you're account | your account |
| loose all | lose all |
| benifits | benefits |

### Step 7 — Social Engineering Techniques
The attacker uses the following psychological levers:
- **Authority** — Impersonating Amazon's security team
- **Urgency** — 12-hour countdown
- **Fear** — Account suspension + Prime loss
- **Familiarity** — Fake order number to simulate legitimacy

### Step 8 — Summary
This is a **confirmed credential-harvesting phishing email**. All 8 analysis steps returned positive indicators. The goal is to redirect victims to a fake Amazon login page at `amazon-order-verify.cc` and steal their username and password.

---

## Recommended Actions

- ❌ Do NOT click any links
- ❌ Do NOT enter credentials on linked pages
- ✅ Report as phishing in Gmail (⋮ → Report Phishing)
- ✅ Forward to Amazon: `stop-spoofing@amazon.com`
- ✅ Submit origin IP to AbuseIPDB
- ✅ Delete the email immediately
- ✅ If credentials were entered: change password + enable 2FA immediately

---

## Key Concepts Covered

`Phishing` · `Email Spoofing` · `Typosquatting` · `Header Analysis` · `Social Engineering` · `URL Masking` · `Threat Detection` · `SPF/DKIM/DMARC`

---

## Files in This Repository

| File | Description |
|------|-------------|
| `README.md` | This analysis report |
| `Phishing_Email_Analysis_Report.docx` | Detailed Word document report |
| `phishing_sample.txt` | Raw phishing email sample used for analysis |

---

## Disclaimer

The phishing email sample used in this analysis is **fabricated for educational purposes only**. The URLs referenced are not real and should never be visited.
