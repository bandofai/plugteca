# Interactive requirements brainstorming

Start an interactive Q&A session to build comprehensive requirements for a feature.

# Instructions

When the user runs `/brainstorm <name>`:

1. **Validate the name parameter**
   - If no name provided, ask: "What would you like to name this requirement?"
   - Suggest using kebab-case (e.g., `user-authentication`, `payment-flow`)

2. **Check if requirement already exists**
   - Look for `.requirements/<name>.md`
   - If exists, ask if they want to overwrite or create a new version

3. **Start interactive brainstorming**
   Ask these questions systematically, adapting based on answers:

   a. **Overview**
      - "What is the main goal of this feature?"
      - "Who are the primary users/beneficiaries?"

   b. **Functionality**
      - "What are the core functionalities needed?"
      - "Are there any specific user flows or interactions?"

   c. **Technical Context**
      - "What technologies/frameworks should be used?"
      - "Are there any existing systems this integrates with?"

   d. **Constraints & Edge Cases**
      - "Are there any performance requirements?"
      - "What edge cases should we consider?"
      - "What are the security considerations?"

   e. **Success Criteria**
      - "How will we know this is successfully implemented?"
      - "What are the acceptance criteria?"

4. **Generate structured requirement document**
   Create `.requirements/<name>.md` with this structure:

   ```markdown
   # [Feature Name]

   **Created:** [date]
   **Status:** draft

   ## Overview
   [Summary of the feature and its purpose]

   ## User Stories
   - As a [user type], I want to [action] so that [benefit]

   ## Functional Requirements
   1. [Requirement 1]
   2. [Requirement 2]

   ## Technical Requirements
   - Technology stack
   - Integration points
   - Architecture considerations

   ## Edge Cases & Constraints
   - [Edge case 1]
   - [Edge case 2]
   - Performance requirements
   - Security considerations

   ## Acceptance Criteria
   - [ ] [Criteria 1]
   - [ ] [Criteria 2]

   ## Implementation Checklist
   - [ ] Design database schema (if applicable)
   - [ ] Create API endpoints
   - [ ] Implement business logic
   - [ ] Add validation
   - [ ] Write tests
   - [ ] Update documentation
   ```

5. **Update index metadata**
   Create/update `.requirements/_index.json`:
   ```json
   {
     "<name>": {
       "created": "2025-01-17T10:30:00Z",
       "status": "draft",
       "lastModified": "2025-01-17T10:30:00Z",
       "lastWorked": null
     }
   }
   ```

6. **Confirm completion**
   - Show summary of created requirement
   - Suggest next steps: "You can now run `/implement <name>` to start implementation"

## Best Practices

- Ask follow-up questions for clarity
- Suggest considerations the user might not have thought of
- Be thorough but don't overwhelm - balance depth with usability
- Adapt questions based on the feature type (API, UI, background job, etc.)
- If user is unsure, provide examples or suggest options
