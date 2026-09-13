# Introduction to the Conversational Analytics in BigQuery

**Duration:** 1 hour  
**Cost:** No cost

> **Note:** This lab may incorporate AI tools to support your learning.

## Introduction

Getting insights from data often requires significant time, effort, and deep SQL expertise. In this lab, you will explore **BigQuery's Agent Catalog**, a new platform that delivers instant, AI-driven insights through conversational data agents.

You will move beyond simple text-to-SQL conversion by creating a curated data agent. You will learn how to enrich the agent with business context, system instructions, and verified queries to ensure highly accurate results. Finally, you will publish this agent for use by others in your organization.

### Prerequisites

- A basic understanding of Google Cloud

### What you'll learn

- How to navigate the BigQuery Agent Catalog
- How to create a Custom Agent and define knowledge sources
- How to use Gemini to generate semantic metadata
- How to add System Instructions and Verified Queries to guide the agent
- How to publish and share agents

## Set Up Your Environment

### Before you click the Start Lab button

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click **Start Lab**, shows how long Google Cloud resources are made available to you.

This hands-on lab lets you do the lab activities in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials you use to sign in and access Google Cloud for the duration of the lab.

To complete this lab, you need:

- Access to a standard internet browser (Chrome browser recommended).

**Note:** Use an Incognito (recommended) or private browser window to run this lab. This prevents conflicts between your personal account and the student account, which may cause extra charges incurred to your personal account.

- Time to complete the labâ€”remember, once you start, you cannot pause a lab.

**Note:** Use only the student account for this lab. If you use a different Google Cloud account, you may incur charges to that account.

### How to start your lab and sign in to the Google Cloud console

1. Click the **Start Lab** button. If you need to pay for the lab, a dialog opens for you to select your payment method. On the left is the Lab Details pane with the following:
   - The Open Google Cloud console button
   - Time remaining
   - The temporary credentials that you must use for this lab
   - Other information, if needed, to step through this lab
2. Click **Open Google Cloud console** (or right-click and select **Open Link in Incognito Window** if you are running the Chrome browser).

   The lab spins up resources, and then opens another tab that shows the Sign in page.

   ***Tip:*** Arrange the tabs in separate windows, side-by-side.

   **Note:** If you see the **Choose an account** dialog, click **Use Another Account**.
3. If necessary, copy the **Username** below and paste it into the **Sign in** dialog.
   ```
   "Username"
   ```
You can also find the Username in the Lab Details pane.
4. Click **Next**.
5. Copy the **Password** below and paste it into the **Welcome** dialog.
   ```
   "Password"
   ```
You can also find the Password in the Lab Details pane.
6. Click **Next**.

   **Important:** You must use the credentials the lab provides you. Do not use your Google Cloud account credentials.

   **Note:** Using your own Google Cloud account for this lab may incur extra charges.
7. Click through the subsequent pages:
   - Accept the terms and conditions.
   - Do not add recovery options or two-factor authentication (because this is a temporary account).
   - Do not sign up for free trials.

After a few moments, the Google Cloud console opens in this tab.

