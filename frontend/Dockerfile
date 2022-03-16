FROM node:14 as builder

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

EXPOSE 3000
ENTRYPOINT ["npm", "start"]
#CMD [ "node", "src/index.js" ]

FROM nginx
COPY --from=builder /usr/src/app/build/ /usr/share/nginx/html
COPY frontend.conf /etc/nginx/conf.d/default.conf
