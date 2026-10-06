# 6. Implementation Plan

This document turns the agreed requirements into ordered work. It identifies what to build first, dependencies between tasks, and evidence needed to mark work complete.

**Project:** [App name]  
**Status:** [Draft / Agreed / Revised]  
**Owner:** [Name or role]  
**Last updated:** [YYYY-MM-DD]

## Inputs and release scope

Reference the agreed versions of [Product Requirements](product-requirements.md), [Technical Requirements](technical-requirements.md), [App Flow](app-flow.md), [Design Brief](design-brief.md), and [Background Schema](background-schema.md).

- **Release objective:** [What this release delivers]
- **Included features:** [Feature IDs]
- **Excluded work:** [Deferred features]
- **Constraints:** [Available people, time, budget, or external dependencies]

## Suggested build order

Adapt these phases to the app. Within a phase, schedule tasks according to their actual dependencies.

| Phase | Work | Deliverable | Exit check |
| --- | --- | --- | --- |
| 1. Resolve prerequisites | Answer blocking questions and verify required service access. | [Confirmed decisions and dependencies] | [No unresolved blockers for foundation work] |
| 2. Project foundation | Set up the repository, runtime, configuration, build tools, and local execution. | [Runnable app skeleton] | [Documented setup and build work] |
| 3. Data and access foundation | Add the schema, migrations, authentication if needed, and authorization rules. | [Usable persistence and access controls] | [Data integrity and allowed/denied access checks pass] |
| 4. Shared UI and navigation | Implement design tokens, reusable components, routes, and the app shell. | [Consistent page structure] | [Navigation, responsive layout, and keyboard checks pass] |
| 5. First complete feature | Build one core journey across UI, API, and storage, including failure states. | [Working feature from start to finish] | [Feature acceptance criteria pass] |
| 6. Remaining MVP features | Implement the remaining journeys in dependency order. | [Complete MVP scope] | [Each included feature meets its criteria] |
| 7. Release verification | Check complete journeys, permissions, compatibility, and agreed performance targets. | [Release candidate and recorded results] | [Required checks pass and critical defects are resolved] |
| 8. Deployment and handover | Deploy, verify health, confirm recovery steps, and document operations. | [Usable release and operational instructions] | [Deployment and post-release checks pass] |

Some work can overlap after its prerequisites are complete. For example, shared UI components may be developed alongside database work when their interfaces are agreed.

## Task breakdown

Use tasks small enough to build and review independently. Each task needs a concrete result, dependencies, and a completion check.

| Task ID | Phase | Task | Related requirements | Depends on | Owner | Estimate | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T-01 | [Phase] | [Action and deliverable] | [F-01, P-01, E-01] | [Task IDs or none] | [Owner] | [Estimate] | [Not started / In progress / Blocked / Done] |

### T-01: [Task name]

- **Deliverable:** [Specific behavior or artifact]
- **Implementation notes:** [Useful constraints or agreed approach]
- **Dependencies:** [What must exist first?]
- **Acceptance checks:** [Observable behavior that proves completion]
- **Verification evidence:** [Result or artifact recorded after checking]

## Milestones

| Milestone | Required tasks or features | Target date | Completion evidence |
| --- | --- | --- | --- |
| [Milestone] | [IDs] | [Date or TBD] | [Demonstrable outcome] |

## Risks and blockers

| Risk or blocker | Impact | Response | Owner | Status |
| --- | --- | --- | --- | --- |
| [Item] | [Affected work] | [Action or contingency] | [Owner] | [Status] |

## Release and completion checklist

- [ ] Every included feature meets its product acceptance criteria.
- [ ] App flows cover success, empty, loading, and relevant error states.
- [ ] Visual behavior follows the design brief across supported screen sizes.
- [ ] Data validation and permissions work for allowed and denied operations.
- [ ] Required tests, builds, and deployment checks pass.
- [ ] Configuration, migrations, health checks, backups, and recovery steps are ready where applicable.
- [ ] Documentation matches the delivered app, and remaining work is explicitly tracked.

Mark a task or milestone complete only after its checks have passed. Record the environment used for verification so local or simulated results are distinguishable from production validation.
