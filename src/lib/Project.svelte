<script>
  import { Globe } from "@lucide/svelte";

  let {
    label = "Project",
    image,
    imagePosition = "center",
    name,
    description,
    role,
    focus,
    outcome,
    techStacks,
    link,
  } = $props();
</script>

<article class="project-entry">
  <div class="project-media">
    <img
      src={image}
      alt={`Preview of ${name}`}
      class="project-image"
      style:object-position={imagePosition}
      width="1600"
      height="900"
      loading="lazy"
      decoding="async"
    />
  </div>

  <div class="project-copy">
    <div class="project-header">
      <div class="project-title-block">
        <p class="project-label">{label}</p>
        <h3>{name}</h3>
      </div>

      <a
        href={link}
        target="_blank"
        rel="noopener noreferrer"
        class="project-link"
        aria-label={`Visit ${name}`}
      >
        <Globe size="14" /> Visit site
      </a>
    </div>

    <p class="project-description">{description}</p>

    <dl class="project-facts">
      <div>
        <dt>Role</dt>
        <dd>{role}</dd>
      </div>
      <div>
        <dt>Focus</dt>
        <dd>{focus}</dd>
      </div>
      <div>
        <dt>Result</dt>
        <dd>{outcome}</dd>
      </div>
    </dl>

    <div class="project-tech-line">
      <span class="project-tech-label">Stack</span>
      <div class="project-tech">
        {#each techStacks as tech (tech)}
          <span>{tech}</span>
        {/each}
      </div>
    </div>
  </div>
</article>

<style>
  .project-entry {
    display: grid;
    gap: clamp(1.25rem, 3vw, 2rem);
    padding-block: clamp(1.5rem, 3vw, 2rem);
    container-type: inline-size;
  }

  .project-media {
    max-width: 30rem;
    justify-self: start;
    overflow: hidden;
    border: 1px solid color-mix(in oklch, var(--line) 68%, var(--accent-cool) 32%);
    border-radius: 1.5rem;
    background: color-mix(in oklch, var(--surface) 90%, var(--accent-cool-soft) 10%);
    box-shadow: var(--shadow-sm);
    transition:
      transform 420ms var(--ease-out-quint),
      box-shadow 420ms var(--ease-out-quint),
      border-color 260ms var(--ease-out-quint);
    will-change: transform;
  }

  .project-image {
    width: 100%;
    aspect-ratio: 16 / 9;
    object-fit: cover;
    transition: transform 500ms cubic-bezier(0.22, 1, 0.36, 1);
  }

  .project-entry:hover .project-image {
    transform: scale(1.03);
  }

  .project-entry:hover .project-media {
    transform: translateY(-4px);
    border-color: color-mix(in oklch, var(--accent-cool) 56%, var(--line-strong) 44%);
  }

  .project-copy {
    display: flex;
    flex-direction: column;
    gap: 0.85rem;
    align-self: center;
  }

  .project-header {
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    justify-content: space-between;
    gap: var(--space-sm);
  }

  .project-title-block {
    display: flex;
    flex-direction: column;
    gap: 0.45rem;
  }

  .project-label {
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: var(--tracking-label-wide);
    text-transform: uppercase;
    color: color-mix(in oklch, var(--accent) 72%, var(--text) 28%);
  }

  .project-title-block h3 {
    font-size: var(--text-title);
    font-weight: var(--weight-bold);
    line-height: 1.08;
    letter-spacing: -0.03em;
  }

  .project-description {
    max-width: 62ch;
    font-size: var(--text-body);
    line-height: 1.68;
    color: var(--muted);
  }

  .project-facts {
    display: grid;
    gap: 0.9rem;
  }

  .project-facts div {
    display: grid;
    gap: 0.25rem;
    padding-top: 0.9rem;
    border-top: 1px solid color-mix(in oklch, var(--line) 74%, var(--accent-cool) 26%);
    transition:
      transform 260ms var(--ease-out-quint),
      border-color 260ms var(--ease-out-quint);
    will-change: transform;
  }

  .project-facts div:nth-child(2) {
    transition-delay: 40ms;
  }

  .project-facts div:nth-child(3) {
    transition-delay: 80ms;
  }

  .project-entry:hover .project-facts div {
    transform: translateX(0.35rem);
    border-top-color: color-mix(in oklch, var(--accent-cool) 56%, var(--line-strong) 44%);
  }

  .project-facts dt,
  .project-tech-label {
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: var(--tracking-label);
    text-transform: uppercase;
    color: color-mix(in oklch, var(--accent-cool) 62%, var(--text) 38%);
  }

  .project-tech-label {
    color: color-mix(in oklch, var(--accent-warm) 68%, var(--text) 32%);
  }

  .project-facts dd {
    margin: 0;
    font-size: var(--text-body);
    line-height: 1.6;
  }

  .project-tech-line {
    display: grid;
    gap: 0.6rem;
  }

  .project-tech {
    display: flex;
    flex-wrap: wrap;
    gap: 0.7rem 1rem;
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: 1.5;
    letter-spacing: var(--tracking-label);
    text-transform: uppercase;
    color: color-mix(in oklch, var(--muted) 70%, var(--accent) 30%);
  }

  .project-tech span {
    white-space: nowrap;
  }

  .project-link {
    display: inline-flex;
    min-height: 2.6rem;
    align-items: center;
    gap: 0.5rem;
    border: 1px solid color-mix(in oklch, var(--line) 62%, var(--accent) 38%);
    border-radius: 999px;
    background: color-mix(in oklch, var(--surface) 84%, var(--accent-soft) 16%);
    padding: 0 0.95rem;
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: var(--tracking-label);
    text-transform: uppercase;
    transition:
      border-color 180ms ease,
      background-color 180ms ease,
      transform 180ms ease;
    will-change: transform;
  }

  .project-link:hover {
    border-color: color-mix(in oklch, var(--accent) 62%, var(--line-strong) 38%);
    background: color-mix(in oklch, var(--surface) 74%, var(--accent-soft) 26%);
    transform: translateY(-1px) scale(1.015);
  }

  .project-link:active {
    transform: translateY(0) scale(0.985);
  }

  @container (min-width: 48rem) {
    .project-entry {
      grid-template-columns: minmax(12rem, 0.62fr) minmax(0, 1.38fr);
      align-items: start;
    }

    .project-media {
      max-width: 21rem;
    }

    .project-facts {
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 0.85rem 1.1rem;
    }

    .project-facts div {
      padding-top: 0.8rem;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .project-media,
    .project-image,
    .project-facts div,
    .project-link {
      transition: none;
    }

    .project-entry:hover .project-media,
    .project-entry:hover .project-facts div,
    .project-link:hover {
      transform: none;
    }
  }
</style>
