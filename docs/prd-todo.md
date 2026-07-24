# Product Requirements Document (PRD) - TODO App Upgrade

## 1. Overview

Upgrade the basic TODO app with due dates, priorities, and date-based filters so users can organize tasks and identify time-sensitive work. The MVP must remain simple and teachable, use local storage, and require no backend changes.

---

## 2. MVP Scope

- Preserve the existing task title and completion status.
- Require a non-empty `title` for every task.
- Add an optional `dueDate` field in ISO `YYYY-MM-DD` format.
- Ignore invalid `dueDate` values and treat them as absent.
- Add a `priority` field with the allowed values `P1`, `P2`, and `P3`.
- Default `priority` to `P3` when no priority is provided.
- Add three date filter views: **All**, **Today**, and **Overdue**.
- Show completed and incomplete tasks in the **All** view.
- Show only incomplete tasks due on the current date in the **Today** view.
- Show only incomplete tasks with a due date before the current date in the **Overdue** view.
- Keep task storage local to the application, with no backend or external storage changes.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks so they stand out, such as with red styling.
- Sort tasks using the following precedence:
  1. Overdue tasks first.
  2. Priority from `P1` to `P3`.
  3. Due date in ascending order.
  4. Tasks without a due date last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user functionality.
- Keyboard navigation and additional specialized accessibility features.
- Backend changes.
- External or remote storage.