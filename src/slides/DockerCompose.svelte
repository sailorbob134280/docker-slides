<script>
  import Slide from '../lib/Slide.svelte';
  import Code from '../lib/Code.svelte';

  export let part;
</script>

<section data-background="assets/BG6.png" data-background-opacity="0.3">
  <h1 class="font-sans font-thin text-12xl">Part {part}</h1>
  <h2 class="fragment fade-up font-sans font-light text-4xl">A lot of containers</h2>
</section>

<Slide title="Docker Compose">
  <ul>
    <li class="fragment fade-up">Docker Compose is a tool for defining and running multi-container Docker applications.</li>
    <li class="fragment fade-up">It uses a YAML file to configure the application's services, networks, and volumes.</li>
    <li class="fragment fade-up">Containers may depend on each other, and reference configurations from each other</li>
  </ul>
  <p class="fragment fade-up font-thin"><i>Unless you need a lot of scalability, this is typically how you'll see microservices in the wild</i></p>
</Slide>

<Slide title="Docker Compose Example">
  <p>Here's an example of a Docker Compose file:</p>
  <Code trim={true} lineNumbers="1-36">
    {`
  version: "3.8"
  
  services:
    frontend:
      image: gitea.shrukanslab.xyz/tj-central-bank/web:latest
      ports:
        - "8080:8080"
      depends_on:
        - backend
      environment:
        - ORIGIN=http://localhost:8080
        - NODE_ENV=development
  
    backend:
      image: gitea.shrukanslab.xyz/tj-central-bank/backend:latest
      ports:
        - "5000:80"
      environment:
        - DATABASE_CONNECTION_STRING=Server=db,1433;User ID=SA;Password=YourStrong!Passw0rd;Database=BankDb;Trusted_Connection=True;TrustServerCertificate=True;Integrated Security=false;
        - JWT_SECRET_KEY=mysuperduperubereepykeepysecretkey
      depends_on:
        - db
  
    db:
      image: mcr.microsoft.com/mssql/server
      environment:
        - ACCEPT_EULA=Y
        - MSSQL_SA_PASSWORD=YourStrong!Passw0rd
        - MSSQL_PID=Express
      ports:
        - "1433:1433"
      volumes:
        - mssql-data:/var/opt/mssql
  
  volumes:
    mssql-data:
    `}
  </Code>
</Slide>

<Slide title="Building and Running">
  <p>To run the deployment, we'd run:</p>
  <Code trim={true}>
    {`
  docker-compose up -d
    `}
  </Code>
  <p>To stop the deployment, we'd run:</p>
  <Code trim={true}>
    {`
  docker-compose down
    `}
  </Code>
</Slide>
