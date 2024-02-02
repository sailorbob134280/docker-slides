<script>
  import Slide from '../lib/Slide.svelte';

  export let part;
</script>

<section data-background="assets/BG5.png" data-background-opacity="0.3">
  <h1 class="font-sans font-thin text-12xl">Part {part}</h1>
  <h2 class="fragment fade-up font-sans font-light text-4xl">Practical Use Cases</h2>
</section>

<Slide title="Neat Uses">
  <ul>
    <li class="fragment fade-up">Web Services (obvs)</li>
    <li class="fragment fade-up">Development Environments</li>
    <li class="fragment fade-up">Cross-compiler Environments</li>
    <li class="fragment fade-up">CI/CD Runners and Jobs</li>
    <li class="fragment fade-up">Test Harnesses</li>
  </ul>
</Slide>


