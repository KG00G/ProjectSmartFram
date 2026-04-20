FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install express cors mysql2 bcryptjs jsonwebtoken
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
