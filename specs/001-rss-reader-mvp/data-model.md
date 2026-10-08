# Data Model: RSS Reader MVP

## Core entity: Subscription

The subscription model is intentionally simple because the MVP is focused on managing feed URLs rather than fetching or storing feed content.

### Subscription

- Id: unique identifier for the entry in memory
- Url: string containing the feed address entered by the user
- CreatedAt: timestamp when the subscription was added

### Subscription Collection

- Items: ordered list of Subscription entries
- Add operation: append a new subscription after validation of a non-empty URL
- Display operation: render the Url values in the UI list

## Validation rules

- Url must not be null or empty after trimming whitespace
- Duplicate entries may be treated as duplicates for the MVP and either ignored or shown separately depending on the product decision; a single consistent rule should be chosen before implementation
- Data is ephemeral and lives only for the application process lifetime

## Relationship summary

- One user can have zero or more subscriptions
- The frontend displays the complete collection returned by the backend
- The backend owns the canonical in-memory list and exposes a read/write API surface
