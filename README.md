# PurifyPDF – Email-Based PDF Sanitizer

**PurifyPDF** is a privacy-first PDF sanitization workflow built using [n8n](https://n8n.io), [Postmark](https://postmarkapp.com), [PDF.co](https://pdf.co), and [Airtable](https://airtable.com).

Users send a PDF as an email attachment to `clean@yourdomain.com`, and the system returns a sanitized version, free of metadata, embedded scripts, and potentially unsafe content.

---

## 🚀 Demo

1. Send an email to `clean@yourdomain.com` with the subject: `register`
2. You’ll receive a verification link. Click to activate your email
3. Send another email with a PDF attached
4. Receive a sanitized version in your inbox

**Limits**  
- Max PDF size: 5 MB  
- Recommended page count: 25  
- Each user may sanitize up to 3 files

---

## 🧰 Tech Stack

- **n8n** – Orchestrates workflow logic
- **Postmark** – Handles incoming and outgoing emails
- **PDF.co** – Converts and rebuilds PDFs for sanitization
- **Airtable** – Tracks users, limits, and verification

---

## 🔒 Privacy

PurifyPDF never stores files permanently. All PDFs are purged automatically after one hour. Only metadata for usage tracking and verification is retained.

---

## 📁 Setup

### 1. Import the Workflow

Import `purifypdf.json` into your n8n instance.

### 2. Configure Credentials

Create credentials in n8n for the following:
- **Postmark (SMTP)** – for sending/receiving emails
- **PDF.co** – for PDF processing
- **Airtable Token** – for user tracking

### 3. Replace Placeholders

In the imported workflow, update:
- Webhook URLs with your n8n domain
- `demo@yourdomain.com` with your real service address
- Airtable base and table IDs

---

## 📦 Files

- `purifypdf.json` – Main workflow file

---

## 🙋‍♀️ Contributing

Feel free to fork, customize, and extend for your own use case. Pull requests are welcome!

---

## 🔐 Required Credentials

Before importing the workflow, create the following credentials in n8n:

### Postmark (SMTP)
- Service: Postmark
- Type: SMTP or API
- Credentials: Use your Postmark server token or SMTP credentials

### Airtable
- Type: Personal Access Token
- Scopes: `data.records:read` and `data.records:write`
- Base ID and Table ID: Find these in your Airtable API URL

### PDF.co
- Create a free or paid API key at [https://app.pdf.co](https://app.pdf.co)
- Add as an HTTP Header credential with:
  - Header Name: `x-api-key`
  - Value: `YOUR_PDFCO_API_KEY`

---

## ⚙️ Requirements

- A running instance of n8n (self-hosted or Cloud)
- A verified domain for receiving inbound email via Postmark
- Airtable base and table set up as described below
- PDF.co API key with available credits

---

## 🌐 Webhook Setup

Ensure the following webhook URLs are accessible and mapped correctly:

- `/webhook/user-verification` – Confirms user email tokens
- `/webhook/email-ingest` – Handles incoming Postmark emails with attachments

If you're using **n8n Cloud**, these URLs are public by default.  
If you're **self-hosting**, make sure your instance is HTTPS-enabled and reachable from Postmark.

---

## ✉️ Postmark Email Routing

To receive inbound emails:

1. Log into [Postmark](https://postmarkapp.com) and create a Transactional Server
2. Go to **Settings → Inbound** and add your domain (e.g. `@yourdomain.com`)
3. Add the required MX and TXT records to your DNS
4. Set the Inbound Webhook URL to:
   ```
   https://your-n8n-instance.com/webhook/email-ingest
   ```

Once DNS is verified, emails sent to addresses like `clean@yourdomain.com` will trigger your workflow.

## 🗂 Airtable Structure

This workflow expects a table to track users, verification, and usage limits.

### Table: `Users`

| Field Name           | Type             | Description                                  |
|----------------------|------------------|----------------------------------------------|
| `email`              | Single line text | The user's email address                     |
| `verified`           | Checkbox         | True if the user has completed verification  |
| `verificationToken`  | Single line text | One-time token for email verification        |
| `tokenExpiry`        | Date             | When the verification link expires           |
| `pdfCount`           | Number           | Number of PDFs sanitized by this user        |
| `pdfLimit`           | Number           | Max PDFs allowed (e.g. 3 for demo users)     |
| `verifiedAt`         | Date             | Timestamp of successful verification         |

> Tip: Set a default value of `3` for `pdfLimit` if you're enforcing demo limits.

## 📜 License

The name **PurifyPDF** and associated branding (e.g., logo, domain name) are not covered by the MIT license and may not be used without permission.

MIT – Free to use, modify, and share.
