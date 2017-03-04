# Geting started with Azure Blob storage using Form builder

## Requirements

+ Azure subscription or free trial account
  + Create [Azure Storage Account](https://azure.microsoft.com/en-us/free/)
+ [Visual Studio 2015 or above] (https://www.visualstudio.com/)
+ [.NET Framework 4.5 or above] (https://www.microsoft.com/en-us/download/details.aspx?id=30653)
+ [Microsoft Azure Storage Connected Service] (https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.MicrosoftAzureStorageConnectedService) 

## Setting up The WorkSpace
1. Open Visual Studio

2. Select **File->New->Project** from the main menu

3. On the **New Project** dialog, specify the options as highlighted in the following figure:

![Win Forms Creation](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Project%20dialog.PNG "Creatinga Win forms Project")
4. Select **OK**.

## Use Connected Services to connect to an Azure storage account

1. In the **Solution Explorer**, right-click the reference node, and from the context menu, select **Add->Connected Service**.
![Connecting Azure Storage Account](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Adding%20Connected%20Service.png "Connecting Azure Storage Account")

2. On the **Add Connected Service** dialog, select **Azure Storage**. 
  + For visual studio 2015 select **Azure Storage** and then select **Configure**.
![Adding Account](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Cloud%20storage.PNG "Adding Account") 

3. Select **Reenter your credentials**.
![Reenter Credentials](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/credentials.PNG "Enter")

4. Enter Azure account **Email** and **password**
![email & password](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Entering%20Credentials.PNG "email & pass")

## Creating an Azure Blob Storage account (non-classic version)

1. Choose the **Create a New Storage Account** button at the bottom of the Azure Storage dialog box.
![creating a storage](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/Create%20Storage.PNG "create storage account")

2. Fill out the **Create Storage Account** dialog box and then select **Create** button.
![Fill Form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/Fill%20up%20the%20form.PNG "Fill Form")

3. Choose the added **storage** in the list, and select **Add**.
![Add Storage](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/add%20storage.PNG "Add storage")

4. The storage connected service appears under the **Connected Services** node of your project.
![Added Service](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/show.PNG "Added Service")

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

![App settings](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Connection%20String.PNG "App settings")

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
![open form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/Open%20form.PNG "Opening form")

2. Add a `button` from **toolbox** and name it as **Create Container**
![container](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/create%20button1.PNG "container")

3. Right Click the `button` and select **View Code** 
![view Code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/button%20code.png "View Code")

4. Add this snippet inside `button`onclick Event.
![code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/adding%20snippet.PNG "addin code")
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

Debug and run the Code, By Clicking on the `button` **Create Container** will _create a Container_ on the Storage.
![form click1](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/form%20clicks/create%20click.PNG "click1")
![Generated](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/generated.PNG "Generated Cntainer")

## Seeing what containers exist within the storage account.

1. Sign in to the [Azure portal](https://portal.azure.com/)

2. Select **SHOW MENU**, & choose **All Resources** and click on **Storage Account**.
![menu](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Seeing%20and%20deleting%20storage/Menu.PNG "menu")

3. Slide down to **Conatainer**
![slide](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Seeing%20and%20deleting%20storage/delt.PNG "slide")

4. Under **_Blob Service_** Select **Containers**, _There is the List of Existing containers_.
![containers](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Seeing%20and%20deleting%20storage/conatainers.PNG "containers")

## Uploading data to that container

1. Open the `Forms.cs` file from **Solution Explorer** in Visual Studio.
![open form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/Open%20form.PNG "Opening form")

2. Add a `button` from **toolbox** and name it as **Upload**
![upload button](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/uploading%20data%20to%20blob/button.PNG "uploade")

3. Right Click the `button` and select **View Code<>** 
![view Code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/uploading%20data%20to%20blob/view%20code.png "View Code")

4. Add this snippet inside `button`onclick Event.
![code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/uploading%20data%20to%20blob/path1.PNG "addin code")
```C#
// Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
                CloudConfigurationManager.GetSetting("StorageConnectionString"));

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.Replace 'mycontainer' with name of your container
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create or overwrite the "myblob" blob with contents from a local file. (Replace C:\users\.... With your file path)
            using (var fileStream = System.IO.File.OpenRead(@"C:\Users\DELL\Desktop\icon48.png"))
            {
                blockBlob.UploadFromStream(fileStream);
            }
```
Debug and run the Code, By Clicking on the `button` **upload** will _upload_ on the Storage.
![upload click](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/form%20clicks/upload%20click.PNG "upload click")
![Generated](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/uploading%20data%20to%20blob/blob.PNG "Generated Cntainer")

## Seeing items are inside of that container

### First Setting the console to see output

1. In the **Solution Explorer**, right-click the project, and from the context menu, select **properties**. 
![properties](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/listing%20blobs/click%20properties.png "properties")

2. Under the **application Settings**, select **output type** as **console application**
![console application](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/listing%20blobs/properties.png "console application")

### Listing the items in a container

1. Open the `Forms.cs` file from **Solution Explorer** in Visual Studio.
![open form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/Open%20form.PNG "Opening form")

2. Add a `button` from **toolbox** and name it as **List Blobs**
![upload button](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/listing%20blobs/add%20button.PNG "uploade")

3. Right Click the `button` and select **View Code** 
![view Code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/listing%20blobs/view%20code.png "View Code")

4. Add this snippet inside `button`onclick Event.
![code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/listing%20blobs/add%20sniping.PNG "addin code")
``` C#
// Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
                CloudConfigurationManager.GetSetting("StorageConnectionString"));

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container. (replace 'mycontainer' with your container name) 
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Loop over items within the container and output the length and URI.
            foreach (IListBlobItem item in container.ListBlobs(null, false))
            {
                if (item.GetType() == typeof(CloudBlockBlob))
                {
                    CloudBlockBlob blob = (CloudBlockBlob)item;

                    Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

                }
                else if (item.GetType() == typeof(CloudPageBlob))
                {
                    CloudPageBlob pageBlob = (CloudPageBlob)item;

                    Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

                }
                else if (item.GetType() == typeof(CloudBlobDirectory))
                {
                    CloudBlobDirectory directory = (CloudBlobDirectory)item;

                    Console.WriteLine("Directory: {0}", directory.Uri);
                }
```
Debug and run the Code, By Clicking on the `button` **list blobs** will list the contents of the container on console.
![list click](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/form%20clicks/list%20click.PNG "list click")
![listed](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/listing%20blobs/listed.PNG "listed")

## Deleting an item in that container

1. Open the `Forms.cs` file from **Solution Explorer** in Visual Studio.
![open form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/Open%20form.PNG "Opening form")

2. Add a `button` from **toolbox** and name it as **delete blob**
![del button](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20an%20item%20in%20container/button.PNG "del button")

3. Right Click the `button` and select **View Code** 
![view Code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20an%20item%20in%20container/view%20code.png "View Code")

4. Add this snippet inside `button`onclick Event.
![code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20an%20item%20in%20container/adding%20snippet.PNG "addin code")
``` C#
// Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
                CloudConfigurationManager.GetSetting("StorageConnectionString"));

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container. (replace 'mycontainer' with container name
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Retrieve reference to a blob. Replace 'myblob' with item name you want to delete.
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Delete the blob.
            blockBlob.Delete();
```


Debug and run the Code, By Clicking on the `button` **delete blob** will _delete the item_ on the Storage.
![delete click](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/form%20clicks/delete%20click1.PNG "delete click")
![deleted](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20an%20item%20in%20container/deleted.PNG "deleted")


## Deleting the container

1. Open the `Forms.cs` file from **Solution Explorer** in Visual Studio.
![open form](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Creating%20Blob%20Storage/Open%20form.PNG "Opening form")

2. Add a `button` from **toolbox** and name it as **delete container**
![del c button](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20a%20container/button.PNG "del c button")

3. Right Click the `button` and select **View Code** 
![view Code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20a%20container/view%20code.png "View Code")

4. Add this snippet inside `button`onclick Event.
![code](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20a%20container/sniiping.PNG "addin code")
``` C#
// Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
                CloudConfigurationManager.GetSetting("StorageConnectionString"));

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container. (replace 'mycontainer' with the container name.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Delete the container.
            container.DeleteIfExists();
```

Debug and run the Code, By Clicking on the `button` **delete conotainer** will _delete the container_ from the Storage.
![del con click](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/form%20clicks/delete%20container%20click.PNG "del con click")
![deleted](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/deleting%20a%20container/delete.PNG "deleted")


## Deleting the storage account

1. Sign in to the [Azure portal](https://portal.azure.com/)

2. Select **SHOW MENU**, & choose **All Resources** and click on **Storage Account**.
![menu](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Seeing%20and%20deleting%20storage/resourses.PNG "menu")

3. Click on **Overview** on the top right corner click **Delete**
![delete](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Seeing%20and%20deleting%20storage/Delete.PNG "delete")

4. Enter **Name of the storage** you want to delete.
![name](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Seeing%20and%20deleting%20storage/name.PNG "name")

5. Successfule Deletion of the **Storage Account**
![successful](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/master/Images/Seeing%20and%20deleting%20storage/successful%20deletion1.PNG "successful")
