<script>
  let title = $state('');
  let issues = $state([
    { id: 1, title: 'Wi-Fi not working', status: 'Open' },
    { id: 2, title: 'Water supply problem', status: 'Open' }
  ]);
  let search = $state('');
  let statusFilter = $state('All');
  // @ts-ignore
  function addIssue(event) {
    event.preventDefault();

    if (!title.trim()) return;

    issues.push({
      id: Date.now(),
      title: title.trim(),
      status: 'Open'
    });

    title = '';
  }

  let filteredIssues = $derived(
          issues.filter(issue =>
                  issue.title.toLowerCase().includes(search.toLowerCase()) &&
                  (statusFilter === 'All' || issue.status === statusFilter)
          )
  );

  // @ts-ignore
  function resolveIssue(id) {
    const issue = issues.find(issue => issue.id === id);

    if (issue) {
      issue.status = 'Resolved';
    }
  }

  let totalIssues = $derived(issues.length);

  let openCount = $derived(
          issues.filter(issue => issue.status === 'Open').length
  );

  let resolvedCount = $derived(
          issues.filter(issue => issue.status === 'Resolved').length
  );

</script>
<main>
  <h1>CampusOS</h1>
  <p>Your campus, in one place.</p>

  <section class="stats">
    <article>
      <p>Total issues</p>
      <h2>{totalIssues}</h2>
    </article>

    <article>
      <p>Open issues</p>
      <h2>{openCount}</h2>
    </article>

    <article>
      <p>Resolved issues</p>
      <h2>{resolvedCount}</h2>
    </article>
  </section>

  <h2>Report a campus issue</h2>

  <form class="issue-form" onsubmit={addIssue}>
    <input
            bind:value={title}
            placeholder="Describe the issue"
    />
    <button type="submit">Add issue</button>
  </form>

  <h2>Campus issues</h2>

  <div class="issue-filters">
    <input
            bind:value={search}
            placeholder="Search campus issues..."
    />

    <select bind:value={statusFilter}>
      <option value="All">All issues</option>
      <option value="Open">Open issues</option>
      <option value="Resolved">Resolved issues</option>
    </select>
  </div>

  {#each filteredIssues as issue (issue.id)}
    <article>
      <h3>{issue.title}</h3>

      {#if issue.status === 'Open'}
        <p><span class="open-badge">Open</span></p>
        <button onclick={() => resolveIssue(issue.id)}>
          Mark resolved
        </button>
      {:else}
        <span class="resolved-badge">Resolved</span>
      {/if}
    </article>
  {:else}
    <p class="empty-state">No matching campus issues found.</p>
  {/each}

</main>

<style>

  :global(body) {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    background: #f4f6fb;
    color: #172033;
  }

  main {
    width: 100%;
    max-width: 1000px;
    box-sizing: border-box;
    margin: 0 auto;
    padding: 40px 24px;
  }

  h1 {
    font-size: 32px;
    margin-bottom: 8px;
  }

  h2 {
    margin-top: 32px;
    font-size: 20px;
  }

  article {
    background: white;
    border: 1px solid #e3e8f0;
    border-radius: 12px;
    padding: 16px;
    margin: 12px 0;
  }

  .stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    margin: 28px 0;
  }

  .stats article {
    margin: 0;
    padding: 20px;
  }

  .stats p {
    margin: 0;
    color: #64748b;
  }

  .stats h2 {
    margin: 10px 0 0;
    font-size: 28px;
  }

  @media (max-width: 600px) {
    .stats {
      grid-template-columns: 1fr;
    }
  }

  .open-badge {
    display: inline-block;
    padding: 5px 10px;
    border-radius: 999px;
    background: #fef3c7;
    color: #92400e;
    font-size: 13px;
    font-weight: 600;
  }

  .resolved-badge {
    display: inline-block;
    padding: 5px 10px;
    border-radius: 999px;
    background: #dcfce7;
    color: #166534;
    font-size: 13px;
    font-weight: 600;
  }

  article h3 {
    margin-top: 0;
    margin-bottom: 10px;
  }

  article p {
    margin: 0 0 14px;
  }

  button {
    cursor: pointer;
    border: none;
    border-radius: 7px;
    padding: 8px 12px;
    background: #2563eb;
    color: white;
    font-weight: 600;
  }

  button:hover {
    background: #1d4ed8;
  }

  input,
  select {
    box-sizing: border-box;
    padding: 10px 12px;
    border: 1px solid #dbe2ea;
    border-radius: 8px;
    background: white;
    color: #172033;
    font: inherit;
    font-size: 14px;
  }

  input:focus,
  select:focus {
    outline: 2px solid #93b4ff;
    outline-offset: 1px;
  }

  input::placeholder {
    color: #94a3b8;
  }

  .issue-form,
  .issue-filters {
    display: flex;
    align-items: center;
    gap: 10px;
    flex-wrap: wrap;
  }

  .issue-form input {
    width: min(320px, 100%);
  }

  .issue-filters input {
    width: min(320px, 100%);
  }

  .issue-filters select {
    min-width: 150px;
  }

  @media (max-width: 480px) {
    main {
      padding: 24px 16px;
    }

    .issue-form input,
    .issue-filters input,
    .issue-form button,
    .issue-filters select {
      width: 100%;
    }
  }

  .empty-state {
    padding: 24px;
    text-align: center;
    color: #64748b;
    background: white;
    border: 1px dashed #cbd5e1;
    border-radius: 12px;
  }
</style>