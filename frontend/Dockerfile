# ---------------------------
# Stage 1: Build Angular App
# ---------------------------
FROM node:18-alpine AS build

WORKDIR /app

# Copy package files first (for caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy remaining project files
COPY . .

# Build Angular in production mode
RUN npm run build -- --configuration production


# ---------------------------
# Stage 2: Serve with Nginx
# ---------------------------
FROM nginx:alpine

# Copy built Angular app to Nginx html folder
COPY --from=build /app/dist/angular-15-crud/ /usr/share/nginx/html

# Replace default Nginx config with custom reverse proxy config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
