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
4. This will Take **some time**
![loading](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/Loading%20bar.PNG "loading")
5. The storage connected service appears under the **Connected Services** node of your project.
![Added Service](https://github.com/mohammadahsan/Azure-Blob-Storage/blob/Editing/Images/Creating%20Blob%20Storage/show.PNG "Added Service")
