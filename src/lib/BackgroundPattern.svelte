<div class="background-shell">
  <div class="background-glow"></div>
  <div class="background-grid"></div>
  <slot></slot>
</div>

<style>
  .background-shell {
    position: relative;
    z-index: 0;
    min-height: 100vh;
    width: 100%;
    overflow: hidden;
    background: var(--bg);
    color: var(--text);
    transition: background-color 180ms ease, color 180ms ease;
  }

  .background-glow {
    position: absolute;
    inset: 0;
    z-index: -2;
    pointer-events: none;
    background:
      radial-gradient(circle at 14% 10%, var(--accent-glow), transparent 30%),
      radial-gradient(circle at 86% 16%, var(--accent-glow-soft), transparent 24%),
      radial-gradient(circle at 72% 72%, var(--accent-glow-warm), transparent 22%);
  }

  .background-grid {
    position: absolute;
    inset: 0;
    z-index: -1;
    pointer-events: none;
    opacity: 0.82;
    background-image:
      linear-gradient(to right, var(--pattern-line) 1px, transparent 1px),
      linear-gradient(to bottom, var(--pattern-line) 1px, transparent 1px);
    background-size: 32px 32px;
    mask-image: linear-gradient(to bottom, black 10%, black 55%, transparent 100%);
    -webkit-mask-image:
      linear-gradient(to bottom, black 10%, black 55%, transparent 100%);
  }
</style>
