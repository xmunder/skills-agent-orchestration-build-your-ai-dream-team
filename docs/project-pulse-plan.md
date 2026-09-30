# Project Pulse Implementation Plan

## Goal

Build a lightweight, polished static Project Pulse dashboard for Mona's
contributors. The dashboard should make active projects, owners, current
status, recent activity, priority or risk, and contributor-friendly summaries
easy to scan. It must open the Project Pulse UI from `app/index.html`, not a
server directory listing.

## Team Responsibilities

### Orchestrator

Coordinate the work, ask the Planner for this implementation plan, assign
non-overlapping file scopes, sequence dependent work, integrate the results,
and perform the final review. The Orchestrator does not implement files or
perform Git operations.

### Planner

Research the brief and repository, define phases, file ownership,
dependencies, parallel work decisions, edge cases, and validation expectations.

### Designer

Own the dashboard experience within the assigned scope: information hierarchy,
project-card layout, status badges, priority treatment, readable spacing,
responsive behavior, visual clarity, and accessibility. The Designer should
provide guidance for `app/index.html` and own or guide `app/styles.css` without
changing the data contract.

### Coder

Implement the static dashboard within the assigned scope. The Coder connects
`app/index.html` to `app/styles.css` and `app/project-data.json`, renders the
project fields, creates `.vscode/launch.json` as strict JSON when assigned, and
validates that the result is deterministic and runnable.

## Implementation Phases

### Phase 1: Confirm requirements and contracts

- **Owner:** Planner, coordinated by Orchestrator.
- Confirm the Project Pulse goal and the required project fields: `name`,
  `owner`, `status`, `recentActivity`, and `priority`.
- Define the top-level `projects` array in `app/project-data.json` as the data
  contract.
- Confirm that the launch configuration serves from `app/` and opens
  `index.html`.
- **Output:** agreed file assignments and acceptance criteria.

### Phase 2: Establish data and experience direction

- **Owner:** Designer for experience direction; Coder for data fixture.
- Designer defines the page hierarchy, project-card structure, status and
  priority affordances, accessible labels, responsive layout, and styling
  guidance.
- Coder creates `app/project-data.json` with representative projects covering
  active work, status, recent activity, priority, and short summaries.
- **File assignments:** Designer guides `app/index.html` and owns the visual
  direction for `app/styles.css`; Coder owns `app/project-data.json`.

### Phase 3: Implement the static dashboard

- **Owner:** Coder, using the Designer's direction.
- Create `app/index.html` with the Project Pulse title, semantic structure,
  accessible project cards, visible status and priority values, recent activity,
  and contributor-friendly summaries.
- Create `app/styles.css` with the polished responsive layout, readable
  spacing, contrast, rounded cards, status badges, and clear priority styling.
- Ensure `app/index.html` references both `styles.css` and
  `project-data.json`, and that the data fields are represented in the UI.
- **File assignments:** Coder owns `app/index.html` and `app/styles.css` during
  implementation; Designer reviews those files for experience and accessibility.

### Phase 4: Configure and validate preview

- **Owner:** Coder creates `.vscode/launch.json`; Orchestrator validates the
  integrated result.
- Add a deterministic **Run Project Pulse Dashboard** launch configuration.
- Serve from `${workspaceFolder}/app` and open `index.html` directly.
- Validate JSON syntax, HTML/CSS references, visible project fields, responsive
  layout hooks, and launch configuration behavior.
- **File assignment:** Coder owns `.vscode/launch.json`; Orchestrator owns the
  final review and handoff notes.

## File Assignments and Dependencies

| File | Primary owner | Purpose | Dependencies |
| --- | --- | --- | --- |
| `app/project-data.json` | Coder | Static Project Pulse project records and the `projects` data contract. | Requirements from the brief; no UI dependency. |
| `app/index.html` | Coder, guided by Designer | Dashboard structure and rendered project information. | Depends on the data fields and Designer's information hierarchy; references `styles.css` and `project-data.json`. |
| `app/styles.css` | Designer direction, Coder implementation | Responsive visual system, cards, badges, spacing, contrast, and priority treatment. | Depends on the HTML class hooks and visual direction. |
| `.vscode/launch.json` | Coder | Preview configuration that serves `app/` and opens `index.html`. | Depends on the app entry point and required launch name. |

The data contract should be agreed before the UI is finalized. The HTML needs
the data field names and CSS hooks, so implementation and styling review depend
on the contract and structure. The launch configuration depends on the final
`app/` entry point but does not change the application files.

## Parallel Work Decisions

- After Phase 1, the Designer can define the experience direction in parallel
  with the Coder creating `app/project-data.json`; these scopes do not overlap.
- `app/index.html` and `app/styles.css` should be implemented as a coordinated
  sequence or with explicit shared class hooks, because CSS depends on the
  markup structure. They should not be treated as independent final changes.
- `.vscode/launch.json` can be prepared in parallel with final styling once
  `app/index.html` and the `app/` serving assumptions are known.
- The Orchestrator's integration review and validation must run after all
  assigned files are complete.

## Validation Expectations

1. Confirm all four assigned paths exist: `app/index.html`, `app/styles.css`,
   `app/project-data.json`, and `.vscode/launch.json`.
2. Parse `app/project-data.json` and verify a top-level `projects` array whose
   records include `name`, `owner`, `status`, `recentActivity`, `priority`, and
   a contributor-friendly summary.
3. Check that `app/index.html` includes the Project Pulse title, references
   `styles.css` and `project-data.json`, and exposes project cards with status,
   activity, priority, and summary content.
4. Check that `app/styles.css` contains the dashboard and project-card hooks,
   responsive behavior, readable spacing, rounded corners, shadows, and
   sufficient contrast.
5. Parse `.vscode/launch.json` as strict JSON and verify the configuration is
   named **Run Project Pulse Dashboard**, serves from `app/`, and opens
   `index.html` rather than a directory listing.
6. Run the launch configuration and inspect the rendered dashboard on desktop
   and mobile-sized viewports. Confirm keyboard-accessible controls and clear
   status and priority distinctions.
7. The Orchestrator reviews the complete result against this plan and records
   remaining limitations in the final handoff.

## Risks and Mitigations

- **Markup and styling drift:** keep shared class hooks explicit and have the
  Designer review the Coder's integrated HTML/CSS result.
- **Data/UI mismatch:** define the JSON contract before implementation and
  validate every required field in both data and rendered output.
- **Directory listing opens instead of the dashboard:** set the launch working
  directory to `app/` and target `index.html` explicitly, then verify the
  preview URL.
- **Unreadable status or priority indicators:** pair color with text and use
  accessible labels, contrast, and non-color distinctions.
