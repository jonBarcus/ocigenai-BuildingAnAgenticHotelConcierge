# Lab 2: Build an Agentic Hotel Concierge

### Introduction
This lab guides you through creating an AI Concierge. In this version, we'll use a Python script to quickly create all the necessary components (agent, knowledge base, and tools) automatically.

Three months after implementing her AI review analysis system, Maria, General Manager of the Grand Plaza Hotel, can now quickly understand and respond to guest reviews in multiple languages, greatly improving guest satisfaction ⭐⭐⭐⭐⭐ and response times ⏱️. A new challenge arose: identifying patterns across complaints like noisy construction, slow Wi-Fi, or event disruptions. Manually tracking these across spreadsheets and review platforms is slow and error-prone.

The solution is an AI Concierge 🛎️ using Retrieval Augmented Generation (RAG) that can instantly search thousands of reviews, identify trends, provide context-aware responses, and solve real-time issues. Maria can now ask the AI questions like *"How many guests reported Wi-Fi issues this month?"* or *"What event disrupted guests last weekend?"* and get instant insights.

### Objectives
In this lab, you will build the AI Concierge using Retrieval Augmented Generation (RAG) and complete three main tasks:

- Run a script to upload the dataset and create the KnowledgeBase and agent.  
- Create and Test your First Agent with Retrieval Augmented Generation (RAG).  

### Prerequisites
This lab assumes you have the following:

- Access to Oracle Cloud Infrastructure (OCI), paid account or free tier, in a region that has Generative AI.  
- Basic experience with OCI Cloud Console and standard components.  
- The `handson-lab` repository cloned.  

Estimated Time:  45-50 minutes

Tasks
---

## Task 1: Create ObjectStorage, Knowledge-base and Agent
In this task, you'll run the cloud shell to run a script before we test the AI agents. This script will create object storage, knowledge-base and Agents. 


1.  Setup OCI config file
    
    Open Cloud Shell from the top-right corner of the OCI Console, then run this one-liner to create the `.oci` folder, set permissions, and open the config file in `vi`:

    ![Open Cloud Shell](./images/open_cloud_shell.png "Open Cloud Shell")

    ```bash
    <copy>
    mkdir -p ~/.oci && chmod 700 ~/.oci && vi ~/.oci/config
    </copy>
    ```

    Inside the editor, press i to insert and paste the following (replace values with your own):

    **~/.oci/config file**
    
    ```bash
    <copy>
    user=ocid1.user.oc1..aaaaaaxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    fingerprint=3c:1f:1b:c8:69:d0:0a:f1:b2:4e:aa:aa:aa:aa:aa:aa:aa
    tenancy=ocid1.tenancy.oc1..aaaaaaaaihbmw6hm3xxxxxxxxxxxxxxxxxxxxxxxxxx
    region=us-chicago-1
    key_file=~/.oci/xxxxxxxxxxxPRIVATE_KEY@oracle.com-2025-07-31T12_49_17.566Z.pem
    </copy>
    ```

    Save and exit by pressing Esc, typing :wq, and pressing Enter.
    Finally, secure the file permissions:
    
    ```bash
    <copy>
    chmod 600 ~/.oci/config ~/.oci/*.pem
    </copy>
    ```

    *Note: You can get the user OCID,fingerprint, tenancy, key_file after creating a fingerprint. Please see below screenshot to create and update to cloud shell*

    ![Open Cloud Shell](./images/add_api_key.png "Open Cloud Shell")    

    ![Open Cloud Shell](./images/add_api_key_click_add.png "Open Cloud Shell")    

    ![Open Cloud Shell](./images/copy_config.png "Open Cloud Shell")    

    ![Open Cloud Shell](./images/copy_private_key_set_permission.png "Open Cloud Shell")            

    Verify if config file is setup correctly 

    ![Setup Config](./images/config.png "Setup Config")

2.  Run the following command to check if the region is set to us-chicago-1. 

    ```bash
    <copy>
    awk -F= '/^region/ {print $2}' ~/.oci/config
    </copy>
    ```

3.  Copy the [setup.py](./files/setup.py) and [TripAdvisorReviewsMultiLang.md](./files/TripAdvisorReviewsMultiLang.md) file to your local machine.Drag and drop inside the Cloud Shell. 

    ![Run Python](./images/drag_drop_files.png)

4.  Check python script >3.9 and run setup.py in CloudShell

    ```bash
    <copy>
    python -V
    python setup.py
    </copy>
    ```

    ![Run Python to Create ObjectStorage Knowledge-base Agents](./images/create_storage_kb_agents.png "Run Python to Create ObjectStorage Knowledge-base Agents")

    *Note:* 

    *If you run the script in your own tenancy and if you get any error on limits, you need to request to increase the Generative-Agent count, Knowledgebase count and Agent Endpoint count limits.*

    ![Limit Increase](./images/limit_increase_1.png "Limit Increase")
    ![Increase the Limit for Generative-Agent count, Knowledgebase count and Agent Endpoint count limits](./images/limit_increase_2.png "Increase the Limit for Generative-Agent count, Knowledgebase count and Agent Endpoint count limits")

5.  View the newly created storage bucket and the uploaded dataset in the UI.

    ![Newly created Buckets](./images/new_bucket_created.png "Newly created Buckets")    
    ![Datasets in Buckets](./images/dataset_in_bucket.png "Datasets in Buckets")    

6.  Explore your newly created knowledge base and the data source in the UI.

    ![Newly created knowledge base](./images/knowledgebase_created.png "Newly created knowledge base")    
    ![Newly created knowledge base](./images/knowledgebase_datasource.png "Newly created knowledge base")    

7.  Confirm that the agents have been created successfully in the UI.

    ![Newly created Agents](./images/new_agents_created.png "Newly created Agents")    

## Task 2: Test Your RAG agent

    Once the agent is active, click Launch chat. Test its knowledge from the dataset to confirm the RAG tool is working.

    ```
    <copy>
    "Summarize the most common positive comments people make about their rooms."
    "Are there any negative reviews that mention the check-in process?"
    </copy>
    ```


![Test the RAG Agent](./images/chat_response.png "Chat Response")


---

## Acknowledgements  

**Authors:**  
- Felipe Garcia, Master Principal Cloud Architect 
- Karol Stuart, Master Principal Cloud Architect  

**Last Updated by/Date** – Karol Stuart, August 2025  
