# Node-RED Flow: Home Assistant Weight to Google Fit Sync

## Project Description

This project contains a Node-RED flow designed for personal use. Its purpose is to automatically synchronize weight measurements recorded in a Home Assistant sensor entity (e.g., `sensor.my_weight`) with the user's personal Google Fit account.

## Functionality

The Node-RED flow performs the following steps:

1.  **Listens:** Monitors state changes of a specified weight sensor entity within Home Assistant.
2.  **Authenticates:** Uses configured Google OAuth 2.0 credentials (Client ID, Client Secret, and a Refresh Token obtained through user consent) to request temporary Access Tokens from Google.
3.  **Formats Data:** Prepares the weight measurement payload according to the requirements of the Google Fit API for body weight data points.
4.  **Sends Data:** Makes an authenticated API call to the Google Fit `users.dataSources.datasets.patch` endpoint to insert the new weight data point into the user's Google Fit account.

## Google OAuth Consent Screen Information

This section provides information relevant to the Google OAuth Consent Screen configuration required for this application to function.

### Scopes Requested

This application requests the following Google API scope:

- **`https://www.googleapis.com/auth/fitness.body.write`**: This scope is required solely to grant the application permission to write body measurement data (specifically, weight measurements in this case) to your Google Fit platform.

### Data Handling and Usage (Privacy Information)

- **Data Accessed:** The application accesses the `fitness.body.write` scope only when a new weight measurement is received from Home Assistant. It reads the weight value provided by your Home Assistant sensor.
- **Data Usage:** The weight data obtained from Home Assistant is used exclusively to create a data point object which is then sent directly to the Google Fit API. The data is **not** used for any other purpose (e.g., analysis, advertising, improving other services).
- **Data Storage:**
  - This Node-RED flow itself **does not store** your weight data or Google Fit data long-term. Data is processed transiently within the flow execution.
  - Your weight data resides within your Home Assistant instance (as configured by you) and subsequently within your personal Google Fit account after successful synchronization.
  - The Google OAuth 2.0 Refresh Token provided during the initial authorization is stored securely within your Node-RED environment's configuration or credentials file to allow the flow to obtain new Access Tokens without requiring manual re-authentication frequently. Access Tokens are short-lived and used only for immediate API calls.
- **Data Sharing:** Your weight data and any data related to your Google Fit account accessed via the API are **not shared** with any third parties by this application. The data flow is strictly limited to: Your Home Assistant instance -> Your Node-RED instance -> Your Google Fit Account (via the official Google Fit API).

### Purpose of Application

This application is developed and intended solely for **personal use** by the individual user setting it up to automate the logging of their weight data from their smart home system into their personal fitness tracking service (Google Fit). It is not intended for distribution or use by others without them setting up their own instance and configuration.

## Terms of Service

This Node-RED flow is provided "as-is" for personal use. By using this flow, you assume all responsibility for its operation and configuration. The developer provides no warranties and assumes no liability for its use, data accuracy, or any issues arising from its operation. Use at your own risk.

## Contact

For inquiries specifically related to this application's functionality or data handling as described here, please use the developer support email provided during the Google OAuth Consent Screen setup or open an issue in this GitHub repository (if applicable).
