# Automate Insurance Claim Processing with Agentic AI

## Table of Contents

- [Automate Insurance Claim Processing with Agentic AI](#automate-insurance-claim-processing-with-agentic-ai)
  - [Table of Contents](#table-of-contents)
  - [Use case description](#use-case-description)
  - [Architecture](#architecture)
  - [Implementation](#implementation)
    - [Pre-requisites](#pre-requisites)
    - [Open Agent Builder](#open-agent-builder)
    - [Information Agent](#information-agent)
      - [Create the Information Agent](#create-the-information-agent)
      - [Test the Information Agent](#test-the-information-agent)
    - [Customer Claims Agent](#customer-claims-agent)
      - [Create the Customer Claims Agent](#create-the-customer-claims-agent)
      - [Test the Customer Claims Agent](#test-the-customer-claims-agent)
    - [Claim Processor Agent](#claim-processor-agent)
      - [Create the Claim Processor Agent](#create-the-claim-processor-agent)
      - [Test the Claim Processor Agent](#test-the-claim-processor-agent)
    - [Further testing via AI Chat](#further-testing-via-ai-chat)

## Use case description

Powered by Agentic AI and watsonx Orchestrate, this solution enables the creation of an intelligent, agent-driven system that transforms and streamlines the entire claims process. It simplifies claim submission for customers while equipping insurers with automation to reduce manual effort and accelerate processing times.

Customers can initiate a claim by answering a few guided questions, even with minimal initial information. From there, the agentic system orchestrates the full claims workflow—automatically handling document generation, data extraction, and verification. This ensures a fast, accurate, and user-friendly experience, with real-time claim status updates that enhance transparency and customer satisfaction.

For insurers, incoming claims are automatically retrieved and intelligently cross-verified against policy documents. The system extracts critical data and evaluates it against business rules and regulatory standards, generating structured recommendations for claim approval or denial. While final decisions remain with the insurer, each recommendation is backed by a clear, concise summary of all supporting details—minimizing errors and enabling faster, more informed decision-making.
## Architecture

![Architecture](Insurance_Autoclaims_Architecture_v2.png)

## Implementation

### Pre-requisites

- Check with your instructor to ensure **all systems** are up and running before you continue.
- Validate that you have access to the right TechZone environment for this lab.
- Validate that you have access to a credentials file that your instructor will share with you before starting the labs.
- If you're an instructor running this lab, check the Instructor's guides to set up all environments and systems.
- Make sure that your instructor has provided the following:
  - **OpenAPI Specs**
  - **A customer username registered in the insurance database.**

### Open Agent Builder

- Log in to IBM Cloud (cloud.ibm.com). Navigate to top left hamburger menu, then to Resource List. Open the AI/Machine Learning section. You should see a **watsonx Orchestrate** service, click to open.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/0.png">

- Click the "Launch watsonx Orchestrate" button.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/0.5.png">

- Welcome to watsonx Orchestrate. Open the hamburger menu, click on **Build** -> **Agent Builder**.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/2.png">

### Information Agent
#### Create the Information Agent

- Click on **Create Agent**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/3.png">

- Follow the steps according to the screenshot below.
  - Select **Create from scratch**
  - Name the agent `information_agent`
  - Use the following description:
    ```
    The Information agent will fetch the news and different articles and use this information to summarize results and share.
    ```
  - Click **Create** 
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/29.png">

- On the `information_agent` page, take the defaults for **Profile** and **Knowledge** sections. Under the **Toolset** section, click on the **Add tool** button to upload the OpenAPI Spec.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/30.png">

- Click on **Import**.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/31.png">

- Upload the `duckduckgo.json` OpenAPI Spec which will be provided by the instructor.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/32.png">
- Once the file is uploaded, select **Next**.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/33.png">

- Select the all of the **Operations** and click **Done**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/34.png">

- Go to the **Behavior** section. Add the following for **Instructions**. This will define how the Agent should behave and what it should expect:
  ```
  The Information Agent will use the tool to search for information and return a summarized result.
  ```
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/35.png">
- Click on **Deploy** to deploy the agent
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/36.png">

#### Test the Information Agent

  Type this query:
  ```
  Insurance laws for fire in California
  ```
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/ia-flow-1.png">

- You will get a summarized version of all the search results. You can click on the **Step 1** and see the tool results

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/ia-flow-2.png">

### Customer Claims Agent
#### Create the Customer Claims Agent

- Click on hamburger menu, then **Build** -> **Agent Builder**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/17.png">

- On the next screen, click on **Create Agent**
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/18.png">

- Follow the steps according the screenshot below
  - Select **Create from scratch**
  - Name the agent `customer_claims_agent`
  - Use the following description:
    ```
    The Customer Claims agent will allow customers to query the status of their claim request and create a new claim request. You will also answer questions based on the claim process and insurance policy using the knowledge base.
    ```
    <img width="1000" alt="image" src="./screenshots_hands_on_lab/19.png">
  - Click **Create**
- In the **Knowledge** section, add the following to the **Description**:
  ```
  This knowledge base is about insurance and the claim process. This knowledge base will help the customer in getting information about the claims process and the rules and regulations of processing insurance claims.
  ```

- Download [Automobile Insurance Knowledge Base.pdf](<./data/Automobile Insurance Knowledge Base.pdf>) to your local system, then upload by clicking on **Upload files** under **Documents**
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/20.png">
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/21.png">
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/21_1.png">

- In the **Toolset** section, click on **Add tool** 

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/22.png">

- Click on **Import**. Import the `customer_claims_agent_tools.json` OpenAPI Spec file provided by your instructor

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/23.png">
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/24.png">

- Select **Next**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/25.png">
- Select all of the **Operations** and click **Done**
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/26.png">

- In the **Behavior** section, add the following prompt to the **Instructions**:

  ```
  If the user requests to submit a claim, follow these steps:
  1. Collect Required Information (no assumptions). Ask the user to provide the following details:
  - Full name (for authentication)
  - The location of the incident
  - The date of the incident
  - Vehicle details and type
  - A detailed description of the incident

  If any of these are missing, pause and request them before continuing.

  2. Request the all of the following additional information (only if not already provided):
  - Was the incident reported to the police? If yes, what date and time?
  - Were there any damages? What is the estimated cost?
  - Were there any medical expenses? If yes, how much?

  Compute the total estimated cost by summing up damages and medical expenses.

  3. Create the Claim Request. Once all necessary information is collected:
  - Create a concise, structured summary of the incident and related details.
  - Use this information as claim_request_details in the ‘Create a Claim Request’ tool.

  If the tool returns a successful claim, do all of the following:
  - Display the results in a formatted table, with each detail on a new line
  - Highlight the claim number
  - Inform the user: “You will receive a confirmation of your claim request by mail.”

  If the tool returns "customer not found":
  - Respond with: “You are not authorized to submit a claim.”
  - Do not display any additional tool output.

  If the user asks about Claim Status, follow these steps:
  1. Ask for their name 
  2. Ask for the claim number
  3. Use the ‘Check Claim Status’ tool to retrieve the claim status
  4. Display the result in a clean, tabular format. Each detail should be on a new line.
  5. End the conversation after displaying the claim status

  If the user asks questions about:
  - Insurance processes
  - Claim eligibility
  - Documentation
  Refer to the “Automobile Insurance Knowledge Base.pdf” knowledge base only. If the answer is not in the knowledge base, reply: “I don’t know.”

  Do not reference the knowledge base while interacting with tools.
  ```
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/27.png">

- Click on **Deploy** to deploy the agent

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/28.png">

#### Test the Customer Claims Agent
  
  Step 1. Enter a basic query:
   ```
   What are the different types of automobile insurance?
   ```

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claims-flow-1.png">

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claims-flow-2.png">

  Step 2. Check the flow for creating a new claim

   Enter the following:
   ```
   Submit a new claim
   ```
   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-3.png">

   **NOTE** your instructor will provide you with a name from the deployed database to use for all of your claims entries. Enter the name provided. Each participant needs to use a different name.

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-4.png">

   For location, enter `St Mary's Street, San Francisco, California` or any other address.

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-5.png">

   For date, enter `23-05-2025` or any other date

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-6.png">

   For vehicle information, enter `Toyota Corolla, 2003` any other vehicle details

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/vehicle_details.png">

   For details, enter: 
   ```
   I was driving to work when a red pickup truck ran a red light and collided with the rear right side of my vehicle at the intersection. The impact caused my car to spin slightly, resulting in damage to the rear bumper, right-side tail light, and a dent in the rear quarter panel. I was wearing a seatbelt and did not sustain serious injuries, but I reported minor back pain and visited a doctor the same day. Medical expenses were $3400 and the damages repair cost was $4500.
   ```

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-7.png">

  Step 3. Check the flow for claim status

   Enter the query

   ```
   Check claim status
   ```

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-8.png">

   Enter the name you were provided

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-10.png">

   For claim number, enter the claim number from the summary of the claim you just created

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/claim-flow-11.png">

You can create additional claims for your assigned name to test the next agent.

### Claim Processor Agent
#### Create the Claim Processor Agent

- Click on hamburger menu, then **Build** -> **Agent Builder**.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/2.png">

- Click on **Create Agent**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/38.png">

- Follow the steps according the screenshot below.
  - Select **Create from scratch**
  - Name the agent `claim_processor_insurance_agent`
  - Use the following description:

    ```
    The Claim Processor agent assists the claim processor to fetch the open claim request, approve, validate, and verify the open request. This agent will suggest to the claim processor whether they should accept or reject the claim.
    ```

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/4.png">

- In the **Knowledge** section, add the following to the **Description**:
  ```
  This knowledge base is about insurance and the claim process. This knowledge base will help the claim processor in processing the claims according to the rules and regulations defined by the insurance company. 
  ```
- Download [Policy.pdf](<./data/Policy.pdf>) to your local system, then upload by clicking on **Upload files** under **Documents**. 

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/5.png">
  <img width="1000" alt="image" src="./screenshots_hands_on_lab/6.png">

- In the **Toolset** section, click on **Add tool**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/37.png">

- Click on **Import**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/8.png">

- Upload the `claim_processor_agent_tools.json` OpenAPI Spec provided by the instructor

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/9.png">

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/10.png">

- Select all of the **Operations**. Then, select **Done**.

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/11.png">

  <img width="1000" alt="image" src="/usecases/autoclaim-insurance/assets/screenshots_hands_on_lab/11_1.png">

- Click on **Add Agent**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/12.png">
- Click **Add from local instance**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/13.png">

- Select **information_agent** and then the **Add to Agent button**

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/14.png">

- In the **Behavior** section, add the following for **Instructions**:
  ```
  You will begin by welcoming the claim processor and displaying the open claims in a table. 
  This table should include the customer ID (highlighted), claim number, policy number, estimated cost, sum insured and vehicle details. Do not show duplicates.

  Ask the claim processor to select a customer ID 

  If there are multiple claims for a customer ID, ask claim processor to select a claim number.

  Use the claim number and customer id to fetch details using the Fetch Open Claims tool, it's very important, return error if unable to run the tool.

  Once a customer ID is selected, fetch the corresponding claim and policy details for that customer ID and show them in a tabular format and then generate summary on the following points

  1. Compare the estimated cost with the sum insured and calculate the approved claim amount by subtracting the deductible. Highlight the approved amount.

  2. Check if the policy is currently active and whether the claim falls within the coverage period.

  3. Classify the accident into one of the following types: rear-end collision, head-on collision, side-impact, sideswipe, single-vehicle, multi-vehicle pileup, hit-and-run, parking lot, animal collision, weather-related, mechanical failure-related, vandalism, or theft.

  4. Determine if the classified accident type is covered by the policy. If policy details are not clear, refer to the knowledge base to verify.

  5. It is mandatory for you to use the information_agent to query for the accident type you discovered in step 4. Query: The rules and regulations for accident type in US. Use the result to verify if the claim details are compliant.

  6. Provide a clear recommendation to accept or reject the claim based on these checks.

  7. Highlight the total claim amount (estimated cost minus deductible).

  8. Create a clear and concise summary for the claim processor, emphasizing key details like approved amount, claim number, and policy number.
  HIGHLIGHT ALL THE DETAILS IN NEAR FORMAT.

  Finally, ask the claim processor "Whether they accept the claim?"
  Do not give next steps. 

  Once a decision is made, update the claim status and send a message confirming that emails have been sent to the customer and finance team.
  ```

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/15.png">

- Click on **Deploy** to deploy the agent

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/16.png">

#### Test the Claim Processor Agent

  Step 1. Enter the basic query

   ```
   Show open claims
   ```

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/cp-flow-1.png">

  Step 2. Enter a Customer ID from the list

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/cp-flow-2-new.png">

  Step 3. Input Claim Number from the list

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/cp-flow-3.0-new.png">

  Step 4. When prompted to accept the claim respond:

   ```
   Yes
   ```

   <img width="1000" alt="image" src="./screenshots_hands_on_lab/cp-flow-4-new.png">

  Step 5. You should see an update confirmation

  <img width="1000" alt="image" src="./screenshots_hands_on_lab/cp-flow-5-new.png">

### Further testing via AI Chat
>
> ***You can also test the agents from AI chat.***

Navigate to AI chat by going to the hamburger menu at top left and select **Chat**.

<img width="1000" alt="image" src="./screenshots_hands_on_lab/39.png">

Then select the agent to test: 

<img width="1000" alt="image" src="./screenshots_hands_on_lab/40.png">
