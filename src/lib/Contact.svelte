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

<div class="grid grid-cols-1 lg:grid-cols-2 gap-3 mt-3">
  <div
    class="border border-gray-200 dark:border-slate-700 rounded-md p-3 bg-white/50 dark:bg-slate-900/40 transition-colors"
  >
    <h3 class="text-sm md:text-base font-semibold">Let’s connect</h3>
    <p class="text-[10px] md:text-xs text-slate-700 dark:text-slate-300 mt-1.5">
      Have a project, a role, or just want to say hi? Send a message and I’ll
      get back to you.
    </p>

    <div class="flex flex-col gap-2 mt-3">
      <a
        href={`mailto:${CONTACT_EMAIL}`}
        class="inline-flex items-center gap-2 border border-gray-200 dark:border-slate-700 rounded-md px-3 py-2 text-[10px] md:text-xs hover:bg-gray-100 dark:hover:bg-slate-800 transition-colors"
      >
        <Mail class="size-3 md:size-4" />
        {CONTACT_EMAIL}
      </a>

      <a
        href={LINKEDIN_URL}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 border border-gray-200 dark:border-slate-700 rounded-md px-3 py-2 text-[10px] md:text-xs hover:bg-gray-100 dark:hover:bg-slate-800 transition-colors"
      >
        <LucideLinkedin class="size-3 md:size-4" />
        LinkedIn
      </a>

      <a
        href={GITHUB_URL}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 border border-gray-200 dark:border-slate-700 rounded-md px-3 py-2 text-[10px] md:text-xs hover:bg-gray-100 dark:hover:bg-slate-800 transition-colors"
      >
        <GithubIcon class="size-3 md:size-4" />
        GitHub
      </a>
    </div>
  </div>

  <form
    class="border border-gray-200 dark:border-slate-700 rounded-md p-3 bg-white/50 dark:bg-slate-900/40 transition-colors"
    on:submit|preventDefault={handleSubmit}
  >
    <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
      <div>
        <label
          class="block text-[10px] md:text-xs text-slate-700 dark:text-slate-300 mb-1"
          for="name"
          >Name</label
        >
        <input
          id="name"
          class="w-full border border-gray-200 dark:border-slate-700 bg-white dark:bg-slate-950 rounded-md px-3 py-2 text-[10px] md:text-xs focus:outline-none focus:ring-2 focus:ring-gray-300 dark:focus:ring-slate-700 transition-colors"
          autocomplete="name"
          placeholder="Your name"
          bind:value={name}
        />
      </div>

      <div>
        <label
          class="block text-[10px] md:text-xs text-slate-700 dark:text-slate-300 mb-1"
          for="email"
          >Email</label
        >
        <input
          id="email"
          type="email"
          required
          class="w-full border border-gray-200 dark:border-slate-700 bg-white dark:bg-slate-950 rounded-md px-3 py-2 text-[10px] md:text-xs focus:outline-none focus:ring-2 focus:ring-gray-300 dark:focus:ring-slate-700 transition-colors"
          autocomplete="email"
          placeholder="you@example.com"
          bind:value={email}
        />
      </div>
    </div>

    <div class="mt-3">
      <label
        class="block text-[10px] md:text-xs text-slate-700 dark:text-slate-300 mb-1"
        for="msg"
        >Message</label
      >
      <textarea
        id="msg"
        required
        rows="5"
        class="w-full border border-gray-200 dark:border-slate-700 bg-white dark:bg-slate-950 rounded-md px-3 py-2 text-[10px] md:text-xs focus:outline-none focus:ring-2 focus:ring-gray-300 dark:focus:ring-slate-700 resize-none transition-colors"
        placeholder="Tell me a bit about what you’re working on…"
        bind:value={message}
      ></textarea>
    </div>

    <div class="flex items-center justify-between mt-3 gap-3">
      <p class="text-[10px] md:text-xs text-slate-500 dark:text-slate-400">
        Submitting opens your email app.
      </p>

      <button
        type="submit"
        class="inline-flex items-center gap-2 bg-gray-900 dark:bg-slate-200 text-white dark:text-slate-900 rounded-md px-3 py-2 text-[10px] md:text-xs hover:bg-gray-800 dark:hover:bg-white transition-colors"
      >
        <Send class="size-3 md:size-4" />
        Send
      </button>
    </div>
  </form>
</div>
