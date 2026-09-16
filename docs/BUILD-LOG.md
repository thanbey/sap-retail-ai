# How I keep the build log

The build log has three layers. Each one feeds the next, and the habit that
matters is the first.

## 1. Capture as you go (raw)

One scratch file per day: `docs/log/day-NN.md`. Add a line whenever something
happens worth remembering: a command that finally worked, a quota error, a
number from a notebook, a decision and the alternative rejected. Fragments and
timestamps, not prose. Keep the file open in a split pane all day.

Claude Code writes to it too: `/log <note>` appends a timestamped line to
today's file, so notes are written in the moment instead of reconstructed at
the end of the day.

## 2. Structure at the end of the day (curated)

Last 30 minutes, from the scratch file:

- `docs/DECISIONS.md`: real decisions only, dated, 3 to 5 lines each, with the
  alternative and why it lost.
- `README.md` status table: flip the day's row to done or partial, one-line note.
- Commit with a message that names the day: `day3: synthetic AIF error generator`.

`git log --stat` for the day is the honest record of what shipped versus what
was planned.

## 3. Publish (narrative)

Written from the curated layer, never from memory, the same day. In the blog
repo (`~/Dev/projects/blog`) run `/post NN`. It reads the work-plan entry,
`docs/log/day-NN.md`, `DECISIONS.md` and the day's git log, then drafts the
post in this shape: what I set out to do, what happened, the numbers, what I
decided and why, what is next. Edit for voice, keep the failures in, push.
Screenshots go in the blog's `src/assets/`; one per post is enough.

## Rules

- Real numbers every day, including bad ones. "F1 0.71, worse than expected,
  here is why" is worth more than any success story.
- Post the same day. By Day 4 you will not remember Day 2.
- 400 to 900 words. Code blocks only for things worth copying.
- A day that goes sideways is still a post: "what went wrong on Day 6".

## Daily rhythm

First 30 min: read yesterday's log and DECISIONS.md, create today's
`docs/log/day-NN.md` with the day's deliverable as the first line.
During: `/log` freely.
Last 30 min: curate, commit, `/post`.
