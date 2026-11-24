FROM node:24-alpine AS base
WORKDIR /app
RUN apk add --no-cache curl
COPY package*.json ./
RUN npm ci
COPY prisma ./prisma/
RUN npx prisma generate
COPY . .

FROM base AS dev
USER node
CMD ["npm", "run", "dev"]

FROM base AS prod
RUN npm run build
USER node
CMD ["npm", "run", "start"]
