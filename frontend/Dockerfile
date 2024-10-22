FROM node:22

WORKDIR /website

COPY package*.json .

RUN npm ci

COPY . .

RUN npm run build

ENTRYPOINT ["npm", "run", "start"]