**Note:** To access Google Cloud products and services, click the **Navigation menu** or type the service or product name in the **Search** field. ![Navigation menu icon and Search field](https://cdn.qwiklabs.com/9Fk8NYFp3quE9mF%2FilWF6%2FlXY9OUBi3UWtb2Ne4uXNU%3D)

## Before you begin

### Grant required roles

Navigate to the [project's IAM page](https://console.cloud.google.com/iam-admin/iam) and grant `Username` the **Gemini Data Analytics Data Agent Owner** role and **Save**:

![4bc781d1a83ba367.png](https://cdn.qwiklabs.com/sn2roIS6BgGGnGnfi%2BCkUEyVXWdvMltun0NllghyAwk%3D)

This role grants you permission to create, edit, share, and delete all data agents in the project.

### Enable the required APIs

Use the sidebar navigation menu or search menu at the top of the page to navigate to **BigQuery > Agents**.

Click **Enable conversational analytics**:

![4bc781d1a83ba367.png](https://cdn.qwiklabs.com/TiuZaJUxvMhuMr5wk4tdyzPkK7oNlln2L6YQm8LV9Ug%3D)

Enable both the **Data Analytics API with Gemini** and the **Gemini for Google Cloud API**:

![71678b9b8900a7a6.png](https://cdn.qwiklabs.com/ETtXQprhmPIrhz2pa3ZLGY%2Flgom5%2B1alHqxuFqupYaU%3D)

You should now see the new agent page:

![23935c00cd4b23c1.png](https://cdn.qwiklabs.com/ORwHuc8whtT4BFdgRdGlFZNpE7cQBg7C73Vp2BxyKYo%3D)

Please follow these steps:

- On the BigQuery page, click on **Studio**, then select **Explorer**.
![BigQuery Explorer](https://cdn.qwiklabs.com/dvAERfHQR9aQx7E8hV%2B6TJ6xjk5V%2BmvOnLsdBjBGZj4%3D)

- Click on **+ Add data**.
- At the bottom of the page, click on **Star a project by name** and enter the name: **bigquery-public-data**.

![Star a project by name](https://cdn.qwiklabs.com/AjAq8M3xRNKBU6pjnjN8fkQIEp9E1aJJUXhxbpkf0vY%3D)

## Task 1. Create an agent

Let's create your first data agent using the [Google Trends International Public dataset](https://cloud.google.com/blog/products/data-analytics/international-google-trends-datasets-in-bigquery). This dataset is useful for asking questions about what search terms are trending internationally, and how those interests compare historically.

Navigate to **BigQuery > Agents**. Click **+ Create Agent**, let's start by giving your agent a name and brief description. This description is purely used for other users to understand the agent's purpose.
### Agent Name
Enter the Agent Name
```
Google Trends Agent
```
### Agent Description
Enter the Agent Description:
```
Data agent for the Google Trends International Top Terms public dataset
```
### Knowledge Sources
Now add the knowledge sources. A knowledge source is a BigQuery table, view, or UDF that the agent can use to answer questions.

For this lab, add only one table to keep things simple. However, keep in mind that you can add up to 50 knowledge sources per agent to handle more complex data scenarios.

Click **Add source** and enter the following table in the search box, press **Enter** check the box, and click **Add**:
```
bigquery-public-data.google_trends.international_top_terms
```
**Note:** It may take some time to show the suggested table. If not found, select `bigquery-public-data` database and then `google_trends` dataset and then `international_top_terms` table manually.

![7.png](https://cdn.qwiklabs.com/Mp80ABk3au2ZeImO0rTZau9hr8NH9XA2LcxgxHmcrgc%3D)

To improve the data agent's accuracy, add structured context to the table and columns. Click **Customise**:

![f802527c7d72ae63.png](https://cdn.qwiklabs.com/aPW9JiN3ZX7aIbQryZHDLuwvwSlqKMHd3uhItzF1wKA%3D)

**Note:** This allows adding descriptions at the table and column levels. Since the source is a public dataset that cannot be modified directly, these overrides help the agent understand the data without altering the original table.




Gemini automatically generates suggestions for descriptions. Click **Accept** next to the Table description:

![cc02e10c0c74bf4b.png](https://cdn.qwiklabs.com/WNmlgsDQ8sf9fTUklRN4dbTjpMkwAttF%2BCt7KB1jdiA%3D)

To apply descriptions to all columns, check **Select all rows** and then click **Accept suggestions**:

![f811458ff0240c.png](https://cdn.qwiklabs.com/1k4HQqZ9Kzr01oB25ppaCjnkzD0IVN1thJiMepyc9jU%3D)

**Optional:** Manually edit specific fields by clicking the edit icon next to a column name.

Click **Update** at the bottom of the page to save changes and return to the Agent Editor.
### Region
Please leave the **Default Region** unchanged and proceed.
### Instructions
The agent instructions dialog is where you can give the agent additional guidance for it to interpret and query the data sources. This includes:
- **Synonyms**: Alternative terms for key fields.
- **Key fields**: The most important fields for analysis.
- **Excluded fields**: Fields that the data agent should avoid.
- **Filtering and grouping**: Fields that the agent should use to filter and group data.
- **Join relationships**: How two or more tables are combined based on common fields.
To learn more about the nuances between agent instructions (free-form supplemental guidance) and structured context, refer to the [authored context guide for the Conversational Analytics API](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/data-agent-authored-context-bq).

For best practices on agent instructions, refer to the [Create data agent guide](https://docs.cloud.google.com/bigquery/docs/create-data-agents#best-practices-instructions).

Copy and paste the following instructions:
```
### System Instruction

* You are an expert data analyst for the Google Trends International public dataset.
* Always filter on yesterday's refresh_date = DATE_SUB(CURRENT_DATE(), INTERVAL 1 DAY).
* If yesterday returns no data, filter on 2 days ago's refresh_date = DATE_SUB(CURRENT_DATE(), INTERVAL 2 DAY).
* Default to country-level results (one row per term).
* "Top" queries must deduplicate snapshot rows.
* Only include week or score when the user explicitly asks for trends over time.
* This is an international dataset and does not include any data for the United States.

### Additional Descriptions

#### 1. Core model:

* refresh_date selects the daily Top-25 term set.
* week + score are historical weekly values attached to those terms.
* Filtering week does not change which terms appear.

#### 2. Deduplication rule (critical):

* Snapshot rows repeat across weeks and regions.
* For "top" queries, always GROUP BY term (country-level) and compute rank as MIN(rank).

#### 3. Defaults:

* Country-level results only.
* Use region_code only if the user explicitly asks for regions.
* Limit results unless the user asks otherwise.

#### 4. Time series usage:

* Only include week or score when the user asks for trends over time, historical context, or week-over-week score changes.

#### 5. Field guidance:

* Prefer country_code or region_code for filters.
* country_name / region_name are for display only.
* score is normalized; compare trends within a term, not across terms.
```
### Verified Queries
Verified queries, previously known as *golden queries*, are used as a reference for the agent to improve response accuracy. They shape an agent's response structure and help teach the agent the business logic that your organization uses.

Let's add two examples for your agent. Click **Add query**, and copy / paste the following question and query:

**Question 1:**
```
What are the top search terms in the UK right now?
```
**Query 1:**
```
SELECT term, MIN(rank) AS rank
FROM bigquery-public-data.google_trends.international_top_terms
WHERE refresh_date = DATE_SUB(CURRENT_DATE(), INTERVAL 1 DAY)
  AND country_name = 'United Kingdom'
GROUP BY term
ORDER BY rank
LIMIT 25;
```
Before **saving** this query, let's **run** it to make sure that it's valid.

![e3fb570a4109e93c.png](https://cdn.qwiklabs.com/1Nh%2BUeeHenKBh3kZWvEzDCu14ECcXb96nHAreFXysqo%3D)

Looks good to me! Click **Add** to save the verified query.

Let's add one more example for a more complex use case. Click **Add query**:

**Question 2:**
```
Show the last 12 weeks of interest for the current top 5 terms in Auckland.
```
**Query 2:**
```
WITH top5 AS (
  SELECT term, MIN(rank) AS rank
  FROM bigquery-public-data.google_trends.international_top_terms
  WHERE refresh_date = DATE_SUB(CURRENT_DATE(), INTERVAL 1 DAY) 
  AND region_name = 'Auckland'
  GROUP BY 1
  ORDER BY 2
  LIMIT 5
),
series AS (
  SELECT term, week, score,
    ROW_NUMBER() OVER (PARTITION BY term ORDER BY week DESC) AS rn
  FROM bigquery-public-data.google_trends.international_top_terms
  WHERE refresh_date = DATE_SUB(CURRENT_DATE(), INTERVAL 1 DAY) 
    AND region_name = 'Auckland'
    AND term IN (SELECT term FROM top5)
)
SELECT week, term, score
FROM series
WHERE rn <= 12
ORDER BY 1 DESC, 3
```
Let's **run** and **Add** the verified query.

Before moving on to the next section, let's look at the **Gemini-generated suggestions**:

![b52489d21f503a76.png](https://cdn.qwiklabs.com/s2MEAwspUJEtqF6hmd6i4fJWdHJBWQM3vxU7trUHLwQ%3D)

Here you can see some suggested verified queries. When creating a new agent in the future, this is a great starting point. Just make sure to validate any query that you add!
### Glossary
Let's add a term to the glossary. If your business uses Dataplex, these terms are imported directly from the business glossary in the Dataplex Universal Catalog.

Click **Add term**, and copy / paste the following example:

**Term:**
```
refresh_date
```
**Definition:**
```
Snapshot date that selects the daily Top 25 term set. All rows for that date belong to the same "what's trending now" snapshot. Attach Historical week and score values after this selection.
```
**Synonyms:**
```
today, latest, current, now, recent
```
Please leave the **Default Region** unchanged and proceed.

Then click **Add**, then **Save**.

![33b4a74fcde504d5.png](https://cdn.qwiklabs.com/YGLucdAWM%2FwU6fVaW87gR77hDrcvyIaoY3v4JUCoSRc%3D)
### Agent settings
In the **Agent settings** section, you can configure **Labels** and the **Maximum Bytes Billed**.
#### Labels
[Labels](https://docs.cloud.google.com/bigquery/docs/labels-intro) are key-value pairs used to organize Google Cloud resources into logical groups. To keep this lab focused, leave the labels blank.
#### Maximum Bytes Billed
To ensure you don't accidentally generate any expensive queries, let's set a limit for the maximum bytes billed per query. If the agent's query processes bytes above this limit, the query fails without incurring a charge. Input the following value:
```
10000000000
```
10,000,000,000 bytes is approximately 9.3 GB. If you don't specify a value, the maximum bytes billed defaults to the project's [query usage per day quota](https://docs.cloud.google.com/bigquery/quotas#query_jobs).

Click *Check my progress* to verify the objective.

> **Progress check:** Create an agent.



## Task 2. Saving and sharing your agent
### Preview
We're all set! Let's test your agent before moving on. On the right side of the screen you can dynamically test the agent while making edits to the configuration. The preview automatically uses the new metadata you provide without saving or publishing the changes.

Let's ask what data the agent has access to. Feel free to ask a few questions in your own words:

![b2679cc7c6c926b2.png](https://cdn.qwiklabs.com/RhvZewzqow2TotkMLzF%2BVRPQoITH4QjZkKxZLJoZZ%2FY%3D)
### Save
After testing a few prompts, **Save**, and then **Publish** the agent:

![56a45347d496dd42.png](https://cdn.qwiklabs.com/8GqmnTlLGqLdFl7GLpuI1UNQu%2FzDn%2BnI33eOgzDJbyc%3D)

Publishing the agent will make it available in BigQuery Studio, the Conversational Analytics API, and Looker Studio Pro (subject to licensing):

![a4fbeb3011d409f5.png](https://cdn.qwiklabs.com/pHsx%2BmgHadKeE2Z6frJYK3mxL%2Be9fY3H8px6fr9qiR0%3D)

Support for additional surfaces and integrations is planned for future releases.
### Share
You should see a confirmation message that the agent has been published. You can now share this agent with other users.

![bdd4ee4be02c26d8.png](https://cdn.qwiklabs.com/MeML5VHClkGcD31ZcYIAU4yMtA1hAQP7YsooXuQIy4w%3D)

When you share an agent with other users, you control their level of access by assigning them a specific role. These roles determine whether a collaborator can simply view your agent, or if they have the power to edit and manage its configuration.

It's important to note that these roles can be applied at two different levels:
- **Project Level**: Granting a role at the project level provides the user with those permissions for all agents within that Google Cloud project.
- **Agent Level**: For more granular control, you can grant roles for a specific agent. This is useful when you want a user to have access to one particular data agent without seeing others in the project.
For a detailed breakdown of how to manage access, refer to the Conversational Analytics API documentation on [typical IAM scopes](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/key-concepts#iam-roles) and the specific [permissions included in each predefined role](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/access-control#predefined-roles).




The predefined roles for Conversational Analytics are as follows:
1. **Gemini Data Analytics Data Agent Owner** (roles/geminidataanalytics.dataAgentOwner) **-** Create, Edit, Share, and Delete **all data agents**
2. **Gemini Data Analytics Data Agent Creator** (roles/geminidataanalytics.dataAgentCreator) - Create, Edit, Share, and Delete **your own data agents**
3. **Gemini Data Analytics Data Agent Editor** (roles/geminidataanalytics.dataAgentEditor) - Chat and Edit access to data agents
4. **Data Analytics Data Agent User** (roles/geminidataanalytics.dataAgentUser) - Chat and View access to data agents
5. **Gemini Data Analytics Data Agent Viewer** (roles/geminidataanalytics.dataAgentViewer) - View (read only) access to data agents
Click **Save** then **Close.**

## Task 3. Create conversation with an agent
Let's exit out of the **Share** tab and create a new conversation:

![d7a824ed0aaeaf12.png](https://cdn.qwiklabs.com/vOsxSiK1oHIfvZj%2BVMqRuvZyQRyFIS8QKl07a8YLdAk%3D)

When you click **Create conversation**, a new untitled conversation is generated.

Let's ask about what terms are trending in England (feel free to replace with a location of your choice!):
```
Based on the top 10 terms in England, how did they trend for the past 3 months?
```
### Unpacking the response stream
The data agent typically follows the same response stream when answering questions:
1. **Reasoning**: The agent first "thinks" through the prompt. Expand the **Show reasoning** button to view step-by-step insights into the agent's decision-making process.
2. **Summary**: The agent generates a high-level summary of the query, the resulting report, and the visualization.
3. **Generated SQL**: Expand the **Here's the query...** section to inspect the SQL. Click **Open in Editor** to fine-tune the query manually in BigQuery Studio.
4. **Data Results**: The agent presents the query results in a clear, tabular format.
5. **Visualization**: A chart appears alongside a brief description. The agent automatically infers the best visualization type (e.g., a multi-series line chart) for your data.
6. **Data Insights**: The agent summarizes key trends and takeaways found within the results.
7. **Follow-up Questions**: Finally, the agent suggests relevant follow-up questions to help you continue your analysis.
![4.png](https://cdn.qwiklabs.com/01PJSrIzPnhWoNle9kKPvSnt0Q7bfJ3E1EmYXAvfZz4%3D)
### BigQuery ML support
Let's follow up and ask if the data agent can run some forecasting based on these results. This leverages BigQuery ML functions to predict future points.

**Note:** For more details on which ML functions are supported, refer to the [documentation](https://docs.cloud.google.com/bigquery/docs/conversational-analytics#bigquery-ml-support)

Enter the following prompt (make sure to replace "monopoly board" with a term that's relevant for your query!):
```
Can you predict and visualize how monopoly board will trend in the next 4 weeks?
```
You can see `AI_FORECAST` was used to forecast a time series. No surprises, though it is interesting that you can see a major spike in August 2021, which coincides with the grand opening of the Monopoly Lifesized attraction in London!

![441a92d19f7d15e0.png](https://cdn.qwiklabs.com/tWGVHfUefAAKs4ltK6ldujAaxsFXu7MUVin05Z0fJyk%3D)

Click *Check my progress* to verify the objective.

> **Progress check:** Create a conversation with an agent.



## Task 4. Explore the Agent Catalog
Let's explore the Agent Catalog before wrapping up. Click on **Agent Catalog** at the top of the window:

![5.png](https://cdn.qwiklabs.com/%2BjbJmc8bz61FR%2BJIvALsKi%2F7TJ8bayHl8gzhTZT8bTY%3D)

This page serves as your central hub for data agent management, organized into the following sections:
- **My agents**: Your currently published agents.
- **My draft agents**: Configurations you have saved but not yet published.
- **Shared by others in your organization**: Agents created by colleagues that you have permission to access.
- **Sample agents by Google**: Pre-configured examples to help you get started.

For any agent you manage, you can edit configurations, duplicate agents, and manage sharing permissions.

**Note:** Conversational Analytics in BigQuery is powered by the [Conversational Analytics API](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/overview). Functionality available in the console can also be accessed programmatically via the API, giving you full flexibility to render messages and integrate with additional agents and data sources.

## Conclusion
Congratulations, you've successfully built a Conversational Analytics data agent. Check out the reference materials to learn more!
