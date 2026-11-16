# Checklist "the feature works"

Written before the run, from the text of `task.md`. It is run by hand after the agent said "done", on a database
reset to the demo data (`php artisan migrate:fresh --seed` inside the solidtime container). A point counts only if
the check passed exactly as written; "almost" does not count. The result is written as `k of 9` with the numbers
of the failed points.

The solidtime test suite is a separate line of the measurement, not a point of this checklist.

Demo users (organisation ACME Corp, password `password` for everyone):

| Who | Email | Role |
|---|---|---|
| Owner | `owner@acme.test` | owner |
| Admin | `admin@acme.test` | admin |
| Manager | `test@example.com` | manager |
| Employee | `max.mustermann@acme.test` | employee |

UI: `http://localhost:<port>`, English locale. API: `/api/v1`, a user token from Profile → API Tokens. Emails:
the local mail catcher of the solidtime dev setup (mailpit).

| # | What must work | How to check |
|---|---|---|
| 1 | An employee submits their own week | UI, Employee: Timesheet, current week, add 2 h on Monday, submit the week. The week status is submitted. |
| 2 | An employee cannot change a submitted week | API, Employee: `PUT /api/v1/organizations/{org}/time-entries/{id}` on an entry of the submitted week returns a 4xx error, the entry in the database is unchanged. In the UI the cells of that week cannot be edited. |
| 3 | A manager sees the week and approves it | UI, Manager: the list of submitted weeks of the organisation shows the Employee's week with hours per day; approve. The status is approved. |
| 4 | Reject with a comment, and the email | UI, Employee: submit the next week. UI, Manager: reject it with the comment `Missing project on Monday`. Mailpit: an email to the Employee with this comment. UI, Employee: the comment is visible on Timesheet, the week is editable again, submitting it again works. |
| 5 | Nobody approves their own week, an employee approves nobody's | API, Manager: submit your own week and try to approve it: 403. API, Employee: approve the Manager's week: 403. |
| 6 | A period gets closed | UI or API, Admin: close the period up to yesterday. API, Owner: creating an entry for the day before yesterday returns a 4xx error; changing and deleting an entry in the closed period returns a 4xx error. An entry for today is created. |
| 7 | Reports count only approved hours | UI, Owner: Reporting, a date range with the weeks of points 3 and 4 and the unsubmitted demo entries. The total equals the sum of the approved weeks (point 3), not of all entries. The detailed report shows the same entries. |
| 8 | Exports count only approved hours | UI, Owner: Reporting → Export to CSV and PDF for the same range. Rows and the total of hours are the same as in point 7. A saved report opened by its public link (shared report) shows the same total. |
| 9 | An employee sees all their own entries, with status | UI, Employee: the Time page shows both submitted and unsubmitted own entries; Timesheet shows the status of each week (not submitted, submitted, approved, rejected). |

Note on point 5: the task text does not name the status code. solidtime answers a refused business rule with 400,
so a 400 here is a judgement call, not a plain bug. Decide before the run which code you accept.
