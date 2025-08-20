# OCI Generative AI Agents Workshop: Building an Agentic Hotel Concierge

## Introduction

In this lab, you will extend Maria’s journey from analyzing individual reviews to building a true **AI Concierge**.  
With the **OCI Generative AI Agent Development Kit (ADK)** and **Retrieval Augmented Generation (RAG)**, you’ll give Maria’s AI access to her entire guest feedback knowledge base, enabling it to identify patterns, search the internet for real-time information, and respond proactively.

Estimated Time: 30–40 minutes

### Objectives

In this lab, you will:

- Create a **Knowledge Base** in OCI Generative AI Agents using guest reviews
- Build an **AI Concierge Agent** with RAG capabilities
- Test the agent’s ability to summarize and identify patterns
- Extend the agent with **custom tools (web search)** using the ADK
- Run the concierge locally with Python and `.env` configuration
- Experience the shift from **reactive** review handling to **proactive** hospitality intelligence

### Dataset

We will continue using the multi-language **TripAdvisor Hotel Reviews** dataset from  
[NIAID (Vietnamese)](https://data.niaid.nih.gov/resources?id=zenodo_7967493).  

- **CSV version**: For testing and uploading to Object Storage  
- **Markdown version**: For creating the Knowledge Base  

Both files are provided in the `labs/datasets/` folder.

---

## Part 1: Console Setup and RAG Test (20 minutes)

### Step 1: Create the Knowledge Base

1. In the OCI Console, go to **Storage → Object Storage & Archive Storage**  
2. Create a bucket named: `ai-workshop-labs-datasets`  
3. Upload `tripadvisor_hotel_reviews.csv` into this bucket  
4. Navigate to **Analytics & AI → AI Services → Generative AI Agents**  
5. Go to **Knowledge Bases → Create knowledge base**  
   - Name: `Hotel_Reviews_KB`  
   - Data source: select the bucket you created  

---

### Step 2: Create and Test Your First Agent

1. Go to **Agents → Create agent**  
   - Name: `Hotel_Concierge_Agent`  
   - Add tool: **Retrieval Augmented Generation**  
   - Select the `Hotel_Reviews_KB` knowledge base  
2. Create an endpoint (select **Automatically create endpoint**)  
3. Launch chat and test queries such as:  
   - *“Summarize the most common positive comments about rooms”*  
   - *“Are there negative reviews mentioning the check-in process?”*  

---

## Part 2: The Problem-Solving Concierge with OCI ADK (15 minutes)

### Step 3: Create Another Agent for ADK

1. In **Agents → Create agent**  
   - Name: `Hotel_Concierge_Agent_ADK`  
   - Add tool: **Retrieval Augmented Generation**  
   - Select the `Hotel_Reviews_KB`  
2. Create an endpoint (auto-create)  

---

### Step 4: Local ADK Setup

1. Open the cloned GitHub repository in your editor  
2. Copy `.env.example` to `.env`  
3. Fill in placeholders:  
   - `<replace with your knowledge base id>` → Knowledge Base OCID  
   - `<replace with your agent endpoint id>` → Agent Endpoint OCID  
   - `<replace with your tavily api key>` → Tavily AI API key  

---

### Step 5: Run the Concierge Agent

Execute from terminal:

```bash
python run_concierge_agent.py
```

- The script will connect to your agent  
- The ADK will detect the new **web_search** tool and merge it with RAG  
- The agent will now respond with both **historical insights** and **real-time context**  

---

## Conclusion & Value

Congratulations! You’ve built Maria’s **AI Concierge** that combines guest history with live information.

### What You Accomplished

- **Part 1 – RAG Foundation**: Created a knowledge base and tested RAG queries in the console  
- **Part 2 – Problem-Solving Concierge**: Extended the agent with web search using OCI ADK  

### Business Impact

- **Faster responses**: From hours of manual research to instant insights  
- **Proactive solutions**: Identify recurring issues before they escalate  
- **Operational efficiency**: Staff can focus on service instead of manual searches  
- **Improved guest satisfaction**: Personalized, data-driven responses  

---

## What’s Next

This lab completes Maria’s AI journey so far:

1. **Lab 1** – Multilingual review analysis (summarize, analyze, translate)  
2. **Lab 2, Part 1** – Scale with RAG knowledge base  
3. **Lab 2, Part 2** – Extend with web search tools  

With these skills, you are ready to design AI-powered hospitality solutions that go beyond translation—enabling predictive intelligence, pattern recognition, and real-time problem solving.
