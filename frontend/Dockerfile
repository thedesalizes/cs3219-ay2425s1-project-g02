FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ARG VITE_QUESTION_SERVICE_BACKEND_URL

ENV VITE_QUESTION_SERVICE_BACKEND_URL=$VITE_QUESTION_SERVICE_BACKEND_URL

RUN npm run build

FROM nginx:alpine

COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
