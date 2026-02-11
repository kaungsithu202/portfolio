<script>
  import Marquee from "./Marquee.svelte";
  import HTML from "../assets/skills/HTML5.png";
  import CSS from "../assets/skills/CSS3.png";
  import Tailwind from "../assets/skills/tailwind.svg";
  import JS from "../assets/skills/js.png";
  import React from "../assets/skills/react.svg";
  import Nextjs from "../assets/skills/Next.js.png";
  import Svelte from "../assets/skills/Svelte.png";
  import TypeScript from "../assets/skills/TypeScript.png";
  import Nodejs from "../assets/skills/Node.js.png";
  import Express from "../assets/skills/Express.png";
  import TanstackQuery from "../assets/skills/React-Query.svg";
  import Git from "../assets/skills/Git.png";
  import Jest from "../assets/skills/Jest.png";
  import Webpack from "../assets/skills/Webpack.png";
  import Redux from "../assets/skills/Redux.png";
  import Mysql from "../assets/skills/MySQL.png";
  import Sass from "../assets/skills/sass.png";
  import MongoDb from "../assets/skills/MongoDB.png";

  const skills = [
    { name: "HTML5", img: HTML },
    { name: "CSS3", img: CSS },
    { name: "Tailwind", img: Tailwind },
    { name: "JavaScript", img: JS },
    { name: "React", img: React },
    { name: "Next.js", img: Nextjs },
    { name: "Svelte", img: Svelte },
    { name: "TypeScript", img: TypeScript },
    { name: "Node.js", img: Nodejs },
    { name: "Express", img: Express },
    { name: "TanStack Query", img: TanstackQuery },
    { name: "Git", img: Git },
    { name: "Jest", img: Jest },
    { name: "Webpack", img: Webpack },
    { name: "Redux", img: Redux },
    { name: "MySQL", img: Mysql },
    { name: "Sass", img: Sass },
    { name: "MongoDB", img: MongoDb },
  ];

  let firstRow = skills.slice(0, skills.length / 2);
  let secondRow = skills.slice(skills.length / 2);
</script>

<div
  class="relative flex h-full w-full flex-col items-center justify-center overflow-hidden rounded-lg bg-white/50 dark:bg-slate-900/40 my-6 transition-colors"
>
  <Marquee pauseOnHover>
    {#each firstRow as skill}
      <img src={skill.img} alt={skill.name} class="rounded-full size-16" />
    {/each}
  </Marquee>
  <Marquee reverse pauseOnHover>
    {#each secondRow as skill}
      <img src={skill.img} alt={skill.name} class="rounded-full size-16" />
    {/each}
  </Marquee>

  <div
    class="pointer-events-none absolute inset-y-0 left-0 w-1/3 bg-gradient-to-r from-white dark:from-slate-950"
  ></div>
  <div
    class="pointer-events-none absolute inset-y-0 right-0 w-1/3 bg-gradient-to-l from-white dark:from-slate-950"
  ></div>
</div>
