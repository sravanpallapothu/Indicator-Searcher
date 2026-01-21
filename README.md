
# README.md
# ============================================================

# Indicator Searcher

**Live site:** https://www.indicatorsearcher.org

Indicator Searcher is a no-code web application that provides a searchable catalogue of statistical indicators across public datasets and reports. It helps policy teams, researchers, and analysts quickly discover indicator definitions, data sources, and geographic granularity without manually scanning lengthy documents.

---

## Why this project exists

Government reports and surveys contain thousands of indicators, but locating specific metrics inside long PDF documents is time-consuming. This project creates a structured, searchable directory of indicator metadata so users can find relevant indicators in seconds.

---

## What the system does

Users can:
- Search indicators by keyword  
- View indicator definitions and metadata  
- See which report or dataset contains the indicator  
- Check geographic granularity (national, state, district, etc.)  
- Follow links to original source documents  

---

## High-level architecture

PDF Reports  
↓  
Custom GPT extracts indicator tables (CSV)  
↓  
Master Spreadsheet (Indicator Catalogue)  
↓  
Softr Database  
↓  
Softr Search Interface  
↓  
Public Website (Custom Domain)

No backend code or server management is required.

---

## Tools used

- Custom GPT — Extracts structured indicator metadata from PDF reports  
- Spreadsheet (CSV / Google Sheets) — Master indicator catalogue  
- Softr — No-code platform for database + search UI  
- Namecheap — Domain registration and DNS  
- Softr Hosting + SSL — Automatic HTTPS provisioning  

---

## How the website is built

### Data preparation
Each indicator is stored as one row in a spreadsheet, with columns such as:
- Indicator name  
- Definition  
- Dataset / report name  
- Geographic granularity  
- Time period  
- Source link  

This spreadsheet is imported into Softr as a database table.

### Search interface
A Softr **List block** is connected to the indicator table.  
The built-in **Search bar** is enabled and configured to search key fields such as:
- Indicator name  
- Definition  
- Dataset name  

This provides instant keyword search without writing code.

### Homepage and info pages
Additional pages (for example an introduction page) are created in Softr.  
Pages are connected using simple hyperlink or button blocks inside templates.

### Custom domain setup
A custom domain was purchased from Namecheap:

indicatorsearcher.org

Two DNS records connect the domain to Softr:

A Record  
Host: @  
Value: 35.158.87.123  

CNAME Record  
Host: www  
Value: petrina76978.cname.softr.app  

Once DNS propagates, Softr automatically verifies the domain, issues an SSL certificate, and serves the site securely over HTTPS.

---

## Common setup pitfalls and lessons learned

- Search is built into Softr’s List block in newer versions, not a separate block  
- CSV imports create new tables rather than appending rows  
- CNAME must always point to `.cname.softr.app`, never to the same domain  
- DNS propagation takes time; avoid repeated edits  
- DNS checker tools reflect reality more reliably than UI displays  

---

## What this repository contains

/data  
Example indicator catalogue CSV

/docs  
Step-by-step setup guides

/screenshots  
Reference screenshots of configuration steps

---

## What is not included

The live Softr application itself is hosted on Softr’s platform and does not exist as source code in this repository. This repository contains documentation, configuration steps, and example data for replication.

---

## Live demo

https://www.indicatorsearcher.org

---

## Contact

For questions or collaboration, open an issue in this repository.



# ============================================================
# docs/build_process.md
# ============================================================

# Build Process Overview

This document describes the end-to-end process used to build the Indicator Searcher platform.

## Step 1 — Indicator extraction

A custom GPT is used to extract indicator metadata from PDF reports.  
The GPT outputs structured tables in CSV format containing:

- Indicator name  
- Definition  
- Dataset or report name  
- Geographic granularity  
- Time period  
- Source link  

These CSVs form the raw data inputs.

---

## Step 2 — Master catalogue

All CSV outputs are merged into a single master spreadsheet.  
Each row represents one indicator.  
This spreadsheet acts as the authoritative data source.

---

## Step 3 — Import into Softr

The spreadsheet is imported into Softr’s database feature.  
Softr automatically converts columns into database fields.

---

## Step 4 — Build search page

A List block is added in Softr and connected to the database table.  
Search is enabled inside the List block.  
Relevant fields are marked as searchable.

---

## Step 5 — Build homepage

A simple introduction page is created using text and button blocks.  
Buttons link internally to the search page.

---

## Step 6 — Connect custom domain

Domain purchased via Namecheap.  
DNS records configured to connect domain to Softr hosting.

---

## Step 7 — Publish

Softr publishes the site and automatically provisions HTTPS.

---

## Outcome

A public searchable indicator catalogue with no custom backend code.



# ============================================================
# docs/softr_setup.md
# ============================================================

# Softr Setup Guide

This guide explains how to configure Softr to build the Indicator Searcher.

---

## Create Softr app

- Sign in to Softr  
- Create a new app  
- Choose a blank template  

---

## Import database

- Go to Data → Add new table  
- Import CSV or connect Google Sheet  
- Verify columns are correctly mapped  

---

## Create search page

- Add a List block  
- Connect List block to indicator table  
- Enable Search bar  
- Select searchable fields  

---

## Create homepage

- Add a new page  
- Add Text block describing the tool  
- Add Button block linking to search page  

---

## Make pages public

- Ensure app access is set to Public  
- Publish the app  

---

## Notes

- CSV imports create new tables each time  
- Avoid renaming tables mid-setup  
- Use List block search, not separate search blocks  



# ============================================================
# docs/dns_setup.md
# ============================================================

# Namecheap DNS Setup for Softr

This guide explains how to connect a Namecheap domain to a Softr app.

---

## Step 1 — Purchase domain

Buy a domain from Namecheap (e.g., indicatorsearcher.org).

---

## Step 2 — Open Advanced DNS

- Log into Namecheap  
- Go to Domain List  
- Click Manage next to your domain  
- Open Advanced DNS tab  

---

## Step 3 — Add A record

Type: A Record  
Host: @  
Value: 35.158.87.123  
TTL: Automatic  

---

## Step 4 — Add CNAME record

Type: CNAME Record  
Host: www  
Value: petrina76978.cname.softr.app  
TTL: Automatic  

(Namecheap automatically adds a trailing dot — this is normal.)

---

## Step 5 — Save changes

Click Save All Changes.

---

## Step 6 — Wait for propagation

DNS propagation may take 15–60 minutes.  
Avoid changing records during this time.

---

## Step 7 — Verify

Check:

indicatorsearcher.org → A → 35.158.87.123  
www.indicatorsearcher.org → CNAME → petrina76978.cname.softr.app  

---

## Step 8 — Refresh in Softr

In Softr → Custom Domain → click Refresh.  
Softr will verify DNS and issue SSL automatically.

---

## Outcome

Your site becomes publicly available at:

https://indicatorsearcher.org

with HTTPS enabled automatically.

---

End of documentation.
