FROM node:20-alpine as build_step
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build

FROM nginx as prod
COPY --from=build_step /app/dist/tlcfront /usr/share/nginx/html