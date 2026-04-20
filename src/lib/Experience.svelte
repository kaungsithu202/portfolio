<script>
  import { ExternalLinkIcon } from "@lucide/svelte";

  let { company, position, timeline, link, image, summary = "" } = $props();
</script>

<article class="experience-entry">
  <div class="experience-main">
    <div class="experience-company">
      <img
        src={image}
        alt={`${company} logo`}
        class="experience-image"
        width="56"
        height="56"
        loading="lazy"
        decoding="async"
      />
      <div class="experience-copy">
        <h3>{company}</h3>
        <p>{position}</p>
        {#if summary}
          <p class="experience-summary">{summary}</p>
        {/if}
      </div>
    </div>

    <div class="experience-meta">
      <p class="experience-timeline">{timeline}</p>
      <a
        href={link}
        class="experience-link"
        target="_blank"
        rel="noopener noreferrer"
        aria-label={`Open ${company}`}
      >
        Company <ExternalLinkIcon class="size-3.5" />
      </a>
    </div>
  </div>
</article>

<style>
  .experience-entry {
    padding-block: clamp(1.5rem, 4vw, 2.25rem);
  }

  .experience-main {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
  }

  .experience-company {
    display: flex;
    align-items: flex-start;
    gap: 1rem;
  }

  .experience-image {
    width: 3.5rem;
    height: 3.5rem;
    flex-shrink: 0;
    border-radius: 1rem;
    border: 1px solid color-mix(in oklch, var(--line) 68%, var(--accent) 32%);
    object-fit: cover;
    background: color-mix(in oklch, var(--surface) 90%, var(--accent-soft) 10%);
  }

  .experience-copy {
    display: flex;
    flex-direction: column;
    gap: 0.35rem;
  }

  .experience-copy h3 {
    font-size: 1.0625rem;
    font-weight: var(--weight-bold);
    line-height: 1.25;
    letter-spacing: 0.04em;
    color: color-mix(in oklch, var(--text) 84%, var(--accent) 16%);
  }

  .experience-copy p {
    font-size: var(--text-body);
    line-height: var(--lh-body);
    color: var(--muted);
  }

  .experience-summary {
    max-width: 44ch;
    color: var(--text);
  }

  .experience-meta {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 0.9rem;
  }

  .experience-timeline {
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    letter-spacing: var(--tracking-label-wide);
    font-variant-numeric: tabular-nums;
    text-transform: uppercase;
    color: color-mix(in oklch, var(--accent-cool) 62%, var(--text) 38%);
  }

  .experience-link {
    display: inline-flex;
    min-height: 2.5rem;
    align-items: center;
    gap: 0.45rem;
    border: 1px solid color-mix(in oklch, var(--line) 62%, var(--accent) 38%);
    border-radius: 999px;
    background: color-mix(in oklch, var(--surface) 86%, var(--accent-soft) 14%);
    padding: 0 0.9rem;
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    letter-spacing: var(--tracking-label);
    text-transform: uppercase;
    transition:
      border-color 180ms ease,
      background-color 180ms ease,
      transform 180ms ease;
  }

  .experience-link:hover {
    border-color: color-mix(in oklch, var(--accent) 58%, var(--line-strong) 42%);
    background: color-mix(in oklch, var(--surface) 76%, var(--accent-soft) 24%);
    transform: translateY(-1px);
  }

  @media (min-width: 48rem) {
    .experience-main {
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      gap: 2rem;
    }

    .experience-meta {
      justify-content: flex-end;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .experience-link {
      transition: none;
    }

    .experience-link:hover {
      transform: none;
    }
  }
</style>
