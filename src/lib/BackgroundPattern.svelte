<div
  class="relative z-0 min-h-screen w-full overflow-hidden bg-slate-50 text-slate-900 transition-colors dark:bg-slate-950 dark:text-slate-100"
>
  <div
    class="pointer-events-none absolute -top-24 -left-16 -z-10 h-80 w-80 rounded-full bg-cyan-300/35 blur-3xl dark:bg-cyan-500/20"
  ></div>
  <div
    class="pointer-events-none absolute -right-20 top-40 -z-10 h-96 w-96 rounded-full bg-amber-300/30 blur-3xl dark:bg-amber-500/20"
  ></div>

  <div
    class="absolute inset-0 -z-10 opacity-70"
    style="
      background-image:
        linear-gradient(to right, var(--pattern-line) 1px, transparent 1px),
        linear-gradient(to bottom, var(--pattern-line) 1px, transparent 1px);
      background-size: 20px 20px;
      background-position: 0 0, 0 0;
      mask-image:
        repeating-linear-gradient(
          to right,
          black 0px,
          black 3px,
          transparent 3px,
          transparent 8px
        ),
        repeating-linear-gradient(
          to bottom,
          black 0px,
          black 3px,
          transparent 3px,
          transparent 8px
        );
      -webkit-mask-image:
        repeating-linear-gradient(
          to right,
          black 0px,
          black 3px,
          transparent 3px,
          transparent 8px
        ),
        repeating-linear-gradient(
          to bottom,
          black 0px,
          black 3px,
          transparent 3px,
          transparent 8px
        );
      mask-composite: intersect;
      -webkit-mask-composite: source-in;
    "
  ></div>

  <slot></slot>
</div>
