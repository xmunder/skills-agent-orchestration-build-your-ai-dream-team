# Project Pulse Agent Team

The Project Pulse dashboard will be built by the specialist team defined in
`.github/agents/`.

| Agent | Model | Responsibility | Definition |
| --- | --- | --- | --- |
| **Orchestrator** | Claude Opus 4.7 (copilot) | Coordinates the request, delegates work, assigns explicit file scopes, manages dependencies, and verifies the integrated result. It does not implement the dashboard or perform Git operations. | `.github/agents/orchestrator.agent.md` |
| **Planner** | Claude Opus 4.7 (copilot) | Researches the repository and requirements, identifies risks and dependencies, and creates the ordered implementation plan with file ownership and validation expectations. | `.github/agents/planner.agent.md` |
| **Designer** | Gemini 3.1 Pro (copilot) | Defines the dashboard's user experience, information hierarchy, accessibility, responsive behavior, visual styling, project cards, status badges, and priority treatment. | `.github/agents/designer.agent.md` |
| **Coder** | GPT-5.5 (copilot) | Implements the assigned static application files, follows repository patterns, creates runnable support configuration when assigned, and validates the implementation. | `.github/agents/coder.agent.md` |

## Collaboration Flow

1. The Orchestrator receives the Project Pulse request and asks the Planner to
   research the repository and produce an implementation plan.
2. The Orchestrator turns that plan into phases with non-overlapping file
   ownership and explicit dependencies.
3. The Designer works on the dashboard experience and styling guidance while
   the Coder implements the static HTML, CSS, JSON data, and assigned launch
   configuration. These tasks can run in parallel when their file scopes do not
   overlap.
4. The Orchestrator integrates and reviews the result, checks that the
   dashboard is coherent and runnable, and reports the final outcome.
5. Git staging, commits, and pushes remain under the learner's control.

This workflow keeps planning, design, implementation, and validation separate
while allowing the Orchestrator to coordinate the complete Project Pulse
dashboard.
