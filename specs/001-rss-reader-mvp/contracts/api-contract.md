# API Contract: RSS Reader MVP

## Base URL

The backend exposes a local API base URL configured in the frontend appsettings file.

## Endpoints

### GET /api/subscriptions

Returns the current list of subscriptions in the application memory.

Example response:

```json
[
  "https://example.com/feed.xml",
  "https://feeds.example.org/latest.xml"
]
```

### POST /api/subscriptions

Adds a new subscription to the current in-memory list.

Request body:

```json
{
  "url": "https://example.com/feed.xml"
}
```

Success response:

- Status: 201 Created
- Body: the created subscription record or a success payload

Validation behavior:

- Empty or whitespace-only URLs are rejected
- The endpoint should not fetch or parse the feed at this stage

## Notes

This contract is intentionally minimal and aligns with the MVP scope. Feed fetching, parsing, and persistence are out of scope for the current implementation.
