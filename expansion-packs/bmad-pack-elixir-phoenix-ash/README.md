# BMAD Pack - Elixir Phoenix Ash

An expansion pack for the BMAD Method specifically designed for Elixir Phoenix applications using the Ash Framework.

## Overview

This expansion pack provides a structured approach to feature development in Elixir Phoenix applications with Ash, following the BMAD (Business Method for Agile Development) methodology. It includes specialized agents, tasks, templates, and workflows optimized for the Elixir ecosystem.

## Features

- **Structured Story Management**: Organized approach to user stories with comprehensive tracking
- **Ash Framework Integration**: Templates and patterns specifically for Ash resources, actions, and policies
- **Phoenix LiveView Support**: Architecture patterns for LiveView components
- **Automated Documentation**: Generate specifications from user stories
- **Complete Testing Strategy**: Templates for unit, integration, and acceptance tests

## Quick Start

### 1. Initialize Project Structure
```bash
/init
```
Creates the document folder structure and initial templates.

### 2. Create a User Story
Add your user story to `context_specs/01_stories/000001-YourStoryName/given_user_story_prompt.md`

### 3. Update Story Tracking
```bash
/execute_story_updates
```
Updates the checklist with your new story.

### 4. Generate Specifications
```bash
/execute_specs_from_stories
```
Processes stories and generates all specification documents.

## Folder Structure

```
context_specs/
├── 01_stories/                    # User stories and requirements
│   ├── 000001-StoryName/
│   │   ├── given_user_story_prompt.md
│   │   ├── story.md                    # Formalized story
│   │   ├── changes_for_product_requirement.md
│   │   ├── changes_for_architecture_design.md
│   │   ├── changes_for_implementation.md
│   │   └── changes_for_acceptance_tests.md
│   └── checklist_for_stories.md
├── 02_product_requirements/       # Business requirements by feature (sharded)
├── 03_architecture_design/        # Technical architecture documents (sharded)
└── 04_acceptance_criteria/       # Manual test specifications
```

## Agents

### Initializer Agent
- Sets up project structure
- Creates templates and checklists
- Initializes tracking systems

### Feature Analyst Agent
- Analyzes user stories
- Creates formalized story.md
- Breaks down requirements
- Maps to Ash capabilities

### Product Owner Agent
- Translates stories to business requirements
- Defines acceptance criteria
- Ensures business alignment

### Architect Designer Agent
- Creates technical designs
- Specifies Ash resources
- Plans Phoenix architecture

### Acceptance Tester Agent
- Creates manual test cases
- Defines acceptance criteria
- Ensures requirement coverage

## Commands

### `/init`
Initialize the project structure with all required folders and templates.

### `/execute_story_updates`
Scan story folders and update the tracking checklist with current status.

### `/execute_specs_from_stories`
Process pending stories and generate specification documents using all agents. Updates documentation only, not code.

## Templates

- **given_user_story_prompt.md**: User story template
- **story.md**: Formalized story document
- **changes_for_product_requirement.md**: Business requirements documentation
- **changes_for_architecture_design.md**: Technical architecture with Ash/Phoenix specifics
- **changes_for_implementation.md**: Implementation guide with code templates
- **changes_for_acceptance_tests.md**: Test specifications and manual test cases

## Workflow

1. **Story Creation**: User provides story in standard format
2. **Analysis**: Feature Analyst breaks down requirements
3. **Requirements**: Product Owner creates business specifications
4. **Architecture**: Architect designs technical solution
5. **Implementation**: Development based on specifications
6. **Testing**: Comprehensive test suite execution
7. **Completion**: Update tracking and documentation

## Ash Framework Integration

This pack includes specific support for:
- Resource definitions with attributes and relationships
- Action specifications (CRUD and custom)
- Policy and authorization rules
- Calculations and aggregates
- API layer design (JSON:API, GraphQL)

## Phoenix Features

Optimized templates for:
- LiveView components
- Context modules
- Channel design
- Router configuration
- Plug pipelines

## Best Practices

1. Always start with `/init` for new projects
2. Write clear, detailed user stories
3. Review generated specifications before implementation
4. Keep the checklist updated throughout development
5. Follow Elixir/Phoenix conventions
6. Implement comprehensive tests

## Configuration

The pack can be configured in `config.yaml`:
- `slashPrefix`: Command prefix (default: `bmadash`)
- `version`: Pack version
- Custom agent behaviors

## Contributing

To extend this pack:
1. Add new agents in `agents/`
2. Create tasks in `tasks/`
3. Add templates in `templates/`
4. Define workflows in `workflows/`

## License

Part of the BMAD Method ecosystem.