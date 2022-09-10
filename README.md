# Step 2: Setting up the Javascript frontend
The frontend is a simple javascript project written using Vite, VueJS, TailwindCSS.

## Overview
Vite - Vite (French word for "quick", pronounced /vit/, like "veet") is a build tool that aims to provide a faster and leaner development experience for modern web projects.
VueJS - An approachable, performant and versatile framework for building web user interfaces.
TailwindCSS - A CSS framework to rapidly build modern websites without ever leaving your HTML.

#### 1. Clone this repository onto local
> Ensure you have nodejs v16.17.0 installed on your local. 
> You can install from the installer based on your platform present at the [official nodejs download page](https://nodejs.org/en/download/).
```shell
git clone https://github.com/psgganesh/sandboxing-with-websockets.git
git checkout step2
```

#### 2. Install dependencies
```shell
npm install
```
#### 3. Copy the `.env.example` and paste it as `.env` file at the root of the project
```shell
cp .env.example .env
```

#### 4. Bring up the local server
```shell
npm run dev
```
Open a new browser tab and navigate to `http://127.0.0.1:5173`.

In the next step we will build a chat layout and start using our backend built using SAM CLI.