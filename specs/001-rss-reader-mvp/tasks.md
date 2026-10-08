# Tasks: RSS Reader MVP

**Input**: Design documents from `/specs/001-rss-reader-mvp/`

**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: The examples below include test tasks. Tests are OPTIONAL - only include them if explicitly requested in the feature specification.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create the backend and frontend project structure per the implementation plan in `backend/RSSFeedReader.Api/` and `frontend/RSSFeedReader.UI/`
- [ ] T002 [P] Initialize the ASP.NET Core Web API backend and Blazor WebAssembly frontend with the required .NET project references in `backend/RSSFeedReader.Api/` and `frontend/RSSFeedReader.UI/`
- [ ] T003 [P] Configure the local API and frontend ports and app settings so the backend URL and CORS settings match in `backend/RSSFeedReader.Api/Program.cs`, `backend/RSSFeedReader.Api/Properties/launchSettings.json`, `frontend/RSSFeedReader.UI/Program.cs`, and `frontend/RSSFeedReader.UI/wwwroot/appsettings.json`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before any user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T004 Create the shared in-memory subscription model in `backend/RSSFeedReader.Api/Models/SubscriptionItem.cs`
- [ ] T005 [P] Implement the subscription service with in-memory storage and empty/duplicate URL handling in `backend/RSSFeedReader.Api/Services/SubscriptionService.cs`
- [ ] T006 [P] Configure API routing and CORS in `backend/RSSFeedReader.Api/Program.cs` for the Blazor frontend origin
- [ ] T007 [P] Configure the frontend HTTP client and API base URL in `frontend/RSSFeedReader.UI/Program.cs` and `frontend/RSSFeedReader.UI/wwwroot/appsettings.json`
- [ ] T008 Remove default template demo content and verify routing integrity in `frontend/RSSFeedReader.UI/Pages/` and `frontend/RSSFeedReader.UI/Layout/NavMenu.razor`

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - Add a feed subscription (Priority: P1) 🎯 MVP

**Goal**: Allow a user to add a feed URL and see it appear in the active subscription list.

**Independent Test**: Enter a valid feed URL in the UI, submit it, and verify the new subscription appears immediately in the list.

### Implementation for User Story 1

- [ ] T009 [US1] Add the HTTP endpoint to create subscriptions in `backend/RSSFeedReader.Api/Controllers/SubscriptionsController.cs`
- [ ] T010 [P] [US1] Implement the add-subscription logic for valid URLs and blank-submission rejection in `backend/RSSFeedReader.Api/Services/SubscriptionService.cs`
- [ ] T011 [P] [US1] Build the subscription entry form and input state in `frontend/RSSFeedReader.UI/Pages/Subscriptions.razor`
- [ ] T012 [US1] Add the frontend client method to post a new subscription in `frontend/RSSFeedReader.UI/Services/FeedSubscriptionClient.cs`
- [ ] T013 [US1] Render the subscription list after submission in `frontend/RSSFeedReader.UI/Pages/Subscriptions.razor`
- [ ] T014 [US1] Validate the end-to-end add-subscription workflow by running the backend and frontend and confirming the list updates without a page refresh

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - Review the current subscriptions (Priority: P2)

**Goal**: Let the user see the current list of added subscriptions and keep it accurate as additional feeds are added.

**Independent Test**: Add multiple feed URLs and verify the list continues to show all active entries in the visible order.

### Implementation for User Story 2

- [ ] T015 [US2] Add the API read operation that returns the current subscription list in `backend/RSSFeedReader.Api/Controllers/SubscriptionsController.cs`
- [ ] T016 [P] [US2] Ensure the backend returns the in-memory subscription collection in `backend/RSSFeedReader.Api/Services/SubscriptionService.cs`
- [ ] T017 [P] [US2] Load the current list when the page renders in `frontend/RSSFeedReader.UI/Pages/Subscriptions.razor`
- [ ] T018 [US2] Refresh the displayed list after new entries are added in `frontend/RSSFeedReader.UI/Pages/Subscriptions.razor` and `frontend/RSSFeedReader.UI/Services/FeedSubscriptionClient.cs`
- [ ] T019 [US2] Confirm blank or duplicate URL handling preserves the intended subscription list without producing invalid entries in `backend/RSSFeedReader.Api/Services/SubscriptionService.cs`
- [ ] T020 [US2] Validate the multi-entry list behavior with a manual smoke test across the backend and frontend

**Checkpoint**: At this point, User Stories 1 and 2 should both work independently

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and project hygiene around the MVP scope

- [ ] T021 [P] Review the implementation against the project constitution and MVP scope in `.specify/memory/constitution.md` and `StakeholderDocuments/ProjectGoals.md`
- [ ] T022 [P] Confirm the solution stays within the add-and-list subscription scope and does not introduce feed parsing or persistence prematurely in `backend/RSSFeedReader.Api/` and `frontend/RSSFeedReader.UI/`
- [ ] T023 Run the quickstart validation flow from `specs/001-rss-reader-mvp/quickstart.md` and verify the local app works end-to-end

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) and is the MVP deliverable
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) and validates the list behavior after multiple entries

### Parallel Opportunities

- Setup tasks T002 and T003 can run in parallel
- Foundational tasks T005, T006, T007, and T008 can run in parallel
- User Story 1 tasks T010, T011, and T012 can be implemented in parallel if team capacity allows
- User Story 2 tasks T016, T017, and T018 can be implemented in parallel

---

## Implementation Strategy

### MVP First

1. Complete Setup
2. Complete Foundational
3. Complete User Story 1
4. Validate the add-subscription workflow
5. Stop and confirm the feature is a valid MVP

### Incremental Delivery

1. Setup + Foundational creates the base application
2. User Story 1 delivers the core business value
3. User Story 2 ensures the list remains visible and accurate after repeated additions
4. Final polish ensures the app remains aligned with the project constitution and MVP scope

---

## Notes

- [P] tasks are parallelizable and should target different files with no dependency on incomplete work
- Each user story is independently testable and should remain valid even if the rest of the roadmap is deferred
- The project intentionally excludes feed-fetching, parsing, and persistence from this tasks set to match the approved MVP scope
