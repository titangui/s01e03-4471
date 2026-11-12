# s01e03-4471

Ticket #4471 merged 412 date reports as one known issue. It holds two problems. One issue each:

1. [#1](../../issues/1) parser reads dates month first: 379 reports (5 of them read as a one-day move, footnoted)
2. [#2](../../issues/2) booking-v3 date hint says MM/DD/YYYY: 33 reports

- `kb/routes/kb/incidents/4471-split/+page.svx`: the page, for the support kb
- `4471-split.rendered.html`: the page as the desk will see it
