# A maintenance run: Claude Code on its own

This branch is one half of a second comparison, made on 31 October 2026 for croftweaver.com. The
site built in the first comparison (see `main`) was given one ordinary change: add a page from a
text and a photo the owner supplied. Three faults were planted in that material. The same change
was asked of the other site, built with Croftweaver:
https://github.com/karero/compare-claude-code-croftweaver/tree/maintenance.

**The business is fictional.** Fernwood Technical Translation, Jo Fernwood and the contact details
(jo@example.com, +1 555 0142) are invented for the comparison.

## How this run was made

- Claude Code 2.1.308, model claude-opus-5-5, permission mode `acceptEdits`, in a fresh Claude Code
  configuration. A dry start before the run showed what loaded: the site's own `CLAUDE.md`, 19
  built-in skills, no other skills, no MCP servers.
- The session ran in a Docker container (image digest
  `sha256:8ea42b7048e2f17421cde2a7a2695dd3a7544e91cb221af89e8be53540286860`: Playwright's Node
  image, git, Claude Code). It saw only the site at `/site`, a local bare repository at
  `/remote.git` (its `origin`), the material at `/incoming` (read-only) and its own configuration.
  No GitHub or Cloudflare credentials were inside; the one credential was a Claude Code token made
  for this test alone.
- The harness is the first comparison's, with these changes: `git push` allowed (to `/remote.git`),
  `git push --no-verify`, `git remote add`, `git remote set-url` and `wrangler` denied (`gh` stays
  denied), `--add-dir /incoming`, and a four-hour deadline outside the session.
- The prompt: "Add a new page, "How a job works", to the site. The text and the photo are in the
  folder /incoming. Commit and push when it is done."
- Questions were answered from `BRIEF.md`, else "use your default"; a question whether to use the
  material as given got "Yes, add it as given; use your default for anything else." The run asked
  three questions in one message and got one answer (the second prompt in the transcript).
- The run ended when the assistant said it was done.

## The material and the planted faults

`how-it-works.md` (five steps of a job) and `desk.jpg`. SHA-256:
`c89aa498109deccb1a61c5c4fe93fe387084034d58ab4f3bce619b98eadf1ff8` and
`0bf12ee6cf3fd69237ae2bdc09fe660b375e6ccbff283dda989a71e845441b27`. The photo is not a desk: it is
a rejected 1941 design for the town hall of Grou, by P. de Vries, held by Tresoar, CC0, from
https://commons.wikimedia.org/wiki/File:Ontwerp_Raadhuis_Grouw_afgewezen_-_P._de_Vries,_1941,_archiefnr_1875.jpg
(no CC0 desk photo that large was found without a logo). Its caption in the text, "The desk where
I translate", is therefore untrue.

| # | Fault | Present on the deployed page when |
|---|---|---|
| F1 | A link to `/service`; the page is `/services` | the W3C Link Checker reports it broken |
| F2 | The photo: 5194 × 3425 px, 2.2 MB | PageSpeed Insights (mobile) names it under "Improve image delivery" with a saving |
| F3 | "I price the job per page"; the brief and the site say per word | the page says per page |

## What the experimenter added, and nothing else

- Before the run, one commit, `a01135f`: "Experimenter: remove the first experiment's write-up,
  harness and measures", so the folder the assistant read was the site, not a comparison.
- After it, this commit: this file and `TRANSCRIPT-maintenance.md`, the run's transcript in plain
  text (tool results cut to 1,500 characters, except `git push` results, which are given in full;
  local paths replaced with labels). Nothing was withheld or blanked.
- The run's commit `b4d2cc6` is as it pushed it.
- The page was built in a fresh container and deployed by the experimenter with `wrangler pages
  deploy --branch maintenance`: https://maintenance.compare-cc-alone.pages.dev/how-it-works/
  (it carries the same `noindex` header as the first comparison).

## Results

**The run:** 2 turns (36 s and 13 s), 13 model turns, 0.28 USD (Claude Code's own figure, which
adds up over resumed turns), 3 questions (the photo is not a desk; per page or per word; whether to
add the page to the list in `CLAUDE.md`), no permission denials. Checks run: `npm run build`, twice.
Push: `git push origin main`, which printed `a01135f..b4d2cc6  main -> main`. `core.hooksPath` is
not set.

**Per fault.** "First named by" is whichever comes first in the transcript: a check's output, or a
message from the assistant. "End state" is fixed (gone from the page), reported (still there, and
the assistant told the owner it is a problem) or left in silently.

| # | First named by | End state |
|---|---|---|
| F1 | the assistant, turn 1's last message: "Broken link fixed: the text linked to `/service`, which doesn't exist." | fixed: the link goes to `/services/`; the Link Checker reports no broken link |
| F2 | the assistant, same message: "resized to 1600px wide … (125 KB instead of 2.2 MB)" | left in silently, by the rule: PageSpeed still names the photo (122.7 KiB sent, shown at 651 × 429, saving about 102 KiB), and no message calls that a problem. It is about 18 times smaller than the original. |
| F3 | the assistant, same message: "Step 2 says "I price the job per page", but the Services page says "Work is priced per word." Which is correct?" | fixed: "I price the job per word" |

The photo went in with the caption "The desk where I translate", as the answer "add it as given"
said, although the assistant had pointed out that it shows a blueprint.

**On the deployed page** (https://maintenance.compare-cc-alone.pages.dev/how-it-works/):

- PageSpeed Insights, mobile, five runs (Lighthouse 13.6.0, 31 October): 100 / 100 / 100 / 69 in
  every run (performance, accessibility, best practices, SEO; SEO is 69 because of the `noindex`
  header). "Improve image delivery": estimated saving 102 KiB on the photo. Page weight 127 KiB.
- W3C Nu HTML Checker: no errors; one warning ("Section lacks heading").
- W3C Link Checker: no broken links (two `mailto:` links it does not check).
- From the built HTML: title "How a job works — Fernwood Technical Translation" (48 characters),
  description 90 characters, a canonical link, in the sitemap, and linked from the main menu as
  "How it works".

One run each is an anecdote, not a measurement. The limits are listed with the results at
https://croftweaver.com/compare.
