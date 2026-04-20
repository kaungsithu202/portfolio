<script lang="ts">
  import { onDestroy } from "svelte";
  import { GithubIcon, LucideLinkedin, Mail, Copy, Check } from "@lucide/svelte";

  const CONTACT_EMAIL = "kaungsithu1998202@gmail.com";
  const GITHUB_URL = "https://github.com/kaungsithu202";
  const LINKEDIN_URL = "https://www.linkedin.com/in/kaung-si-thu-7079ba23b/";

  let copied = false;
  let resetTimer: ReturnType<typeof setTimeout> | undefined;

  async function copyEmail() {
    try {
      await navigator.clipboard.writeText(CONTACT_EMAIL);
      copied = true;

      if (resetTimer) clearTimeout(resetTimer);
      resetTimer = setTimeout(() => {
        copied = false;
      }, 1800);
    } catch {
      copied = false;
    }
  }

  onDestroy(() => {
    if (resetTimer) clearTimeout(resetTimer);
  });
</script>

<div class="contact-layout">
  <div class="contact-copy">
    <div class="content-stack">
      <p class="contact-lead">The fastest path is direct email.</p>
      <p class="contact-body">
        For recruiter outreach, send the role, company, or a short brief. If
        email is inconvenient, LinkedIn works too.
      </p>
    </div>

    <div class="contact-guidance">
      <span class="section-kicker">Best first message</span>
      <p>
        Share the role, team, and timing. I can reply with fit,
        availability, and relevant examples.
      </p>
    </div>
  </div>

  <div class:copied class="surface-panel contact-card">
    <div class="contact-primary">
      <span class="section-kicker">Email</span>
      <a href={`mailto:${CONTACT_EMAIL}`} class="contact-email">{CONTACT_EMAIL}</a>
      <p class="contact-note">
        Use the button first. If your device does not open an email app, copy
        the address instead.
      </p>
    </div>

    <div class="contact-actions">
      <a href={`mailto:${CONTACT_EMAIL}`} class="contact-primary-action">
        <Mail class="size-4" />
        Email Kaung
      </a>

      <button type="button" class:copied class="contact-secondary-action" on:click={copyEmail}>
        {#if copied}
          <Check class="size-4" />
          Email copied
        {:else}
          <Copy class="size-4" />
          Copy email
        {/if}
      </button>
    </div>

    <div class="contact-feedback-shell" aria-live="polite">
      <p class:visible={copied} class="contact-feedback">
        Copied. Paste it into an email or LinkedIn message.
      </p>
    </div>

    <div class="contact-links">
      <a href={LINKEDIN_URL} target="_blank" rel="noopener noreferrer" class="contact-link">
        <div>
          <span class="contact-link-label">LinkedIn</span>
          <span class="contact-link-value">Professional profile</span>
        </div>
        <span class="contact-link-icon">
          <LucideLinkedin />
        </span>
      </a>

      <a href={GITHUB_URL} target="_blank" rel="noopener noreferrer" class="contact-link">
        <div>
          <span class="contact-link-label">GitHub</span>
          <span class="contact-link-value">Code and recent work</span>
        </div>
        <span class="contact-link-icon">
          <GithubIcon />
        </span>
      </a>
    </div>
  </div>
</div>

<style>
  .contact-layout {
    display: grid;
    gap: clamp(1.5rem, 4vw, 2.25rem);
  }

  .contact-copy {
    display: flex;
    flex-direction: column;
    gap: var(--space-lg);
  }

  .contact-lead {
    max-width: 18ch;
    font-family: var(--font-display);
    font-size: clamp(1.55rem, 3vw, 2.1rem);
    font-weight: var(--weight-bold);
    line-height: 1.05;
    letter-spacing: -0.05em;
  }

  .contact-body,
  .contact-guidance p,
  .contact-note {
    max-width: 38rem;
    font-size: var(--text-body);
    line-height: var(--lh-body);
    color: var(--muted);
  }

  .contact-guidance {
    display: grid;
    gap: 0.75rem;
    padding-top: var(--space-sm);
    border-top: 1px solid color-mix(in oklch, var(--line) 72%, var(--accent-warm) 28%);
  }

  .contact-card {
    display: flex;
    flex-direction: column;
    gap: var(--space-lg);
    padding: clamp(1.2rem, 3vw, 1.75rem);
    border-color: color-mix(in oklch, var(--line) 68%, var(--accent) 32%);
    background: color-mix(in oklch, var(--surface) 90%, var(--accent-soft) 10%);
    transition:
      transform 420ms var(--ease-out-quint),
      border-color 220ms var(--ease-out-quint),
      box-shadow 420ms var(--ease-out-quint);
  }

  .contact-card.copied {
    border-color: color-mix(in oklch, var(--accent-cool) 58%, var(--line-strong) 42%);
    animation: contact-flash 420ms var(--ease-out-expo);
  }

  .contact-primary {
    display: grid;
    gap: 0.8rem;
  }

  .contact-email {
    max-width: 100%;
    font-family: var(--font-body);
    font-size: clamp(1.05rem, 1.8vw, 1.3rem);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-snug);
    letter-spacing: -0.02em;
    color: color-mix(in oklch, var(--text) 82%, var(--accent) 18%);
    overflow-wrap: anywhere;
  }

  .contact-actions {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
  }

  .contact-primary-action,
  .contact-secondary-action {
    display: inline-flex;
    min-height: 2.7rem;
    align-items: center;
    gap: 0.55rem;
    border-radius: 999px;
    padding: 0 0.95rem;
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: var(--tracking-label);
    text-transform: uppercase;
    transition:
      border-color 180ms ease,
      background-color 180ms ease,
      transform 180ms ease,
      opacity 180ms ease;
    will-change: transform;
  }

  .contact-primary-action {
    background: var(--accent);
    color: var(--accent-contrast);
  }

  .contact-secondary-action {
    border: 1px solid color-mix(in oklch, var(--line) 64%, var(--accent-cool) 36%);
    background: color-mix(in oklch, var(--surface) 86%, var(--accent-cool-soft) 14%);
    color: color-mix(in oklch, var(--text) 82%, var(--accent-cool) 18%);
  }

  .contact-secondary-action.copied {
    background: color-mix(in oklch, var(--accent-cool) 76%, var(--accent) 24%);
    color: var(--accent-contrast);
  }

  .contact-primary-action:hover,
  .contact-secondary-action:hover,
  .contact-link:hover {
    transform: translateY(-1px) scale(1.015);
  }

  .contact-primary-action:hover {
    background: color-mix(in oklch, var(--accent) 84%, var(--accent-warm) 16%);
  }

  .contact-secondary-action:hover {
    border-color: color-mix(in oklch, var(--accent-cool) 58%, var(--line-strong) 42%);
    background: color-mix(in oklch, var(--surface) 76%, var(--accent-cool-soft) 24%);
  }

  .contact-primary-action:active,
  .contact-secondary-action:active {
    transform: translateY(0) scale(0.985);
  }

  .contact-links {
    display: flex;
    flex-direction: column;
  }

  .contact-feedback-shell {
    min-height: 1.35rem;
  }

  .contact-feedback {
    display: inline-flex;
    align-items: center;
    border-radius: 999px;
    background: color-mix(in oklch, var(--accent-cool-soft) 72%, var(--surface) 28%);
    padding: 0.35rem 0.7rem;
    font-size: var(--text-meta);
    font-weight: var(--weight-medium);
    line-height: 1.35;
    color: color-mix(in oklch, var(--accent-cool) 68%, var(--text) 32%);
    opacity: 0;
    transform: translateY(0.25rem) scale(0.985);
    transition:
      opacity 180ms ease,
      transform 220ms var(--ease-out-quint);
    pointer-events: none;
  }

  .contact-feedback.visible {
    opacity: 1;
    transform: translateY(0) scale(1);
  }

  .contact-link {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
    padding-block: 0.85rem;
    border-top: 1px solid color-mix(in oklch, var(--line) 74%, var(--accent-cool) 26%);
    transition:
      transform 180ms ease,
      border-color 180ms ease;
  }

  .contact-link:hover {
    border-top-color: color-mix(in oklch, var(--accent-cool) 56%, var(--line-strong) 44%);
  }

  .contact-link:last-child {
    border-bottom: 1px solid color-mix(in oklch, var(--line) 74%, var(--accent-cool) 26%);
  }

  .contact-link-label {
    display: block;
    margin-bottom: 0.35rem;
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: var(--tracking-label-wide);
    text-transform: uppercase;
    color: color-mix(in oklch, var(--accent) 70%, var(--text) 30%);
  }

  .contact-link-value {
    font-size: var(--text-body);
    font-weight: var(--weight-medium);
    line-height: 1.45;
  }

  .contact-link-icon {
    display: inline-flex;
    flex-shrink: 0;
    color: color-mix(in oklch, var(--accent-cool) 62%, var(--text) 38%);
    transition: transform 220ms var(--ease-out-quint);
  }

  .contact-link:hover .contact-link-icon {
    transform: translateX(3px);
  }

  @keyframes contact-flash {
    0% {
      transform: translateY(0) scale(1);
    }
    50% {
      transform: translateY(-2px) scale(1.01);
    }
    100% {
      transform: translateY(0) scale(1);
    }
  }

  @media (min-width: 64rem) {
    .contact-layout {
      grid-template-columns: minmax(0, 0.82fr) minmax(0, 1fr);
      align-items: start;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .contact-card,
    .contact-primary-action,
    .contact-secondary-action,
    .contact-link,
    .contact-link-icon,
    .contact-feedback {
      transition: none;
    }

    .contact-card.copied {
      animation: none;
    }

    .contact-primary-action:hover,
    .contact-secondary-action:hover,
    .contact-link:hover {
      transform: none;
    }
  }
</style>
