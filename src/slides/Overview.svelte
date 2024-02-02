<script>
  import Slide from '../lib/Slide.svelte';

  export let part;
</script>

<section data-background="assets/BG1.png" data-background-opacity="0.3">
  <h1 class="font-sans font-thin text-12xl">Part {part}</h1>
  <h2 class="fragment fade-up font-sans font-light text-4xl">Why</h2>
</section>

<Slide title="In the beginning...">
  <p class="fragment fade-up my-12">Humanity taught sand to think.</p>
  <p class="fragment fade-up my-12">This made a lot of people very angry, and has widely been regarded as a bad move.</p>
</Slide>

<Slide title="More Recently">
  <ul class="m-10">
    <li class="fragment fade-up">The internet was born</li>
    <li class="fragment fade-up">We started to need servers</li>
    <li class="fragment fade-up">And then we needed a lot of servers</li>
    <li class="fragment fade-up">And then a LOT of servers</li>
    <li class="fragment fade-up">This got expensive alarmingly fast</li>
  </ul>
</Slide>

<Slide title="The Solution(?)">
  <img src="assets/virtual-machines.png" class="mx-auto my-8" width="480" />
  <p class="mx-auto font-thin text-5xl text-center">We created Virtual Machines! 🥳</p>
  <p class="fragment fade-up mx-auto font-thin text-5xl text-center">But there were problems... 🤨</p>
</Slide>

<Slide title="Virtual Machines">
  <ul class="m-10">
    <li class="fragment fade-up">Run as a full OS</li>
    <li class="fragment fade-up">Generally unaware it isn't a real machine</li>
    <li class="fragment fade-up">Has its own kernel</li>
    <li class="fragment fade-up">Generally easy to separate (depending on the hypervisor)</li>
  </ul>
</Slide>

<Slide title="The Problem with VMs">
  <ul class="m-6">
    <li class="fragment fade-up">They're heavy</li>
      <ul class="text-4xl fragment fade-up">
        <li>The kernel is usually expensive</li>
        <li>They usually don't like to play nice when sharing resources</li>
      </ul>
    <li class="fragment fade-up">They're hard to manage</li>
      <ul class="text-4xl fragment fade-up">
        <li>Usually close to the physical host</li>
        <li>Often slow to start</li>
        <li>Large fleets get cumbersome fast</li>
      </ul>
  </ul>
  <p class="fragment fade-up font-sans font-thin font-xl"><i>In reality, people mostly just wanted isolation and reproducible environments.</i></p>
</Slide>

<Slide title="The Core Problem">
  <ul>
    <li class="fragment fade-up">Running a bunch of kernels is expensive, and typically unnecessary</li>
    <li class="fragment fade-up">VMs don't really solve the issue of portability</li>
    <ul class="fragment fade-up text-4xl font-thin">
      <li>They're usually tied to a specific hypervisor</li>
      <li>They're usually very hardware-dependent</li>
      <li>Most panic if you change settings much</li>
    </ul>
    <li class="fragment fade-up">While VMs provide <i>excellent</i> isolation, there are lighterweight alternatives</li>
    <ul class="fragment fade-up text-4xl font-thin">
      <li>Namespaces - Allows segregation of processes</li>
      <li>Cgroups - Allows limitations to be placed on resources (e.g. CPU time, memory, etc)</li>
  </ul>
</Slide>

<Slide title="Containers">
  <ul class="m-10">
    <li class="fragment fade-up">Small, easy way to package a "system", sans kernel</li>
    <li class="fragment fade-up">Distro-agnostic (though generally limited to POSIX systems)</li>
    <li class="fragment fade-up">Fast to update</li>
    <li class="fragment fade-up">Reproducable</li>
    <li class="fragment fade-up">Highly configurable</li>
    <li class="fragment fade-up">Extensible</li>
  </ul>
</Slide>
