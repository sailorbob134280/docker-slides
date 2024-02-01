<script>
  import Slide from '../lib/Slide.svelte';
  import Code from '../lib/Code.svelte';
</script>

<section data-background="assets/BG3.png" data-background-opacity="0.3">
  <h1 class="font-sans font-thin text-12xl">Part 3</h1>
  <h2 class="fragment fade-up font-sans font-light text-4xl">Ok but really, how</h2>
</section>

<Slide title="Dockerfile">
  <p class="fragment fade-up">Containers are generally built with instructions in a <i>Dockerfile</i></p>
  <ul class="m-10">
    <li class="fragment fade-up">A text file that contains all the commands a user could call on the command line to assemble an image</li>
    <li class="fragment fade-up">Each command creates a new layer</li>
    <li class="fragment fade-up">The final layer is the image</li>
  </ul>
</Slide>

<Slide title="Dockerfile Example">
  <p>Here's an example of a Dockerfile I regularly use:</p>
  <Code>
    {`
FROM gcc:12

# Install build tools
RUN apt-get update && apt-get install -y python3 python3-pip ninja-build gdb graphviz
RUN pip install meson gcovr
# The version of doxy in the Debian repos is too old to support concepts, so we grab the latest release and manually install
RUN wget --progress=bar:force:noscroll https://www.doxygen.nl/files/doxygen-1.9.5.linux.bin.tar.gz && \
    tar -xzf doxygen-1.9.5.linux.bin.tar.gz && \\
    cd doxygen-1.9.5 && \\
    make install && \\
    cd .. && \\
    rm -r doxygen-1.9.5.linux.bin.tar.gz && \\
    rm -r doxygen-1.9.5

WORKDIR /usr/src/app
    `}
  </Code>
</Slide>

<Slide title="Building and Running">
  <p>To build that image, we'd run:</p>
  <Code>
    {`
docker build -t my-cool-build-env:latest ./Dockerfile .
    `}
  </Code>
  <p>To run that container, we'd run:</p>
  <Code>
    {`
docker run my-cool-build-env:latest
    `}
  </Code>
</Slide>
