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

Import `purifypdf_sanitized_final.json` into your n8n instance.

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

- `purifypdf_sanitized_final.json` – Main workflow file

---

## 🙋‍♀️ Contributing

Feel free to fork, customize, and extend for your own use case. Pull requests are welcome!

---

## 📜 License

The name **PurifyPDF** and associated branding (e.g., logo, domain name) are not covered by the MIT license and may not be used without permission.

MIT – Free to use, modify, and share.