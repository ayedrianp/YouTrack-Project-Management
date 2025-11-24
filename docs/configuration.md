# Configuration Guide
>YouTrack already comes with a good amount of preconfigs for projects with their templates.
If you need something more sepecific you can always add and change what you need.
The documentation is pretty expansive so you can find almost anything.

## Project Setup

### Creating Projects (Examples)

1. **Homelab Infrastructure**
   - Workflow: Backlog → In Progress → Testing → Done
   - Issue Types: Feature, Improvement, Infrastructure

2. **Maintenance & Operations**
   - Workflow: Scheduled → In Progress → Resolved
   - Issue Types: Maintenance, Update, Configuration

3. **Incidents & Problems**
   - Workflow: New → Investigating → Resolving → Closed
   - Issue Types: Incident, Bug, Problem

4. **Personal Tasks**
   - Workflow: Todo → Doing → Done
   - Issue Types: Task, Reminder, Idea

## Custom Fields

### Priority Levels
- Show Stopper
- Critical
- Major
- Normal
- Minor

### Environment
- Production
- Testing
- Development

### Categories
- Hardware
- Software
- Network
- Security
- General

## Agile Boards

### Kanban Board (Daily Tasks)
- Continuous flow for maintenance and todos
- No sprints
- Quick capture and completion

### Sprint Board (Projects)
- 2-week sprint cycles
- Planning and retrospectives

## Automation Rules (In Progress)



## Backup Configuration

See [backup script](../scripts/backup.sh) for automated backup setup.
