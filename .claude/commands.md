# Todo Management Commands

## Overview
This document describes the available commands for managing todos in this project. Todos are stored and managed in the `todos.json` file using natural language commands.

## Core Principles

### 1. Date Rule
When creating or updating any todo, the current date MUST be determined:
- Use `date` command in terminal
- Or JavaScript `new Date().toISOString()`
- NEVER enter a made-up date!

### 2. Intelligent Task Capture
When adding new todos:
- Claude analyzes the task context within the project code
- Researches relevant connections in the project
- Formulates the task more precisely and understandably
- Asks: "Would you like the raw or improved version?"
- The improved version should be approximately the same length (unless requested otherwise)

### 3. Structured Data Processing
- The JSON file should generally NOT be read and written directly by LLM
- Instead, LLM should read the data and execute appropriate modifications via code
- Or obtain a subset by applying filter rules to the JSON
- LLM can then be used for interpretation of results
- Example: "Filter for" or "show me all Priority 1 todos created yesterday" should be translated into JSON/JS filters that iterate over data and find structured datasets
- Results can then be included as context in prompts to answer complex questions like "Which appears most security-relevant?"

## Todo Operations

### Adding Todos
```
"Add a new todo: Implement user authentication with JWT tokens"
"Create todo for setting up CI/CD pipeline with high priority"
"Add security todo: Review API endpoints for vulnerabilities"
```

### Updating Todo Status
Automatically updates the `updated` timestamp with current date:
```
"Mark 'Set up TypeScript configuration' as done"
"Set 'Implement user authentication' to in-progress"
"Change status of API documentation todo to pending"
```

### Managing Todo Priority
```
"Set all security todos to high priority"
"Change 'Add dark mode support' to low priority"
"Make all authentication-related todos high priority"
```

### Viewing Todos
```
"Show all pending todos"
"List all high priority todos"
"What are the current in-progress tasks?"
"Display todos tagged with 'security'"
"Show todos created today"
"List all done todos from this week"
```

### Filtering and Searching
```
"Find todos containing 'authentication'"
"Show todos assigned to specific person"
"List todos with 'backend' tag"
"Display todos created after 2025-01-15"
"Show overdue todos"
```

### Deleting Todos
```
"Delete the todo 'Old feature request'"
"Remove all completed todos"
"Delete todos older than 30 days with status done"
```

### Bulk Operations
```
"Set all pending todos tagged 'security' to high priority"
"Mark all documentation todos as in-progress"
"Add 'urgent' tag to all high priority todos"
"Update all backend todos to include assignee 'john.doe'"
```

## Todo Viewer Usage

### Opening the Viewer
1. Open `todo-viewer.html` in browser
2. Filter and search through todos
3. Click on actions to generate Claude commands
4. Copy the generated command and paste it here

### Viewer Features
- **Filter by Status**: pending, in-progress, done
- **Filter by Priority**: high, medium, low
- **Search**: Full-text search across title and description
- **Tag Filtering**: Filter by specific tags
- **Date Range**: Filter by creation or update date
- **Sorting**: Sort by priority, date, or status
- **Export**: Export filtered results as JSON or CSV

## Data Structure

### Todo Object Schema
Each todo in `todos.json` contains:

```json
{
  "id": "UUID",
  "title": "Short descriptive title",
  "description": "Detailed description of the task",
  "status": "pending | in-progress | done",
  "priority": "high | medium | low",
  "created": "ISO-8601 timestamp",
  "updated": "ISO-8601 timestamp",
  "assignee": "Optional assignee name/email",
  "tags": ["array", "of", "tags"],
  "requestedBy": "user | ai-agent"
}
```

### Requested By Field
The `requestedBy` field indicates who initiated the creation of the todo:
- **"user"**: The todo was explicitly requested by the user through a command
- **"ai-agent"**: The todo was created by the AI while working on another task

