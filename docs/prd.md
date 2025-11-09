## Goal and context
Many people struggle to get a consolidated and high-level overview of their entire Azure spend.

The primary goals of this project are to:
- showcase how to extract cost information from Azure Subscriptions
  - consolidated view
  - make an open-source dashboard to support that
- This is supposed to be simple and offer a high-level view of costs
- This IS NOT supposed to replace Azure Cost Management ... just complement it.

## Fucntional requirements
- User Authentication against Azure
  - people should use their Entra ID, the App should not store that
- Subscription selection/configuration
  - user must be able to specify which subscriptions to monitor (simple text field suffice for now)
- Aggreated cost display
  - prominent, single view of total costs across selected subscriptions
  - (later) breakdown by subscription, resource group, resource type
  - (later) cost projections? trends?
- Top 5 costly resources
  - list of top 5 resources incurring the highest costs across selected subscriptions (name, cost, subscription, rg?)
- IaC
  - the entire infra should be deployable via Bicep templates
  - KISS

## Non-functional requirements
The usual suspects:
- Security
- Performance
- Usability
- OSS
- Maintainability - crap AI code is a no-go (except for FE)

## UI and Design
TBD
- Clean, simple
- minimal clicks to get to the core data.
Interaction flow: login, config, dashboard
Core views: login/welcome, dashboard
Target: desktop-first browser (mobile later)

## Technology Stack
- Frontend: React (Vite)
- Backend: Azure Functions (C#)
- Database: None
  - Perhaps later: localdb, or table storage whenever they make sense
- Infrastructure: Bicep
- GitHub Actions for CI/CD on Monorepo

---

<small>FYI: I use Markdown and AI auto-complete to help me write "faster" documentation.</small>

Despite this, the bullet points I put everywhere is just my natural preference after many years of using Markdown for notes and documentation. It is a way to deal with the "trailing space" that I always forget. 😅
While GenAI usually adds a lot of bullets everywhere, they, recognized the pattern that many do this for years.
