<script>
  let { name, level } = $props();
</script>

<article class="education-entry">
  <p class="education-name">{name}</p>
  <p class="education-level">{level}</p>
</article>

<style>
  .education-entry {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    padding-block: clamp(1.25rem, 3vw, 1.75rem);
  }

  .education-name {
    font-size: 1.0625rem;
    font-weight: var(--weight-semibold);
    line-height: 1.4;
    letter-spacing: 0.03em;
  }

  .education-level {
    font-size: var(--text-label);
    line-height: 1.6;
    letter-spacing: var(--tracking-label);
    text-transform: uppercase;
    color: color-mix(in oklch, var(--accent-warm) 66%, var(--text) 34%);
  }

  @media (min-width: 48rem) {
    .education-entry {
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      gap: 1.5rem;
    }
  }
</style>
