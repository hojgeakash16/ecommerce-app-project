# -----------Stage 1 : Build the image ----------------

# Get the base image
FROM node:22-alpine AS builder

# Create the working directory
WORKDIR /app

ARG VITE_API_BASE_URL
ENV VITE_API_BASE_URL=$VITE_API_BASE_URL

# Copy the source code
COPY . .

# Install the dependencies
RUN npm install --legacy-peer-deps

# Run the build image
RUN npm run build 


# ----------Stage 2 : Run with optimised image -----------

# Get the optimised image
FROM nginx:alpine AS runner

# Get the working directory
WORKDIR /app

# Copy from the builder
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose the port
EXPOSE 80

# Run the application
CMD ["nginx", "-g", "daemon off;"]
