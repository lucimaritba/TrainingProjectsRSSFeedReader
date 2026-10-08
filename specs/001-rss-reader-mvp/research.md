# Research: RSS Reader MVP

## Decision

Use a lightweight ASP.NET Core Web API and Blazor WebAssembly architecture, with a single in-memory subscription list managed by the backend and displayed by the frontend.

## Rationale

This choice matches the project goals and tech stack: it is fast to implement, simple to run locally, and compatible with future production-ready extensions such as persistence, feed fetching, and background refresh.

The project is intentionally scoped to a single-user MVP, so the solution does not need a database, queue, or background scheduler in the first release. Keeping the subscription state in memory supports the immediate user workflow of adding a feed URL and seeing it appear in the UI.

## Alternatives considered

- Single-project Blazor app only: rejected because the project goals specifically call for a backend API and a frontend, and the stack document explicitly recommends separation of concerns.
- Database-backed storage from day one: rejected because the MVP purposely avoids persistence and focuses on the simplest valid demonstration.
- Feed fetching in the MVP: rejected because the MVP description explicitly excludes parsing, fetching, and item display until a later phase.
- Full production-ready architecture: rejected because it would add complexity and distract from the minimal subscription-management use case.

## Open questions resolved

- Subscription storage: in-memory list only
- User flow: add a URL, list it immediately
- Supported features: subscription management only
- Deferred work: feed parsing, item display, persistence, background polling
