
## Epics overview
============
1. Foundational setup + Deployment
  - The goal is to have the basic Azure infra deployable and a basic "App Shell".
  - If a user can fully deploy a non-functional app to their own Azure, that is a win.
2. User Authentication + UI
  - The goal is to have users authenticate against Azure/Entra ID and have a basic UI to interact with.
  - Lorem ipsum data would be fine.
3. Cost Data Extraction + Display
  - The goal is to implement core logic. 
  - Fetch cost data from selected subscriptions and display it in the UI.
  - Basic aggregated cost display and top 5 costly resources.
  - Meaning: this is a fully functional MVP. Users can see real cost data.

---

## User Stories breakdown
At this point, AI can't mess this up with all the context behind. LOL. From here on, this is Gemini doing. :)


### Epic 1: Foundational Setup & Deployment

-   **Goal**: To create the complete, deployable Azure infrastructure and a basic application shell using Bicep. The result of this epic is a user being able to deploy a non-functional version of the application to their Azure subscription successfully.

-   **Story 1.1**: As a DevOps Engineer, I want a comprehensive Bicep template that defines all necessary Azure resources, so that I can deploy the entire application infrastructure with a single command.
    -   **Acceptance Criteria**:
        1.  The Bicep template defines an Azure Static Web App resource.
        2.  The Bicep template defines an Azure Function App resource (C# runtime).
        3.  The template correctly links the Function App to the Static Web App's backend API endpoint.
        4.  The template includes Application Insights for basic monitoring.
        5.  The template uses parameters for resource names and location to avoid hardcoding.

-   **Story 1.2**: As a Developer, I want placeholder application code checked into the repository, so that the Bicep deployment can link to a functional codebase.
    -   **Acceptance Criteria**:
        1.  A default C# Azure Function project is created with a single "Hello World" HTTP trigger.
        2.  A basic placeholder frontend app (e.g., a single `index.html` file) is created.
        3.  The code is organized in a logical folder structure within the monorepo (e.g., `/src/api`, `/src/frontend`).

-   **Story 1.3**: As an Open Source User, I want a `README.md` file with clear instructions on how to deploy the Bicep template, so that I can get the application infrastructure running in my own Azure subscription.
    -   **Acceptance Criteria**:
        1.  The `README.md` explains the prerequisites (e.g., Azure CLI).
        2.  The `README.md` provides the exact Azure CLI commands to run the Bicep deployment.
        3.  The `README.md` explains how to find the URL of the deployed application after a successful deployment.

<small>Well, unfortunately, AI put a shit ton of space in stuff, but fork it.</small>

---

### Epic 2: User Authentication & UI Shell

-   **Goal**: To implement secure user authentication using Azure AD. The result of this epic is a user being able to log into the application, see a basic dashboard UI with placeholder data, but not yet be able to fetch real cost data.

-   **Story 2.1**: As a User, I want to log in with my Azure AD account, so that I can securely access the application.
    -   **Acceptance Criteria**:
        1.  The frontend application presents a clear "Login with Microsoft" button.
        2.  Clicking the login button initiates the standard Azure AD authentication flow.
        3.  Upon successful authentication, the user is redirected to the main dashboard page.
        4.  The user's name or email is displayed on the dashboard to confirm their identity.

-   **Story 2.2**: As an Open Source User, I need instructions on how to configure Azure AD for the application, so that it can be used in my own tenant.
    -   **Acceptance Criteria**:
        1.  The Bicep template is updated to include placeholder settings for the Static Web App's Azure AD authentication provider.
        2.  The `README.md` provides a step-by-step guide on how to register a new application in their own Azure AD.
        3.  The guide clearly explains how to find the `Client ID` and `Tenant ID` and where to put them in the Bicep parameters file.

-   **Story 2.3**: As a User, I want to see the basic layout of the dashboard after logging in, so that I understand the application's structure.
    -   **Acceptance Criteria**:
        1.  The dashboard displays a clear title, "Azure Multi-Subscription Cost Governance Dashboard".
        2.  A text input area for entering subscription IDs is visible.
        3.  A button labeled "Fetch Costs" is present.
        4.  Placeholder sections for "Total Monthly Cost" and "Top 5 Costly Resources" are displayed.
        5.  A "Logout" button is available.

---

### Epic 3: Cost Data Fetching & Dashboard Display

-   **Goal**: To implement the core logic for fetching cost data from the Azure API and displaying it on the dashboard. The result of this epic is the fully functional MVP where a logged-in user can input their subscription IDs and see their actual cost data.

-   **Story 3.1**: As a DevOps Engineer, I need the application's backend to have secure, read-only permissions to the Cost Management API, so that it can query cost data without exposing credentials.
    -   **Acceptance Criteria**:
        1.  The Bicep template is updated to enable a System-Assigned Managed Identity for the Azure Function App.
        2.  The `README.md` is updated with a script (Azure CLI or PowerShell) that the user must run to assign the "Cost Management Reader" role to the Function App's Managed Identity for each subscription they wish to monitor.

-   **Story 3.2**: As a Developer, I need an Azure Function that receives subscription IDs, fetches cost data, and returns it to the frontend.
    -   **Acceptance Criteria**:
        1.  The Azure Function is triggered by an HTTP request from the authenticated frontend.
        2.  It accepts a list of subscription IDs in the request body.
        3.  The function uses its Managed Identity to authenticate with the Azure SDK.
        4.  It queries the Azure Cost Management API for each subscription and aggregates the total cost.
        5.  It queries the API to get the top 5 most expensive resources across all provided subscriptions.
        6.  It returns a single JSON response containing the aggregated total cost and the list of the top 5 resources (including resource name, cost, subscription, and resource group).

-   **Story 3.3**: As a User, I want to input my subscription IDs and see the real cost data on the dashboard.
    -   **Acceptance Criteria**:
        1.  I can enter one or more comma-separated subscription IDs into the input field.
        2.  Clicking the "Fetch Costs" button triggers the backend function call.
        3.  The UI displays a loading indicator while the data is being fetched.
        4.  Upon success, the "Total Monthly Cost" placeholder is updated with the value from the API.
        5.  The "Top 5 Costly Resources" placeholder is replaced with a list displaying the data from the API.
        6.  The UI displays a "Data last refreshed" timestamp.

---
