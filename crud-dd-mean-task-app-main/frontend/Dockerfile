FROM node:18 as build

WORKDIR /app

COPY package*.json ./

# Fix network timeout issue
RUN npm config set fetch-retries 5
RUN npm config set fetch-retry-mintimeout 20000
RUN npm config set fetch-retry-maxtimeout 120000

RUN npm install

COPY . .

RUN npm run build --prod

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80