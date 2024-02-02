<script>
  import Slide from '../lib/Slide.svelte';
  import Code from '../lib/Code.svelte';

  export let part;
</script>

<section data-background="assets/BG3.png" data-background-opacity="0.3">
  <h1 class="font-sans font-thin text-12xl">Part {part}</h1>
  <h2 class="fragment fade-up font-sans font-light text-4xl">Ok but really, how</h2>
</section>

<Slide title="Dockerfile">
  <p class="fragment fade-up">Containers are generally built with instructions in a <i>Dockerfile</i></p>
  <ul class="m-10">
    <li class="fragment fade-up">A text file that contains all the commands a user could call on the command line to assemble an image</li>
    <li class="fragment fade-up">Each command creates a new layer</li>
    <li class="fragment fade-up">The final layer is the image</li>
  </ul>
  <p class="fragment fade-up font-thin"><i>This gives us the concept of "compile time" vs "runtime"</i></p>
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

<Slide title="Notable Commands">
  <ul class="text-4xl">
    <li>FROM - The base image [read: set of layers] to start from</li>
    <li>RUN - Run a shell command</li>
    <li>COPY - Copy files from the host to the image</li>
    <li>CMD - Overrideable command to execute on start</li>
    <li>ENTRYPOINT - Non-overrideable CMD</li>
    <li>ENV - Set an environment variable</li>
    <li>ARG - Set build-time variables</li>
    <li>VOLUME - Create a mount point</li>
    <li>EXPOSE - Expose a port</li>
    <li>WORKDIR - Set the working directory</li>
  </ul>
  <p class="fragment fade-up font-thin"><i>There are many more, but these are the most common</i></p>
</Slide>

<Slide title="Build Time (Image)">
  <p class="fragment fade-up">Some notable features and patterns at build time:</p>
  <ul class="m-10">
    <li class="fragment fade-up">Build Arguments - Pass in variables at build time</li>
    <li class="fragment fade-up">Multi-Stage Builds - Use a full-featured build image to create a stripped-down production one</li>
    <li class="fragment fade-up">Build Cache - Leverage the cache to speed up builds</li>
    <li class="fragment fade-up">User/Group Management - Fix file permissions and enhance security by not running everything as root</li>
  </ul>
</Slide>

<section>
  <div class="flex-col">
    <h3 class="font-sans font-thin text-12xl flex-col">Please do not run production apps as root.</h3>
    <img src="assets/sad-whale.png" alt="A sad whale" class="mx-auto object-contain flex-col" width="300" />
    <h3 class="fragment fade-up font-sans font-thin text-12xl flex-col">This makes the whale sad.</h3>
  </div>
</section>

<Slide title="Runtime (Container)">
  <p class="fragment fade-up">At runtime, there are a lot more features you can leverage</p>
  <ul class="m-4">
    <li class="fragment fade-up">Virtual Networks - Private, named networks for containers to talk to each other</li>
    <li class="fragment fade-up">Volumes - Link a file or directory in the container to one on the host</li>
    <li class="fragment fade-up">CLI Flags - Override settings or change the behavior of a built image</li>
    <li class="fragment fade-up">Healthchecks - Define a command to run to determine if the container is healthy</li>
  </ul>
</Slide>

<Slide title="Example Runtime Command">
  <p class="fragment fade-up">Here's an example of a more complex run command:</p>
  <Code>
    {`
  docker run -d \\
    --name my-flask-container \\
    -p 4000:80 \\
    -v /host/path/to/app:/app \\
    -e "ENV_VAR_NAME=value" \\
    --restart unless-stopped \\
    my-flask-app
    `}
  </Code>
</Slide>

<Slide title="Another Snag">
  <p class="fragment fade-up">Some projects contain lots of containers...</p>
  <img src="assets/overloaded-whale.png" alt="An overloaded whale" class="fragment fade-up mx-auto object-contain" width="300" />
  <p class="fragment fade-up font-thin"><i>...a LOT of containers.</i></p>
  <p class="fragment fade-up font-thin"><i>And they all need to be configured for the specific project.</i></p>
</Slide>
