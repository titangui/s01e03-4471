<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import notes from '#lib/data/desk-notes.json';
  import { causeOf, uniqueById, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  let { ticket, issues }: { ticket: number; issues: { parser: string; hint: string; oneDay: string } } = $props();

  const merged = $derived(uniqueById(reports as Report[]).filter((r) => r.mergedInto === ticket));
  // One-day moves are read from the report text (desk-notes.json), so they leave `parser`.
  const rows = $derived.by(() => {
    const n = { parser: 0, hint: 0, oneDay: 0 };
    for (const r of merged) {
      if (notes.oneDayMove.includes(r.id)) n.oneDay++;
      else if (causeOf(r, tenantOf(r)) === 'hint') n.hint++;
      else n.parser++;
    }
    return [
      { name: 'Parser reads dates month first', n: n.parser, href: issues.parser },
      { name: 'booking-v3 form hint says MM/DD/YYYY', n: n.hint, href: issues.hint },
      { name: 'Date moves by one day (likely time zones)', n: n.oneDay, href: issues.oneDay },
    ];
  });
</script>

<table>
  <thead><tr><th>problem</th><th>reports</th><th>issue</th></tr></thead>
  <tbody>
    {#each rows as r (r.name)}
      <tr><td>{r.name}</td><td>{r.n}</td><td><a href={r.href}>{r.href.split('/').pop() === '' ? r.href : '#' + r.href.split('/').pop()}</a></td></tr>
    {/each}
  </tbody>
</table>
<p>{rows.reduce((s, r) => s + r.n, 0)} of {merged.length} reports placed.</p>
