<script lang="ts">
  import {
    ExternalLinkIcon,
    GithubIcon,
    Globe,
    LucideLinkedin,
    Mail,
  } from "@lucide/svelte";
  import IconButton from "./lib/IconButton.svelte";
  import IconCanvas from "./lib/icons/IconCanvas.svelte";
  import IconSocialX from "./lib/icons/IconSocialX.svelte";
  import Marquee from "./lib/Marquee.svelte";
  import SparkleText from "./lib/SparkleText.svelte";
  import SectionTitle from "./lib/SectionTitle.svelte";
  import Skills from "./lib/Skills.svelte";
  import Experience from "./lib/Experience.svelte";
  import Project from "./lib/Project.svelte";
  import BackgroundPattern from "./lib/BackgroundPattern.svelte";
  import Education from "./lib/Education.svelte";
  import Contact from "./lib/Contact.svelte";
  import ThemeToggle from "./lib/ThemeToggle.svelte";
</script>

<BackgroundPattern>
  <main
    class="mx-10 md:mx-[200px] lg:mx-[500px] py-10 font-geist-pixel-circle transition-colors"
  >
    <h1
      class="text-start flex items-center gap-5 text-3xl md:text-5xl font-bold text-slate-900 dark:text-slate-100 transition-colors"
    >
      <span class="z-50">Kaung Si Thu</span>
      <IconCanvas />
    </h1>
    <SparkleText
      text="Every line of code is a stroke of art."
      class="text-lg md:text-2xl mt-6"
    />

    <div class="flex items-center mt-5 gap-3">
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

      <div class="ml-auto">
        <ThemeToggle />
      </div>
    </div>

    <SectionTitle title="About" />

    <p class="text-slate-700 dark:text-slate-300 text-xs md:text-base">
      I love taking an idea, turning it into something real, and seeing people
      actually use it. From IoT-powered healthcare to open-source fitness tools,
      I’m all about shipping fast and solving real problems. My stack? A good
      dose of curiosity and a drive to keep building.
    </p>

    <Skills />

    <div class="mt-6">
      <SectionTitle title="Experience" />

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

      <SectionTitle title="Projects" />

      <p class="text-slate-700 dark:text-slate-300 text-xs md:text-base">
        Throughout my experience, I’ve contributed to diverse projects, tackling
        both simple and complex challenges. Below are some of my favorite
        projects.
      </p>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-3 mt-3">
        <Project
          image="/imgs/projects/mypet.png"
          name="MyPetMM.com"
          description="Developed an e-commerce platform for MyPet Myanmar, a leading online pet supply store offering a wide range of products for pets including dogs,cats, and birds."
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
          description="M21 Sport is a prominent Myanmar-based sportswear brand established in 2015, specializing in the design, production, and retail of high-quality sports apparel and equipment. Initially starting as a retail store, the company expanded into manufacturing custom items and has since become a key player in Myanmar's sports industry."
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

      <SectionTitle title="Education" />

      <Education name="Pathein Technology University" level="Mechanical 3 BE" />
      <Education name="NCC Education" level="Level 4 : Diploma In Computing" />

      <SectionTitle title="Contact" />
      <Contact />
    </div>
  </main>
</BackgroundPattern>
