# 🎯 Lead Generation System

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io/)
[![Airtable](https://img.shields.io/badge/Airtable-Database-blue)](https://airtable.com/)
[![AI Powered](https://img.shields.io/badge/AI-Powered-brightgreen)](https://github.com)

> **Complete B2B lead generation machine combining Apollo.io, Google Search, LinkedIn scraping, and AI-powered qualification into one automated system.**


## 🎬 Demo Video

### See the Full System in Action

<div align="center">

  <a href="https://youtu.be/8sg8xINL4iQ">
    <img src="https://img.https://youtu.be/8sg8xINL4iQ/maxresdefault.jpg" alt="Facebook Ad Manager - Complete Demo" width="100%">
  </a>

  <br><br>

  <a href="https://www.youtube.com/watch?v=Z_zoyLifS1s">
    <strong>▶️ Watch Full Demo on YouTube (5 minutes)</strong>
  </a>

</div>




Generate, enrich, and qualify thousands of high-quality B2B leads automatically. This intelligent system finds prospects from multiple sources, enriches profiles with complete data, and scores lead quality using AI.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Five Automated Workflows](#-five-automated-workflows)
- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage Guide](#-usage-guide)
- [Airtable Structure](#-airtable-structure)
- [API Configuration](#-api-configuration)
- [Lead Qualification](#-lead-qualification)
- [Troubleshooting](#-troubleshooting)
- [Best Practices](#-best-practices)
- [License](#-license)

---

## 🎯 Overview

**Lead Generation System** is an enterprise-grade automation that combines multiple lead sources and enrichment methods into a single, intelligent workflow. It scrapes leads from Apollo.io, finds prospects via Google Search, enriches all profiles with LinkedIn data, and uses AI to qualify leads against your Ideal Customer Profile (ICP).

### Who Is This For?

- 🏢 **B2B Sales Teams** - Scale prospecting from dozens to thousands of leads
- 📈 **Marketing Agencies** - Build targeted prospect lists for clients
- 💼 **Growth Teams** - Automate entire lead generation pipeline
- 🚀 **Startups** - Compete with enterprise-level prospecting capabilities
- 👥 **SDR Teams** - Focus on outreach instead of manual research

### The Problem It Solves

Traditional B2B lead generation requires:
- Manually searching Apollo or LinkedIn Sales Navigator
- Copying data into spreadsheets one by one
- Researching company websites for qualification
- Scoring leads subjectively
- **Days of work for hundreds of leads**

This system automates everything in **hours**, processing thousands of leads with consistent quality and AI-powered scoring.

---

## ✨ Key Features

### 🔄 **Multi-Source Lead Generation**
- Apollo.io search result scraping
- Google Search for LinkedIn profiles
- Dual-channel approach maximizes coverage
- Configurable lead limits per campaign

### 🔍 **Comprehensive Lead Enrichment**
- Full LinkedIn profile scraping via Apify
- Company website data extraction
- 25+ data fields per lead
- Mobile numbers and emails
- Work experience history
- Company size and details

### 🤖 **AI-Powered Lead Qualification**
- Google Gemini analyzes each lead
- Scores 0-10 based on ICP fit
- Considers job title, company type, size, location
- Analyzes website content automatically
- Natural language ICP definitions

### 📊 **Intelligent Data Management**
- Organized Airtable base structure
- Campaign-based lead organization
- Automatic status tracking
- ICP details stored with each lead
- Easy export to CRM systems

### ⚡ **Flexible Workflow Routing**
- 5 distinct workflow paths
- Webhook-triggered automation
- Process leads from any source
- Enrich existing databases
- Qualify pre-scraped leads

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      WEBHOOK TRIGGER                             │
│              (Single endpoint, multiple actions)                 │
└───────────────────────┬─────────────────────────────────────────┘
                        │
                        ↓
┌─────────────────────────────────────────────────────────────────┐
│                    SWITCH ROUTER                                 │
│          Directs to appropriate workflow branch                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. ScrapeApollo                                                │
│  2. EnrichApolloProfiles                                        │
│  3. ScrapeLinkedInProfiles                                      │
│  4. EnrichLinkedInProfiles                                      │
│  5. QualifyLeads                                                │
│                                                                  │
└───────────────────────┬─────────────────────────────────────────┘
                        │
            ┌───────────┴───────────┐
            │                       │
            ↓                       ↓
┌─────────────────────┐  ┌─────────────────────┐
│  APOLLO WORKFLOW    │  │ LINKEDIN WORKFLOW   │
├─────────────────────┤  ├─────────────────────┤
│                     │  │                     │
│ • Scrape Apollo     │  │ • Build Google Query│
│ • Extract Leads     │  │ • Search LinkedIn   │
│ • Store in Airtable │  │ • Paginate Results  │
│ • Trigger Enrich    │  │ • Store Profiles    │
│                     │  │ • Trigger Enrich    │
└──────────┬──────────┘  └──────────┬──────────┘
           │                        │
           └────────────┬───────────┘
                        │
                        ↓
┌─────────────────────────────────────────────────────────────────┐
│                  ENRICHMENT WORKFLOW                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  • Fetch Lead from Airtable                                     │
│  • Scrape LinkedIn Profile (Apify)                              │
│  • Extract 25+ data fields                                      │
│  • Parse experience, company, contact info                      │
│  • Update Airtable with enriched data                           │
│                                                                  │
└───────────────────────┬─────────────────────────────────────────┘
                        │
                        ↓
┌─────────────────────────────────────────────────────────────────┐
│                 QUALIFICATION WORKFLOW                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. Fetch Lead Data from Airtable                               │
│  2. Extract Company Website with Tavily                         │
│  3. Send to Google Gemini with ICP                              │
│  4. AI Analyzes Fit (Job, Company, Industry)                    │
│  5. Returns Score 0-10                                          │
│  6. Update Airtable with Qualification Score                    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
                        │
                        ↓
┌─────────────────────────────────────────────────────────────────┐
│                      AIRTABLE DATABASE                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  • Apollo Campaigns & Leads                                     │
│  • Google Search Campaigns & Leads                              │
│  • Aggregated Emails (Qualified Leads)                          │
│  • Full lead profiles with 25+ fields                           │
│  • Qualification scores and ICP details                         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔄 Five Automated Workflows

### 1️⃣ **Workflow: ScrapeApollo**

**Purpose:** Extract leads from Apollo.io search results

**Trigger:** Webhook with `action=ScrapeApollo`

**Process:**
1. Reads Apollo campaign from Airtable
2. Calls Apify Apollo Scraper with search URL
3. Scrapes specified number of leads
4. Inserts into Apollo Leads table
5. Updates campaign status to "Scraping Complete"

**Output:** Apollo leads with basic info (name, title, company, email)

---

### 2️⃣ **Workflow: EnrichApolloProfiles**

**Purpose:** Enrich Apollo leads with full LinkedIn profile data

**Trigger:** Webhook with `action=EnrichApolloProfiles`

**Process:**
1. Reads lead from Apollo Leads table
2. Calls Apify LinkedIn Profile Scraper
3. Extracts 25+ data fields
4. Parses experience, company details
5. Updates lead with enriched data

**Output:** Fully enriched Apollo lead ready for qualification

---

### 3️⃣ **Workflow: ScrapeLinkedInProfiles**

**Purpose:** Find LinkedIn profiles via Google Search based on ICP

**Trigger:** Webhook with `action=ScrapeLinkedInProfiles`

**Process:**
1. Reads Google Search campaign from Airtable
2. Builds search query: `site:linkedin.com/in/ [Job Title] [Company Type] [Location]`
3. Calls Serper.dev API for Google results
4. Handles pagination (20 results per page)
5. Extracts LinkedIn profile URLs from search results
6. Inserts into Google Search Leads table
7. Stores ICP details with each lead
8. Updates campaign status

**Output:** LinkedIn profile URLs matching ICP criteria

---

### 4️⃣ **Workflow: EnrichLinkedInProfiles**

**Purpose:** Enrich Google-found LinkedIn profiles with full data

**Trigger:** Webhook with `action=EnrichLinkedInProfiles`

**Process:**
1. Reads lead from Google Search Leads table
2. Calls Apify LinkedIn Profile Scraper
3. Extracts complete profile information
4. Updates lead with enriched data

**Output:** Fully enriched LinkedIn lead ready for qualification

---

### 5️⃣ **Workflow: QualifyLeads**

**Purpose:** Score leads using AI against ICP

**Trigger:** Webhook with `action=QualifyLeads`

**Process:**
1. Reads lead from Aggregated Emails table
2. Extracts company website content with Tavily
3. Sends to Google Gemini with:
   - Target ICP (job title, location, company type, size)
   - Lead data (title, headline, about, company)
   - Raw website content
4. AI analyzes fit and returns score 0-10
5. Updates Airtable with qualification score

**Output:** Qualified lead with AI-generated score

---

## 🛠️ Tech Stack

| Category | Technology | Purpose |
|----------|------------|---------|
| **Automation** | n8n | Workflow orchestration |
| **Database** | Airtable | Lead storage and campaign management |
| **Scraping** | Apify | Apollo scraper, LinkedIn profile scraper |
| **Search** | Serper.dev | Google Search API for LinkedIn discovery |
| **Web Extraction** | Tavily | Company website content extraction |
| **AI Qualification** | Google Gemini 2.0 Flash | Lead scoring against ICP |
| **Triggers** | Webhooks | Airtable automation triggers |

---

## 📦 Prerequisites

### Required Accounts

| Service | Required? | Purpose | Cost |
|---------|-----------|---------|------|
| **n8n** | ✅ Yes | Workflow automation | Free (self-hosted) or $20/mo |
| **Airtable** | ✅ Yes | Database & UI | Free tier available |
| **Apify** | ✅ Yes | LinkedIn scraping | $49/mo or pay-per-use |
| **Serper.dev** | ✅ Yes | Google Search API | $50/mo for 5,000 searches |
| **Tavily** | ✅ Yes | Web content extraction | Free tier: 1,000 requests/mo |
| **Google Gemini** | ✅ Yes | AI lead qualification | Free tier available |

### API Keys Needed

- ✅ Airtable Personal Access Token
- ✅ Apify API Token
- ✅ Serper.dev API Key
- ✅ Tavily API Key
- ✅ Google Gemini API Key

---

## 🚀 Installation

### Step 1: Download Workflow

1. Download `Lead Generation System.json` from this repository
2. Save to your local machine

### Step 2: Import to n8n

1. Open your n8n instance
2. Click **"Workflows"** → **"Import from File"**
3. Select the JSON file
4. Click **"Import"**

### Step 3: Set Up Airtable Base

#### Create Airtable Base

1. Create new base: "Lead Generation Machine"
2. Create the following tables:

**Table 1: Apollo Campaigns**
```
Fields:
- Campaign Name (Single line text)
- Apollo Search URL (URL)
- Number Of Leads (Number)
- ICP Details (Long text)
- Start Campaign (Checkbox)
- Campaign Status (Single select: Idle, Scraping Leads, Scraping Complete)
```

**Table 2: Apollo Leads**
```
Fields:
- Name (Single line text)
- First Name (Single line text)
- Last Name (Single line text)
- Title (Single line text)
- Headline (Single line text)
- Company (Single line text)
- Industry (Single line text)
- Website (URL)
- Company LinkedIn Url (URL)
- Email (Email)
- LinkedIn Profile Url (URL)
- City (Single line text)
- Country (Single line text)
- LinkedIn Headline (Long text)
- About (Long text)
- Experience (Long text)
- Mobile Number (Phone)
- Company Size (Single line text)
- ICP Details (Long text)
- Apollo Campaigns (Link to Apollo Campaigns)
```

**Table 3: Google Search Campaigns**
```
Fields:
- Campaign Name (Single line text)
- Job Title (Single line text)
- Company Type (Single line text)
- Location (Single line text)
- CompanySize (Single line text)
- Industry (Single line text)
- Number Of Leads (Number)
- Campaign Status (Single select)
- Start Campaign (Checkbox)
```

**Table 4: Google Search Leads**
```
Fields:
- Title (Single line text)
- Linkedin Profile Url (URL)
- LinkedIn Profile Snippet (Long text)
- ICP Details (Long text)
- First Name (Single line text)
- Last Name (Single line text)
- Headline (Long text)
- Address (Single line text)
- About (Long text)
- experianceDetails (Long text)
- email (Email)
- Company Name (Single line text)
- companyWebsite (URL)
- Company LinkedIn (URL)
- Company Size (Single line text)
- Job Title (Single line text)
- Mobile Number (Phone)
- Google Search Campaigns (Link to Google Search Campaigns)
```

**Table 5: Aggregated Emails**
```
Fields:
- First Name (Single line text)
- Last Name (Single line text)
- Title (Single line text)
- Headline (Long text)
- Company (Single line text)
- Industry (Single line text)
- Website (URL)
- Company LinkedIn Url (URL)
- Email (Email)
- LinkedIn Profile Url (URL)
- City (Single line text)
- Country (Single line text)
- LinkedIn Headline (Long text)
- About (Long text)
- Experience (Long text)
- Mobile Number (Phone)
- Company Size (Single line text)
- ICP (Long text)
- Qualification Score (Number)
- Apollo Campaigns (Link to Apollo Campaigns)
```

#### Get Airtable Credentials

1. Go to https://airtable.com/create/tokens
2. Create new token with scopes:
   - data.records:read
   - data.records:write
   - schema.bases:read
3. Add access to your base
4. Copy token

### Step 4: Configure API Keys

Open the imported workflow and update these nodes:

#### 1. Airtable Credentials

**All Airtable nodes need credentials:**
- In n8n: Settings → Credentials
- Add "Airtable Personal Access Token"
- Paste your token

#### 2. Apify Token

**In nodes:**
- "Apollo Scraper"
- "Apify" (both instances)
- "Apify1"

Replace `INSERT_API_KEY_HERE` with your Apify token in the URL:
```
https://api.apify.com/v2/acts/[actor]/run-sync-get-dataset-items?token=YOUR_TOKEN
```

#### 3. Serper.dev Key

**Nodes:** "SerperDev", "SerperDev1"

1. Create Header Auth credential in n8n
2. Header name: `X-API-KEY`
3. Header value: Your Serper.dev API key

#### 4. Tavily API Key

**Node:** "Tavily Extract"

In header parameters:
```
Authorization: Bearer YOUR_TAVILY_API_KEY
```

#### 5. Google Gemini

**Node:** "Google Gemini Chat Model6"

1. Get API key from https://aistudio.google.com/app/apikey
2. Add to n8n credentials: "Google Gemini(PaLM) Api"

### Step 5: Update Base IDs

In all Airtable nodes, update:
- Base ID: Your Airtable base ID
- Table IDs: Your table IDs

Find these in Airtable URL:
```
https://airtable.com/appXXXXXXXXXXXXXX/tblYYYYYYYYYYYYYY
                      ^^^^^^^^^^^^^^^^  ^^^^^^^^^^^^^^^^
                      Base ID           Table ID
```

### Step 6: Activate Workflow

1. Click **"Active"** toggle (top-right)
2. Workflow is now live and ready!

---

## ⚙️ Configuration

### Webhook URL

After activation, get your webhook URL from the "Webhook" node:

```
https://your-n8n-instance.com/webhook/lead-machine-v2
```

### Airtable Automations

Create automations in each campaign table:

**For Apollo Campaigns:**
```
When: Record matches conditions
Condition: Start Campaign = true
Action: Send webhook request
URL: [Your webhook URL]?action=ScrapeApollo&recordId={Record ID}
Method: GET
```

**For Google Search Campaigns:**
```
When: Record matches conditions
Condition: Start Campaign = true
Action: Send webhook request
URL: [Your webhook URL]?action=ScrapeLinkedInProfiles&recordId={Record ID}
Method: GET
```

---

## 📖 Usage Guide

### Scenario 1: Generate Leads from Apollo

#### Step 1: Create Campaign

1. Open **Apollo Campaigns** table
2. Add new record:
   - Campaign Name: "SaaS Founders Q1 2025"
   - Apollo Search URL: [Your saved search URL]
   - Number Of Leads: 100
   - ICP Details: "Series A/B SaaS founders in USA"
   - Start Campaign: ☑️

#### Step 2: Wait for Scraping

- Campaign Status changes to "Scraping Leads"
- Workflow scrapes leads from Apollo
- Leads appear in **Apollo Leads** table
- Status updates to "Scraping Complete"

#### Step 3: Enrich Profiles

For each lead you want to enrich:
1. In Airtable, create automation or button
2. Trigger webhook: `?action=EnrichApolloProfiles&recordId={ID}`
3. System scrapes full LinkedIn profile
4. Updates lead with 25+ data fields

---

### Scenario 2: Find Leads via Google Search

#### Step 1: Define ICP Campaign

1. Open **Google Search Campaigns** table
2. Add new record:
   - Campaign Name: "Agency Founders NYC"
   - Job Title: "Founder"
   - Company Type: "Marketing Agency"
   - Location: "New York"
   - CompanySize: "10-50"
   - Industry: "Marketing"
   - Number Of Leads: 50
   - Start Campaign: ☑️

#### Step 2: Automatic Discovery

- System builds Google query automatically
- Searches: `site:linkedin.com/in/ Founder Marketing Agency New York`
- Handles pagination (20 results per page)
- Extracts LinkedIn profile URLs
- Inserts into **Google Search Leads** table

#### Step 3: Enrich & Qualify

1. Trigger enrichment for each lead
2. Then trigger qualification
3. AI scores lead 0-10 based on ICP fit

---

### Scenario 3: Qualify Existing Leads

If you have leads in **Aggregated Emails** table:

1. Ensure lead has:
   - Company website
   - Title, Headline, About
   - ICP Details field populated
2. Trigger webhook: `?action=QualifyLeads&recordId={ID}`
3. System extracts website content
4. AI analyzes fit against ICP
5. Returns score 0-10
6. Updates Qualification Score field

**Score Interpretation:**
- **10:** Perfect ICP fit - highest priority
- **8-9:** Strong fit - definitely contact
- **7:** Good fit - contact-worthy
- **5-6:** Moderate fit - investigate further
- **2-4:** Weak fit - low priority
- **0-1:** Not qualified - skip

---

## 📊 Airtable Structure

### Workflow

```
Campaign Creation → Lead Scraping → Profile Enrichment → Lead Qualification
       ↓                  ↓                 ↓                    ↓
Apollo/Google      Raw Profiles    Full LinkedIn Data    Scored Leads
  Campaigns           Table           Updated            Ready for Outreach
```

### Data Flow

```
Apollo Campaign
    ↓
Apollo Leads (Basic)
    ↓
Apollo Leads (Enriched) ─────→ Aggregated Emails
                                       ↓
Google Search Campaign          Qualified Leads
    ↓                           (With Scores)
Google Search Leads (URLs)
    ↓
Google Search Leads (Enriched) ──→ Aggregated Emails
```

---

## 🔐 API Configuration

### Apify Actors Used

**1. Apollo Scraper**
```
Actor: (Custom Apify actor)
Endpoint: /v2/acts/[actor-id]/run-sync-get-dataset-items
Parameters:
- url: Apollo search URL
- totalRecords: Number of leads to scrape
- fileName: Output file name
```

**2. LinkedIn Profile Scraper**
```
Actor: dev_fusion~linkedin-profile-scraper
Endpoint: /v2/acts/dev_fusion~linkedin-profile-scraper/run-sync-get-dataset-items
Parameters:
- profileUrls: Array of LinkedIn URLs
```

### Serper.dev Configuration

```javascript
POST https://google.serper.dev/search

Headers:
{
  "X-API-KEY": "your_api_key",
  "Content-Type": "application/json"
}

Body:
{
  "q": "site:linkedin.com/in/ Founder Marketing Agency",
  "num": 20,
  "page": 1
}
```

### Tavily Configuration

```javascript
POST https://api.tavily.com/extract

Headers:
{
  "Authorization": "Bearer your_api_key"
}

Body:
{
  "urls": ["https://company-website.com"],
  "include_images": false,
  "extract_depth": "basic"
}
```

### Google Gemini Prompt

The AI uses this system prompt for qualification:

```
You are a Lead Qualification Analyst. Analyze lead data against ICP.
Return ONLY a number 0-10 representing fit quality.

Input:
- Target ICP (job title, location, company type, size)
- Lead Data (title, headline, about, company details)
- Raw Website Content

Scoring:
- 10: Perfect fit on all criteria
- 7-9: Strong fit
- 4-6: Moderate fit
- 0-3: Weak/no fit

Output: Single integer only.
```

---

## 🐛 Troubleshooting

### Issue: Apollo Scraping Fails

**Error:** "Actor not found" or 401 error

**Solution:**
1. Verify Apify token is correct
2. Check actor ID is correct in URL
3. Ensure sufficient Apify credits
4. Test actor directly in Apify console

---

### Issue: LinkedIn Profiles Not Found

**Error:** Empty results from Google Search

**Solution:**
1. Check Serper.dev API key is valid
2. Verify search query is constructed correctly
3. Try broader search terms
4. Ensure Number Of Leads is reasonable (50-100)

---

### Issue: Profile Enrichment Fails

**Error:** "Profile not found" or timeout

**Solution:**
1. Verify LinkedIn URL is valid and public
2. Check Apify actor is running
3. Increase timeout in HTTP Request node (60s)
4. Ensure profile URL format: `linkedin.com/in/username`

---

### Issue: AI Qualification Returns Invalid Score

**Error:** AI returns text instead of number

**Solution:**
1. Check Gemini API key is valid
2. Verify prompt hasn't been modified
3. Ensure model is "gemini-2.0-flash"
4. Check if website URL is accessible
5. Add parsing logic to extract number from response

---

### Issue: Airtable Webhook Not Triggering

**Error:** Campaign starts but workflow doesn't run

**Solution:**
1. Verify workflow is Active in n8n
2. Check webhook URL is correct in Airtable automation
3. Include `?action=` and `&recordId=` parameters
4. Test webhook URL manually in browser
5. Check n8n execution logs for errors

---

## 💡 Best Practices

### Campaign Setup

✅ **Do:**
- Start with 50-100 leads per campaign
- Define clear ICP criteria
- Use specific job titles and locations
- Test with small batch first

❌ **Don't:**
- Request 1000+ leads at once (rate limits)
- Use vague search terms
- Skip ICP definition
- Forget to activate workflow

---

### Lead Enrichment

✅ **Do:**
- Enrich in batches of 50-100
- Verify URLs are public LinkedIn profiles
- Check Apify credits before large batches
- Monitor for failures and retry

❌ **Don't:**
- Enrich thousands simultaneously
- Use expired or invalid URLs
- Skip manual spot-checks
- Ignore errors in logs

---

### Lead Qualification

✅ **Do:**
- Define detailed ICP in natural language
- Include company website when possible
- Review AI scores for accuracy
- Adjust ICP based on results

❌ **Don't:**
- Use vague ICP definitions
- Qualify without website data
- Trust scores blindly without review
- Skip manual validation of top scores

---

## 📄 License

This project is licensed under the **MIT License**.

### What This Means

✅ Commercial use allowed  
✅ Modification allowed  
✅ Distribution allowed  
✅ Private use allowed  
⚠️ No warranty or liability

---

## 🌟 Acknowledgments

Built with powerful tools:

- [n8n](https://n8n.io) - Workflow automation
- [Airtable](https://airtable.com) - Database and UI
- [Apify](https://apify.com) - Web scraping
- [Serper.dev](https://serper.dev) - Google Search API
- [Tavily](https://tavily.com) - Web content extraction
- [Google Gemini](https://ai.google.dev/) - AI qualification

---

## 🚀 Roadmap

### Planned Features

- [ ] Email verification integration
- [ ] CRM direct export (HubSpot, Salesforce)
- [ ] Automated outreach sequences
- [ ] Duplicate detection across campaigns
- [ ] Lead scoring dashboard
- [ ] Bulk enrichment interface
- [ ] Apollo.io direct API integration
- [ ] LinkedIn Sales Navigator scraping
- [ ] Company technographics data
- [ ] Industry-specific ICP templates

---

## 💬 Support

### Get Help

- 📧 **Email:** letsautomatewithawais@gmail.com
- 🐛 **GitHub Issues:** [Report bugs](https://github.com/yourusername/lead-gen-system/issues)

---

## 📈 Performance Stats

**Processing Times:**
- Apollo scraping: ~2 min per 100 leads
- LinkedIn profile enrichment: ~30 sec per lead
- Google Search: ~1 min per 50 profiles
- AI qualification: ~5 sec per lead

**Capacity:**
- Apollo: 1,000+ leads/day
- Google Search: 500+ profiles/day
- Enrichment: 2,000+ profiles/day
- Qualification: Unlimited (API dependent)

---

**Made with ❤️ for B2B Sales & Marketing Teams**

⭐ Star this repo if it supercharges your lead generation!

📢 Share with teams who need automated prospecting!

🔗 Fork and customize for your specific needs!

---

**Ready to generate 50,000+ leads?** Set up your first campaign and start automating! 🚀
