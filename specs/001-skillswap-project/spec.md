# Feature Specification: SkillSwap — Community Skill Exchange

**Project Title**: SkillSwap — Community Skill Exchange  
**Project Description**: A community marketplace where people share skills they can teach, find skills they want to learn, and arrange reciprocal skill exchanges.  
**Feature Branch**: `001-skillswap-project`  
**Created**: 2026-11-14  
**Status**: Draft  
**Input**: User request to specify a SkillSwap project with accounts, skill offer/request management, browsing and search, swap decisions, profiles, API endpoints, and implementation priorities.

## Purpose and Target Audience

SkillSwap helps people exchange practical knowledge directly with one another, without requiring money to be the center of the transaction. It gives members a way to describe what they can teach, find what they want to learn, and manage an agreed exchange.

The target audience is community members, students, hobbyists, and other people who want to teach or learn skills through peer-to-peer exchanges. The primary user is a registered member. Visitors may discover public skills and member profiles, but must sign in to create listings or initiate an exchange.

## User Scenarios & Testing

### User Story 1 - Create an account and sign in (Priority: P1)

As a prospective member, I want to register and securely sign in so I can manage listings and participate in skill exchanges.

**Why this priority**: An account is required to own listings and make or respond to exchange requests.

**Independent Test**: Register a new account, sign out, and sign back in; verify invalid or duplicate registration and incorrect credentials are handled without granting access.

**Acceptance Scenarios**:

1. **Given** a visitor provides a valid name, email address, and password, **When** they submit registration, **Then** an account is created and they are signed in or shown a clear next step to sign in.
2. **Given** an email address is already registered, **When** a visitor attempts registration with it, **Then** the account is not duplicated and a helpful error is shown.
3. **Given** a registered member enters valid credentials, **When** they submit sign-in, **Then** they gain access to member actions and their own profile.
4. **Given** a visitor enters invalid credentials or leaves required fields invalid, **When** they submit the form, **Then** access is denied and actionable validation feedback is shown without exposing whether a password is correct.
5. **Given** a signed-in member signs out, **When** they next visit a protected action, **Then** they must sign in again before the action can be completed.

### User Story 2 - Create and manage skill offers and requests (Priority: P1)

As a member, I want to create, view, edit, and remove both skills I can teach and skills I want to learn so other members can find accurate opportunities to exchange.

**Why this priority**: Current, member-owned skill listings are the core inventory that makes a skill exchange possible.

**Independent Test**: Sign in as a member, create one offer and one request, view both, edit each, and delete each; verify another member cannot edit or delete them.

**Acceptance Scenarios**:

1. **Given** a signed-in member has not created a listing, **When** they submit a skill offer with a title, description, and category, **Then** the offer is saved, associated with that member, and available in browse results.
2. **Given** a signed-in member wants to learn a skill, **When** they submit a skill request with a title, description, and category, **Then** the request is saved as a request (not an offer), associated with that member, and available in browse results.
3. **Given** a member owns an active offer or request, **When** they open it, **Then** they can view its details and edit its title, description, category, or availability information.
4. **Given** a member saves an edit, **When** the update is valid, **Then** the listing reflects the new details in its page and browse results.
5. **Given** a member owns a listing, **When** they choose to remove it and confirm, **Then** it is no longer publicly discoverable and cannot be used to start a new swap request.
6. **Given** a member attempts to change or remove another member's listing, **When** the action is submitted, **Then** the change is refused and the listing remains unchanged.
7. **Given** a required listing field is missing or exceeds the supported length, **When** the member submits the listing, **Then** it is not saved and the invalid field is identified.
8. **Given** a member changes their listing's availability to inactive, **When** the change is saved, **Then** it is excluded from discovery and new swap proposals; the owner can make it active again by editing it.

### User Story 3 - Browse and search skills (Priority: P1)

As a visitor or member, I want to browse and search skill offers and requests so I can find people and opportunities relevant to what I want to teach or learn.

**Why this priority**: Discovery connects available skills with people seeking them and provides value even before registration.

**Independent Test**: Create public offers and requests with distinct titles and categories, then search and filter them as a visitor and verify the matching results and listing types.

**Acceptance Scenarios**:

1. **Given** active public skill listings exist, **When** a visitor opens skill discovery, **Then** they can browse offers and requests with their type, title, summary, category, and member identity.
2. **Given** a visitor searches by a word or phrase, **When** matching listing titles or descriptions contain it, **Then** matching listings are shown and non-matching listings are excluded.
3. **Given** a visitor chooses a listing type or category filter, **When** the filter is applied, **Then** only listings matching all selected filters are shown.
4. **Given** no listing matches a search or filter, **When** results load, **Then** an empty state explains that no matches were found and allows the visitor to adjust the search.
5. **Given** a listing has been removed or made inactive, **When** a visitor browses or searches, **Then** that listing is not available as a current opportunity.

### User Story 4 - Send and respond to swap requests (Priority: P1)

