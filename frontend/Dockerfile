# Stage 1: Build the application
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Install dependencies first for layer caching
COPY package*.json ./
RUN npm install

# Copy the rest of the code and build the project
COPY . .
# Note: If you are using Vite, the output folder is usually 'dist'. 
# If you are using Create React App, it is 'build'.
RUN npm run build 

# Stage 2: Serve the application with Nginx
FROM nginx:alpine

# Remove the default Nginx configuration
RUN rm /etc/nginx/conf.d/default.conf

# Copy our custom configuration file
COPY nginx.conf /etc/nginx/conf.d/

# Copy the built assets
COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]