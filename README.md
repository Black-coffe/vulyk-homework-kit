# VULYK homework kit

▶️ Video: https://youtu.be/ohvrMPViEYw

Homework for the video "Claude Code on a large project: a plan, waves and review by another model (VULYK)".
The video runs one real task on solidtime, an open-source time tracker of about 134,000 lines of code, through
VULYK: a plan with a file list, building in waves, a council review by another model, checks without a model and
a human check. The run was made on VULYK 0.51.0-dev.1, a local build; the install in the video is the public
release 0.53.0, and what the video shows works the same way in it.

## Homework in two levels

**Level 1, no install.** In your next task, write down the list of files the task may touch. When the agent is
done, give the finished diff to a different model for review. The prompt template is `review-prompt.md`.

**Level 2.** Install VULYK on your real project and run one small task through it. Write in the chat what the
council said: GREEN counts as an answer too.

## Level 1: step by step (about 15 minutes on top of your task)

1. Before the agent starts, write `## Files` for the task: every path it may create or change, one per line.
   `task-files.md` is the list from the video, for the solidtime task in `task.md`.
2. Let the agent do the task as usual: Claude Code, Cursor, anything.
3. Take the diff: `git diff <start-commit> > task.diff` (add `git diff --stat` if the diff is large).
4. Open a chat with a model of a different family than the one that wrote the code (code by Claude, review by
   GPT or Gemini, or the other way round). Paste `review-prompt.md` below its line, then your file list, the task
   text and the diff.
5. Read the verdict. Every file outside your list is either a real need you forgot or the agent wandering off.

**What you get:** a verdict `GREEN` or `RED`, a list of files outside the task with a reason for each, and
findings the authoring model did not report. A `GREEN` with no findings is a normal result.

## Level 2: VULYK on your project

VULYK is open source (MIT): https://github.com/Black-coffe/vulyk. It runs inside Claude Code.

```sh
git clone https://github.com/Black-coffe/vulyk ../vulyk
../vulyk/install.sh .
```

Then, inside Claude Code in your project: `/vulyk-bootstrap`, and `/vulyk-plan <your small task>`. Approve the
plan, let it build, and read what the council said. The README of VULYK says when it is overkill: on a
project below about 20,000 lines of code, plain Claude Code is enough.

**What you get:** a plan with a file list per story, the built change, the council verdict (`GREEN`, or `RED`
with a repair round) and the list of what to check yourself before release.

## Files

- `task.md`: the task from the video, word for word, as it was given to the agent.
- `checklist.md`: the nine-point "feature works" checklist, run by hand after the agent said "done".
- `task-files.md`: the file list of the task, the yardstick for "files outside the task".
- `review-prompt.md`: the prompt for a review by another model (level 1).
- `vulyk-homework.md`: level 2 in more detail.

All users, emails and organisations in the examples are solidtime demo data.