As a member, I want to propose a skill exchange and accept or decline incoming proposals so both participants can agree on an exchange.

**Why this priority**: The exchange proposal and decision are the action that turns skill discovery into a mutually agreed swap.

**Independent Test**: Use two member accounts and active listings to send a proposal, then accept it as its recipient; repeat with a separate proposal and decline it.

**Acceptance Scenarios**:

1. **Given** a signed-in member views another member's active skill offer, **When** they send a swap request with the skill they can offer and an optional message, **Then** a pending request is created and associated with the sender, recipient, and relevant listings.
2. **Given** a member attempts to request a swap with their own listing, an inactive listing, or a listing already unavailable for new proposals, **When** they submit the request, **Then** it is rejected and no pending request is created.
3. **Given** a member receives a pending swap request, **When** they open their requests, **Then** they can see the proposer, proposed skill exchange, message, and current status.
4. **Given** the recipient owns the target listing and the request is pending, **When** they accept it, **Then** the status becomes accepted and both participants can see that decision.
5. **Given** the recipient owns the target listing and the request is pending, **When** they decline it, **Then** the status becomes declined and both participants can see that decision.
6. **Given** a request has already been accepted or declined, **When** either participant attempts to change that decision through the normal response action, **Then** the request remains in its decided state and the user is told it can no longer be changed.
7. **Given** a member is not the sender or recipient, **When** they attempt to view or decide a private swap request, **Then** access is refused.
8. **Given** an equivalent proposal from the sender to the recipient is already pending, **When** the sender submits it again, **Then** no duplicate pending request is created and the existing request is identified.

### User Story 5 - View and maintain a member profile (Priority: P2)

As a member, I want a profile page that introduces me and shows my active skills so potential exchange partners can understand my interests and offerings.

**Why this priority**: Profiles build context and trust around listings, while the core exchange can be validated first.

**Independent Test**: Create a member profile, view it publicly, update its editable fields, and verify that another member cannot change it.

**Acceptance Scenarios**:

1. **Given** a member opens their profile page, **When** the page loads, **Then** it displays their name, optional biography, and active skill offers and requests.
2. **Given** a signed-in member updates their permitted profile details, **When** they save valid changes, **Then** the profile page reflects the updates.
3. **Given** a visitor views a member profile, **When** the profile loads, **Then** public profile information and active listings are visible without exposing private account credentials or contact details.
4. **Given** a member attempts to edit another person's profile, **When** the change is submitted, **Then** it is refused and the profile remains unchanged.
5. **Given** a member has no biography or active listings, **When** their profile is viewed, **Then** an appropriate empty state is shown instead of missing or misleading information.

### Edge Cases

- Duplicate registration emails, malformed email addresses, missing fields, and invalid credentials must not create partial accounts or reveal sensitive credential information.
- Empty, whitespace-only, excessively long, or unsupported listing fields must be rejected with field-level guidance.
- Search results must handle no matches and must not expose removed or inactive listings.
- Concurrent responses to a pending swap request must result in only one valid decision; a later action must see the decided state.
- A swap request must not be sent to oneself, based on a missing or inactive listing, or duplicated while an equivalent request remains pending.
- Members must not be able to read private request details or modify another member's listings or profile.
- If an account or listing becomes unavailable while a user is viewing it, the next attempted action must be refused with a clear explanation.

## Requirements

### Functional Requirements

- **FR-001**: The system MUST allow a visitor to register with a non-empty display name of no more than 80 characters, a syntactically valid unique email address, and a password of at least 8 characters, and MUST provide sign-in and sign-out.
- **FR-002**: The system MUST validate required account fields and MUST provide understandable errors for invalid registration or sign-in attempts without disclosing password data.
- **FR-003**: The system MUST distinguish a skill offer (a skill a member can teach) from a skill request (a skill a member wants to learn).
- **FR-004**: A signed-in member MUST be able to create, view, edit, and remove their own offers and requests.
- **FR-005**: The system MUST associate each skill listing with its owner and MUST prevent other members from editing or removing it.
- **FR-006**: Each listing MUST include a type, a non-empty title of no more than 100 characters, a non-empty description of no more than 2,000 characters, a non-empty category, an owner, and active/inactive availability; optional details MAY include scheduling preferences.
- **FR-007**: Visitors and members MUST be able to browse active public listings, search listing text, and filter by listing type and category.
- **FR-008**: Search and browse results MUST exclude removed or inactive listings and MUST provide a clear empty state when there are no matches.
- **FR-009**: A signed-in member MUST be able to send a pending swap request to another member for an active offer, identifying a skill they can contribute and optionally adding a message.
- **FR-010**: The system MUST prevent self-directed swap requests and requests for unavailable listings.
- **FR-011**: Only the recipient of a pending swap request MUST be able to accept or decline it; accepted and declined requests MUST retain their decision and show the current status to both participants.
- **FR-012**: The system MUST make swap request details visible only to the sender and recipient.
- **FR-013**: Each member MUST have a profile page showing their display name, optional biography of no more than 500 characters, and active offers and requests.
- **FR-014**: A signed-in member MUST be able to update their own permitted profile information, and MUST NOT be able to alter another member's profile.
- **FR-015**: Public profiles MUST NOT expose passwords, private authentication data, or private contact information.
- **FR-016**: The system MUST display understandable feedback for successful actions, validation errors, unavailable content, and unauthorized actions.
- **FR-017**: Duplicate pending proposals for the same proposed exchange MUST be prevented or clearly identified to the sender.

