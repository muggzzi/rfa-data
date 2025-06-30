# Restore Fair Access™: FAR Comment System - Transfer Summary

## 📌 Project Purpose

This project supports the **Restore Fair Access™** campaign by enabling small business owners to submit personalized comments on the Revolutionary FAR Overhaul directly to the FAR Council via GSA web forms. The system then transitions users to contact Congress, leveraging integrated congressional lookup and economic data.

---

## 🧭 Core Flow Overview

1. **User Intake** at `/take-action-far-council`
   - Collects name, title, company, address, personal story
   - Uses Geocodio API to determine congressional district
   - Pulls district data from Google Sheets
   - Stores data in `sessionStorage`

2. **Comment Submission Loop** at `/take-action-far-parts`
   - Loads list of FAR Parts with active deadlines from a live JSON feed
   - Walks user through each comment: explainer, pre-filled comment, GSA link
   - Submits form acknowledgment via Google Apps Script backend
   - Sends confirmation email and logs submission timestamp to Google Sheets

3. **Thank You + Congressional Outreach**
   - Redirects to `/take-action-far-council-thank-you`
   - Thanks the user and presents their representatives and action steps
   - Ready to email/call elected officials using the pre-built data

---

## ⚙️ Tools and Platforms Used

| Tool/Platform       | Purpose                                                                 |
|---------------------|-------------------------------------------------------------------------|
| **Squarespace**     | Hosts public pages and HTML blocks                                      |
| **Geocodio API**    | Converts full address to congressional district                         |
| **Google Sheets**   | Stores district-level data + submission logs                            |
| **Google Apps Script** | Backend logic for email and spreadsheet updates                    |
| **Cloudflare Workers** | Proxy to overcome Squarespace fetch security restrictions          |
| **GitHub (muggzzi/rfa-data)** | Stores live JSON data and campaign source files            |
| **JavaScript (in-browser)** | Frontend interaction and comment generation logic             |

---

## 🔗 Live Data Links

- District + Economic Data Sheet:  
  `https://docs.google.com/spreadsheets/d/1FBY_BRQsiDK6vnZ-W_q33Tj7pX_32TwFWCoepfeO6ok/edit#gid=1459322906`

- JSON Feed for FAR Parts:  
  `https://raw.githubusercontent.com/muggzzi/rfa-data/refs/heads/main/RFA_FARParts_Steps_MASTER_9PARTS_GSAFIXED.json`

- Cloudflare Proxy URL:  
  `https://rfa-far-proxy.muggzzi.workers.dev`

- Apps Script Webhook:  
  `https://script.google.com/macros/s/AKfycbwJ0epu01xeKBOVdnCziCxrSDxfu-gveh9xalZeaNscSEH7PjMVuFWBXnb9Sn097eIV/exec`

---

## 🛠️ Current Technical Status

- ✅ Squarespace flow working: form → comment → thank you
- ✅ Proxy resolved previous JSON load errors
- ✅ Emails send per part
- ✅ Submission logs update Google Sheets
- ⚠️ Minor issues remain:
  - Progress bar styling needs final tweak
  - Need to deploy working “Contact Congress” follow-up section
  - Add fallback if no FAR Parts are live

---

## 📁 Recommended Files for This Repo

Structure your repo like this:

```
rfa-data/
│
├── docs/
│   └── Transfer_Summary.md     ← this file
│
├── data/
│   ├── RFA_FARParts_Steps_MASTER_9PARTS_GSAFIXED.json
│   ├── district-data.csv
│
├── scripts/
│   ├── take-action-far-council.html
│   ├── take-action-far-parts.html
│   ├── google-apps-script.gs
│   └── cloudflare-worker.js
```

---

## 📌 Final Notes

This session reflects over 14 hours of collaborative development. The core system now functions from intake to email logging. Additional upgrades for UX, contact Congress integration, and responsiveness remain planned.

Please preserve this summary for all future sessions or developer handoffs.

— *Restore Fair Access™ Project (ChatGPT Assist)*
