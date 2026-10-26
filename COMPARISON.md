# A comparison run: Claude Code on its own

This repository is one half of a comparison, made on 26 October 2026 for croftweaver.com. The same
brief for a fictional business was given to Claude Code twice: once on its own, once with
Croftweaver's skills. The other half: https://github.com/karero/compare-claude-code-croftweaver.

**The business is fictional.** Fernwood Technical Translation, Jo Fernwood and the contact details
(jo@example.com, +1 555 0142) are invented for the comparison.

## How this run was made

- Claude Code 2.1.308, model claude-opus-5-5, in a fresh, empty Claude Code configuration with no
  user instructions loaded (checked by a dry start before the run).
- The working folder held only `BRIEF.md`. First and only prompt: "Build the website described in BRIEF.md. Its address will be https://compare-cc-alone.pages.dev."
- The harness, the same for both runs, is `HARNESS-run.sh`: `claude -p` in permission mode
  `acceptEdits`, the same allowed commands, and publishing commands (`gh`, `wrangler`,
  `git push`) blocked. The run asked no questions.
- The run ended when the assistant said the site was done; `npm run build` succeeded.
- The run made no git repository; the experimenter's first commit records its files unchanged.
- `TRANSCRIPT.md` is the run's full transcript in plain text (tool results cut to 1,500
  characters; local paths replaced with labels).

## What the experimenter added, and nothing else

- A commit adding an `X-Robots-Tag: noindex` header, so a fictional business is not indexed. Both
  sites carry it.
- This file, `TRANSCRIPT.md`, `HARNESS-run.sh`.
- The site was deployed by the experimenter, the same way for both runs: `wrangler pages deploy` of
  the build output. It is at https://compare-cc-alone.pages.dev.

## Results

Measured with neutral tools (PageSpeed Insights, Google's Rich Results Test, the W3C Nu HTML
Checker), side by side on https://croftweaver.com/compare once complete. One run each is an
anecdote, not a measurement.
