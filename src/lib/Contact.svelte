<script lang="ts">
  import { GithubIcon, LucideLinkedin, Mail, Send } from "@lucide/svelte";

  const CONTACT_EMAIL = "kaungsithu1998202@gmail.com";
  const GITHUB_URL = "https://github.com/kaungsithu202";
  const LINKEDIN_URL = "https://www.linkedin.com/in/kaung-si-thu-7079ba23b/";

  let name = "";
  let email = "";
  let message = "";

  function handleSubmit() {
    const trimmedMessage = message.trim();
    if (!trimmedMessage) return;

    const subject = `Portfolio contact${name.trim() ? ` — ${name.trim()}` : ""}`;
    const body = [
      `Name: ${name.trim() || "-"}`,
      `Email: ${email.trim() || "-"}`,
      "",
      trimmedMessage,
    ].join("\n");

    const mailto = `mailto:${CONTACT_EMAIL}?subject=${encodeURIComponent(
      subject,
    )}&body=${encodeURIComponent(body)}`;

    window.location.href = mailto;
  }
</script>

<div class="mt-4 grid grid-cols-1 gap-3 lg:grid-cols-2">
  <div
    class="rounded-2xl border border-slate-200/80 bg-white/75 p-4 backdrop-blur transition-colors dark:border-slate-700/70 dark:bg-slate-900/50"
  >
    <h3 class="text-sm font-semibold tracking-[0.12em] uppercase md:text-base">
      Let's connect
    </h3>
    <p class="mt-2 text-[10px] leading-5 text-slate-700 md:text-xs dark:text-slate-300">
      Have a project, a role, or just want to say hi? Send a message and I'll
      get back to you.
    </p>

    <div class="mt-4 flex flex-col gap-2">
      <a
        href={`mailto:${CONTACT_EMAIL}`}
        class="inline-flex items-center gap-2 rounded-lg border border-slate-200 bg-white/80 px-3 py-2 text-[10px] transition hover:border-cyan-300 hover:text-cyan-700 md:text-xs dark:border-slate-700 dark:bg-slate-950/50 dark:hover:border-cyan-700 dark:hover:text-cyan-300"
      >
        <Mail class="size-3 md:size-4" />
        {CONTACT_EMAIL}
      </a>

      <a
        href={LINKEDIN_URL}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 rounded-lg border border-slate-200 bg-white/80 px-3 py-2 text-[10px] transition hover:border-cyan-300 hover:text-cyan-700 md:text-xs dark:border-slate-700 dark:bg-slate-950/50 dark:hover:border-cyan-700 dark:hover:text-cyan-300"
      >
        <LucideLinkedin class="size-3 md:size-4" />
        LinkedIn
      </a>

      <a
        href={GITHUB_URL}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 rounded-lg border border-slate-200 bg-white/80 px-3 py-2 text-[10px] transition hover:border-cyan-300 hover:text-cyan-700 md:text-xs dark:border-slate-700 dark:bg-slate-950/50 dark:hover:border-cyan-700 dark:hover:text-cyan-300"
      >
        <GithubIcon class="size-3 md:size-4" />
        GitHub
      </a>
    </div>
  </div>

  <form
    class="rounded-2xl border border-slate-200/80 bg-white/75 p-4 backdrop-blur transition-colors dark:border-slate-700/70 dark:bg-slate-900/50"
    on:submit|preventDefault={handleSubmit}
  >
    <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
      <div>
        <label
          class="mb-1 block text-[10px] tracking-[0.12em] text-slate-700 uppercase md:text-xs dark:text-slate-300"
          for="name"
          >Name</label
        >
        <input
          id="name"
          class="w-full rounded-lg border border-slate-200 bg-white px-3 py-2 text-[10px] focus:ring-2 focus:ring-cyan-200 focus:outline-none md:text-xs dark:border-slate-700 dark:bg-slate-950 dark:focus:ring-cyan-900"
          autocomplete="name"
          placeholder="Your name"
          bind:value={name}
        />
      </div>

      <div>
        <label
          class="mb-1 block text-[10px] tracking-[0.12em] text-slate-700 uppercase md:text-xs dark:text-slate-300"
          for="email"
          >Email</label
        >
        <input
          id="email"
          type="email"
          required
          class="w-full rounded-lg border border-slate-200 bg-white px-3 py-2 text-[10px] focus:ring-2 focus:ring-cyan-200 focus:outline-none md:text-xs dark:border-slate-700 dark:bg-slate-950 dark:focus:ring-cyan-900"
          autocomplete="email"
          placeholder="you@example.com"
          bind:value={email}
        />
      </div>
    </div>

    <div class="mt-3">
      <label
        class="mb-1 block text-[10px] tracking-[0.12em] text-slate-700 uppercase md:text-xs dark:text-slate-300"
        for="msg"
        >Message</label
      >
      <textarea
        id="msg"
        required
        rows="5"
        class="w-full resize-none rounded-lg border border-slate-200 bg-white px-3 py-2 text-[10px] focus:ring-2 focus:ring-cyan-200 focus:outline-none md:text-xs dark:border-slate-700 dark:bg-slate-950 dark:focus:ring-cyan-900"
        placeholder="Tell me a bit about what you're working on..."
        bind:value={message}
      ></textarea>
    </div>

    <div class="flex items-center justify-between mt-3 gap-3">
      <p class="text-[10px] md:text-xs text-slate-500 dark:text-slate-400">
        Submitting opens your email app.
      </p>

      <button
        type="submit"
        class="inline-flex items-center gap-2 rounded-lg bg-cyan-700 px-3 py-2 text-[10px] text-white transition hover:bg-cyan-600 md:text-xs dark:bg-cyan-500 dark:text-slate-950 dark:hover:bg-cyan-400"
      >
        <Send class="size-3 md:size-4" />
        Send
      </button>
    </div>
  </form>
</div>
