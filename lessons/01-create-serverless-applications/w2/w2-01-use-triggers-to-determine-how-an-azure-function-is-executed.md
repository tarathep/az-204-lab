# Use triggers to determine how an Azure Function is executed

## The best trigger for azure function

- ``Timer``
- ``HTTP``
- ``Blob``
- Queue
- Azure CosmosDB
- Event Hub

## Run an azure function a schedule

that use CRON Expression

execute every 5 min

```cron
0 */5 * * * *
```

What is the correct order for the time fields in a CRON expression?

- Seconds, minutes, hour, day, month, weekday of the week
  - The correct sequence of a CRON expression is Seconds, minutes, hour, day, month, weekday of the week.

can create at azure portal and on program at VScode, Visual studio , others


## Knowledage Check

```1.When creating a timer trigger, what information do you need to provide?```

Select all options that apply.

- A schedule via a CRON expression
  - A CRON expression sets the interval for the timer.
- A timestamp parameter name
  - This parameter is used as an identifier to access the trigger in code.

```2.You want to write a CRON expression that creates a trigger that executes every 10 minutes.```

Which of the following is the correct string?

- 0 */10 * * * *
  - this string executes every 10 minutes.

```3.You plan to execute a function any time a document changes in a collection inside a database. Which type of trigger should you configure?```

- Azure Cosmos DB
  - This type of trigger executes a function when a document changes inside a collection.

```4.True or False?```

You can create a timer trigger using Visual Studio Code.

- You can also create triggers programmatically using Core Tools, Visual Studio or Visual Studio Code.

```5.You want to build a function app that does not run continuously. Which plan should you use to minimize costs and maintenance?```

- Serverless
  - You only pay for the time your functions run. Billing is based on number of executions, execution time, and memory used.


## Test Prep

```Question 1```

You’re developing an HTTP-triggered Azure Function app to process Azure Storage blob data. The app is triggered using an output binding on the blob. The app continues to time out after four minutes. The app must process the blob data. You need to ensure the app does not time out and processes the blob data.

Solution: Pass the HTTP trigger payload into an Azure Service Bus queue to be processed by a queue trigger function and return an immediate HTTP success response.

Does the solution meet the goal?

- Yes
  - Large, long-running functions can cause unexpected timeout issues. Whenever possible, refactor large functions into smaller function sets that work together and return responses fast. For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it's common for webhooks to require an immediate response. You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function. This approach lets you defer the actual work and return an immediate response.


```Question 2```
You are developing an Azure Function App that processes images that are uploaded to an Azure Blob container. ```Images must be processed as quickly as possible after they are uploaded```, and the solution must ```minimize latency```. You create code to process images when the Function App is triggered.

You need to configure the Function App.

What should you do?

- Use an App Service plan. Configure the Function App to use an Azure Blob Storage trigger.
  - The requirement is to minimize the latency. If your function app is on the ```Consumption plan, there can be up to a 10-minute delay``` in processing new blobs if a function app has gone idle. To ```avoid this latency```, you should use an ```App Service plan``` with Always On enabled.

```Question 3```
You are developing a software as a service (SaaS) offering to manage photos. Users upload photos to a web service which then stores the photos in Azure Storage Blob storage. The storage account type is General-purpose V2. When photos are uploaded, they must be processed to produce a thumbnail version of the image. The process to produce a mobile-friendly version of the image should start in less than one minute.

You need to design the process that starts the photo processing.

Solution: Move photo processing to an Azure Function triggered from the blob upload.

Does the solution meet the goal?

- Yes
  - The Blob storage trigger starts a function when a new or updated blob is detected. The blob contents are provided as input to the function. The Azure Blob storage trigger requires a general-purpose storage account. Storage V2 accounts with hierarchal namespaces are also supported.


```Question 4```
You are developing a software as a service (SaaS) offering to manage photos. Users upload photos to a web service which then stores the photos in Azure Storage Blob storage. The storage account type is General-purpose V2. When photos are uploaded, they must be processed to produce a thumbnail version of the image. The process to produce a mobile-friendly version of the image should start in less than one minute.

You need to design the process that starts the photo processing.

Which of the following solutions is the most efficient and meets the goal?

- Create an Azure Function App that uses the Consumption hosting model and that is triggered from the blob upload.
  - If your function app is on the Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle. To avoid this latency, you can switch to an App Service plan with Always On enabled.

```Question 5```
You have an application named Application1. Application1 uses Azure Cosmos DB that is configured with 200 RU/s. You need to configure the database to auto scale based on the working hours. The database must scale-up to 500 RU/s during working hours whereas scale-down to 200 RU/s in non-working hours.

How should you configure auto-scale?

- Create a time-based Azure Function to scale Azure Cosmos DB
  - One of the ways to achieve this requirement is to create a function that handles scale-up and scale-down of Azure Cosmos DB.

```Question 6```
What are the three authorization levels supported by the HTTP triggers?

Select all options that apply.

- ``Function`` : authorization level requires a function-key or a host-key.
- ``Admin`` : This authorization level requires a host key.
-``Anonymous`` : The Anonymous level means that there's no authentication required.


```Question 7```
You are developing an Azure function that has a blob trigger associated with it and it must execute only when PNG images are uploaded. Which blob trigger path values should you use?

- samples-workitems/{name}.png
  - This path will filter all the files and execute only when a PNG file is uploaded. 