# SaaS Platform Direction

The current static app is a client-side workflow mapper. The product direction is a hosted SaaS platform where users log in and manage workflows, knowledge base entries, and connected operational data in the cloud.

## Target Product Shape

Users should eventually access:

- Their organisation workspace.
- Workflow maps and journey layers.
- Knowledge base entries linked to nodes, gaps, outcomes, and decisions.
- Model health and impact analysis across workflows.
- Version history and release review before changes go live.
- Shared ownership, comments, approvals, and permissions.

## Suggested Architecture

```text
client/
  index.html
  styles/
  src/

server/
  api/
    auth
    workspaces
    workflows
    nodes
    kb-entries
    validation
    audit-log

database/
  organisations
  users
  workspaces
  workflows
  workflow_versions
  nodes
  connections
  kb_entries
  gap_register
  comments
  audit_events

storage/
  attachments
  exports
  imports
```

## Migration Path

1. Keep the static app working on GitHub Pages.
2. Split frontend files so releases are easier to review.
3. Define the `.kbwf` schema formally.
4. Add a hosted API that can save and load workflows by logged-in user.
5. Replace local file save/load with cloud workspace save/load.
6. Add workflow versioning, approvals, and audit events.
7. Add knowledge base entries linked to graph nodes.
8. Add organisation-level permissions and sharing.

## Important Design Decision

The frontend should not permanently own the source of truth. It can still export `.kbwf` files, but the SaaS platform should treat the cloud database as the main source of truth, with `.kbwf` as an import/export format.
