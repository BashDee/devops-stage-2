# Stage 1: Build the React app
FROM node:14 as build
WORKDIR /app
COPY package.json ./
RUN npm install
# RUN yarn install
COPY . .
RUN npm run build
# RUN npm run dev
# RUN yarn build

RUN npm install -g serve


# Set the environment variables (ensure .env is correctly set)
COPY .env .env

# Run the command to serve the application
CMD ["serve", "-s", "build"]

# Expose the port the app runs on
EXPOSE 80