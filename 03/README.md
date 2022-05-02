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
        
        //Enumerate the existing containers
        await EnumerateContainersAsync(serviceClient);
    }

    private static async Task EnumerateContainersAsync(BlobServiceClient client){
        await foreach (BlobContainerItem container in client.GetBlobContainersAsync()){
            await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
        }
    }
```


```bash
> dotnet run

Connected to Azure Storage Account
Account name:   mediastorkie
Account kind:   StorageV2
Account sku:    StandardLrs
Container:      compressed-audio
Container:      raster-graphics
Container:      vector-graphics
```


### 4 Retrieve blob Uniform Resource Identifiers (URIs) by using the .NET SDK

#### Enumerate the blobs in an existing container by using the SDK

```c#
using Azure.Storage;
using Azure.Storage.Blobs;
using Azure.Storage.Blobs.Models;

using System;
using System.Threading.Tasks;


public class Program
{
    private const string blobServiceEndpoint = "https://mediastorkie.blob.core.windows.net/";
    private const string storageAccountName = "mediastorkie";
    private const string storageAccountKey = "xxx";

    public static async Task Main(string[] args)
    {
        StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
        
        BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
        
        string existingContainerName = "raster-graphics";
        await EnumerateBlobsAsync(serviceClient, existingContainerName);

    }

    private static async Task EnumerateBlobsAsync(BlobServiceClient client, string containerName){
        BlobContainerClient container = client.GetBlobContainerClient(containerName);

        await Console.Out.WriteLineAsync($"Searching:\t{container.Name}");

        await foreach (BlobItem blob in container.GetBlobsAsync()){
            await Console.Out.WriteLineAsync($"Existing Blob:\t{blob.Name}");
        }
    }
}
```

```bash
> dotnet run
Searching:      raster-graphics
Existing Blob:  graph.jpg
```

#### Create a new container by using the SDK

```c#
using Azure.Storage;
using Azure.Storage.Blobs;
using Azure.Storage.Blobs.Models;

using System;
using System.Threading.Tasks;


public class Program
{
    private const string blobServiceEndpoint = "https://mediastorkie.blob.core.windows.net/";
    private const string storageAccountName = "mediastorkie";
    private const string storageAccountKey = "xxx";

    public static async Task Main(string[] args)
    {
        StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
        
        BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
        
        string newContainerName = "vector-graphics";
        BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);
    }

    private static async Task<BlobContainerClient> GetContainerAsync(BlobServiceClient client, string containerName){
        BlobContainerClient container = client.GetBlobContainerClient(containerName);await container.CreateIfNotExistsAsync(PublicAccessType.Blob);
        await Console.Out.WriteLineAsync($"New Container:\t{container.Name}");
        return container;
    }
}
```
output

```bash
> dotnet run
New Container:  vector-graphics
```
 ![](/media/lab3-1.png)

Upload a new blob by using the portal 

\Images, select the graph.svg


#### Access blob URI by using the SDK

```c#
using Azure.Storage;
using Azure.Storage.Blobs;
using Azure.Storage.Blobs.Models;

using System;
using System.Threading.Tasks;


public class Program
{
    private const string blobServiceEndpoint = "https://mediastorkie.blob.core.windows.net/";
    private const string storageAccountName = "mediastorkie";
    private const string storageAccountKey = "CU1Q2fcGxlMv9HaAoRXEUoYiXZbwyo0NXCyCaoOjwk3XQAaXTaPOhEEcturLcO8+X3PCURhOhxSX+AStRb4DCw==";

    public static async Task Main(string[] args)
    {
        StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
        
        BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);

        // Create Blob new
        string newContainerName = "vector-graphics";
        BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);

        // Get URI
        string uploadedBlobName = "graph.svg";
        BlobClient blobClient = await GetBlobAsync(containerClient, uploadedBlobName);
        await Console.Out.WriteLineAsync($"Blob Url:\t{blobClient.Uri}");

    }

    private static async Task<BlobContainerClient> GetContainerAsync(BlobServiceClient client, string containerName){
        BlobContainerClient container = client.GetBlobContainerClient(containerName);await container.CreateIfNotExistsAsync(PublicAccessType.Blob);
        await Console.Out.WriteLineAsync($"New Container:\t{container.Name}");
        return container;
    }

    private static async Task<BlobClient> GetBlobAsync(BlobContainerClient client, string blobName){
        BlobClient blob = client.GetBlobClient(blobName);
        await Console.Out.WriteLineAsync($"Blob Found:\t{blob.Name}");
        return blob;
    }
}

```
output

```bash
> dotnet run
New Container:  vector-graphics
Blob Found:     graph.svg
Blob Url:       https://mediastorkie.blob.core.windows.net/vector-graphics/graph.svg
```

Observe the output from the currently running console application. The updated output includes the final URL to access the blob online. Record the value of this URL to use later in the lab

Test the URI by using a browser
On the taskbar, activate the shortcut menu for the Microsoft Edge icon, and then select New window.

In the new browser window, refer to the URL that you previously copied in this lab for the blob.

You should now notice the Scalable Vector Graphics (SVG) file in your browser window.

![](/media/lab3-2.png)


### 5 Clean up your subscription

login

```ps
az login
```

set supscription

```ps
az account set --subscription "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx"
```

Delete a resource group with command

```ps
az group delete --name StorageMedia --no-wait --yes
```








