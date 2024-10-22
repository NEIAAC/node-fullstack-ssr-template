# Template 📝📦

This is a template repository for small scale fullstack projects, with a focus on self-hosting.

The repository is a _monorepo_ but the project architecture is **not** a _monolith_, the API and frontend are different services and can even be further split into additional microservices, such as a separate auth service.

The base of this template focus on server side rendered (SSR) frontends, meaning the frontend is served by a server instead of as a static file. To use this template for a static frontend, e.g Vite only, simply remove the `docker-compose.override.yaml`/`docker-compose.yaml` at the root and the `Dockerfile`/`docker-compose.yaml` in the `frontend` directory. The docker script in the root `package.json` also becomes useless so it can be removed too.

**Note that this is a very initial stage of the template, as we are still migrating some of our best project architecture practices from internal projects to this repository. Currently this template should be used for the file structure, base workflows and docker utilities it provides.**

## Requirements 📋

- Node 22.0.0+
- Docker Engine 25.0.0+
- Docker Compose 2.24.0+

## Development 🛠️

- Clone the repository and open a terminal **inside** it.

- Install the dependencies:

    ```bash
    npm i

    # Note that when installing dependencies pre-commit hooks will also be installed.

    # This means that commits will fail if they don't pass the lint/format checks.
    ```

- Inside either the `frontend` or `backend` directory, run the following commands to perform a lint/format check and auto fix all possible issues:

    ```bash
    npm run check
    ```

### Backend 🗄️

- Create a `.env` file inside the `frontend` directory based on the `.env.example` file.

- Start only the database from the docker compose file:

    ```bash
    cd backend

    docker compose up --force-recreate database

    # This service has a volume, meaning the database retains it's contents between rebuilds and restarts.

    # The --force-recreate flag will restart the container if it is already running!
    ```

- Start the API:

    ```bash
    cd backend
    npm run dev
    ```

### Frontend 🖥️

- Create a `.env` file inside the `frontend` directory based on the `.env.example` file.

- Start the website:

    ```bash
    cd frontend
    npm run dev
    ```

## Deployment 🚀

- Setup the environment variables used in the development phase.

- Deploy the entire stack in the **background** with the root utility script:

    ```bash
    npm run docker
    ```

- All services are defined with the `restart: unless-stopped` compose flag, meaning they will restart any time they fail/crash, this includes systems restarts. What this essentially accomplishes is a hands-off management of the deployment since maintenance will be done automatically along with the system.
