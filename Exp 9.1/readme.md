.

🧩 Folder Structure dockerized-react-app/ │ ├── Dockerfile ├── .dockerignore ├── package.json ├── package-lock.json └── src/ ├── index.js └── App.js

⚛️ Step 1: React Application Code src/App.js import React from "react";

function App() { return ( <div style={{ textAlign: "center", marginTop: "50px" }}>

🚀 Dockerized React App
This React app is running inside a Docker container using a multi-stage build!

); }
export default App;

src/index.js import React from "react"; import ReactDOM from "react-dom/client"; import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root")); root.render();

package.json

(If not created by Create React App)

{ "name": "dockerized-react-app", "version": "1.0.0", "private": true, "dependencies": { "react": "^18.3.1", "react-dom": "^18.3.1", "react-scripts": "5.0.1" }, "scripts": { "start": "react-scripts start", "build": "react-scripts build", "test": "react-scripts test", "eject": "react-scripts eject" } }

🐳 Step 2: .dockerignore node_modules build .git .gitignore Dockerfile .dockerignore npm-debug.log

🧱 Step 3: Dockerfile (Multi-Stage Build)

---------- Stage 1: Build the React app ----------
FROM node:18 AS build

WORKDIR /app COPY package*.json ./ RUN npm install COPY . . RUN npm run build

---------- Stage 2: Serve the app with Nginx ----------
FROM nginx:stable-alpine

Copy the production build to Nginx html directory
COPY --from=build /app/build /usr/share/nginx/html

Expose port 80
EXPOSE 80

Start Nginx server
CMD ["nginx", "-g", "daemon off;"]

⚙️ Step 4: Build and Run Commands 🏗️ Build the Docker Image docker build -t react-multistage-app .

🚀 Run the Container docker run -d -p 80:80 react-multistage-app

Then open your browser and visit: 👉 http://localhost

✅ Expected Output

A webpage displaying:

🚀 Dockerized React App This React app is running inside a Docker container using a multi-stage build!
