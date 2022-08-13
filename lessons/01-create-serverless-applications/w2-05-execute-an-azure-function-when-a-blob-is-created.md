# Execute an Azure function when a blob is created

## What is Azure Storage?

Azure Storage is Microsoft's cloud storage solution that supports all types of data, including blobs, queues, and NoSQL. The goal of Azure Storage is to provide data storage that's:

- Highly available
- Secure
- Scalable
- Managed

For example, Azure Blob storage is great at doing things like:

- Storing files
- Serving files
- Streaming video and audio
- Logging data

## What is a blob trigger?
A blob trigger is a trigger that executes a function when a file is uploaded or updated in Azure Blob storage. To create a blob trigger, you create an Azure Storage account and provide a location that the trigger monitors.

## How to create a blob trigger
Just like the other triggers we've seen so far, we create a blob trigger in the Azure portal. Inside your Azure function, select Blob trigger from the list of predefined trigger types. Then, enter the logic to execute when a blob is created or updated.

One setting that you'll want to look at is the Path. The Path tells the blob trigger where to monitor to see if a blob is uploaded or updated. By default, the Path value is:

```path
samples-workitems/{name}
```
