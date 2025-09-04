# Task: Initialize Project Structure

## Command
`/init`

## Description
Creates the initial docs folder structure and initializes all required directories and template files for an Elixir Phoenix Ash project following BMAD methodology.

## Steps
1. Create base documentation structure:
   ```
   context_specs/
   ├── 01_stories/
   │   └── checklist_for_stories.md
   ├── 02_product_requirements/
   ├── 03_architecture_design/
   └── 04_acceptance_criteria/
   ```

2. Initialize checklist_for_stories.md with template

3. Create .gitkeep files in empty directories

4. Generate initial project README with BMAD instructions

## Prerequisites
- Project root directory exists
- Write permissions in project directory

## Output
- Complete folder structure created
- Checklist template initialized
- Success message with next steps

## Error Handling
- Check for existing folders before creation
- Warn if folders already exist
- Provide rollback option if initialization fails

## Next Steps
After initialization:
1. Create first user story with `/create_story`
2. Run `/execute_story_updates` to process stories
3. Generate specifications with `/execute_specs_from_stories`