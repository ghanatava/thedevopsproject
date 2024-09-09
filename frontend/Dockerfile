FROM node:alpine AS BUILDER

WORKDIR /app
COPY package*.json .
RUN npm install

COPY . .

RUN npm run build

FROM nginx:alpine AS Runner

WORKDIR /app
COPY --from=BUILDER /app/build /app/build

COPY ./custom.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
