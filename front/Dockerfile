FROM node:21 as build_step
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build -- --outputPath=./dist/out

FROM nginx as prod
COPY --from=build_step /app/dist/out/ /usr/share/nginx/html