# Task: Execute Story Updates

## Command
`/execute_story_updates`

## Description
Processes story folders and updates the checklist_for_stories.md file with current status. Ensures all stories are tracked and their completion status is accurately reflected.

## Steps
1. Scan context_specs/01_stories/ for all story folders (pattern: NNNNNN-StoryName)

2. Read current checklist_for_stories.md

3. For each story folder found:
   - Check if listed in checklist
   - If not listed, add with status "pending"
   - If listed, verify completion status

4. For each story, check existence of:
   - given_user_story_prompt.md
   - story.md (formalized story)
   - changes_for_product_requirement.md (created)
   - changes_for_architecture_design.md (created)
   - changes_for_implementation.md (created)
   - changes_for_acceptance_tests.md (created)
   - Check if changes have been applied

5. Update checklist with current status:
   - ⬜ Not created
   - 🔄 Created but not applied
   - ✅ Created and applied
   - ❌ Error or blocked

## Checklist Format
```markdown
# Story Checklist

## 000001-UserAuthentication
- [x] created changes_for_product_requirements.md
- [x] created changes_for_architecture_design.md
- [x] created changes_for_implementation.md
- [ ] created changes_for_acceptance_tests.md
- [x] applied changes_for_product_requirements.md
- [ ] applied changes_for_architecture_design.md
- [ ] applied changes_for_implementation.md
- [ ] applied changes_for_acceptance_tests.md
Status: In Progress (4/8 completed)
```

## Output
- Updated checklist_for_stories.md
- Summary report of story statuses
- List of blocked or incomplete stories

## Error Handling
- Handle missing story folders gracefully
- Report corrupted or invalid story structures
- Preserve manual edits to checklist where possible