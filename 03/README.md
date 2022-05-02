# Lab 03: Retrieve Azure Storage resources and metadata by using the Azure Storage SDK for .NET

### Architecture diagram

![Architecture diagram depicting a user retrieving Azure Storage resources and metadata by using the Azure Storage SDK for .NET.](../media/Lab03-Diagram.png)


### 1 Create Azure resources

- resource group
  - name : StorageMedia

- stroage account
  - name : mediastor

go to the setting > endpoints > copy blob service, account name , key

### 2 Upload a blob into a container

- Create containers 
  - name : raster-graphics
  - name : compressed-audio

- Upload /Images/graph.jpg into raster-graphics (Overwrite if files already exist check box)

### 3 Access containers by using the .NET SDK

Create .NET project 
Open with vscode inside BlobManager

```bash
dotnet new console --name BlobManager --output .
```

Add dependency Azure.Storage.Blobs from NuGet

```bash
dotnet add package Azure.Storage.Blobs --version 12.0.0
```

and then build for run

```bash
dotnet build
```

Modify the Program class to access Storage in program.cs and then saved

```c#
// using for import Azure.Storage.Blobs
using Azure.Storage;
using Azure.Storage.Blobs;
using Azure.Storage.Blobs.Models;

using System;
using System.Threading.Tasks;


public class Program
{
    // Ref from copied on clipboard
    private const string blobServiceEndpoint = "https://mediastorkie.blob.core.windows.net/";
    private const string storageAccountName = "mediastorkie";
    private const string storageAccountKey = "xxxx";

    public static async Task Main(string[] args)
    {
        StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
        
        BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
        
        AccountInfo info = await serviceClient.GetAccountInfoAsync();
        
        await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
        await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
        await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
        await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
        
        await EnumerateContainersAsync(serviceClient);
    }
```



```bash
dotnet run
```










