# xlsx-to-netsuitexml-invoice
This Mule application transforms the users' invoice data available in Excel format(.xlsx) to NetSuite compatible XML format so that the xml invoice can be posted to the NetSuite tools.

## Key Features
This Mule 4 application executes:
1.  **File Retrieval:** fetches a specific Excel file (e.g., `Sample_Invoice_Data.xlsx`) from a designated Google Drive folder.
2.  **Data Retrieval & Transformation:** Reads the tabular data from the Excel file and transforms it into a structured JSON format, then further converts this JSON into a NetSuite Web Services XML payload. This XML is specifically designed for `upsertList` operations for `Invoice` records in NetSuite Tools.

## Technologies Used

* **MuleSoft Anypoint Platform (Mule 4)**
* **DataWeave 2.0**
* **Google Drive API**

## Connectors Used

* **HTTP Connector:**
    * **HTTP Listener:** To expose endpoints for triggering the integration flows.
    * **HTTP Request:** To make calls to external APIs (e.g., calling a process API from an experience API).
* **Google Drive Connector:**
    * `Get Files`: To list files in a Google Drive folder and find the target Excel file.
    * `Get Files by File ID`: To retrieve the binary content of the specific Excel file.
    * `Create Media File`: To save the generated NetSuite XML back to Google Drive.

## Google Cloud Console Setup for OAuth 2.0 (Google Drive)

To enable your MuleSoft application to securely interact with Google Drive, you need to set up an OAuth 2.0 client in the Google Cloud Console. This process will provide you with the **Client ID** (Consumer Key) and **Client Secret** (Consumer Secret) required by the Google Drive Connector.

1.  **Go to Google Cloud Console:**
    * Navigate to [https://console.cloud.google.com/](https://console.cloud.google.com/).
    * Sign in with your Google account.

2.  **Create a New Project:**

3.  **Enable the Google Drive API:**
    * Go to `APIs & Services` > `Enabled APIs & services`.

4.  **Configure the OAuth Consent Screen:**
    * **Test Users (for External apps):** If your app is `External` and not yet `Published`, you must add `Test Users` who can authenticate. Add the Google accounts you'll use for testing.

5.  **Create OAuth Client ID Credentials:**
    * In the navigation menu, go to `APIs & Services` > `Credentials`.
    * Click `+ CREATE CREDENTIALS` and select `OAuth client ID`.
    * **Application type:** Select `Web application`.
    * **Name:** Give it a descriptive name (e.g., `MuleSoft Web Client`).
    * **Authorized redirect URIs:** This is the callback URL of your MuleSoft application's HTTP Listener. This is where Google will send the authorization code after a user grants consent.
        * For local development, it's typically `http://localhost:8081/callback`.

6.  **Retrieve Client ID and Client Secret:**
    * After creating the credentials, a dialog box will appear showing your **Client ID** and **Client Secret**.
