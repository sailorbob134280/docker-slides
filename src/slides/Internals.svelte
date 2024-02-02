<script>
  import Slide from '../lib/Slide.svelte';
  import Code from '../lib/Code.svelte';

  export let part;
</script>

<section data-background="assets/BG2.png" data-background-opacity="0.3">
  <h1 class="font-sans font-thin text-12xl">Part {part}</h1>
  <h2 class="fragment fade-up font-sans font-light text-4xl">How</h2>
</section>

<Slide title="The Solution(...)">
  <ul class="m-10">
    <li class="fragment fade-up">We created Containers 🥳</li>
    <h1> TODO: Add a diagram of a container </h1>
  </ul>
</Slide>

<Slide title="Containers">
  <ul class="m-10">
    <li class="fragment fade-up">Run as a process on the host kernel, rather than its own</li>
    <li class="fragment fade-up">Generally aware it isn't a real machine</li>
    <li class="fragment fade-up">Segregated from other processes through kernel namespaces</li>
    <li class="fragment fade-up">May be resource-limited using cgroups</li>
    <li class="fragment fade-up">Can be nested, with the right settings</li>
  </ul>
  <p class="fragment fade-up"><i>Generally cannot load kernel modules or execute in kernel space... Unless you make it privileged</i></p>
</Slide>
  
<Slide title="Under the hood">
  <ul class="m-4">
    <li>File system bundle - what makes it "it"</li>
    <ul>
      <li>System libraries</li>
      <li>App-level shared libraries</li>
      <li>Application binaries</li>
      <li>Configuration files</li>
      <li>Distro-level components(e.g. init system, shell, package manager, etc)</li>
    </ul>
    <li>A set of layered archives that, when applied, produces the filesystem</li>
  </ul>
</Slide>

<Slide title="Under the hood">
  <ul>
    <li>Image Manifest</li>
  </ul>
  <Code>
    {`
{
   "schemaVersion": 2,
   "mediaType": "application/vnd.oci.image.index.v1+json",
   "manifests": [
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 861,
         "digest": "sha256:e2fc4e5012d16e7fe466f5291c476431beaa1f9b90a5c2125b493ed28e2aba57",
         "platform": {
            "architecture": "amd64",
            "os": "linux"
         }
      },
...
    `}
  </Code>
</Slide>

<Slide title="Under the hood">
  <ul>
    <li>Configuration File</li>
  </ul>
  <Code>
    {`
[
    {
        "ID": "eo7jnzguqgtpdah3cm5srfb97",
        "Version": {
            "Index": 17
        },
        "CreatedAt": "2017-03-24T08:15:09.735271783Z",
        "UpdatedAt": "2017-03-24T08:15:09.735271783Z",
        "Spec": {
            "Name": "my_config",
            "Labels": {
                "env": "dev",
                "rev": "20170324"
            },
            "Data": "aGVsbG8K"
        }
    }
]
    `}
  </Code>
</Slide>

<Slide title="At Runtime">
  <ul>
    <li>Container Runtime</li>
    <ul>
      <li>Responsible for creating and managing containers</li>
      <li>Interacts with the kernel to create the container</li>
      <li>May be a daemon or a CLI tool</li>
      <li>Most common is Docker, though containerd is starting to take over</li>
    </ul>
    <li>Pulls layers and metadata from a registry</li>
    <li>Creates a container from the image</li>
    <li>Runs the container entrypoint</li>
  </ul>
</Slide>
