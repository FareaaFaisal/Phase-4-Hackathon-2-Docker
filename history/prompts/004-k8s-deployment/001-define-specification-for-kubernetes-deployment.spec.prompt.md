---
id: 001
title: Define Specification for Kubernetes Deployment
stage: spec
date: 2026-02-08
surface: agent
model: gemini-cli
feature: 004-k8s-deployment
branch: 004-k8s-deployment
user: user
command: /sp.specify
labels: [spec, kubernetes, deployment]
links:
  spec: specs/004-k8s-deployment/spec.md
  ticket: null
  adr: null
  pr: null
files:
  - specs/004-k8s-deployment/spec.md
  - specs/004-k8s-deployment/checklists/requirements.md
tests:
  - None
---

## Prompt
/sp.specify
---
description: Create or update the feature specification from a natural language feature description.
handoffs: 
  - label: Build Technical Plan
    agent: sp.plan
    prompt: Create a plan for the spec. I am building with...
  - label: Clarify Spec Requirements
    agent: sp.clarify
    prompt: Clarify specification requirements
    send: true
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Outline

The text the user typed after `/sp.specify` in the triggering message **is** the feature description. Assume you always have it available in this conversation even if `Project: Phase IV - Local Kubernetes Deployment of Todo Chatbot Input: Use the previously generated `/sp.constitution` for Phase IV deployment. Objective: - Transform the constitution into detailed **specifications**. - Each spec should be **actionable**, **tool-specific**, and **AI-agent ready**. Requirements: 1. Containerize both frontend and backend using Docker (use Gordon if available). 2. Create Kubernetes manifests (Deployments, Services, ConfigMaps) and Helm charts. 3. Use **kubectl-ai** and **kagent** to plan deployment, scaling, and monitoring. 4. Specify replicas, resource requests/limits, and service types for backend/frontend. 5. Include steps for local Minikube deployment. 6. Ensure the AI chatbot backend connects properly to frontend services. 7. Include optional AI-driven optimization tasks for Gordon, kubectl-ai, and kagent. Output: - Return structured JSON with: - `tasks`: array of high-level tasks. - `subtasks`: detailed steps per task. - Tool assignments: which tool or agent should perform the step (Gordon, kubectl-ai, kagent, Helm, Docker CLI, etc.) - Expected outcomes for each subtask. - Optional verification or test steps for each major task. - Ensure steps are **clear, unambiguous, and ready for AI-agent execution**. - Do not include manual code implementation; focus on spec-level instructions. Notes: - Focus only on **Phase IV deployment**. - Maintain **spec-driven approach**: everything should be actionable by AI agents. - Keep references to Phase III only as context (no modification). - Make it human-readable but **structured for AI planning**.` appears literally below. Do not ask the user to repeat it unless they provided an empty command.

Given that feature description, do this:

1. **Generate a concise short name** (2-4 words) for the branch:
   - Analyze the feature description and extract the most meaningful keywords
   - Create a 2-4 word short name that captures the essence of the feature
   - Use action-noun format when possible (e.g., "add-user-auth", "fix-payment-bug")
   - Preserve technical terms and acronyms (OAuth2, API, JWT, etc.)
   - Keep it concise but descriptive enough to understand the feature at a glance
   - Examples:
     - "I want to add user authentication" → "user-auth"
     - "Implement OAuth2 integration for the API" → "oauth2-api-integration"
     - "Create a dashboard for analytics" → "analytics-dashboard"
     - "Fix payment processing timeout bug" → "fix-payment-timeout"

