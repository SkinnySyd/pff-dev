#Build stage
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
# Install the npm dependencies.
RUN npm install 
# Copy the rest of the source code to the working directory.
COPY . .
# Run the production build of the application.
ARG configuration=production
 
RUN npm run build -outputPath=/app/dist/ --configuration=$configuration
# Dev build but we need prod

# Step 2: Run stage
FROM nginx:stable-alpine

COPY --from=build /app/dist /usr/share/nginx/html

COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Expose the port that nginx will use
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]