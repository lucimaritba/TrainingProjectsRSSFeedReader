# Quickstart: RSS Reader MVP

## Prerequisites

- .NET 8 SDK or later
- A local terminal
- Access to the repo root

## Run the backend

```bash
dotnet run --project backend/RSSFeedReader.Api
```

Expected result: the ASP.NET Core API starts successfully and exposes the subscription endpoints on the configured local port.

## Run the frontend

```bash
dotnet run --project frontend/RSSFeedReader.UI
```

Expected result: the Blazor application starts and loads in the browser at the configured frontend URL.

## Validate the MVP workflow

1. Open the frontend in a browser.
2. Enter a valid feed URL such as `https://example.com/feed.xml`.
3. Submit the form.
4. Confirm the new item appears in the list without refreshing the page.

## Expected outcome

The MVP is considered successful when a user can add a feed URL and immediately see it appear in the subscription list. Feed parsing, content display, and persistence are not required in this phase.
