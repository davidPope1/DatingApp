# Stage 1: Build the Angular app using Node.js: 18
FROM node:18 AS build 

WORKDIR /app 

# Copy Angular project files and install dependencies 
COPY package.json ./

RUN npm install --force 

# Build the Angular app 
COPY . .

RUN npm run build

# Stage 2: Use Nginx to serve the Angular app
FROM nginx:latest 

WORKDIR /usr/share/nginx/html 

# Remove the default Nginx static files 
RUN rm -rf ./* 

# Copy the built Angular app from the build stage
COPY --from=build /app/dist/client ./ 

# Expose port 8080 for the frontend 
EXPOSE 8080 

# Start Nginx to serve the Angular app
CMD [ "nginx", "-g", "daemon off;" ]