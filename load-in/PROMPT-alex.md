# Prompt for Alex's Claude: QA the Load-In demo before 6:30 PM ET

You're picking up a working prototype called **Load-In** for a demo tonight, Fri Oct 23, at 6:30 PM ET. It's a class project by James and Alex. For the next few hours, your job is to find and fix anything that would break or embarrass the live demo. Take no bigger risks than that.

## Context

- **Product:** one shared page per show, where the act and the venue settle the stage plot, input list and backline instead of trading email replies. There are four v1 features. (1) The act's stage plot builds the input list. (2) A house check compares the plot against the venue's gear ("needs 26 inputs, house has 24"). (3) Questions are pinned to individual gear items. (4) A week board shows every show's status and what is still open. There's also a patch sheet for show day.
- **Code:** repo `jamesharkins/ide`, branch `load-in-demo`, folder `load-in/`. `index.html` is the whole app: Preact + htm 3.1.1 from unpkg, no build step. Read `load-in/README.md` first. It has the feature list and the 7-step demo script James will run.
- **Live page:** a claude.ai artifact owned by James's account (https://claude.ai/artifact/98WX4cniBnZeEpmNhYWAuB). You can't publish to it from this account. Don't try, and don't publish a copy unless Alex asks. James republishes it from your branch.
- **Data:** in the hosted page, the store uses the artifact's shared database (`await window.claude.use('db')`). Anywhere else, such as a local file, it falls back to an in-memory sample week built by `makeSeed()`. So you can test everything locally except syncing between two devices.

## Rules

- Branch `load-in-fixes` off `load-in-demo` and push only there. Never push to `load-in-demo` or `main`, and never force-push.
- Keep it to one file: no build step, no new libraries, no new CDN hosts. The hosted page only loads scripts from unpkg, cdnjs and jsDelivr, and fonts from Google Fonts.
- One fix per commit, each with a line saying what broke and how you checked it.
- Don't change the sample week's story, because the demo script depends on it:
  - 4 of 7 shows are locked.
  - Wed's show asks for 4 mixes; the house has 3.
  - Sat's show has an open question on the drum riser.
  - Velvet Cassette's saved plot is 26 inputs against 24 channels.
  - Switching the guitar to 1 mic and percussion to 2 mics brings it under 24.
- Be economical: no subagents or workflows, and only a few screenshots. Read code before running anything heavy.
- Hard stop at **5:00 PM ET**: push your branch and write the report, even if work is unfinished.

## Tasks, in order

1. **Run the demo script end to end** in a headless browser against the local file. Serve `load-in/` with a static server so unpkg loads. If unpkg is blocked, route it to `htm@3.1.1/preact/standalone.umd.js` from `npm pack htm@3.1.1`. Check at 1280px and 390px wide, in light and dark. Local mode is one tab, so play both roles with "See the act's page" and "Back to the venue view". Write down anything that breaks, looks wrong or reads wrong.
2. **Check the act page on a phone:**
   - dragging plot items by touch inside the horizontally scrolling plot
   - tapping items, and the item panel
   - editing a label, choosing a mix, and posting a question
3. **Review the store** (the `store` IIFE: `write`, `connect`, `reset`) and the `showStatus`, `houseCheck` and `diffItems` logic. Check these against the db contract:
   - one write at a time per document
   - `update` only on documents that already exist
   - snapshot handling
   - remote-change toasts, which should never fire on load or for this tab's own writes

   The contract's type definitions aren't in the repo, so flag anything you're unsure of rather than guessing. Fix real bugs only.
4. **Fix what you found, in this priority:**
   1. crash or blank page
   2. wrong numbers or status on the board or house check
   3. a broken step in the demo script
   4. sideways scrolling or clipped text on a phone
   5. copy
5. **Only if steps 1–4 come back clean,** add at most one small extra:
   - arrow keys nudge the selected plot item, or
   - the board row shows when the act last changed the advance.

## Report

Write `load-in/QA-REPORT.md` on your branch and paste it in chat. Cover:
- what you tested
- what you fixed, with commit hashes
- what you didn't fix and why
- anything James should know before 6:30, such as a demo step to skip or a known rough edge
