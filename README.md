# Template 📝📦

This is a template repository for all self-hosted fullstack needs.

## Requirements 📋

- Node 22.0.0+
- Docker Engine 25.0.0+
- Docker Compose 2.24.0+

## Development 🛠️

- Clone the repository and open a terminal **inside** it.

### Backend 🗄️

- Start only the database from the docker compose file:

```bash
cd backend
# The --force-recreate flag will restart the container if it is already running!
docker compose up --force-recreate database
```

- Start the API:

```bash
cd backend
npm run dev
```

### Frontend 🖥️

- Start the website:

```bash
cd frontend
npm run dev
```

## Deploy 🚀

TODO
