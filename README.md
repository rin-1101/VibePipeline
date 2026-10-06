# Web App Documentation Overview

Use these six documents to define a web app before building it. Together, they explain what the app does, how people use it, how it looks, how it handles data, and how to implement it.

These documents are reusable templates. Replace `[placeholders]` with project decisions, mark unresolved decisions as `TBD`, and remove sections that do not apply. Examples describe the expected format; they are not chosen requirements or technologies.

## The six documents

| Document | Main question | Required contents |
| --- | --- | --- |
| [1. Product Requirement Document](product-requirements.md) | What are we building, and why? | Problem, target users, goals, features, priorities, scope, business rules, and acceptance criteria. |
| [2. Technical Requirements Document](technical-requirements.md) | What technologies and architecture will support it? | Frontend and backend stack, database technology, architecture, APIs, integrations, security, performance, testing, and deployment. |
| [3. App Flow](app-flow.md) | What happens when a user takes an action? | Pages, entry points, clicks, navigation, role restrictions, loading states, errors, and complete user journeys. |
| [4. Design Brief](design-brief.md) | What should the app look and feel like? | Brand direction, colors, fonts, layout, reusable components, responsive behavior, and accessibility. |
| [5. Background Schema](background-schema.md) | What data exists, who can access it, and where is it stored? | Entities, fields, relationships, validation, access control, storage locations, retention, backups, and migrations. |
| [6. Implementation Plan](implementation-plan.md) | In what order should we build and verify it? | Dependencies, phases, ordered tasks, deliverables, acceptance checks, release steps, and completion criteria. |

## What each document owns

- **Product Requirement Document:** feature behavior and the business reason for it.
- **Technical Requirements Document:** technology choices and engineering constraints.
- **App Flow:** user actions and the resulting page or state.
- **Design Brief:** visual rules and consistent branding.
- **Background Schema:** data structure, permissions, and storage rules. Here, “Background Schema” covers the app's backend data model.
- **Implementation Plan:** the sequence of work and how completion is verified.

Link to the document that owns a decision instead of repeating it in several places. For example, a task in the implementation plan should reference the feature, flow, and data entity it implements.

## Suggested preparation order

1. Write the product requirements to establish the problem, users, and minimum viable product (MVP).
2. Map the app flow so every feature has a clear user journey.
3. Define the design brief so the pages share one visual language.
4. Develop the technical requirements and background schema together, checking that the proposed stack supports the data and access rules.
5. Write the implementation plan once the feature, flow, design, and data decisions are concrete enough to estimate and build.

Revisit earlier documents when later decisions reveal a missing requirement. This preparation order is separate from the build order described in the implementation plan.

## Keep the documents connected

Use stable identifiers where useful:

| Identifier | Represents | Example reference |
| --- | --- | --- |
| `F-01` | Product feature | A flow or implementation task references `F-01`. |
| `P-01` | Page | A click takes the user from `P-01` to `P-02`. |
| `E-01` | Data entity | An API or task reads or writes `E-01`. |
| `T-01` | Implementation task | A phase includes `T-01` and its acceptance checks. |

Every feature included in the release should have acceptance criteria, an applicable user flow, necessary data and permissions, and an implementation task.

## Ready to build checklist

- [ ] The MVP, excluded features, and success measures are explicit.
- [ ] Every user action has a defined result, including failure states.
- [ ] Colors, fonts, components, and responsive behavior are documented.
- [ ] Required technologies and integrations have a stated purpose.
- [ ] Data fields, relationships, permissions, and storage rules are defined.
- [ ] Tasks have dependencies, deliverables, and checks for completion.
- [ ] Decisions that block implementation are resolved; other open questions have owners.

Keep all six documents updated as the app changes. Record the status, owner, and last-updated date in each document so readers can distinguish a draft from an agreed decision.
