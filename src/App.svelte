<script lang="ts">
  import { onMount } from "svelte";
  import { Motion } from "svelte-motion";
  import BackgroundPattern from "./lib/BackgroundPattern.svelte";
  import Contact from "./lib/Contact.svelte";
  import Education from "./lib/Education.svelte";
  import Experience from "./lib/Experience.svelte";
  import IconCanvas from "./lib/icons/IconCanvas.svelte";
  import Project from "./lib/Project.svelte";
  import ThemeToggle from "./lib/ThemeToggle.svelte";

  let heroVisible = false;
  let aboutVisible = false;
  let experienceVisible = false;
  let projectsVisible = false;
  let educationVisible = false;
  let contactVisible = false;
  let prefersReducedMotion =
    typeof window !== "undefined"
      ? window.matchMedia("(prefers-reduced-motion: reduce)").matches
      : false;

  const EASE_OUT_EXPO = [0.16, 1, 0.3, 1];

  type MotionState = {
    opacity: number;
    x?: number;
    y?: number;
    scale?: number;
    rotate?: number;
  };

  type RevealOptions = {
    onChange: (visible: boolean) => void;
    threshold?: number;
    rootMargin?: string;
    once?: boolean;
  };

  function revealOnView(
    node: HTMLElement,
    {
      onChange,
      threshold = 0.16,
      rootMargin = "0px 0px -10% 0px",
      once = false,
    }: RevealOptions,
  ) {
    if (typeof IntersectionObserver === "undefined") {
      onChange(true);
      return;
    }

    const observer = new IntersectionObserver(
      ([entry]) => {
        onChange(entry.isIntersecting);
        if (once && entry.isIntersecting) {
          observer.unobserve(node);
        }
      },
      {
        threshold,
        rootMargin,
      },
    );

    observer.observe(node);

    return {
      destroy() {
        observer.disconnect();
      },
    };
  }

  function hiddenOffset(axis: "x" | "y" = "y", distance = 12): MotionState {
    if (prefersReducedMotion) return { opacity: 1, x: 0, y: 0, scale: 1, rotate: 0 };

    return axis === "x"
      ? { opacity: 0, x: distance, y: 0 }
      : { opacity: 0, x: 0, y: distance };
  }

  function visibleState(extra: Partial<MotionState> = {}): MotionState {
    return {
      opacity: 1,
      x: 0,
      y: 0,
      scale: 1,
      rotate: 0,
      ...extra,
    };
  }

  function motionTransition(duration: number, delay = 0) {
    return prefersReducedMotion
      ? { duration: 0 }
      : { duration, delay, ease: EASE_OUT_EXPO };
  }

  onMount(() => {
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

<BackgroundPattern>
  <main class="page-shell relative z-10">
    <Motion
      initial={hiddenOffset("y", 18)}
      animate={heroVisible ? visibleState() : hiddenOffset("y", 12)}
      transition={motionTransition(heroVisible ? 0.68 : 0.22, heroVisible ? 0.04 : 0)}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (heroVisible = visible), threshold: 0.1 }}
        class="hero-shell"
      >
        <Motion
          initial={hiddenOffset("y", 20)}
          animate={heroVisible ? visibleState() : hiddenOffset("y", 16)}
          transition={motionTransition(0.82, 0.12)}
          let:motion
        >
          <div class="hero-copy" use:motion>
            <div class="hero-meta">
              <p class="section-kicker">Frontend-heavy full-stack developer</p>
              <p class="hero-status">
                <span class="hero-status-dot" aria-hidden="true"></span>
                Open to recruiter conversations
              </p>
            </div>

            <div class="hero-title-row">
              <h1 class="hero-title">Kaung Si Thu</h1>
              <div class="hero-mark">
                <div class="hero-mark-aura" aria-hidden="true"></div>
                <div class="hero-mark-inner">
                  <IconCanvas size={40} />
                </div>
              </div>
            </div>

            <p class="hero-lead">
              I ship clear product interfaces for commerce and business tools with
              React, Svelte, and TypeScript.
            </p>

            <p class="hero-body">
              Over 3 years of experience building responsive web apps with a
              frontend-first approach. My best work is turning dense flows into
              interfaces that are easier to scan, easier to maintain, and ready
              for production delivery.
            </p>

            <div class="hero-actions">
              <a href="mailto:kaungsithu1998202@gmail.com" class="hero-primary-action">
                Email Kaung
              </a>
              <a href="#projects" class="hero-secondary-action">See selected work</a>
            </div>
          </div>
        </Motion>

        <Motion
          initial={prefersReducedMotion ? visibleState() : { opacity: 0, x: 28, scale: 0.98, rotate: 1.5 }}
          animate={heroVisible ? visibleState() : prefersReducedMotion ? visibleState() : { opacity: 0, x: 20, scale: 0.98, rotate: 1 }}
          transition={motionTransition(0.9, 0.22)}
          let:motion
        >
          <aside class="hero-rail" use:motion>
            <ThemeToggle />

            <div class="surface-panel hero-summary">
              <p class="section-kicker">Quick fit</p>

              <ul class="summary-list">
                <li>3+ years building production web interfaces.</li>
                <li>Strongest in frontend delivery, comfortable through API integration.</li>
                <li>Best fit for product teams that need fast, readable UI execution.</li>
              </ul>
            </div>
          </aside>
        </Motion>
      </section>
    </Motion>

    <Motion
      initial={hiddenOffset("y", 14)}
      animate={aboutVisible ? visibleState() : hiddenOffset("y", 10)}
      transition={motionTransition(aboutVisible ? 0.58 : 0.2, aboutVisible ? 0.04 : 0)}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (aboutVisible = visible) }}
        class="section-shell"
      >
        <div class="section-label">
          <p class="section-kicker">Profile</p>
          <p class="section-note">
            A recruiter-focused read on where I add value fastest.
          </p>
        </div>

        <div class="profile-grid">
          <div class="content-stack">
            <p class="profile-copy">
              I work closest to product-facing frontend: the parts users see,
              click, compare, and depend on. I am most useful when a team needs
              clean UI delivery without losing momentum on implementation.
            </p>

            <p class="section-intro">
              My strongest contribution is translating business or product needs
              into interfaces that are easier to read, easier to trust, and
              easier for the team to keep shipping on top of.
            </p>
          </div>

          <article class="surface-panel profile-aside">
            <h2>Best Fit</h2>

            <ul class="profile-list">
              <li>Product-facing frontend work in React, Svelte, and TypeScript.</li>
              <li>Interfaces that rely on structured state, forms, and responsive behavior.</li>
              <li>Teams that want readable code and steady collaboration, not handoff friction.</li>
            </ul>
          </article>
        </div>
      </section>
    </Motion>

    <Motion
      initial={hiddenOffset("y", 14)}
      animate={experienceVisible ? visibleState() : hiddenOffset("y", 10)}
      transition={motionTransition(experienceVisible ? 0.58 : 0.2, experienceVisible ? 0.04 : 0)}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (experienceVisible = visible) }}
        class="section-shell"
      >
        <div class="section-label">
          <p class="section-kicker">Experience</p>
          <p class="section-note">
            Teams, timelines, and the kind of product work I have already been
            trusted to ship.
          </p>
        </div>

        <div class="experience-list stack-separated">
          <Experience
            company="Myanmar High Society"
            position="Frontend Developer"
            timeline="Nov 2022 - Jun 2025"
            image="/imgs/mhs.jpg"
            summary="Frontend delivery for production web interfaces, including commerce-oriented work for Myanmar brands."
            link="https://myanmarhighsociety.com/"
          />

          <Experience
            company="Recite Design ATS"
            position="Frontend Developer"
            timeline="Apr 2025 - Sep 2025"
            image="/imgs/recite.svg"
            summary="Frontend work for an ATS product, with attention to readable hiring flows and structured interface patterns."
            link="https://www.recsitedesign.com/"
          />

          <Experience
            company="A3L"
            position="Full-stack Developer"
            timeline="Dec 2025 - Present"
            image="/imgs/a3l.jpg"
            summary="Current full-stack role covering product features, interface delivery, and integration work across the stack."
            link="https://www.linkedin.com/company/a3l-dev/posts/?feedView=all"
          />
        </div>
      </section>
    </Motion>

    <Motion
      initial={hiddenOffset("y", 14)}
      animate={projectsVisible ? visibleState() : hiddenOffset("y", 10)}
      transition={motionTransition(projectsVisible ? 0.58 : 0.2, projectsVisible ? 0.04 : 0)}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (projectsVisible = visible) }}
        class="section-shell"
        id="projects"
      >
        <div class="section-label">
          <p class="section-kicker">Selected Work</p>
          <p class="section-note">
            Quick examples of product work I have owned end to end or led on the frontend.
          </p>
        </div>

        <div class="content-stack">
          <p class="section-intro">
            Each example shows the product, the part I handled, and the kind of
            UI or full-stack delivery I can take on quickly.
          </p>

          <div class="project-list">
            <Project
              label="Project 01"
              image="/imgs/projects/mypet.png"
              name="MyPetMM.com"
              description="Ecommerce site for a pet-supply retailer with a large consumer catalog."
              role="Built the customer-facing frontend for browsing, cart, and checkout flows."
              focus="Responsive product lists, product details, and form-heavy purchase steps."
              outcome="Turned a broad catalog into a cleaner online buying experience."
              techStacks={[
                "React",
                "Tailwind CSS",
                "Redux",
                "Headless UI",
                "React Hook Form",
              ]}
              link="https://mypetmm.com/"
            />

            <Project
              label="Project 02"
              image="/imgs/projects/m21.png"
              name="M21Sport.com"
              description="Storefront for a sportswear brand expanding further into online sales."
              role="Built the frontend for the brand storefront and core shopping flow."
              focus="Product presentation, mobile browsing, and structured purchase UI."
              outcome="Gave the brand a clearer ecommerce presence beyond in-store retail."
              techStacks={[
                "React",
                "Tailwind CSS",
                "Redux",
                "Headless UI",
                "React Hook Form",
              ]}
              link="https://m21sport.com/"
            />

            <Project
              label="Project 03"
              image="/imgs/projects/tide-focus.png"
              imagePosition="top"
              name="Tide Focus"
              description="Full-stack focus timer app for deep work with wave-based session tracking, ambient sound, review history, and analytics."
              role="Built the app end to end across the React frontend, Node.js backend, and MongoDB persistence layer."
              focus="Structured timer flows, dashboard-style productivity UI, and reusable shadcn components on an Rsbuild stack."
              outcome="Shipped a calmer productivity experience that helps users track focused sessions and review momentum over time."
              techStacks={[
                "React",
                "Rsbuild",
                "Node.js",
                "MongoDB",
                "shadcn/ui",
              ]}
              link="https://tide-focus-web.vercel.app/"
            />
          </div>

          <p class="project-footnote">
            More work samples and implementation details are available on
            request.
          </p>
        </div>
      </section>
    </Motion>

    <Motion
      initial={hiddenOffset("y", 14)}
      animate={educationVisible ? visibleState() : hiddenOffset("y", 10)}
      transition={motionTransition(educationVisible ? 0.58 : 0.2, educationVisible ? 0.04 : 0)}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (educationVisible = visible) }}
        class="section-shell"
      >
        <div class="section-label">
          <p class="section-kicker">Education</p>
          <p class="section-note">
            Formal study and computing education that support the practical work
            above.
          </p>
        </div>

        <div class="education-list stack-separated">
          <Education
            name="Pathein Technology University"
            level="Mechanical Engineering (Year 3)"
          />
          <Education name="NCC Education" level="Level 4 Diploma in Computing" />
        </div>
      </section>
    </Motion>

    <Motion
      initial={hiddenOffset("y", 14)}
      animate={contactVisible ? visibleState() : hiddenOffset("y", 10)}
      transition={motionTransition(contactVisible ? 0.58 : 0.2, contactVisible ? 0.04 : 0)}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (contactVisible = visible) }}
        class="section-shell"
        id="contact"
      >
        <div class="section-label">
          <p class="section-kicker">Contact</p>
          <p class="section-note">
            Direct outreach is the simplest path to an interview conversation.
          </p>
        </div>

        <Contact />
      </section>
    </Motion>
  </main>