2. **Check for existing branches before creating new one**:

   a. First, fetch all remote branches to ensure we have the latest information:

      ```bash
      git fetch --all --prune
      ```

   b. Find the highest feature number across all sources for the short-name:
      - Remote branches: `git ls-remote --heads origin | grep -E 'refs/heads/[0-9]+-<short-name>$'`
      - Local branches: `git branch | grep -E '^[* ]*[0-9]+-<short-name>$'`
      - Specs directories: Check for directories matching `specs/[0-9]+-<short-name>`

   c. Determine the next available number:
      - Extract all numbers from all three sources
      - Find the highest number N
      - Use N+1 for the new branch number

   d. Run the script `.specify/scripts/powershell/create-new-feature.ps1 -Json "Project: Phase IV - Local Kubernetes Deployment of Todo Chatbot Input: Use the previously generated `/sp.constitution` for Phase IV deployment. Objective: - Transform the constitution into detailed **specifications**. - Each spec should be **actionable**, **tool-specific**, and **AI-agent ready**. Requirements: 1. Containerize both frontend and backend using Docker (use Gordon if available). 2. Create Kubernetes manifests (Deployments, Services, ConfigMaps) and Helm charts. 3. Use **kubectl-ai** and **kagent** to plan deployment, scaling, and monitoring. 4. Specify replicas, resource requests/limits, and service types for backend/frontend. 5. Include steps for local Minikube deployment. 6. Ensure the AI chatbot backend connects properly to frontend services. 7. Include optional AI-driven optimization tasks for Gordon, kubectl-ai, and kagent. Output: - Return structured JSON with: - `tasks`: array of high-level tasks. - `subtasks`: detailed steps per task. - Tool assignments: which tool or agent should perform the step (Gordon, kubectl-ai, kagent, Helm, Docker CLI, etc.) - Expected outcomes for each subtask. - Optional verification or test steps for each major task. - Ensure steps are **clear, unambiguous, and ready for AI-agent execution**. - Do not include manual code implementation; focus on spec-level instructions. Notes: - Focus only on **Phase IV deployment**. - Maintain **spec-driven approach**: everything should be actionable by AI agents. - Keep references to Phase III only as context (no modification). - Make it human-readable but **structured for AI planning**." with the calculated number and short-name:
      - Pass `--number N+1` and `--short-name "your-short-name"` along with the feature description
      - Bash example: `.specify/scripts/powershell/create-new-feature.ps1 -Json "Project: Phase IV - Local Kubernetes Deployment of Todo Chatbot Input: Use the previously generated `/sp.constitution` for Phase IV deployment. Objective: - Transform the constitution into detailed **specifications**. - Each spec should be **actionable**, **tool-specific**, and **AI-agent ready**. Requirements: 1. Containerize both frontend and backend using Docker (use Gordon if available). 2. Create Kubernetes manifests (Deployments, Services, ConfigMaps) and Helm charts. 3. Use **kubectl-ai** and **kagent** to plan deployment, scaling, and monitoring. 4. Specify replicas, resource requests/limits, and service types for backend/frontend. 5. Include steps for local Minikube deployment. 6. Ensure the AI chatbot backend connects properly to frontend services. 7. Include optional AI-driven optimization tasks for Gordon, kubectl-ai, and kagent. Output: - Return structured JSON with: - `tasks`: array of high-level tasks. - `subtasks`: detailed steps per task. - Tool assignments: which tool or agent should perform the step (Gordon, kubectl-ai, kagent, Helm, Docker CLI, etc.) - Expected outcomes for each subtask. - Optional verification or test steps for each major task. - Ensure steps are **clear, unambiguous, and ready for AI-agent execution**. - Do not include manual code implementation; focus on spec-level instructions. Notes: - Focus only on **Phase IV deployment**. - Maintain **spec-driven approach**: everything should be actionable by AI agents. - Keep references to Phase III only as context (no modification). - Make it human-readable but **structured for AI planning**." --json --number 5 --short-name "user-auth" "Add user authentication"
      - PowerShell example: `.specify/scripts/powershell/create-new-feature.ps1 -Json "Project: Phase IV - Local Kubernetes Deployment of Todo Chatbot Input: Use the previously generated `/sp.constitution` for Phase IV deployment. Objective: - Transform the constitution into detailed **specifications**. - Each spec should be **actionable**, **tool-specific**, and **AI-agent ready**. Requirements: 1. Containerize both frontend and backend using Docker (use Gordon if available). 2. Create Kubernetes manifests (Deployments, Services, ConfigMaps) and Helm charts. 3. Use **kubectl-ai** and **kagent** to plan deployment, scaling, and monitoring. 4. Specify replicas, resource requests/limits, and service types for backend/frontend. 5. Include steps for local Minikube deployment. 6. Ensure the AI chatbot backend connects properly to frontend services. 7. Include optional AI-driven optimization tasks for Gordon, kubectl-ai, and kagent. Output: - Return structured JSON with: - `tasks`: array of high-level tasks. - `subtasks`: detailed steps per task. - Tool assignments: which tool or agent should perform the step (Gordon, kubectl-ai, kagent, Helm, Docker CLI, etc.) - Expected outcomes for each subtask. - Optional verification or test steps for each major task. - Ensure steps are **clear, unambiguous, and ready for AI-agent execution**. - Do not include manual code implementation; focus on spec-level instructions. Notes: - Focus only on **Phase IV deployment**. - Maintain **spec-driven approach**: everything should be actionable by AI agents. - Keep references to Phase III only as context (no modification). - Make it human-readable but **structured for AI planning**." -Json -Number 5 -ShortName "user-auth" "Add user authentication"

   **IMPORTANT**:
   - Check all three sources (remote branches, local branches, specs directories) to find the highest number
   - Only match branches/directories with the exact short-name pattern
   - If no existing branches/directories found with this short-name, start with number 1
   - You must only ever run this script once per feature
   - The JSON is provided in the terminal as output - always refer to it to get the actual content you're looking for
   - The JSON output will contain BRANCH_NAME and SPEC_FILE paths
   - For single quotes in args like "I'm Groot", use escape syntax: e.g 'I'\''m Groot' (or double-quote if possible: "I'm Groot")

3. Load `.specify/templates/spec-template.md` to understand required sections.

4. Follow this execution flow:

    1. Parse user description from Input
       If empty: ERROR "No feature description provided"
    2. Extract key concepts from description
       Identify: actors, actions, data, constraints
    3. For unclear aspects:
       - Make informed guesses based on context and industry standards
       - Only mark with [NEEDS CLARIFICATION: specific question] if:
         - The choice significantly impacts feature scope or user experience
         - Multiple reasonable interpretations exist with different implications
         - No reasonable default exists
       - **LIMIT: Maximum 3 [NEEDS CLARIFICATION] markers total**
       - Prioritize clarifications by impact: scope > security/privacy > user experience > technical details
    4. Fill User Scenarios & Testing section
       If no clear user flow: ERROR "Cannot determine user scenarios"
    5. Generate Functional Requirements
       Each requirement must be testable
       Use reasonable defaults for unspecified details (document assumptions in Assumptions section)
    6. Define Success Criteria
       Create measurable, technology-agnostic outcomes
       Include both quantitative metrics (time, performance, volume) and qualitative measures (user satisfaction, task completion)
       Each criterion must be verifiable without implementation details
    7. Identify Key Entities (if data involved)
    8. Return: SUCCESS (spec ready for planning)

5. Write the specification to SPEC_FILE using the template structure, replacing placeholders with concrete details derived from the feature description (arguments) while preserving section order and headings.

6. **Specification Quality Validation**: After writing the initial spec, validate it against quality criteria:

   a. **Create Spec Quality Checklist**: Generate a checklist file at `FEATURE_DIR/checklists/requirements.md` using the checklist template structure with these validation items:

      ```markdown
      # Specification Quality Checklist: [FEATURE NAME] 
      
      **Purpose**: Validate specification completeness and quality before proceeding to planning
      **Created**: [DATE]
      **Feature**: [Link to spec.md]
      
      ## Content Quality
      
      - [ ] No implementation details (languages, frameworks, APIs)
      - [ ] Focused on user value and business needs
      - [ ] Written for non-technical stakeholders
      - [ ] All mandatory sections completed
      
      ## Requirement Completeness
      
      - [ ] No [NEEDS CLARIFICATION] markers remain
      - [ ] Requirements are testable and unambiguous
      - [ ] Success criteria are measurable
      - [ ] Success criteria are technology-agnostic (no implementation details)
      - [ ] All acceptance scenarios are defined
      - [ ] Edge cases are identified
      - [ ] Scope is clearly bounded
      - [ ] Dependencies and assumptions identified
      
      ## Feature Readiness
      
      - [ ] All functional requirements have clear acceptance criteria
      - [ ] User scenarios cover primary flows
      - [ ] Feature meets measurable outcomes defined in Success Criteria
      - [ ] No implementation details leak into specification
      
      ## Notes
      
      - Items marked incomplete require spec updates before `/sp.clarify` or `/sp.plan`
      ```

   b. **Run Validation Check**: Review the spec against each checklist item:
      - For each item, determine if it passes or fails
      - Document specific issues found (quote relevant spec sections)

   c. **Handle Validation Results**:

      - **If all items pass**: Mark checklist complete and proceed to step 6

      - **If items fail (excluding [NEEDS CLARIFICATION])**:
        1. List the failing items and specific issues
        2. Update the spec to address each issue
        3. Re-run validation until all items pass (max 3 iterations)
        4. If still failing after 3 iterations, document remaining issues in checklist notes and warn user

      - **If [NEEDS CLARIFICATION] markers remain**:
        1. Extract all [NEEDS CLARIFICATION: ...] markers from the spec
        2. **LIMIT CHECK**: If more than 3 markers exist, keep only the 3 most critical (by scope/security/UX impact) and make informed guesses for the rest
        3. For each clarification needed (max 3), present options to user in this format:

           ```markdown
           ## Question [N]: [Topic] 
           
           **Context**: [Quote relevant spec section] 
           
           **What we need to know**: [Specific question from NEEDS CLARIFICATION marker] 
           
           **Suggested Answers**: 
           
           | Option | Answer | Implications |
           |--------|--------|--------------|
           | A      | [First suggested answer] | [What this means for the feature] |
           | B      | [Second suggested answer] | [What this means for the feature] |
           | C      | [Third suggested answer] | [What this means for the feature] |
           | Custom | Provide your own answer | [Explain how to provide custom input] |
           
           **Your choice**: _[Wait for user response]_
           ```

        4. **CRITICAL - Table Formatting**: Ensure markdown tables are properly formatted:
           - Use consistent spacing with pipes aligned
           - Each cell should have spaces around content: `| Content |` not `|Content|`
           - Header separator must have at least 3 dashes: `|--------|`
           - Test that the table renders correctly in markdown preview
        5. Number questions sequentially (Q1, Q2, Q3 - max 3 total)
        6. Present all questions together before waiting for responses
        7. Wait for user to respond with their choices for all questions (e.g., "Q1: A, Q2: Custom - [details], Q3: B")
        8. Update the spec by replacing each [NEEDS CLARIFICATION] marker with the user's selected or provided answer
        9. Re-run validation after all clarifications are resolved

   d. **Update Checklist**: After each validation iteration, update the checklist file with current pass/fail status

7. Report completion with branch name, spec file path, checklist results, and readiness for the next phase (`/sp.clarify` or `/sp.plan`).

**NOTE**: The script creates and checks out the new branch and initializes the spec file before writing.

## General Guidelines

## Quick Guidelines

- Focus on **WHAT** users need and **WHY**.
- Avoid HOW to implement (no tech stack, APIs, code structure).
- Written for business stakeholders, not developers.
- DO NOT create any checklists that are embedded in the spec. That will be a separate command.

### Section Requirements

- **Mandatory sections**: Must be completed for every feature
- **Optional sections**: Include only when relevant to the feature
- When a section doesn't apply, remove it entirely (don't leave as "N/A")

### For AI Generation

When creating this spec from a user prompt:

1. **Make informed guesses**: Use context, industry standards, and common patterns to fill gaps
2. **Document assumptions**: Record reasonable defaults in the Assumptions section
3. **Limit clarifications**: Maximum 3 [NEEDS CLARIFICATION] markers - use only for critical decisions that:
   - Significantly impact feature scope or user experience
   - Have multiple reasonable interpretations with different implications
   - Lack any reasonable default
4. **Prioritize clarifications**: scope > security/privacy > user experience > technical details
5. **Think like a tester**: Every vague requirement should fail the "testable and unambiguous" checklist item
6. **Common areas needing clarification** (only if no reasonable default exists):
   - Feature scope and boundaries (include/exclude specific use cases)
   - User types and permissions (if multiple conflicting interpretations possible)
   - Security/compliance requirements (when legally/financially significant)

**Examples of reasonable defaults** (don't ask about these):

- Data retention: Industry-standard practices for the domain
- Performance targets: Standard web/mobile app expectations unless specified
- Error handling: User-friendly messages with appropriate fallbacks
- Authentication method: Standard session-based or OAuth2 for web apps
- Integration patterns: RESTful APIs unless specified otherwise

### Success Criteria Guidelines

Success criteria must be:

1. **Measurable**: Include specific metrics (time, percentage, count, rate)
2. **Technology-agnostic**: No mention of frameworks, languages, databases, or tools
3. **User-focused**: Describe outcomes from user/business perspective, not system internals
4. **Verifiable**: Can be tested/validated without knowing implementation details

**Good examples**:

- "Users can complete checkout in under 3 minutes"
- "System supports 10,000 concurrent users"
- "95% of searches return results in under 1 second"
- "Task completion rate improves by 40%"

**Bad examples** (implementation-focused):

- "API response time is under 200ms" (too technical, use "Users see results instantly")
- "Database can handle 1000 TPS" (implementation detail, use user-facing metric)
- "React components render efficiently" (framework-specific)
- "Redis cache hit rate above 80%" (technology-specific)

---

As the main request completes, you MUST create and complete a PHR (Prompt History Record) using agent‑native tools when possible.

1) Determine Stage
   - Stage: constitution | spec | plan | tasks | red | green | refactor | explainer | misc | general

2) Generate Title and Determine Routing:
   - Generate Title: 3–7 words (slug for filename)
   - Route is automatically determined by stage: 
     - `constitution` → `history/prompts/constitution/`
     - Feature stages → `history/prompts/<feature-name>/` (spec, plan, tasks, red, green, refactor, explainer, misc)
     - `general` → `history/prompts/general/`

3) Create and Fill PHR (Shell first; fallback agent‑native)
   - Run: `.specify/scripts/bash/create-phr.sh --title "<title>" --stage <stage> [--feature <name>] --json`
   - Open the file and fill remaining placeholders (YAML + body), embedding full PROMPT_TEXT (verbatim) and concise RESPONSE_TEXT
   - If the script fails:
     - Read `.specify/templates/phr-template.prompt.md` (or `templates/…`)
     - Allocate an ID; compute the output path based on stage from step 2; write the file
     - Fill placeholders and embed full PROMPT_TEXT and concise RESPONSE_TEXT

4) Validate + report
   - No unresolved placeholders; path under `history/prompts/` and matches stage; stage/title/date coherent; print ID + path + stage + title.
   - On failure: warn, don't block. Skip only for `/sp.phr`.

## Response snapshot

I have created the feature specification for the "Application Deployment Modernization".
- **Branch**: `004-k8s-deployment`
- **Spec File**: `specs/004-k8s-deployment/spec.md`
- **Checklist**: `specs/004-k8s-deployment/checklists/requirements.md`

The specification is written in a technology-agnostic way as required. The technical details from your prompt will be used in the next step, `/sp.plan`.

As you requested a JSON output for planning, here is a structured JSON that can be used as input for `/sp.plan`.

## Outcome

- ✅ Impact: Major. New spec for Phase IV created.
- 🧪 Tests: None.
- 📁 Files: 2 created.
- 🔁 Next prompts: `/sp.plan` with the provided JSON.
- 🧠 Reflection: The script for creating a new feature failed, so I had to perform the steps manually. The user's request was very technical for a spec, so I abstracted it.

## Evaluation notes (flywheel)

- Failure modes observed: Script failure.
- Graders run and results (PASS/FAIL): PASS
- Prompt variant (if applicable): null
- Next experiment: n/a

