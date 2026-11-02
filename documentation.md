Team Organizer — Documentation
Capacity-based sprint planning for Jira Cloud.

What the app does
Sprint planning usually starts from nominal hours: five people × ten days × eight hours = 400 hours. In reality that 400 loses leave, public holidays, meetings, unplanned support work and the rework that comes back from testing. What is actually plannable is often half.
Team Organizer makes that gap visible, plans your Jira work against what is left, and writes the finished plan back to Jira.

Installation
Install the app from the Atlassian Marketplace.
Open any Jira project and look for Team Organizer under Apps in the left sidebar. It is also available from the top Apps menu.
The app needs these permissions:
Permission
Why
Storage
Keeps your team, plans and actual hours inside your own Atlassian cloud
Read Jira work
Reads issues, projects, saved filters and worklogs
Read Jira user
Reads assignable users so you can add them to the team
Write Jira work
Only used by Apply plan to Jira
Jira Software (board, sprint)
Reads sprints and adds planned items to them
The app requests the Jira permissions listed above. Access to Jira resources is governed by Atlassian's authorization model and the permissions applicable to each request. Persisted planning data is stored in Atlassian Forge storage. The current implementation does not make external network calls.

Getting started
1. Add your projects
Open the settings icon in the top bar, then Get projects from Jira. Pick the Jira projects you plan for. Each one becomes a project in the app with its own plans and backlog.
2. Add your team
Open the people icon, then Get people from Jira. The list shows users who can be assigned work in the project.
For each person set:
Kind — Developer or Tester
Level — Junior, Mid or Senior
Dedication % — what share of their working time goes to this project. Someone at 0% produces no capacity in that project's plans.
Support % — the share of their time that goes to unplanned support work
Bug % — the fix allowance stacked on top of development hours. On a 10-hour job, 20% reserves 2 more hours. For a tester the retest % applies instead.
Meetings — hours per person; leave it empty to use the template default
Jira has no equivalent for these fields, so they live only in the app.
3. Pick a sprint
The Sprint selector in the top bar lists your Jira sprints. Choosing one creates a plan for it. The period name and dates come from the sprint and cannot be edited in the app.
If the selector says there is no sprint, create one on your Jira board first, then press the refresh button next to the selector.
4. Enter leave and holidays
In the period bar, open Leave and holidays. Click a cell to cycle it: empty → full day leave → half day → empty. The top row is the public holiday row and affects the whole team. Weekends are already excluded.
5. Bring in the work
Press Get items from Jira. There are four sources:
JQL — write a query; results come with key, summary, assignee and estimate
Sprint — everything in the sprint the plan is linked to
Saved filter — your favourite Jira filters
Paste — from Excel or a Jira export
Subtasks are never imported. See Known limitations below for why.
6. Plan
Write effort straight into a person's column, in junior hours. Within one item the developers' effort runs in parallel; the tester's effort starts when development is done.
Tick items in the Take column, or press Fill automatically to take them in priority order without pushing anyone above the target band. The red line marks where capacity runs out.
Open Planning results at the bottom for capacity ribbons, the weekly split, the schedule, the chain simulation and the action list.
7. Write the plan back to Jira
Press Apply plan to Jira. Every change is previewed row by row before anything is written.
One person on an item → assignee and original estimate go straight onto the issue
Several people on an item → the issue carries only the title, and a subtask is created for each person with their hour estimate
Estimates are written in hours. Parent items are added to the linked sprint; subtasks inherit their parent's sprint.
Running it again only writes what changed. If a person's effort is removed, the subtask is reported but never deleted — that decision stays with you.
8. After the sprint
On the Actuals & history page, enter what really happened, or press Get worklog from Jira to import it.
The worklog is read-only. Hours you type in the app are never written back to Jira, so teams that do not track time in Jira can still use the analysis.
Mark finished periods as Closed. Their averages feed the calibration suggestions, which re-tune the bug, support and meeting allowances from your own history.

How capacity is calculated
For each person:
contracted      = working days × daily hours
usable          = available days × (daily hours − unplanned loss) × dedication
plannable       = usable − meetings − support − rework allowance
Identity check:
contracted = leave + unplanned loss + other projects + meetings
           + support + rework allowance + plannable
The effort you write into the backlog competes only with plannable.
Effort baseline. Effort is written in junior hours. If you set level factors below 1, a mid or senior does the same work in less time. Leave all three at 1 if you do not want this behaviour; the column header shows the factor whenever it is not 1.

Languages
The interface follows each user's Jira language. English and Turkish are supported; you can also switch manually from the top bar. Numbers, dates and percentages follow the selected language.

Known limitations
Please read these before you roll the app out to a team.
No role-based permissions. Plan data is shared per installation, not per user. Anyone who can open the app page can edit the plan. If you need to restrict it, use Jira project permissions.
Subtasks are not imported. A multi-person item is written back to Jira as subtasks, and Jira does not allow a subtask under a subtask. Imports therefore filter subtasks out and report how many were skipped.
One assignee per issue. Jira issues have a single assignee. That is why multi-person items become subtasks rather than being squeezed into one issue.
Pasted keys are not verified. If you paste an issue key from Excel, the app cannot tell whether it is a subtask. Assigning several people to it and applying the plan will be rejected by Jira, and the row will show the error.
Time tracking must be enabled. Hour estimates are written to the original estimate field. If time tracking is disabled in your Jira project, those writes will fail and the preview result will say so.

Data and privacy
The app stores:
Team member names and their Jira account IDs
Period plans, backlog items, effort figures and actual hours
Jira issue keys and summaries for the items you imported
All of it lives in Atlassian's own Forge storage, inside your installation. The app makes no external network calls and sends nothing to third parties. When the app is uninstalled, its Forge storage is handled under Atlassian's Forge app data lifecycle and deletion procedures.
Full statement: see the privacy policy linked from the Marketplace listing.

Support
Questions, bug reports and feature requests: emredelice100@gmail.com
When reporting a problem, please include:
What you were doing and what you expected
The Jira project key and sprint name
Any message the app showed, copied exactly
