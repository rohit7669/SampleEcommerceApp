# -----------------------------
# Stage 1: Build Angular app
# -----------------------------
FROM node:18-alpine AS build
WORKDIR /app

# Copy package.json and package-lock.json to install dependencies
COPY package*.json ./
RUN npm install

# Copy all frontend source code
COPY . .

# Build Angular app for production
# The output folder will be: dist/<angular-app-name>
RUN npm run build -- --configuration production

# -----------------------------
# Stage 2: Serve with NGINX
# -----------------------------
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Remove default nginx content
RUN rm -rf ./*

# Copy built Angular app to nginx html folder
# Replace 'your-app-name' with the actual folder inside dist/
COPY --from=build /app/dist/my-store ./

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
