<script lang="ts">
  import {
    GithubIcon,
    LucideLinkedin,
    Mail,
  } from "@lucide/svelte";
  import { Motion } from "svelte-motion";
  import BackgroundPattern from "./lib/BackgroundPattern.svelte";
  import Contact from "./lib/Contact.svelte";
  import Education from "./lib/Education.svelte";
  import Experience from "./lib/Experience.svelte";
  import IconButton from "./lib/IconButton.svelte";
  import IconCanvas from "./lib/icons/IconCanvas.svelte";
  import IconSocialX from "./lib/icons/IconSocialX.svelte";
  import Project from "./lib/Project.svelte";
  import SectionTitle from "./lib/SectionTitle.svelte";
  import SparkleText from "./lib/SparkleText.svelte";
  import ThemeToggle from "./lib/ThemeToggle.svelte";

  let heroVisible = false;
  let aboutVisible = false;
  let experienceVisible = false;
  let projectsVisible = false;
  let educationVisible = false;
  let contactVisible = false;

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
</script>

<BackgroundPattern>
  <main
    class="relative z-10 mx-auto max-w-6xl px-5 py-8 font-roboto md:px-10 md:py-12"
  >
    <Motion
      initial={{ opacity: 0, y: 12 }}
      animate={heroVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 0 }}
      transition={heroVisible
        ? { duration: 0.55, delay: 0.05 }
        : { duration: 0.22 }}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (heroVisible = visible), threshold: 0.1 }}
        class="rounded-2xl border border-slate-200/80 bg-white/75 p-5 shadow-[0_30px_80px_-45px_rgba(14,116,144,0.5)] backdrop-blur md:p-8 dark:border-slate-700/70 dark:bg-slate-900/65 dark:shadow-[0_30px_80px_-45px_rgba(14,165,233,0.45)]"
      >
        <div class="flex flex-wrap items-start gap-4 md:gap-6">
          <div class="min-w-0 flex-1">
            <p
              class="w-fit rounded-full border border-cyan-200 bg-cyan-50 px-3 py-1 text-[10px] tracking-[0.18em] text-cyan-700 uppercase dark:border-cyan-900/80 dark:bg-cyan-950/40 dark:text-cyan-200"
            >
              Full-stack developer
            </p>

            <h1
              class="mt-4 flex flex-wrap items-center gap-3 text-3xl font-bold leading-tight text-slate-900 md:text-5xl dark:text-slate-100"
            >
              <span>Kaung Si Thu</span>
              <IconCanvas />
            </h1>

            <SparkleText
              text="I design and ship products that feel fast, clear, and alive."
              class="mt-4 text-base md:text-xl"
              colors={{ first: "#0891b2", second: "#f97316" }}
              sparklesCount={8}
            />

            <p
              class="mt-4 max-w-3xl text-xs leading-6 text-slate-700 md:text-sm dark:text-slate-300"
            >
              Full-stack developer with over 3 years of experience in frontend
              and product-focused engineering. I build responsive web apps with
              clean interfaces, reliable performance, and thoughtful user flows.
            </p>
          </div>

          <div class="ml-auto">
            <ThemeToggle />
          </div>
        </div>

        <div class="mt-6 grid gap-3 md:grid-cols-[1fr_auto] md:items-end">
          <div class="flex flex-wrap items-center gap-2">
            <span
              class="rounded-full border border-slate-300 bg-white/80 px-3 py-1 text-[10px] tracking-[0.12em] uppercase dark:border-slate-700 dark:bg-slate-950/50"
              >3+ years building production apps</span
            >
            <span
              class="rounded-full border border-slate-300 bg-white/80 px-3 py-1 text-[10px] tracking-[0.12em] uppercase dark:border-slate-700 dark:bg-slate-950/50"
              >Frontend-first, full-stack capable</span
            >
            <a
              href="#contact"
              class="rounded-full border border-amber-300 bg-amber-100 px-3 py-1 text-[10px] tracking-[0.12em] text-amber-900 uppercase transition hover:bg-amber-200 dark:border-amber-700/70 dark:bg-amber-900/25 dark:text-amber-100 dark:hover:bg-amber-900/40"
            >
              Available for new projects
            </a>
          </div>

          <div class="flex items-center gap-2">
            <IconButton href="https://github.com/kaungsithu202">
              <GithubIcon size="16" />
            </IconButton>
            <IconButton href="https://www.linkedin.com/in/kaung-si-thu-7079ba23b/">
              <LucideLinkedin size="16" />
            </IconButton>
            <IconButton href="https://x.com/karl2021998">
              <IconSocialX size="16" />
            </IconButton>
            <IconButton href="mailto:kaungsithu1998202@gmail.com">
              <Mail size="16" />
            </IconButton>
          </div>
        </div>
      </section>
    </Motion>

    <Motion
      initial={{ opacity: 0, y: 12 }}
      animate={aboutVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 0 }}
      transition={aboutVisible
        ? { duration: 0.5, delay: 0.05 }
        : { duration: 0.2 }}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (aboutVisible = visible) }}
        class="mt-8 grid gap-3 md:grid-cols-2"
      >
        <article
          class="rounded-2xl border border-slate-200/80 bg-white/70 p-5 backdrop-blur dark:border-slate-700/70 dark:bg-slate-900/45"
        >
          <SectionTitle title="About" />
          <p
            class="mt-3 text-xs leading-6 text-slate-700 md:text-sm dark:text-slate-300"
          >
            I turn ideas into websites that are easy to use and easy to scale.
            My focus is on smooth interfaces, maintainable code, and strong
            collaboration with product teams.
          </p>
        </article>

        <article
          class="rounded-2xl border border-slate-200/80 bg-white/70 p-5 backdrop-blur dark:border-slate-700/70 dark:bg-slate-900/45"
        >
          <SectionTitle title="What I Bring" />
          <ul
            class="mt-3 space-y-2 text-[11px] leading-6 text-slate-700 md:text-xs dark:text-slate-300"
          >
            <li>
              Build polished, responsive UIs with React, Svelte, and Tailwind.
            </li>
            <li>
              Ship API-connected flows with clear state handling and UX
              feedback.
            </li>
            <li>Maintain clean architecture for long-term product velocity.</li>
          </ul>
        </article>
      </section>
    </Motion>

    <Motion
      initial={{ opacity: 0, y: 12 }}
      animate={experienceVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 0 }}
      transition={experienceVisible
        ? { duration: 0.5, delay: 0.05 }
        : { duration: 0.2 }}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (experienceVisible = visible) }}
        class="mt-10"
      >
        <SectionTitle title="Experience" />

        <div class="mt-3 space-y-3">
          <Experience
            company="MYANMAR HIGH SOCIETY"
            position="Frontend Developer"
            timeline="2022 NOV - 2025 JUN"
            image="/imgs/mhs.jpg"
            link="https://myanmarhighsociety.com/"
          />

          <Experience
            company="RECITE DESIGN ATS"
            position="Frontend Developer"
            timeline="2025 APR - 2025 SEP"
            image="/imgs/recite.svg"
            link="https://www.recsitedesign.com/"
          />

          <Experience
            company="A3L"
            position="Fullstack Developer"
            timeline="2025 DEC - Present"
            image="/imgs/a3l.jpg"
            link="https://www.linkedin.com/company/a3l-dev/posts/?feedView=all"
          />
        </div>
      </section>
    </Motion>

    <Motion
      initial={{ opacity: 0, y: 12 }}
      animate={projectsVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 0 }}
      transition={projectsVisible
        ? { duration: 0.5, delay: 0.05 }
        : { duration: 0.2 }}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (projectsVisible = visible) }}
        class="mt-10"
      >
        <SectionTitle title="Projects" />

        <p
          class="mt-3 max-w-3xl text-xs leading-6 text-slate-700 md:text-sm dark:text-slate-300"
        >
          I have contributed to products ranging from e-commerce to custom
          business platforms. Here are a few projects that represent my
          favorite kinds of work.
        </p>

        <div class="mt-4 grid grid-cols-1 gap-3 lg:grid-cols-2">
          <Project
            image="/imgs/projects/mypet.png"
            name="MyPetMM.com"
            description="Developed an e-commerce platform for MyPet Myanmar, a leading online pet supply store offering a wide range of products for dogs, cats, and birds."
            techStacks={[
              "React",
              "Tailwindcss",
              "Redux",
              "HeadlessUi",
              "React Hook Form",
            ]}
            link="https://mypetmm.com/"
          />

          <Project
            image="/imgs/projects/m21.png"
            name="M21Sport.com"
            description="Built a modern storefront for M21 Sport, a Myanmar sportswear brand, supporting their transition from retail-first operations to a scalable digital commerce experience."
            techStacks={[
              "React",
              "Tailwindcss",
              "Redux",
              "HeadlessUi",
              "React Hook Form",
            ]}
            link="https://m21sport.com/"
          />
        </div>
      </section>
    </Motion>

    <Motion
      initial={{ opacity: 0, y: 12 }}
      animate={educationVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 0 }}
      transition={educationVisible
        ? { duration: 0.5, delay: 0.05 }
        : { duration: 0.2 }}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (educationVisible = visible) }}
        class="mt-10"
      >
        <SectionTitle title="Education" />
        <div class="mt-3 space-y-2">
          <Education
            name="Pathein Technology University"
            level="Mechanical 3 BE"
          />
          <Education name="NCC Education" level="Level 4 : Diploma In Computing" />
        </div>
      </section>
    </Motion>

    <Motion
      initial={{ opacity: 0, y: 12 }}
      animate={contactVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 0 }}
      transition={contactVisible
        ? { duration: 0.5, delay: 0.05 }
        : { duration: 0.2 }}
      let:motion
    >
      <section
        use:motion
        use:revealOnView={{ onChange: (visible) => (contactVisible = visible) }}
        class="mt-10"
        id="contact"
      >
        <SectionTitle title="Contact" />
        <Contact />
      </section>
    </Motion>
  </main>
</BackgroundPattern>
