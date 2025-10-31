
# 📂 Dropbox‑Centric n8n Workflows  
**30 ready‑to‑import, advanced n8n workflows** that turn Dropbox into a powerful automation hub for a wide range of niche use‑cases (reporting, notifications, data sync, content publishing, ops alerts, …).  

All workflows are **stand‑alone JSON files** (see the `*.json` files listed in the repository). After importing each file you only need to attach the required credentials and replace placeholder IDs/keys with your own values.

---  

## Table of Contents
| # | Workflow | Trigger | Destination / Action | Short description |
|---|----------|---------|----------------------|-------------------|
| 01 | **Daily Folder‑Size Audit** | Cron (02:00 UTC) | Google Sheets | Log size of every file in a Dropbox folder each day. |
| 02 | **New PDF Auto‑Summarizer** | Dropbox *file created* (`/incoming‑pdfs`) | Slack | Summarise PDF via OpenAI then post to a Slack channel. |
| 03 | **Media Asset Auto‑Tagger** | Cron (hourly) | Airtable | Send images through a Computer‑Vision API → store tags. |
| 04 | **Invoice Auto‑Catalog** | Dropbox *file created* (`/invoices`) | Notion | OCR → extract amount/date → create Notion page. |
| 05 | **Urgent Document SMS Alert** | Dropbox *file created* (`/urgent`) | Twilio SMS | If > 5 MB, shorten link via Bitly and SMS a list of numbers. |
| 06 | **Weekly Top‑10 Largest Files** | Cron (Mon 09:00) | Microsoft Teams | Post a markdown table with the biggest files. |
| 07 | **Legacy System Sync (Zapier)** | Dropbox *file created* (`/legacy‑sync`) | Zapier webhook | Forward metadata as JSON to a Zapier catch hook. |
| 08 | **Random Meme Generator** | Cron (every 6 h) | Telegram | Pick a random meme from `/memes` and send it. |
| 09 | **Bidirectional Drive Mirror** | Dropbox *file created* (`/mirror`) | Google Drive | Upload new files or update existing ones; keep a mapping. |
| 10 | **Contract Enricher** | Dropbox *file created* (`/contracts`) | HubSpot | Extract contract number → locate contact → create a deal. |
| 11 | **Shopify Product Media Upload** | Dropbox *file created* (`/shopify‑media`) | Shopify | Parse product ID from filename and add image to that product. |
| 12 | **Asana Task Attachment Auto‑Link** | Cron (30 min) | Asana | Attach files whose name contains `TASKID‑<num>` to the matching task. |
| 13 | **Freshdesk Ticket Attachment** | Dropbox *file created* (`/support`) | Freshdesk | Attach file to ticket based on `FD‑<num>` naming convention. |
| 14 | **ClickUp Design Review Queue** | Cron (hourly) | ClickUp | Create a task for each new design file (`.sketch/.fig`). |
| 15 | **Monday.com Asset Version Tracker** | Dropbox *file created* (`/assets`) | Monday.com | Store latest revision number and link. |
| 16 | **Calendly Meeting Material Distributor** | Webhook (Calendly event) | Email (SMTP) | Zip all files under `/meetings/<event‑id>` and email the invitee. |
| 17 | **Social Media Calendar Auto‑Populate** | Cron (07:00) | Airtable | Parse filenames like `2025-11-01_Instagram_Post.png` → calendar record. |
| 18 | **Data‑Lake Ingest Trigger (Pub/Sub)** | Dropbox *file created* (`/data‑lake/raw`) | Google Cloud Pub/Sub | Publish a base‑64 payload to a topic for downstream processing. |
| 19 | **S3 Backup** | Cron (every 4 h) | AWS S3 | Copy everything in `/backups` → S3 bucket, then archive locally. |
| 20 | **Docs Auto‑Commit to GitHub** | Dropbox *file created* (`/docs`) | GitHub | Commit new/updated markdown files to a repo. |
| 21 | **Zendesk Ticket Attachment** | Dropbox *file created* (`/zendesk‑uploads`) | Zendesk | Attach file to ticket based on `ticket‑<num>` naming convention. |
| 22 | **File‑Based Calendar Events** | Cron (07:00) | Google Calendar | Create an event from files named `YYYYMMDD_HHMM_Title.txt`. |
| 23 | **Power Automate Webhook Sync** | Dropbox *file created* (`/power‑automate`) | Power Automate HTTP trigger | POST minimal JSON payload to a Power Automate flow. |
| 24 | **JIRA Bug Report Attachment** | Dropbox *file created* (`/jira‑bugs`) | JIRA | Attach file to issue key parsed from filename (`PROJ‑1234_`). |
| 25 | **Trello Board Media Sync** | Cron (twice‑daily) | Trello | Turn Dropbox folder hierarchy `/Board/List/file` into cards. |
| 26 | **Confluence Knowledge Base Updater** | Dropbox *file created* (`/confluence‑content`) | Confluence | Create or update a page from `.md` / `.html` files. |
| 27 | **ElasticSearch File‑Metadata Indexer** | Cron (hourly) | ElasticSearch | Bulk‑index path, size, mime‑type, modification date. |
| 28 | **Airtable Delete Sync** | Dropbox *file deleted* (any path) | Airtable | Remove the matching Airtable row and email admin. |
| 29 | **Mailchimp Asset Delivery Campaign** | Cron (every 2 days) | Mailchimp | Build a campaign with download links for assets belonging to “segment A”. |
| 30 | **PagerDuty Critical Log Alert** | Dropbox *file created* (`/critical‑logs`) | PagerDuty & Email | If > 1 MB, raise a high‑urgency incident and notify ops via email. |

