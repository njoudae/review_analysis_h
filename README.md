# Review Analysis Project

This project automatically collects Google Maps reviews, analyzes negative feedback using a language model, and sends alerts via Telegram (or Email).

---

## 📁 Project Structure

### `main.py`
The main entry point of the project.  
Coordinates the full pipeline:
- Load configuration
- Fetch reviews
- Store new reviews
- Analyze reviews with LLM
- Send alerts
- Update state

---

### `app/`
Core application logic, split into clear modules.

#### `app/config.py`
Handles configuration and environment variables:
- API keys (Apify, OpenAI, Telegram)
- File paths
- Global constants

---

#### `app/db.py`
Database layer (SQLite):
- Initialize tables
- Save and check reviews
- Save and check analysis results
- Manage state (last run, last processed review)

---

#### `app/apify_client.py`
Responsible for data collection:
- Calls Apify actor
- Retrieves raw review data
- Normalizes review structure

---

#### `app/llm.py`
Language Model logic:
- Decide whether a review needs analysis
- Build prompt payload
- Call OpenAI API
- Parse and validate model output
- Decide whether to trigger an alert

---

#### `app/helpers.py`
Utility helpers:
- Date/time helpers
- Console database snapshot
- Shared small utility functions

---

### `apify_input.json`
Input configuration for the Apify actor:
- Target places
- Scraping options
- Review limits

---

### `outbox/`
Fallback storage:
- Stores unsent alerts when network or API fails

---

### `.env`
Environment variables (NOT committed):
- API keys
- Tokens
- Secrets

---

### `.gitignore`
Specifies files and folders excluded from Git:
- Virtual environments
- Database files
- Secrets

---

### `requirements.txt`
Python dependencies required to run the project.

---

### `README.md`
Project documentation and usage instructions.

---

## ⚙️ How It Works (High Level)

1. Fetch reviews from Google Maps via Apify  
2. Store only new reviews  
3. Analyze negative or risky reviews using LLM  
4. Send alerts to Telegram  
5. Keep state to avoid duplicate processing  

---
