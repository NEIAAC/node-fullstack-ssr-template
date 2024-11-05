# Template 📝📦

This is a template repository for small scale fullstack projects, with a focus on self-hosting.

The repository is a _monorepo_ but the project architecture is **not** a _monolith_, the API and frontend are different services and can even be further split into additional microservices, such as a separate auth service.

**Note that this is a very initial stage of the template, as we are still migrating some of our best project architecture practices from internal projects to this repository. Currently this template should be used for the file structure, base workflows and docker utilities it provides.**

### Notice 🚨

The base of this template focus on server side rendered (SSR) frontends, meaning the frontend is served by a server instead of as a static file. To use this template for a static frontend builder, e.g Vite only, simply remove the `docker-compose.override.yaml`/`docker-compose.yaml` at the root and the `Dockerfile`/`docker-compose.yaml` in the `frontend` directory. The docker script in the root `package.json` also becomes useless so it can be removed too.

## Requirements 📋

- Node 22.0.0+
- Docker Engine 25.0.0+
- Docker Compose 2.24.0+

## Development 🛠️

- Clone the repository and open a terminal **inside** it.

- Install the dependencies:

    ```shell
    npm i

    # Note that when installing dependencies pre-commit hooks will also be installed.

    # This means that commits will fail if they don't pass the lint/format checks.
    ```

- Inside either the `frontend` or `backend` directory, run the following commands to perform a lint/format check and auto fix all possible issues:

    ```shell
    npm run check
    ```

### Backend 🗄️

- Create a `.env` file inside the `backend` directory based on the `.env.example` file.

- Start only the database from the docker compose file:

    ```shell
    cd backend

    docker compose up --force-recreate database

    # Using the --force-recreate flag will restart the container if it is already running!

    # The volume in this service ensures the database keeps data between rebuilds and restarts.
    ```

- Start the API:

    ```shell
    cd backend
    npm run dev
    ```

### Frontend 🖥️

- Create a `.env` file inside the `frontend` directory based on the `.env.example` file.

- Start the website:

    ```shell
    cd frontend
    npm run dev
    ```

### Tooling 🧰

- Biome is used as a linter and formatter:

    ```shell
    # In both the frontend and backend!
    npm run check

    # When installing dependencies, pre-commit hooks are added to lint and format automatically.
    # If for some reason the hooks do not install correctly, do it manually:
    npx lefthook install

    # When using pre-commit hooks, git commands will fail if any files are checked with errors.
    # Changed files must be added to the staged area and commited again to apply fixes.
    ```

## Deployment 🚀

- Setup the environment variables used in the development phase.

- Deploy the entire stack in the **background** with the root utility script:

    ```shell
    npm run docker

    # The --build flag will ensure the latest code is used for each container.

    # All services are defined with the "restart: unless-stopped" compose flag.
    # This means they will restart anytime they fail, including for systems restarts.
    # Defining this flag ensures the services are automatically re-available as soon as possible.
    ```
- Serve the port of each service using a reverse proxy.
