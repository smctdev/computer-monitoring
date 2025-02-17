# Use an official Node runtime as a parent image
FROM node:16-alpine AS build

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json to the working directory
COPY ./package*.json ./

# Install the dependencies
RUN npm cache clean --force && npm install --force

# Copy the remaining application files to the working directory
COPY . .

# Build the application
RUN npm run build

# Use a minimal Node.js image to serve the static files
FROM node:16-alpine

# Install the `serve` package globally
RUN npm install -g serve

# Set the working directory to the app's build folder
WORKDIR /app

# Copy the build files from the previous stage
COPY --from=build /app/build /app/build

# Expose port 3000 (default for `serve`)
EXPOSE 9001

# Start the `serve` command to serve the static build
CMD ["serve", "-s", "build", "-l", "3000"]
