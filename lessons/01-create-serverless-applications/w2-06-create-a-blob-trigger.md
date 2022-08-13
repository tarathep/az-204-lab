# Create a Blob trigger


## 1 Create a Blob trigger

Select a template, select ```Azure Blob Storage trigger```.

at Template detail make to default values and select Storage account connection click new or link to exsiting.

![](../../media/l-8.png)

## 2 Create a blob container

open storage accout and create new container 

```path
samples-workitems/{name}
```

To create a container called ``samples-workitems``:

Select Blob containers, then select Add container. The New container pane appears.

In the Name field, enter samples-workitems, accept the default ```Private``` setting in the Public access level field, and then select Create.

## 3 Upload file to Container blob storage

![](../../media/l-10.png)


![](../../media/l-9.png)

```c#
public static void Run(Stream myBlob, string name, ILogger log)
{
    log.LogInformation($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```
