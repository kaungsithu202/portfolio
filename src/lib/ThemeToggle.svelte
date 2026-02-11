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
  class="inline-flex items-center gap-2 border border-gray-200 dark:border-slate-700 bg-white/70 dark:bg-slate-900/50 rounded-md px-3 py-1.5 hover:bg-gray-100 dark:hover:bg-slate-800 cursor-pointer transition-colors"
  aria-label="Toggle dark mode"
  aria-pressed={theme === "dark"}
  title="Toggle dark mode"
  on:click={() => apply(theme === "dark" ? "light" : "dark")}
>
  {#if theme === "dark"}
    <Sun size="16" />
    <span class="text-[10px] md:text-xs">Light</span>
  {:else}
    <Moon size="16" />
    <span class="text-[10px] md:text-xs">Dark</span>
  {/if}
</button>
