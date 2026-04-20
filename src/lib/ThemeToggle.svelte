<script lang="ts">
  import { Moon, Sun } from "@lucide/svelte";
  import { onMount } from "svelte";
  import { fade, scale } from "svelte/transition";

  type Theme = "light" | "dark";
  const STORAGE_KEY = "theme";
  let prefersReducedMotion =
    typeof window !== "undefined"
      ? window.matchMedia("(prefers-reduced-motion: reduce)").matches
      : false;

  let theme: Theme =
    typeof document !== "undefined" &&
    document.documentElement.classList.contains("dark")
      ? "dark"
      : "light";

  function apply(next: Theme) {
    theme = next;
    const isDark = next === "dark";
    document.documentElement.classList.toggle("dark", isDark);
    document.documentElement.style.colorScheme = next;
    try {
      localStorage.setItem(STORAGE_KEY, next);
    } catch (e) {}
  }

  function getInitialTheme(): Theme {
    let stored: string | null = null;
    try {
      stored = localStorage.getItem(STORAGE_KEY);
    } catch (e) {}
    if (stored === "dark" || stored === "light") return stored;

    return window.matchMedia?.("(prefers-color-scheme: dark)")?.matches
      ? "dark"
      : "light";
  }

  onMount(() => {
    apply(getInitialTheme());

    const media = window.matchMedia("(prefers-reduced-motion: reduce)");
    const update = () => {
      prefersReducedMotion = media.matches;
    };

    update();
    media.addEventListener("change", update);

    return () => {
      media.removeEventListener("change", update);
    };
  });
</script>

<button
  type="button"
  class="theme-toggle"
  aria-label={theme === "dark" ? "Switch to light theme" : "Switch to dark theme"}
  aria-pressed={theme === "dark"}
  title={theme === "dark" ? "Switch to light theme" : "Switch to dark theme"}
  on:click={() => apply(theme === "dark" ? "light" : "dark")}
>
  {#key theme}
    <span
      in:scale={{ duration: prefersReducedMotion ? 0 : 180, start: 0.84 }}
      out:fade={{ duration: prefersReducedMotion ? 0 : 120 }}
      class="theme-toggle-state"
    >
      {#if theme === "dark"}
        <span class="theme-toggle-icon">
          <Sun size="16" />
        </span>
        <span class="theme-toggle-label">Light</span>
      {:else}
        <span class="theme-toggle-icon">
          <Moon size="16" />
        </span>
        <span class="theme-toggle-label">Dark</span>
      {/if}
    </span>
  {/key}
</button>

<style>
  .theme-toggle {
    display: inline-flex;
    min-height: 2.75rem;
    align-items: center;
    gap: 0.6rem;
    align-self: flex-start;
    cursor: pointer;
    border: 1px solid color-mix(in oklch, var(--line) 68%, var(--accent-cool) 32%);
    border-radius: 999px;
    background: color-mix(in oklch, var(--surface) 84%, var(--accent-cool-soft) 16%);
    overflow: hidden;
    padding: 0.75rem 1rem;
    color: var(--text);
    transition:
      border-color 180ms ease,
      background-color 180ms ease,
      transform 180ms ease;
  }

  .theme-toggle-state {
    display: inline-flex;
    align-items: center;
    gap: 0.6rem;
  }

  .theme-toggle-label {
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: 0.14em;
    text-transform: uppercase;
  }

  .theme-toggle-icon {
    color: color-mix(in oklch, var(--accent-cool) 62%, var(--text) 38%);
    transition: transform 220ms var(--ease-out-quint);
  }

  .theme-toggle:hover {
    border-color: color-mix(in oklch, var(--accent-cool) 58%, var(--line-strong) 42%);
    background: color-mix(in oklch, var(--surface) 74%, var(--accent-cool-soft) 26%);
    transform: translateY(-1px) scale(1.015);
  }

  .theme-toggle:hover .theme-toggle-icon {
    transform: rotate(-12deg);
  }

  .theme-toggle:active {
    transform: translateY(0) scale(0.985);
  }

  @media (prefers-reduced-motion: reduce) {
    .theme-toggle,
    .theme-toggle-icon {
      transition: none;
    }

    .theme-toggle:hover {
      transform: none;
    }
  }
</style>
