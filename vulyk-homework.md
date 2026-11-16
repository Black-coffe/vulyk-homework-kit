# Level 2: one small task through VULYK

Install VULYK on your real project, run one small task through it and write in the chat what the council said.
GREEN counts as an answer too.

## Before you start

- Claude Code 2.x, a git repository, `bash` (on Windows: Git Bash).
- A project you work on, not a toy. On a project below about 20,000 lines of code VULYK is overkill by its own
  README; plain Claude Code is enough there.
- Pick a small task: one feature or one bug fix that touches a few files. The task in the video (`task.md`) took
  about six hours; yours should take far less. The size of the task does not matter for the homework, the
  council verdict does.
- Work on a branch. VULYK commits its stories itself.

## Steps

1. Install (from the folder next to your project, VULYK 0.53.0 or newer):

   ```sh
   git clone https://github.com/Black-coffe/vulyk ../vulyk
   ../vulyk/install.sh .
   ```

2. Start Claude Code in the project and run `/vulyk-bootstrap`. It reads the project and asks a few questions in
   one batch (report language, release, wave budget, agent commits).
3. Run `/vulyk-plan "<your task>"`. It asks its questions, then writes a brief, a plan and stories. Each story has
   a `## Files` list: the files it may touch. Read them before you approve: this is the same list as in level 1,
   written by the planner.
4. Approve the plan and run `/vulyk-build`. The stories are built, then the council judges the change. A RED
   verdict cuts a repair story and the round runs again.
5. When the council is GREEN, look at the result yourself: run the feature, read the diff. `/vulyk-ship` merges
   it locally and prints the publish command; it pushes nothing by itself.

## What to send

Write in the chat of the video (or in the Telegram channel):

- the council verdict: `GREEN` or `RED`, and what it caught if it was RED;
- what the scope check reported: files outside the story lists, if any;
- one thing you would not have caught yourself, or "nothing".

## Safety

The video starts Claude Code with `--dangerously-skip-permissions` in an isolated clone with a separate profile.
That is not a sandbox. Do not run it like this on your own machine: start Claude Code normally and answer its
permission prompts.
