<div
  class="min-h-screen w-full relative z-0 bg-white text-slate-900 dark:bg-slate-900 dark:text-slate-100 transition-colors"
>
  <!-- Dashed Gradient Background -->
  <div
    class="absolute inset-0 -z-10"
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