</BackgroundPattern>

<style>
  .hero-shell {
    display: grid;
    gap: clamp(1.5rem, 4vw, 3rem);
    padding-bottom: var(--space-section);
  }

  .hero-copy {
    display: flex;
    flex-direction: column;
    gap: var(--space-md);
  }

  .hero-meta {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: var(--space-xs);
  }

  .hero-status {
    display: inline-flex;
    min-height: 2.5rem;
    align-items: center;
    gap: 0.55rem;
    border: 1px solid color-mix(in oklch, var(--accent) 36%, var(--line) 64%);
    border-radius: 999px;
    padding: 0 1rem;
    background: color-mix(in oklch, var(--surface) 78%, var(--accent-soft) 22%);
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: var(--tracking-label);
    text-transform: uppercase;
    color: color-mix(in oklch, var(--accent) 72%, var(--text) 28%);
  }

  .hero-status-dot {
    width: 0.48rem;
    height: 0.48rem;
    flex-shrink: 0;
    border-radius: 999px;
    background: var(--accent-warm);
    box-shadow: 0 0 0 0 color-mix(in oklch, var(--accent-warm) 34%, transparent);
    animation: status-pulse 2.8s var(--ease-out-quint) infinite;
  }

  .hero-title-row {
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    gap: var(--space-sm);
  }

  .hero-title {
    max-width: 8ch;
    font-size: var(--text-display);
    font-weight: var(--weight-bold);
    line-height: 0.94;
    letter-spacing: -0.06em;
  }

  .hero-mark {
    position: relative;
    display: grid;
    place-items: center;
    margin-top: 0.35rem;
    flex-shrink: 0;
  }

  .hero-mark-aura {
    position: absolute;
    inset: -0.65rem;
    z-index: -1;
    border-radius: 999px;
    background:
      radial-gradient(circle, color-mix(in oklch, var(--accent-soft) 78%, transparent) 0%, transparent 68%),
      radial-gradient(circle at 72% 28%, color-mix(in oklch, var(--accent-cool-soft) 62%, transparent) 0%, transparent 52%);
    filter: blur(10px);
    opacity: 0.72;
    animation: hero-aura-breathe 6s var(--ease-out-quint) infinite;
  }

  .hero-mark-inner {
    transform-origin: center;
    will-change: transform;
    animation: hero-mark-float 7s var(--ease-out-quint) infinite;
    animation-delay: 0.8s;
  }

  .hero-lead {
    max-width: 26rem;
    font-size: var(--text-lead);
    font-weight: var(--weight-medium);
    line-height: 1.42;
    letter-spacing: -0.02em;
  }

  .hero-body {
    max-width: 38rem;
    font-size: var(--text-body);
    line-height: var(--lh-body);
    color: var(--muted);
  }

  .hero-actions {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
  }

  .hero-primary-action,
  .hero-secondary-action {
    display: inline-flex;
    min-height: 2.7rem;
    align-items: center;
    justify-content: center;
    border-radius: 999px;
    padding: 0 1rem;
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

  .hero-primary-action {
    background: var(--accent);
    color: var(--accent-contrast);
  }

  .hero-primary-action:hover,
  .hero-secondary-action:hover {
    transform: translateY(-2px) scale(1.015);
  }

  .hero-primary-action:hover {
    background: color-mix(in oklch, var(--accent) 84%, var(--accent-warm) 16%);
  }

  .hero-secondary-action {
    border: 1px solid color-mix(in oklch, var(--line) 64%, var(--accent-cool) 36%);
    background: color-mix(in oklch, var(--surface) 82%, var(--accent-cool-soft) 18%);
    color: color-mix(in oklch, var(--text) 82%, var(--accent-cool) 18%);
  }

  .hero-secondary-action:hover {
    border-color: color-mix(in oklch, var(--accent-cool) 56%, var(--line-strong) 44%);
    background: color-mix(in oklch, var(--surface) 72%, var(--accent-cool-soft) 28%);
  }

  .hero-primary-action:active,
  .hero-secondary-action:active {
    transform: translateY(0) scale(0.985);
  }

  .hero-rail {
    display: flex;
    flex-direction: column;
    gap: var(--space-md);
  }

  .hero-summary {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
    padding: clamp(1rem, 2.4vw, 1.45rem);
    border-color: color-mix(in oklch, var(--line) 68%, var(--accent) 32%);
    background: color-mix(in oklch, var(--surface) 88%, var(--accent-soft) 12%);
    transition:
      transform 320ms var(--ease-out-quint),
      box-shadow 320ms var(--ease-out-quint);
  }

  .hero-summary:hover {
    transform: translateY(-3px);
  }

  .summary-list {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
    font-size: var(--text-body);
    line-height: 1.68;
    color: var(--muted);
  }

  .summary-list li + li {
    padding-top: var(--space-sm);
    border-top: 1px solid color-mix(in oklch, var(--line) 74%, var(--accent-cool) 26%);
  }

  .profile-grid {
    display: grid;
    gap: clamp(1.5rem, 4vw, 2.5rem);
    align-items: start;
  }

  .profile-copy {
    max-width: 65ch;
    font-size: var(--text-body);
    font-weight: var(--weight-medium);
    line-height: var(--lh-body-loose);
  }

  .section-intro {
    max-width: 65ch;
    font-size: var(--text-body);
    line-height: var(--lh-body);
    color: var(--muted);
  }

  .profile-aside {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
    padding: clamp(1rem, 2.4vw, 1.4rem);
    border-color: color-mix(in oklch, var(--line) 70%, var(--accent-warm) 30%);
    background: color-mix(in oklch, var(--surface) 90%, var(--accent-warm-soft) 10%);
  }

  .profile-aside h2 {
    font-size: var(--text-label);
    font-weight: var(--weight-semibold);
    line-height: var(--lh-label);
    letter-spacing: var(--tracking-label-wide);
    text-transform: uppercase;
    color: color-mix(in oklch, var(--accent-warm) 70%, var(--text) 30%);
  }

  .profile-list {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
  }

  .profile-list li {
    font-size: var(--text-body);
    line-height: var(--lh-body);
  }

  .profile-list li + li {
    padding-top: var(--space-sm);
    border-top: 1px solid color-mix(in oklch, var(--line) 76%, var(--accent-warm) 24%);
  }

  .experience-list,
  .project-list,
  .education-list {
    display: flex;
    flex-direction: column;
  }

  .project-list {
    gap: clamp(2.5rem, 6vw, 4rem);
  }

  .project-footnote {
    max-width: 60ch;
    font-size: var(--text-meta);
    line-height: 1.65;
    color: var(--muted);
  }

  @keyframes hero-mark-float {
    0%,
    100% {
      transform: translate3d(0, 0, 0) rotate(0deg);
    }
    50% {
      transform: translate3d(0, -6px, 0) rotate(-3deg);
    }
  }

  @keyframes hero-aura-breathe {
    0%,
    100% {
      transform: scale(0.96);
      opacity: 0.56;
    }
    50% {
      transform: scale(1.08);
      opacity: 0.88;
    }
  }

  @keyframes status-pulse {
    0%,
    100% {
      box-shadow: 0 0 0 0 color-mix(in oklch, var(--accent-warm) 34%, transparent);
      transform: scale(1);
    }
    50% {
      box-shadow: 0 0 0 0.45rem color-mix(in oklch, var(--accent-warm) 0%, transparent);
      transform: scale(1.08);
    }
  }

  @media (min-width: 64rem) {
    .hero-shell {
      grid-template-columns: minmax(0, 1.4fr) minmax(16rem, 0.78fr);
      align-items: start;
    }

    .profile-grid {
      grid-template-columns: minmax(0, 1.15fr) minmax(16rem, 0.82fr);
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .hero-status-dot,
    .hero-mark-aura,
    .hero-mark-inner {
      animation: none;
    }

    .hero-primary-action,
    .hero-secondary-action,
    .hero-summary {
      transition: none;
    }

    .hero-primary-action:hover,
    .hero-secondary-action:hover,
    .hero-summary:hover {
      transform: none;
    }
  }
</style>
