# Create serverless logic with azure functions

## Exercise - Create a function app in the Azure portal

https://docs.microsoft.com/en-us/learn/modules/create-serverless-logic-with-azure-functions/3-create-an-azure-functions-app-in-the-azure-portal?pivots=javascript

## Knowleadge check

Question 1 : Which of the following are characteristics of an Azure Functions serverless solution?

- You have no servers to manage
  - Azure Functions is a serverless application platform. It allows developers to host business logic that can be executed without provisioning infrastructure.
- Automatic scaling
  - Serverless computing helps solve the allocation problem by scaling up or down automatically, and you're only billed when your function is processing work.

Question 2 : In terms of execution times, what are the default timeout and the configurable timeout of a function?
In terms of execution times, what are the default timeout and the configurable timeout of a function?

- Default 5 mins, configurable 10 mins.
  - By default, functions have a timeout of 5 minutes. This timeout is configurable to a maximum of 10 minutes.

Question 3 : What makes a function execute in a workflow?

- Triggers
  - Functions are event-driven, which means they run in response to an event, and that type of event is called a trigger.

Question 4 : True or False? Functions cannot be used in traditional compute environments.

- False
  - Functions can also be deployed in non-serverless environments.

Question 5 : Which of the following can you use to test your Azure Functions?

- The Azure Portal itself
  - The portal provides a convenient way to test your functions, by accessing the “Test/Run” blade.
