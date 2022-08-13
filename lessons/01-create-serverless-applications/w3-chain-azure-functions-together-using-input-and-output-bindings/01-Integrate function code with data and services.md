# Integrate function code with data and services

input and output binding types

- Blob Storage
- HTTP endpoints
- Azure Cosmos DB
- External files

bingby JSON

```json
{
    "name":"headshotBlob",
    "type":"blob",
    ...
}
```


## Knownledge check

```Question 1 : True or False?```
 When you are using bindings in your Azure functions, you also need to code specific connection logic to databases or services.

 - False
   - In Azure Functions, bindings provide a declarative way to connect to data from within your code. 


```Question 2 Which types of bindings can be used with AzureFunctions?```

Select all options that apply.

- Input binding
  - Connects to a data source. Our function can read data from these inputs.
- Output binding
  - Connects to a data destination. Our function can write data to these destinations.

```Question 3 In which programming language is a binding defined?```

- JSON
  - Bindings are defined in JSON.


```Question 4 Which of the following services support only output bindings?```

- Event Hubs
  - Event Hubs can be used as output bindings to write events to an event stream.
- HTTP
  - HTTP can be used as output bindings to respond to the HTTP request sender.


```Question 5 Which of the following services support both input and output bindings?```

- Table Storage
  - Table Storage supports both input and output bindings.


  ## Test prep


```Question 1```

You want to create an ```Azure Cosmos DB``` account that uses the SQL API. The account will ```contain data added by a web application```. The web application will ```send data daily```. You need to recommend a notification solution that ```sends an email notification when data is received``` and ```minimizes compute cost```.

What should you include in the recommendation?

- Deploy a function app that is configured to use the Consumption plan, Cosmos DB trigger, and a SendGrid binding.
  - The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function. The document ID or query parameters can be determined based on the trigger that invokes the function. The SendGrid binding enables the function app to send emails.


```Question 2```

You are developing an Azure Function App ```using Visual Studio```. The app will process orders input by an Azure Web App. The web app places the order information into Azure Queue Storage.

You need to review the Azure Function App code shown below:

```c#
public static class OrderProcessor
{
 [FunctionName(“ProcessOrders”)]
 public static void Processorders([QueueTrigger(“incoming-orders”)]CloudQueueMessage myQueueItem [Table (“Orders”)]ICollector<Order> tableBindings,
TraceWriter log)
 {
   log.info($”Processing Order: (myQueueItem.Id)”);
   log.info($”Queue Insertion Time: (myQueueItem.InsertionTime)”);
   log.info($”Queue Expiration Time: (myQueueItem.ExpirationTime)”);
   tableBindings.Add(JsonConvert.DeserializeObject<Order>(myQueueItem.AsString));
}
[FunctionName(“ProcessOrders-Poison”)]
public static void ProcessFailedORders([QueueTrigger(“incoming-orders-poison")[CloudQueueMessage myQueueItem, TraceWriter log)
 {
   LogError($”Failed to process order: (myQueueItem.AsString)”);
 }
}
```

1. The code will log the time that the order was processed from the queue; = ```NO```

2. When the ProcessOrders function fails, the function will retry up to five times for a given order, including the first try; = ```YES```

3. When there are multiple orders in the queue, a batch of orders will be retrieved from the queue and the ProcessOrders function will run multiple instances concurrently to process the orders;  = ```YES```

4. The ProcessOrders function will output the order to an Orders table in Azure Table Storage;  = ```YES```

For each of the following statements mentioned above, select Yes if the statement is true. Otherwise, select No:


```Question 3```

You created a function that ```uses an input binding to read data``` from an Azure ```Cosmos DB``` database.

You now ```want to combine``` that ```input binding with an output binding``` to also ```write data to the Azure Cosmos DB``` database.

You are ```configuring``` the Azure ```Cosmos DB binding from the Portal```.

Which of the following settings should be populated with the container from which you’ll read the data?

- Collection Name
  - In this setting, you’ll need to provide the container name from which the data will be read.


```Question 4```

True or False?

All binding types support both input and output.

- False 
  - There are multiple types of bindings. However, not all types support both input and output.

```Question 5```

Which output binding type can you use to send ```emails through Outlook and modify Excel data?```

- Microsoft Graph


```Question 6```

Which output binding type allows you to send text messages?

- Twilio
  - You can use this binding to send text messages.


```Question 7```

How can you configure an Azure function to read data from a data source?

- You configure an input binding
  - To connect to a data source, you have to configure an input binding.
  