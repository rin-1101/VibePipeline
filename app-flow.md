# 3. App Flow

This document explains what users see, what happens when they click or submit something, and which page or state follows each action.

**Project:** [App name]  
**Status:** [Draft / Agreed / Revised]  
**Owner:** [Name or role]  
**Last updated:** [YYYY-MM-DD]

## Entry points and navigation

- **Entry points:** [Landing page, direct URL, invitation, or other entry]
- **Default destination:** [First page for each user type]
- **Navigation:** [Menu items, tabs, breadcrumbs, and back behavior]
- **Authentication flow:** [Sign-in, sign-out, session expiry, and return destination, if applicable]
- **Direct links:** [Behavior when a page URL is opened without prior navigation]

## Page inventory

| Page ID | Page name | Route | Purpose | Allowed users | Related feature |
| --- | --- | --- | --- | --- | --- |
| P-01 | [Page name] | [Route] | [Main user task] | [Roles or public] | F-01 |

Include dialogs, drawers, or other significant UI states when they affect the journey.

## Action and transition map

Every interactive control should have a defined result. A result may update the current page instead of navigating elsewhere.

| Current page or state | User action | Preconditions | System behavior | Next page or state | Failure behavior |
| --- | --- | --- | --- | --- | --- |
| [P-01 or state] | [Click or submission] | [Required input or access] | [Read, write, or UI change] | [P-02 or updated state] | [Visible error and recovery] |

## User journeys

Repeat this section for each main feature or task.

### Journey: [Name] — F-01

1. **Start:** [Where the user enters and what they need]
2. **Action:** [What the user clicks, enters, or selects]
3. **Response:** [What the app does and displays]
4. **Next step:** [Next page or available action]
5. **Finish:** [Visible confirmation and resulting data state]

Describe alternate paths, such as cancelling, going back, correcting input, or retrying after a failure.

## Page states

| State | What the user sees | Available actions |
| --- | --- | --- |
| Initial | [Content before interaction] | [Actions] |
| Loading | [Progress indicator and control behavior] | [Actions] |
| Empty | [Explanation when no records exist] | [Actions] |
| Success | [Result or confirmation] | [Actions] |
| Validation error | [Field-level guidance] | [Correction actions] |
| System error | [Failure message] | [Retry or recovery actions] |
| Access denied or expired session | [Permission or sign-in message] | [Navigation or sign-in actions] |

Only include states that apply to the page, but explicitly define expected failures for important actions.

## Interaction rules

Describe unsaved changes, refresh behavior, browser back behavior, repeat submissions, destructive-action confirmation, keyboard operation, and focus movement where relevant. Link visual rules to [Design Brief](design-brief.md) and permissions to [Background Schema](background-schema.md).

## Completion criteria

This document is ready when every MVP feature has a complete journey, every control has an outcome, destinations match the page inventory, and users can recover from expected failures.
