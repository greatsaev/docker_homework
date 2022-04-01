FROM node:14 as builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build


FROM nginx
RUN sed -i '/index.html index.htm;/a \\ttry_files $uri $uri/ /index.html;' /etc/nginx/conf.d/default.conf
COPY --from=builder /usr/src/app/build/ /usr/share/nginx/html
HEALTHCHECK --interval=60s --timeout=30s --start-period=5s --retries=3 CMD curl --fail http://localhost || exit 1