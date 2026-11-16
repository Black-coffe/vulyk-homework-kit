# The task

This is the task from the video, word for word. It was pasted into Claude Code as the argument of `/vulyk-plan`.
Nothing was added or removed during the run; the agent got clarifications only as answers to its own questions.
The wording is a product one: what users need, with no hint which files to touch. The file list of the task
(`task-files.md`) was not shown to the agent: it is the yardstick, not a hint.

Project: solidtime (https://github.com/solidtime-io/solidtime), an open-source time tracker on Laravel and Vue,
licence AGPL-3.0.

```text
Add timesheet approval to solidtime.

Today every tracked hour goes straight into reports and exports. Teams that bill clients or run payroll from solidtime need a manager to sign off on each person's week first, and need finished months to stay unchanged.

How it should work:

1. Submit a week. An employee submits their own week for approval from the Timesheet page. A week follows the week start the user already has in their profile. After submitting, the employee can no longer create, edit or delete their time entries in that week.

2. Approve or reject. Owners, admins and managers see the weeks submitted in their organization, with each person's hours per day. They approve a week, or reject it with a comment. Nobody can approve or reject their own week. Employees cannot approve or reject any week.

3. Fix and resubmit. A rejected week becomes editable again. The employee gets an email with the manager's comment, sees the comment on the Timesheet page, fixes the entries and submits the week again.

4. Close a period. An owner or admin closes the period up to a date, for example the end of last month. After that, nobody, including owners, can create, edit or delete time entries on or before that date. Weeks in a closed period that were never approved stay out of reports.

5. Only approved hours count. The Reporting pages, saved and shared reports, and report exports (CSV, Excel, ODS, PDF) include only time entries from approved weeks. The Time and Timesheet pages still show all of a person's own entries, with the status of each week: not submitted, submitted, approved, rejected.

6. Same rules in the API. Everything above works through the existing public API (/api/v1) as well as in the UI, and new endpoints are documented the same way as the existing ones.

Keep the existing behaviour for everything else. The existing test suite must stay green, and the new behaviour must be covered by tests.
```
