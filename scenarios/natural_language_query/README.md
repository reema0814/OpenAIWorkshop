# Build Open AI Application on Power App to allow users to use natural language question on top of SQL data
### Summary.

This scenario allows users to use Open AI as an intelligent agent to get business questions prompts from end users and generating SQL queries from the prompts.This implementation scenario focuses on building a Nautual Language to query from business questions and genarte the queries for database retrieval 
### Architecture Diagram
<img width="693" alt="image" src="https://user-images.githubusercontent.com/50298139/222239136-9149247e-b6e9-4b8b-8519-be7c8f3723b4.png">


### Solution Flow

Step 1: Context information is provided to system through a Power App form, this information is submitted to Azure function

Step 2: Azure Open AI engine converts the user context prompt to SQL query and passes the query to Azure function

Step 3: Azure function passes the context information to Open AI Engine to convert the user context information prompt to SQL Query

Step 4: The Azure function passes the genrated SQL query text and executes the query on Azure SQL databse 

Step 5: The query is executed on SQL database and results are returned to Azure function

Step 6: Azure function returns the results to end user 

## 1. Azure services deployment



- Step 1: Create SQL server with Sample database
    As part of data preperation step, please foolow the below link to create the SQL database in the resourcegroup you wil like to host your databbase and openai service  https://www.sqlshack.com/create-an-azure-sql-database-with-built-in-sample-data/
    

   
## Step 2: Automated orchestrator service with Azure Function App

    Update the below configuration in Azure Function App configuration blade. 

            {
                "name": "GPT_ENGINE",
                "value": "text-davinci-003",
                "slotSetting": false
            },
            {
                "name": "OPENAI_API_KEY",
                "value": "<>",
                "slotSetting": false
            },
            {
                "name": "OPENAI_RESOURCE_ENDPOINT",
                "value": "https://<>.openai.azure.com/",
                "slotSetting": false
            }





## Step 3. Deploy client Power App

From the powerapp folder, download Semantic-Search-App-Template_20230303012916.zip powerapp package. This has a powerapp and powerautomate template app pre-built.
Navigate to https://make.powerapps.com/ and click on Apps on the left navigation. 

![](../../documents/media/powerapps1.png)


From the top nav bar, click Import Canvas App and upload the Semantic-Search-App-Template_20230303012916.zip file from this git repo path. 


![](../../documents/media/powerapps2.png)





Click on Import to import the package into powerapps environment. 




<img width="767" alt="image" src="https://user-images.githubusercontent.com/50298139/222616796-8254cf53-e6d4-4cb4-b321-960615338006.png">
<img width="827" alt="image" src="https://user-images.githubusercontent.com/50298139/222617130-ce142de3-1aae-40bd-94e1-b86dfdf93e74.png">
<img width="929" alt="image" src="https://user-images.githubusercontent.com/50298139/222617513-10bf28ae-a2d7-4211-a702-a951098e3c3c.png">
<img width="926" alt="image" src="https://user-images.githubusercontent.com/50298139/222618019-49eab211-1c77-474c-a3aa-8f377df26255.png">


This will import the Power App canvas app and Power Automate Flow into the workspace. 


<img width="746" alt="image" src="https://user-images.githubusercontent.com/50298139/222619006-e9eaa507-836b-4ba7-bf1f-d78e0d84479d.png">

<img width="706" alt="image" src="https://user-images.githubusercontent.com/50298139/222617320-e84339ba-ecd7-46dd-88e2-a1879df84a5a.png">

In the Flows Pane, PowerAutomate Flow needs to be enabled. At this point, the powerapp can be run as is. It connects to a pre-built Azure Function App. 

<img width="928" alt="image" src="https://user-images.githubusercontent.com/50298139/222619285-09a545a9-73c3-4dd9-a1b6-c9cc2ca7e440.png">
Edit the Power Automate Flow and update Azure Function Url. 



<img width="492" alt="image" src="https://user-images.githubusercontent.com/50298139/222619362-c786a8f7-a070-4846-837b-6b083b82f6c6.png">
## Step 5. Test

Click on the play button on the top right corner in the PowerApps Portal to launch PowerApp and click submit
. 
Feel free to make changes to the PowerApps UI to add your own functionality and UI layout. You can explore expanding PowerAutomate flow to connect to other APIs to provide useful reference links to augment the response returned from OpenAI.

