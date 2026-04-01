# AI-Powered Event Feedback Analyzer 📊

**Problem Statement:** #7 (College Club Feedback Analysis)
**Approach:** No-Code Automated Pipeline

This repository contains the configuration and architecture documentation for an AI-powered feedback analysis system. Instead of writing a traditional script, this solution leverages modern integration platforms (Make.com) and LLM APIs to create a scalable, fully automated data pipeline.

---

## 03. Technical Approach & Architecture

This solution transforms unstructured, qualitative feedback (like responses from a recent college Ugadi celebration) into structured, actionable insights without manual intervention. 

**System Architecture & Data Flow:**
1. **Data Ingestion (Google Forms & Sheets):** Attendees submit feedback via a Google Form. This data is automatically appended to a Google Sheet, acting as our primary database.
2. **Data Aggregation (Make.com):** A Make.com scenario watches the database. When triggered, a "Text Aggregator" module compiles all individual feedback rows into a single, comprehensive text string.
3. **AI Processing (Google Gemini API):** The aggregated text is passed to an AI model via API. The model is constrained by a strict prompt to identify top positive themes, isolate common complaints, and generate three actionable improvements, while explicitly ignoring empty or gibberish edge-case responses.
4. **Data Delivery (Google Docs):** The parsed AI output is automatically formatted and written into a new Google Document, providing the event organizer with an instant, readable summary.

**Why this approach?**
It is highly practical, extremely scalable, and minimizes point-of-failure risks associated with custom-coded scraping or API handling.

---

## 04. Setup Instructions & "Code" Submission

Because this is a no-code solution, the "code" is provided as a JSON blueprint of the Make.com scenario (`blueprint.json` included in this repository).

### How to Replicate and Run Locally:
1. **Import the Blueprint:**
   * Create a free account on [Make.com](https://www.make.com/).
   * Create a new Scenario.
   * Click the three dots (More options) at the bottom and select **Import Blueprint**.
   * Upload the `blueprint.json` file from this repository.
2. **Configure Environment Variables (Connections):**
   * Click on the **Google Sheets** module and authenticate with your Google account. Select your specific feedback spreadsheet.
   * Click on the **AI Module** (Gemini) and input your developer API key. 
   * Click on the **Google Docs** module and authenticate your Google account to authorize document creation.
3. **Execution:**
   * Click **Run Once** in the bottom left corner. The system will pull the database rows, process them through the AI, and generate the summary document in your Google Drive.

### AI Prompt Configuration
If you are building this from scratch, the core logic driving the AI is the following prompt constraint:
> *"You are an expert event coordinator analyzing post-event feedback. Read the following attendee responses. Identify the top 2 positive themes, the top 2 complaints, and suggest 3 actionable improvements for the next event. Ignore blank, one-word, or gibberish answers. Here is the raw feedback: [Aggregated_Text_Variable]"*
