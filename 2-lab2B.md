# Lab 2B: Building an Agentic Hotel Concierge - With ADK using tools and RAG??


## Introduction

This lab walks you through the step-by-step creation of an **AI Concierge** directly in the OCI Console, covering the knowledge base, agent, and tools configuration. This method is recommended if you want a deeper understanding of the underlying components and their relationships. If you prefer a faster setup using a Python script to provision all components automatically, check out [Lab 2A: Automated Deployment](2-lab2A.md)

<!--Watch this short video introducing Maria's AI Concierge and the problem it solves:
![Maria's AI Concierge](videos/maria_ai_concierge_intro.mp4)-->

Three months after implementing her **AI review analysis system**, Maria, General Manager of the Grand Plaza Hotel, can now quickly understand and respond to guest reviews in multiple languages, greatly improving **guest satisfaction ⭐⭐⭐⭐⭐** and **response times ⏱️**. A new challenge arose: identifying **patterns across complaints** like *noisy construction*, *slow Wi-Fi*, or *event disruptions*. Manually tracking these across spreadsheets and review platforms is *slow* and *error-prone*.

The solution is an **AI Concierge 🛎️** using **Retrieval Augmented Generation (RAG)** that can *instantly search thousands of reviews*, *identify trends*, *provide context-aware responses*, and *solve real-time issues*. Maria can now ask the AI questions like **"How many guests reported Wi-Fi issues this month?"** or **"What event disrupted guests last weekend?"** and get instant insights.


### **Objectives**

In this lab, you will build the AI Concierge  using Retrieval Augmented Generation (RAG) and  complete four main tasks:  
1. Upload the TripAdvisor Hotel Reviews dataset to Object Storage
2. Create a Knowledge Base in Generative AI Agents
3. Create and Test your First Agent with Retrieval Augmented Generation (RAG)
4. Run the Problem-Solving Concierge using the OCI Agent Development Kit (ADK)

📋📋📋📝

---

## 📋 Task 1: Upload Dataset to Object Storage

1. Navigate to the **OCI Console** → **Storage** → **Object Storage & Archive Storage**.  
   ![Step 1: Navigate to Object Storage](images/object-storage-navigation.png)

2. Create a new bucket:  
   - **Bucket Name:** `ai-workshop-labs-datasets`  
   ![Step 2: Create a Bucket](images/create-bucket.png)

3. Upload the dataset file into the bucket:  
   - File: `tripadvisor_hotel_reviews.csv`  
   ![Step 3: Upload Dataset](images/upload-dataset.png)

**At the end of this task, the dataset will be securely stored in Object Storage.**

---

## 📋 Task 2: Create a Knowledge Base in Generative AI Agents

The **Knowledge Base** will act as the repository for your dataset (hotel reviews).

1. Navigate to the **OCI Console** → **Analytics & AI** → **AI Services** → **Generative AI Agents**.  
   ![Step 1: Navigate to Generative AI Agents](images/genai-agents-navigation.png)

2. In the left-hand menu, click **Knowledge Bases** → **Create knowledge base**.  
   ![Step 2: Create Knowledge Base](images/create-knowledge-base.png)

3. Fill in the details:  
   - **Name:** `Hotel_Reviews_KB`  
   - **Compartment:** Select your working compartment  
   - **Data Store Type:** Object Storage  

   ![Step 3: Fill Knowledge Base Details](images/kb-details.png)

4. Under **Data Sources**, add the Object Storage bucket you created:  
   - **Name:** `HotelReviews-Reviews-DataSource`  
   - **Bucket:** `ai-workshop-labs-datasets`  
   - **Enable Auto Ingestion:** ✔️ (Check this to auto-ingest new files)  

   ![Step 4: Configure Data Source](images/kb-datasource.png)

5. Click **Create knowledge base**.  
   Data ingestion will begin automatically.  

   ![Step 5: Knowledge Base Created](images/kb-created.png)

 **At the end of this task, you will have a Knowledge Base linked to your dataset in Object Storage.**

---

## 📋 Task 3: Create and Test the First Agent

> **Note:** If you ran the setup scripts, skip to step 3.

### Step 1: Create the Agent with RAG Tool
1. In the **Generative AI Agents** console, click **Agents** → **Create agent**.  
   ![Step 1: Navigate to Create Agent](images/create-agent.png)

2. Fill in the details:  
   - **Name:** `Hotel_Concierge_Agent`  
   ![Step 2: Fill Agent Details](images/agent-details.png)

3. Click **Next**.  
   - Select **Add tool** → **Retrieval Augmented Generation (RAG)**.  
   - Choose the Knowledge Base you created earlier: `Hotel_Reviews_KB`.  

   ![Step 3: Select RAG Tool](images/select-rag.png)

---

### Step 2: Create an Endpoint
1. On the next screen, select:  
   - **Automatically create an endpoint for this agent** ✔️  
   (This is essential for the ADK to connect later.)  
   ![Step 4: Create Endpoint](images/create-endpoint.png)

2. Click **Next**, then **Create agent**.  
   ![Step 5: Agent Created](images/agent-created.png)

---

### Step 3: Chat with and Test Your RAG Agent
1. Once the agent is active, click **Launch chat**.  
   ![Step 6: Launch Chat](images/launch-chat.png)

2. Test its knowledge from the dataset with sample queries:  
   - *“Summarize the most common positive comments people make about their rooms.”*  
   - *“Are there any negative reviews that mention the check-in process?”*  

   ![Step 7: Test Chat](images/test-chat.png)

**At the end of this task, you will have created an agent with RAG and validated that it can retrieve and summarize information from your Knowledge Base.**

---

## 📝 Task 4: The Problem-Solving Concierge (Live Tool with OCI ADK)

This part moves from the **OCI Console** to your **local machine** to run the Python script. *(~15 minutes)*

> **Note:** If you ran the setup scripts, skip to step 3.

### Step 1: Create the Agent with RAG Tool
1. In the **Generative AI Agents** console, click **Agents** → **Create agent**.  
   ![Step 1: Navigate to Create Agent](images/create-agent.png)

2. Fill in the details:  
   - **Name:** `Hotel_Concierge_Agent_ADK`  
   ![Step 2: Fill Agent ADK Details](images/agent-adk-details.png)

3. Click **Next**.  
   - Select **Retrieval Augmented Generation (RAG)** as the tool.  

   ![Step 3: Select RAG Tool](images/select-rag.png)

---

### Step 2: Create an Endpoint
1. On the next screen, select:  
   - **Automatically create an endpoint for this agent** ✔️  
   ![Step 4: Create Endpoint](images/create-endpoint.png)

2. Click **Next**, then **Create agent**.  
   ![Step 5: Agent Created](images/agent-created.png)

---

### Step 3: Update Environment Variables
1. Open the **GitHub repository** you cloned earlier in your text editor.  
   ![Step 6: Open Repo](images/open-repo.png)

2. Copy the example environment file:  
   ```bash
   cp .env.example .env
   ```

3. Edit the `.env` file and update the placeholders:  
   - Replace `<replace with your knowledge base id>` with your **Knowledge Base OCID**  
   - Replace `<replace with your agent endpoint id>` with your **Agent Endpoint OCID**  
   - Replace `<replace with your tavily api key>` with your **Tavily AI API key**  

   ![Step 7: Update ENV](images/update-env.png)

---

### Step 4: Run the Agent
1. From your terminal, execute the script:  
   ```bash
   python run_concierge_agent.py
   ```

2. The script will:  
   - Connect to your existing agent  
   - Run `agent.setup()` to synchronize tools  
   - Detect the new **web_search tool** in your code  
   - Add it to your agent’s capabilities (without removing the RAG tool)  
   - Execute a query and print the **final response**  

   ![Step 8: Run Agent Script](images/run-agent.png)

✅ **At the end of this task, you will have a live, problem-solving concierge agent running locally with the OCI ADK.**

---

## Conclusion & Value

🎉 Congratulations! You've successfully transformed Maria's hotel guest feedback system from a **manual, reactive process** into an **intelligent, proactive AI-powered solution**.

### What You've Accomplished
- **Part 1 – RAG Foundation:**  
  You created a **Knowledge Base** that gives Maria's AI agent access to all her guest feedback.  
  Instead of manually searching through thousands of reviews, the AI can now instantly retrieve relevant information, identify patterns, and surface insights that would normally take hours.  

- **Part 2 – Real-World Problem Solving:**  
  You enhanced Maria’s AI agent with **live web search capabilities** via the OCI ADK.  
  This means her concierge can not only understand historical guest complaints but also **find current information** in real-time to solve problems immediately.  

### The Business Impact for Maria
- 🚀 **Faster Response Times**: From hours of manual research to instant, AI-powered answers  
- 🔍 **Proactive Problem Solving**: Identify and address issues before they affect multiple guests  
- 😀 **Improved Guest Satisfaction**: Provide accurate, helpful responses based on complete data  
- ⚡ **Operational Efficiency**: Free up staff time for higher-value guest interactions  

✅ You’ve built a foundation that can be extended to **any industry scenario** — from customer support, to supply chain management, to healthcare — wherever insights from large datasets and real-time information can transform business outcomes.

