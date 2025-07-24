FROM node:16.20-alpine
LABEL maintainer="DevOps Team"
LABEL description="Dockerfile for DevOps Stage 2 Frontend"
WORKDIR /app
COPY package*.json ./   
RUN npm install --silent
COPY . .            
EXPOSE 5173
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]