#### Behavior Rules:
1. When a user explicitly asks to create a todo (e.g., "Add a new todo: ..."), set `requestedBy: "user"`
2. When the AI discovers a task while working and proactively creates a todo, set `requestedBy: "ai-agent"`
3. Default value is "user" if not specified
4. This field helps track task origin and can be used for filtering AI-suggested vs user-requested tasks

#### Examples:
- User says "Create todo for implementing login feature" → `requestedBy: "user"`
- AI finds missing tests while reviewing code and creates a todo → `requestedBy: "ai-agent"`
- User runs a command that generates multiple todos → all have `requestedBy: "user"`

### Status Values
- **pending**: Todo is created but not started
- **in-progress**: Todo is currently being worked on
- **done**: Todo is completed

### Priority Levels
- **high**: Critical tasks that need immediate attention
- **medium**: Important tasks with moderate urgency
- **low**: Nice-to-have tasks with low urgency

### Common Tags
- `setup`, `configuration`, `infrastructure`
- `frontend`, `backend`, `api`
- `security`, `authentication`, `authorization`
- `testing`, `quality`, `documentation`
- `performance`, `optimization`, `monitoring`
- `feature`, `enhancement`, `bug`, `maintenance`
- `devops`, `ci-cd`, `deployment`

## Advanced Commands

### Analytics and Reporting
```
"Show todo completion statistics for this week"
"How many high priority todos are still pending?"
"What's the average time between creation and completion?"
"Show todos grouped by assignee"
"Generate a progress report for security-related tasks"
```

### Project Management
```
"Create a sprint with all high priority pending todos"
"Show todos that are blocking other tasks"
"List todos that haven't been updated in over a week"
"Find todos without assignees"
"Show the oldest pending todos"
```

### Maintenance Commands
```
"Archive all todos completed more than 30 days ago"
"Clean up duplicate todos"
"Validate all todo data for consistency"
"Backup current todos to timestamped file"
"Restore todos from backup file"
```

## Integration Examples

### With Development Workflow
```
"Create todos from all TODO comments in the codebase"
"Add todo for each failing test in the test suite"
"Generate todos from GitHub issues"
"Create deployment checklist as todos"
```

### With Time Tracking
```
"Add time estimate to 'Implement user authentication'"
"Track time spent on todos tagged 'frontend'"
"Show todos that exceeded their time estimates"
```

## Best Practices

### Writing Good Todos
1. **Clear Titles**: Use descriptive, action-oriented titles
2. **Detailed Descriptions**: Include context, requirements, and acceptance criteria
3. **Appropriate Tags**: Use consistent tagging for better filtering
4. **Realistic Priorities**: Don't make everything high priority
5. **Regular Updates**: Keep status current and add progress notes

### Workflow Recommendations
1. **Daily Review**: Check pending and in-progress todos daily
2. **Weekly Cleanup**: Archive completed todos and reassess priorities
3. **Tag Consistency**: Establish and maintain consistent tagging conventions
4. **Status Updates**: Update status as work progresses
5. **Documentation**: Use descriptions to capture important context

## Troubleshooting

### Common Issues
- **Date Format Errors**: Always use ISO-8601 format for dates
- **Invalid Status**: Only use pending, in-progress, or done
- **Missing Required Fields**: Ensure id, title, status, and priority are present
- **Duplicate IDs**: Each todo must have a unique UUID

### Data Recovery
- Backup files are created automatically before major operations
- Use `git` history to recover from accidental deletions
- Validate JSON structure after manual edits

## API Reference

### Core Functions
- `addTodo(title, description, priority, tags)`
- `updateTodoStatus(id, status)`
- `updateTodoPriority(id, priority)`
- `deleteTodo(id)`
- `searchTodos(query, filters)`
- `filterTodos(criteria)`
- `exportTodos(format, filters)`

### Utility Functions
- `validateTodoData()`
- `backupTodos(filename)`
- `restoreTodos(filename)`
- `generateReport(type, filters)`
- `cleanupCompletedTodos(olderThan)`
