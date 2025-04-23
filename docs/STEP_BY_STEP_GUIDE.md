# Customer-Support-Ticket-Resolver-with-AI

# Google Cloud and Gmail Setup Guide for Customer Support AI Responder

## 1. Create a Google Cloud Project
1. Visit: [https://console.cloud.google.com/](https://console.cloud.google.com/)
2. Click on **“Create Project”**, give it a name.
3. After it's created, open your project.

---

## 2. Enable Google Sheets & Drive API
Navigate to **APIs & Services > Library**:
- Search and Enable:
  - **Google Sheets API**
  - **Google Drive API**

---

## 3. Create a Service Account
1. Go to **IAM & Admin > Service Accounts**
2. Click **"Create Service Account"**
   - Give it a name like `sheet-access-bot`
   - Click **Create and Continue**
   - Grant role: **Editor** (or more limited if needed)
   - Finish creation

---

## 4. Create & Download JSON Key
1. After the service account is created → Click it
2. Go to **“Keys” > “Add Key” > “Create new key”**
3. Choose **JSON**
4. Download the file — name it `google_creds.json`
5. Move it to your project root

---

## 5. Share the Sheet with Service Account
1. Open your Google Sheet (e.g., `SupportTickets`)
2. Click **Share**
3. Paste the service account email (from JSON file, looks like: `sheet-access-bot@your-project.iam.gserviceaccount.com`)
4. Give **Editor** access

---

## Step 1: Use App Password — NOT your Gmail password
Google blocks standard password-based login via SMTP.  
Instead, you must use a special **App Password**.

---

## How to Set It Up (Safe & Easy)

### 1. Enable 2-Step Verification
If not done yet:
- Go to: [https://myaccount.google.com/security](https://myaccount.google.com/security)
- Turn **ON** 2-Step Verification

---

### 2. Generate Gmail App Password
Go to: [https://myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)

- Select:
  - **App:** "Mail"
  - **Device:** "Other" → Name it `TicketBot`
- Click **Generate**
- Copy the **16-character password** Google gives you
