# Geting started with Azure Blob storage using Form builder

## Requirements

+ Azure subscription or free trial account
  + [Azure Storage Account](https://azure.microsoft.com/en-us/free/)
+ [Visual Studio 2015 or above] (https://www.visualstudio.com/)
+ [.NET Framework 4.5 or above] (https://www.microsoft.com/en-us/download/details.aspx?id=30653)
+ [Microsoft Azure Storage Connected Service] (https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.MicrosoftAzureStorageConnectedService) 
  + [How to install] (https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.MicrosoftAzureStorageConnectedService)

## Setting up The WorkSpace
1. Open Visual Studio

2. Select **File->New->Project** from the main menu

3. On the **New Project** dialog, specify the options as highlighted in the following figure:

![Win Forms Creation](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Project%20dialog.PNG "Creatinga Win forms Project")
4. Select **OK**.

## Use Connected Services to connect to an Azure storage account

1. In the **Solution Explorer**, right-click the project, and from the context menu, select **Add->Connected Service**.
![Connecting Azure Storage Account](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Adding%20Connected%20Service.png "Connecting Azure Storage Account")

2. On the **Add Connected Service** dialog, select **Azure Storage**. 
  + For visual studio 2015 select **Azure Storage** and then select **Configure**.
![Adding Account](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Cloud%20storage.PNG "Adding Account") 

3. Select **Reenter your credentials**.
![Reenter Credentials](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/credentials.PNG "Enter")

4. Enter Azure account **Email** and **password**
![email & password](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Entering%20Credentials.PNG "email & pass")

## Creating an Azure Blob Storage account (non-classic version)

1. Choose the **Create a New Storage Account** button at the bottom of the Azure Storage dialog box.
![creating a storage](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/Create%20Storage.PNG "create storage account")

2. Fill out the **Create Storage Account** dialog box and then select **Create** button.
![Fill Form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/Fill%20up%20the%20form.PNG "Fill Form")

3. Choose the added **storage** in the list, and select **Add**.
![Add Storage](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/add%20storage.PNG "Add storage")

4. The storage connected service appears under the **Connected Services** node of your project.
![Added Service](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/show.PNG "Added Service")

## Configure your storage connection string
To configure your connection string, open the `app.config` file from **Solution Explorer** in Visual Studio. Add the contents of the `appSettings` element shown below. 

``` xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <!-- Azure Storage: blobstoragetest1 -->
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=blobstoragetest1;AccountKey=Nq2Z5CGL+vT5RrbezP/TboH0XzYzmvGDs1OGHM1nTj8J94MZc/XUVbUCY9arpp5xx/227yBa+SmGDXPx1obnqg==" />
    </appSettings>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
</configuration>
```

![App settings](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Connection%20String.PNG "App settings")

Replace **account-name** with the name of your `storage account`, 
Replace **account-key** with your `account access key`:

## Add namespace declarations
Add the following using statements to the top of the form1.cs file:
``` C#
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

## Creating a container in that storage account

1. Open the `Forms.cs` file from **Solution Explorer** in Visual Studio.
![open form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/Open%20form.PNG "Opening form")

2. Add a `button` from **toolbox** and name and name it as **Create Container**
![container](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/create%20button1.PNG "container")

3. Right Click the `button` and select **View Code<>** 
![view Code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/button%20code.png "View Code")

4. Add this snippet inside `button`onclick Event.
![code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/adding%20snippet.PNG "addin code")
```C#
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container. (Replace mycontainer with name of your container)
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();
```
By default, the new container is private, meaning that you must specify your storage access key to download blobs from this container. If you want to make the files within the container available to everyone, you can set the container to be public using the following code:
``` C#
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```
5. Debug and run the Code Clicking on the `button` **Create Container** will _create a Container_ on the Storage.
![Generated](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/generated.PNG "Generated Cntainer")
