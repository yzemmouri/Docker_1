FROM node:12

WORKDIR /app

COPY ./nodeappweb/package*.json ./

RUN npm install

COPY ./nodeappweb .

EXPOSE 8080

CMD [ "node", "server.js" ]
#docker run — name node_app -p 8080:8080 -d 

#https://github.com/javahometech/nodeappweb.git