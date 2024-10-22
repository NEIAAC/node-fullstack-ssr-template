FROM node:22

WORKDIR /api

COPY package*.json .

RUN npm ci

COPY . .

RUN npm run build

ENTRYPOINT ["npm", "run", "start"]
