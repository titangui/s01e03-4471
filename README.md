# s01e03-4471

Ticket #4471 merged 412 date reports as one known issue. It holds three problems. One issue each:

1. [#1](../../issues/1) parser reads dates month first: 374 reports
2. [#2](../../issues/2) booking-v3 date hint says MM/DD/YYYY: 33 reports
3. [#3](../../issues/3) dates move by one day, likely time zones: 5 reports

- `kb/routes/kb/incidents/4471-split/+page.svx`: the page, for the support kb
- `kb/lib/kb/SplitCounts.svelte`: the component that computes the counts
- `4471-split.rendered.html`: the page as the desk will see it
