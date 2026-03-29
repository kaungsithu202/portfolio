<script lang="ts">
  import { Moon, Sun } from "@lucide/svelte";
  import { onMount } from "svelte";

  type Theme = "light" | "dark";
  const STORAGE_KEY = "theme";

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
  });
</script>

<button
  type="button"
  class="inline-flex cursor-pointer items-center gap-2 rounded-lg border border-slate-200 bg-white/80 px-3 py-2 text-slate-700 shadow-[0_10px_20px_-18px_rgba(15,23,42,0.8)] transition hover:border-cyan-300 hover:text-cyan-700 dark:border-slate-700 dark:bg-slate-900/70 dark:text-slate-200 dark:hover:border-cyan-700 dark:hover:text-cyan-300"
  aria-label="Toggle dark mode"
  aria-pressed={theme === "dark"}
  title="Toggle dark mode"
  on:click={() => apply(theme === "dark" ? "light" : "dark")}
>
  {#if theme === "dark"}
    <Sun size="16" />
    <span class="text-[10px] tracking-[0.14em] uppercase md:text-xs">Light</span>
  {:else}
    <Moon size="16" />
    <span class="text-[10px] tracking-[0.14em] uppercase md:text-xs">Dark</span>
  {/if}
</button>
