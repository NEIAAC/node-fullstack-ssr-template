FROM node:22

WORKDIR /api

COPY package*.json .

RUN npm i

COPY . .

RUN npm run build

ENTRYPOINT ["npm", "run", "start"]
