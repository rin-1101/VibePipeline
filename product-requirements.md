# 1. Product Requirement Document

This document defines the app's purpose, users, and required features. It should explain expected behavior clearly enough for design, development, and verification.

**Project:** [App name]  
**Status:** [Draft / Agreed / Revised]  
**Owner:** [Name or role]  
**Last updated:** [YYYY-MM-DD]

## Problem and purpose

- **Problem:** [What difficulty do users currently face?]
- **Proposed solution:** [How will the app address it?]
- **Value:** [What improves for users or the business?]

## Target users

| User group | Main need | Relevant role or access level |
| --- | --- | --- |
| [User group] | [Task or problem] | [Role] |

Explain the context in which users will access the app, including relevant devices, frequency of use, or connectivity limitations.

## Goals and success measures

| Goal | Measurement | Target |
| --- | --- | --- |
| [Desired outcome] | [How the outcome is measured] | [Target and timeframe] |

## Scope

- **MVP:** [Features required for the first usable release]
- **Later releases:** [Features planned after the MVP]
- **Out of scope:** [Work this app or release will not cover]

## Feature requirements

Use one entry per feature. Assign stable feature IDs so other documents can reference them.

| Feature ID | Feature | User need | Priority | Release |
| --- | --- | --- | --- | --- |
| F-01 | [Feature name] | [As a user, I want to..., so that...] | [Must / Should / Could] | [MVP / Later] |

### F-01: [Feature name]

- **Users:** [Who can use it?]
- **Behavior:** [Inputs, actions, outputs, and important rules]
- **Preconditions:** [What must already be true?]
- **Acceptance criteria:** [Observable conditions that must pass]
- **Edge cases:** [Empty input, duplicate records, unavailable services, or other relevant cases]
- **Related flow:** [Page or journey in app-flow.md]

Example acceptance criterion format: “Given [starting condition], when [user action], then [observable result].” Include failure and permission cases where applicable.

## Business rules and constraints

Record eligibility rules, calculations, approval requirements, deadlines, or other rules that affect feature behavior. State measurable expectations for usability, accessibility, performance, and reliability; link technical implementation details to [Technical Requirements](technical-requirements.md).

## Dependencies, assumptions, and open questions

| Item | Type | Impact | Owner | Resolution or due date |
| --- | --- | --- | --- | --- |
| [Dependency, assumption, or question] | [Type] | [Affected feature] | [Owner] | [Decision or date] |

## Completion criteria

This document is ready when the release scope is clear, every required feature has observable acceptance criteria, and unresolved questions that block implementation have been answered.
