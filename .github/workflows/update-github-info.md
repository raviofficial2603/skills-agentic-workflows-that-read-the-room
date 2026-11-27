---
name: update-github-info
description: Propose concise, source-backed updates to the GitHub Info page for Mona's review.
intent: Keep the GitHub Info page current with practical, source-backed guidance for developers.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - github
    - awesome-copilot.github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md`. Use the notes as
the editorial guidance and the current page as context; preserve its practical
focus and avoid repeating topics already covered.

Use `web-fetch` to read all three:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Select only recent, useful items from these sources that help developers learn
GitHub faster. Use the Awesome Copilot workflows page to identify practical
workflow examples or skills worth highlighting.
Update `site/content/github-info.md` with concise, practical guidance supported
by those sources. Include direct source links for claims or updates drawn from
the Blog, Changelog, or Awesome Copilot workflows page. Do not invent details,
make unrelated edits, or replace the page with a general news roundup.

If any source cannot be fetched, or the notes or target page are unavailable,
do not guess or create a pull request; report that the update could not be
completed. If there are no relevant new items or the page needs no change, call
`noop` with a brief reason.

When the page changes, open a pull request for Mona to review. Use the
configured `create-pull-request` safe output to include only
`site/content/github-info.md`. Summarize the changes and cite the source URLs in
the PR body. Never write directly to the default branch.
