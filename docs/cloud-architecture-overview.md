# Cloud Architecture Overview

The TODO application is a monorepo with a React browser client and an Express API. The API stores task data in an in-memory SQLite database provided by `better-sqlite3`.

```mermaid
flowchart LR
    user["Task user"]

    subgraph system["TODO application monorepo"]
        frontend["React frontend<br/>packages/frontend"]
        api["Express API<br/>packages/backend"]
        store[("In-memory SQLite<br/>better-sqlite3")]
    end

    user -->|"Uses in a browser"| frontend
    frontend -->|"HTTP JSON via /api/tasks"| api
    api -->|"SQL reads and writes"| store
```

## Context Notes

- The frontend uses the development proxy to send `/api/tasks` requests to the Express API.
- The Express API owns task validation and CRUD operations.
- The SQLite database runs in memory inside the backend process, so its data is not durable across process restarts.
- The current implementation does not use an external database or cloud-managed service.

## Create a TODO Sequence

```mermaid
sequenceDiagram
    actor user as User
    participant form as React TaskForm
    participant app as React App
    participant list as React TaskList
    participant api as Express API
    participant store as In-memory SQLite

    user->>form: Enter task details and submit
    form->>form: Validate non-empty title
    form->>app: Call onSave with task data
    app->>api: POST /api/tasks with JSON
    api->>api: Validate title
    api->>store: INSERT task
    store-->>api: Return new task ID
    api->>store: SELECT created task
    store-->>api: Return created task
    api-->>app: 201 Created with task JSON
    app->>app: Increment refresh key
    app->>list: Remount task list
    list->>api: GET /api/tasks
    api->>store: SELECT tasks
    store-->>api: Return tasks
    api-->>list: 200 OK with task JSON
    list-->>user: Display updated task list
```