---  

## 🎯 Who is this for?
* Teams that already store data in **Dropbox** and want to push that data to other SaaS tools without writing code.  
* Ops / IT teams that need **real‑time alerts** when large or critical files appear.  
* Marketing / Content teams that need **automatic publishing / cataloguing** of assets.  
* Developers looking for **ready‑made reference workflows** that combine Dropbox with other APIs.

---  

## 📦 Prerequisites
| Requirement | Why it’s needed |
|-------------|-----------------|
| **n8n instance** (self‑hosted, desktop, or n8n.cloud) | To run the workflows. |
| **Dropbox OAuth / API token** | All workflows start with a Dropbox node. |
| **Credentials for every destination service** (Google Sheets, Slack, Airtable, etc.) | The nodes need authenticated API access. |
| **Optional external APIs** (OpenAI, Azure Computer Vision, Bitly, etc.) | Used in some workflows for summarisation, OCR, tagging, etc. |
| **Enough quota / storage** on the target services (e.g., S3 bucket, Google Drive folder) | To store the transferred files. |

> **Tip:** In n8n you can create a **“Dropbox OAuth2 API”** credential once and reuse it across all 30 workflows.

---  

## 🚀 Quick Start – Import a Workflow

1. **Download** the JSON you need (e.g., `01-dropbox-google-sheets-audit.json`).  
2. In n8n UI → **Workflows** → **Import** → **From JSON** → paste the content or upload the file.  
3. The workflow appears on the canvas.  
4. Click **Credentials** on each node that shows a warning sign and **select / create** the appropriate credential (e.g., Google Sheets API, Slack, Airtable, etc.).  
5. **Edit placeholder values** (IDs, channel names, bucket names, etc.).  
6. Click **Save** → **Activate** (or **Execute** manually to test).  

Repeat for any other workflow you wish to enable.

---  

## 🔧 Common Customisation Points

| Placeholder | Example | Where it appears |
|------------|----------|------------------|
| `YOUR_GOOGLE_SHEET_ID` | `1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms` | Google Sheets Append node |
| `YOUR_SLACK_CHANNEL` | `#alerts` | Slack Post node |
| `YOUR_OPENAI_KEY` | `sk-…` | HTTP Request → OpenAI Summarizer |
| `YOUR_COMPUTER_VISION_ENDPOINT` / `YOUR_COMPUTER_VISION_KEY` | `https://westus2.api.cognitive.microsoft.com/vision/v3.2/analyze` | Vision Tagging node |
| `YOUR_AIRTABLE_BASE_ID` / `tblAssets` | `app1234567890` | Airtable Upsert nodes |
| `YOUR_GITHUB_USERNAME` / `company-docs` | `jdoe` / `company-docs` | GitHub Commit node |
| `YOUR_PAGERDUTY_SERVICE_ID` | `P123456` | PagerDuty Create Incident node |
| `YOUR_BITLY_TOKEN` | `xxxxxxxxxxxx` | Bitly Shorten node |
| `YOUR_MAILCHIMP_LIST_ID` | `a1b2c3d4e5` | Mailchimp Create Campaign node |

You can also **adjust schedules** (cron expressions) or **add extra IF / error‑handling** nodes to fit your own SLA requirements.

---  

## 🛠️ How the Workflows Are Structured  

| Building block | Purpose |
|----------------|---------|
| **Trigger** (Cron, Webhook, Dropbox Trigger) | Starts the automation. |
| **List / Search / GetMetadata** (Dropbox) | Retrieves files or their meta‑data. |
| **IF / SplitInBatches** | Filters, limits batch size, or branches logic. |
| **Function / FunctionItem** | Lightweight JS for parsing filenames, regex extraction, converting binaries, etc. |
| **External API (HTTP Request)** | OpenAI, Google Vision, Bitly, Azure Computer Vision, etc. |
| **Set** | Normalises data and builds payloads for downstream services. |
| **Destination nodes** (Slack, Teams, Google Sheets, Airtable, Notion, HubSpot, etc.) | The final action (create row, post message, add attachment, etc.). |
| **Error Trigger / Email** | Optional notification when anything goes wrong. |

All workflows are **stateless** except where a mapping is stored (e.g., the Drive‑Mirror workflow uses a “Set” node to keep the Dropbox‑→‑Drive ID mapping). If you need persistent state beyond the run, you can replace that with **n8n’s Data Store** or an external DB.

---  

## 📚 Example: Extending Workflow 02 (PDF Summarizer)  

*Add a secondary notification to Microsoft Teams*  

1. Duplicate the **“Post to Slack”** node.  
2. Change the node type to **Microsoft Teams** (`n8n-nodes-base.microsoftTeams`).  
3. Update the **channel** and **text** as desired.  
4. Connect the new node to the **“Prepare Message”** node (parallel to the Slack node).  

Now every PDF summary will be posted to both Slack and Teams.

---  

## 📝 License  

The workflow JSON files are released under the **MIT License** – feel free to copy, modify, and redistribute them.  

---  

## 🤝 Contributing  

If you develop a new Dropbox‑centric workflow or improve an existing one:

1. Fork the repo.  
2. Add a new JSON file following the naming convention `nn‑short‑description.json`.  
3. Update the **README** table with a short description, trigger, and destination.  
4. Submit a Pull Request.  

We welcome contributions that broaden the niche use‑cases, add more robust error handling, or replace a free‑tier API with an open‑source alternative.

---  

## 📞 Support / Questions  

* **GitHub Issues** – Open a new issue for bugs or feature requests.  

---  

### Happy automating! 🚀  

*Let Dropbox do the heavy lifting while n8n orchestrates the rest.*
