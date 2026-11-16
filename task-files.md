# File list of the task

The yardstick for "files outside the task". It was written before the run by reading the solidtime code, with no
trial run, and it was not shown to the agent. A scope check reads the `## Files` block (lines `- path`) and
compares it with the diff of the run against the starting commit.

How to read it: paths are from the root of the solidtime clone. Under each path, one indented line says why the
task needs it (the scope check reads only lines that start with `- `). A glob `*` also matches across `/`. The
"new files" lines are names with the words of the task itself (`Timesheet`, `approv`, `submi`, `Closed`) and
migrations dated after the starting commit. A new file with another name counts as outside the list.

Write your own list the same way for your next task: level 1 of the homework.

## Files

- app/Models/TimeEntry.php
  a time entry: link to the submitted week, no edits in a submitted week or a closed period
- app/Models/Member.php
  an organisation member: their weeks waiting for approval
- app/Models/Organization.php
  the organisation: the closed period date, link to the weeks
- app/Http/Controllers/Api/V1/TimeEntryController.php
  create, update, delete entries (blocked in a week or period); index, aggregate and their export: approved only
- app/Http/Requests/V1/TimeEntry/*
  validation of entries and report filters (approval status)
- app/Http/Resources/V1/TimeEntry/*
  API response for an entry: week status
- app/Http/Controllers/Api/V1/UserTimeEntryController.php
  an employee's own entries (`/users/me/time-entries`): week status
- app/Service/TimeEntryFilter.php
  the shared filter of entry queries: approved only
- app/Service/TimeEntryAggregationService.php
  aggregates of the Reporting pages and charts: approved hours only
- app/Service/TimeEntryService.php
  the entry service
- app/Service/PermissionStore.php
  role permissions: submit your own week, approve, close a period
- resources/js/utils/permissions.ts
  the same permissions on the UI side
- app/Http/Controllers/Api/V1/ReportController.php
  saved reports
- app/Http/Controllers/Api/V1/Public/ReportController.php
  reports opened by link (shared)
- app/Service/ReportService.php
  building the data of a saved report
- app/Service/Dto/ReportPropertiesDto.php
  properties of a saved report (filters)
- app/Service/ReportExport/*
  CSV, XLSX, ODS export
- resources/views/reports/*
  PDF and spreadsheet export templates
- app/Mail/*
  the new email to the employee about a rejected week
- resources/views/emails/*
  the template of that email
- routes/api.php
  routes to submit, approve, reject a week and to close a period
- openapi.json
  the API description: new endpoints are documented like the existing ones
- resources/js/packages/api/src/openapi.json.client.ts
  the UI API client, generated from the description
- resources/js/ziggy.js
  routes for the UI, generated
- resources/js/ziggy.d.ts
  types of these routes
- resources/js/types/models.ts
  UI model types (`model:typer`)
- resources/js/Pages/Timesheet.vue
  the Timesheet page: submit a week, status, rejection comment
- resources/js/Pages/Time.vue
  the Time page: week status of own entries
- resources/js/Pages/Reporting.vue
  the Reporting page
- resources/js/Pages/ReportingDetailed.vue
  the Detailed report page
- resources/js/Pages/SharedReport.vue
  a report opened by link
- resources/js/Components/Common/Reporting/*
  Reporting export and summary
- resources/js/packages/ui/src/TimeEntry/*
  entry rows and editing: no edits in a submitted week
- resources/js/Layouts/AppLayout.vue
  the menu item of the week approval page
- lang/en/exceptions.php
  API error texts (week submitted, period closed, cannot approve your own week)
- app/Exceptions/Api/*
  new API exceptions for the same errors
- database/factories/TimeEntryFactory.php
  the entry factory for tests
- tests/Unit/Endpoint/Api/V1/TimeEntryEndpointTest.php
  entry endpoint tests: the blocks and the approved-only selection
- tests/Unit/Endpoint/Api/V1/ReportEndpointTest.php
  saved report tests
- tests/Unit/Endpoint/Api/V1/Public/PublicReportEndpointTest.php
  shared report tests
- tests/Unit/Service/TimeEntryAggregationServiceTest.php
  aggregate tests
- tests/Unit/Service/TimeEntryFilterTest.php
  filter tests
- tests/Unit/Service/PermissionStoreTest.php
  role permission tests
- *[Tt]imesheet*
  new files and the Timesheet UI (existing: `resources/js/Components/Timesheet/`, `resources/js/utils/timesheet/`, `useTimesheet*`, `e2e/timesheet*`)
- *[Aa]pprov*
  new files: model, controller, requests, resources, policy, email, page, factory, approval tests
- *[Ss]ubmi*
  new files for submitting a week
- *[Cc]losed*
  new files for the closed period
- database/migrations/2026_11_0[4-9]_*
  new migrations (the last existing one is `2026_11_03_000001`)
- database/migrations/2026_11_[1-3]*
  new migrations
- database/migrations/2026_12_*
  new migrations
- database/migrations/2027_*
  new migrations

## Allowed new

New files the task may create. They are already in `## Files` above (the scope check reads only that block);
here they are for a human reader:

- migrations dated after `2026_11_03`: the table of weeks waiting for approval, the closed period date of the
  organisation;
- models, controllers, requests, resources, exceptions, policies, emails, factories and tests with `Timesheet`,
  `approv`, `submi` or `Closed` in the name;
- Vue pages and components with the same words in the name;
- new exceptions in `app/Exceptions/Api/` and a new email in `app/Mail/` with its template in
  `resources/views/emails/`, under any name.