### Proposed API Endpoints

These endpoint paths describe the expected user-facing API contract for planning and acceptance testing; they do not prescribe a framework or storage design.

| Priority | Method and endpoint | Purpose and access |
|---|---|---|
| P1 | `POST /api/auth/register` | Register a member; public access. |
| P1 | `POST /api/auth/login` | Sign in a member; public access. |
| P1 | `POST /api/auth/logout` | End the current member session; signed-in member. |
| P1 | `GET /api/skills` | Browse/search active listings; public access. Supports query text and type/category filters. |
| P1 | `POST /api/skills` | Create an offer or request; signed-in member. |
| P1 | `GET /api/skills/{skillId}` | View an active public listing. |
| P1 | `PATCH /api/skills/{skillId}` | Edit an owned listing or its active availability; listing owner. |
| P1 | `DELETE /api/skills/{skillId}` | Remove an owned listing from public discovery; listing owner. |
| P1 | `POST /api/swaps` | Send a pending exchange proposal; signed-in member, for another member's active offer. |
| P1 | `GET /api/swaps` | List swap requests involving the signed-in member, optionally filtered by incoming/outgoing and status. |
| P1 | `GET /api/swaps/{swapId}` | View a request; sender or recipient only. |
| P1 | `POST /api/swaps/{swapId}/accept` | Accept a pending incoming request; recipient only. |
| P1 | `POST /api/swaps/{swapId}/decline` | Decline a pending incoming request; recipient only. |
| P2 | `GET /api/members/{memberId}` | View public profile details and active listings; public access. |
| P2 | `PATCH /api/members/me` | Update the signed-in member's permitted profile details; owner only. |

### Implementation Priority

1. **P1 — Core exchange MVP**: account registration and sign-in; create, read, update, and remove skill offers and requests; public browse/search; send, accept, and decline swap requests; authorization and validation required to safely complete these flows.
2. **P2 — Member profiles**: public profile page, editable biography and display details, and profile-linked active listings.
3. **P3 — Enhancements**: optional listing scheduling preferences and richer discovery refinements beyond text search, type, and category. These are not required to validate the initial exchange experience.

### Assumptions

- SkillSwap supports one member account per unique email address; members use email and password for the initial sign-in experience.
- Display names are limited to 80 characters, passwords must contain at least 8 characters, listing titles to 100 characters, listing descriptions to 2,000 characters, and profile biographies to 500 characters.
- Visitors can browse active listings and public profiles, but registration is required to create/edit listings or send/respond to swaps.
- A listing is either an offer or a request; its owner may mark it inactive or remove it.
- A swap request targets another member's active offer and identifies one skill offer from the sender, with an optional free-text message. A request to teach a requester-owned skill can be managed as a listing rather than a separate swap-request direction.
- The recipient's accept/decline decision is final in the initial release. Any later cancellation or negotiation flow is outside this scope.
- Profile display name and biography are public; email, password, and other private authentication/contact information are not.
- The initial release uses a simple text search and category/type filters; recommendation ranking, chat, payments, ratings, and scheduling/booking are outside this scope.
- API paths are proposed product contracts because the user explicitly requested endpoints; exact payload formats and authentication mechanisms are to be defined during planning.

### Key Entities

- **Member**: A person with an account, sign-in identity, public display name, optional biography, and owned listings and swap requests.
- **Skill Listing**: An offer or request owned by a member, with a title, description, category, and active/inactive availability.
- **Swap Request**: A proposal from one member to another, connecting the recipient's offer with the sender's offered skill; includes an optional message and a pending, accepted, or declined status.

## Success Criteria

### Measurable Outcomes

- **SC-001**: At least 90% of first-time users with valid information complete registration and reach a signed-in state in under 2 minutes.
- **SC-002**: At least 90% of members can create and later update one offer and one request in under 5 minutes total, excluding time spent composing descriptions.
- **SC-003**: At least 90% of test searches with known matching listings return the expected matches, and 100% of inactive or removed listings are absent from discovery.
- **SC-004**: At least 90% of members can send a valid swap proposal and its recipient can accept or decline it in under 3 minutes.
- **SC-005**: In acceptance testing, 100% of attempted unauthorized edits, deletions, or swap decisions are refused without changing the protected data.
- **SC-006**: At least 90% of test participants can identify a member's active offers and requests from their profile page without assistance.
