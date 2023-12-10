# AzureDurableFunctionExample
Durable Functions is an extension of Azure Functions that lets you write stateful functions in a serverless compute environment.


# HTTP-Triggered Function with Durable Functions Client Binding
This function is an HTTP-triggered function that serves as the entry point for the Durable Functions workflow.
It expects a JSON payload in the HTTP request with 'folder_name' and 'container_name' parameters.
It extracts these parameters, creates a payload, and starts a new Durable Functions instance using the specified orchestrator function.
The response contains a URL for checking the status of the Durable Functions instance.


# Orchestrator Function
This is the orchestrator function responsible for coordinating the workflow.
It receives input parameters, lists files in the specified folder, and creates a temporary directory.
For each PDF file, it calls the 'vectorization_func' activity function asynchronously.
It waits for all activities to complete using context.task_all.
It validates PDF files, creates a vector database, and uploads the Faiss vector store to Azure Blob Storage.

# Activity Function
This is the activity function responsible for downloading a file from Azure Blob Storage.
It receives parameters, creates a download folder path, and tries to create necessary folders.
If the folders already exist, it logs a message.
It then downloads the file from Azure Blob Storage to the specified folder and returns the path of the downloaded folder.
