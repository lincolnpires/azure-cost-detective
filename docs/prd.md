## Goal and context
Many people struggle to get a consolidated and high-level overview of theirentire Azure spend.

The primary goals of this project are to:
- showcase how to extract cost information from Azure Subscriptions
  - consolidated view
  - make an open-source dashboard to support that
- This is supposed to be simple and offer a high-level view of costs
- This IS NOT supposed to replace Azure Cost Management ... just complement it.

## Fucntional requirements
- User Authentication against Azure
  - Must allow users to sign in using their own Azure EntraID. 
  - The application will not store any user credentials.
- Subscription selection/configuration
  - User must be able to specify which subscriptions to monitor (one or more)
  - For the MVP, this can be a simple text input field where IDs are entered.
- Aggreated cost display
  - Must display a prominent, single view of total costs across selected subscriptions in dashboard.
  - (later) breakdown by subscription, resource group, resource type
  - (later) cost projections? trends?
- Top 5 costly resources
  - Must list the top 5 resources incurring the highest costs across selected subscriptions 
  - Inlcude resource name, cost, subscription, and resource group.
- IaC
  - The entire (Azure) infrastructure of the app should be deployable via Bicep templates
  - KISS

## Non-functional requirements
The usual suspects:
- Security: least privilege, no secrets in code, use managed identities, read-only access to Azure
resources, communicate over secure channels (HTTPS).
- Usability: Intuitive and clean UI. For the deployment, clear instructions in README.
- Performance: UI should indicate loading states, backend should be warm and responsive.
- OSS: permissive license (MIT).
- Maintainability: standard C# and Bicep templates with well organized code. FE can use GenAI code.

## UI and Design
- Clean, simple, but professional look.
- UX should be fast and require minimal clicks to get to the core data.
- Interaction flow: login > configuration > dashboard
- Core views: login/welcome, dashboard
- Target device: desktop-first (web browsers), mobile layout is not a requirement for MVP.

For the AI FE: "The generated UI should adhere to basic web accessibility standards (WCAG 2.2 A)."

## Technology Stack
- Frontend: React (Vite)
- Backend: Azure Functions (C#)
- Database: None
  - Perhaps later: localdb, or table storage whenever they make sense
- Infrastructure: Bicep
- GitHub Actions for CI/CD on Monorepo


## Epics and User Stories
See [docs/todo.md](./todo.md) for detailed breakdown of epics and user stories.

## Out of Scope Ideas Post MVP

The following features and ideas are explicitly out of scope for the initial MVP to ensure a rapid
delivery. They are potential candidates for future versions.

    Breakdown of costs by subscription, resource group, or resource type.
    Cost trend analysis or future cost projections.
    Interactive charts or drill-down capabilities in the dashboard.
    Mobile-responsive UI design.
    Saving subscription ID configurations for users.
    Automated alerts for cost spikes.

## Reference and notes
TBD

---

<small>FYI: I use Markdown and AI auto-complete to help me write "faster" documentation.

Despite this, the bullet points I put everywhere is just my natural preference after many years of
using Markdown for notes and documentation. It is a way to deal with the "trailing space" that I
always forget. 😅
While GenAI usually adds a lot of bullets everywhere, they, recognized the pattern that many do this
for years.
</small>
