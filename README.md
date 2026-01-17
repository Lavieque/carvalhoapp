# CarvalhoApp

A vehicle & maintenance management web application — server-rendered Node.js + Express app with EJS views. This repository contains the server, EJS templates and static assets used by CarvalhoApp.

Status: Prototype / work in progress

## Quick summary

- Platform: Node.js (engine declared: 15.x)
- Framework: Express
- Views: EJS templates (views/*.ejs)
- ORM / DB: Sequelize with mysql2 (MySQL)
- Dev tooling: nodemon (dev)
- Deployment hint: Procfile present (`web:node app.js`) — ready for Heroku-style deployments

## Table of contents

- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Development & Running](#development--running)
- [Production / Deployment](#production--deployment)
- [Database](#database)
- [Project layout](#project-layout)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Requirements

- Node.js (15.x is declared in package.json; use a compatible LTS if you prefer, e.g. 16/18)
- npm (or yarn)
- MySQL server (or a compatible MySQL instance), if you plan to use the database features

## Installation

1. Clone the repository
   git clone https://github.com/Lavieque/carvalhoapp.git
   cd carvalhoapp

2. Install dependencies
   npm install

3. Create env file
   Copy the example (if present) or create a `.env` file with the required variables (see Configuration below).

## Configuration

The app expects environment variables for DB and runtime configuration. Typical variables to set in `.env`:

- PORT — port to run the web server (default used in app: 8000)
- NODE_ENV — `development` or `production`
- DB_HOST — database host (e.g. localhost)
- DB_PORT — database port (default 3306)
- DB_USER — database user
- DB_PASSWORD — database password
- DB_NAME — database name
- SESSION_SECRET — secret for express-session (if sessions used)
- Any other API keys or secrets your app uses

Note: I inferred DB usage from dependencies (`mysql2`, `sequelize`), but search may be incomplete — check your configuration files or DB initialization code for exact env names.

## Development & Running

Development (uses nodemon as defined in package.json):
- npm run start
  - package.json `start` currently runs `nodemon app.js`. If you prefer `npm run dev` add a script accordingly.

Run directly with Node (production):
- node app.js

The repository also contains a Procfile:
- web: node app.js
This indicates the app can be deployed on Heroku-like platforms.

## Production / Deployment

Suggested Heroku steps (Procfile already included):
- heroku create
- git push heroku main
- heroku config:set DB_HOST=... DB_USER=... DB_PASSWORD=... DB_NAME=...
- heroku open

Docker (optional):
- Create a Dockerfile (not present by default). Example:
  - FROM node:16
  - WORKDIR /usr/src/app
  - COPY package*.json ./
  - RUN npm install --production
  - COPY . .
  - ENV PORT=8000
  - EXPOSE 8000
  - CMD ["node", "app.js"]

## Database

This project includes Sequelize + mysql2 as dependencies. Typical workflow:
- Create your MySQL database
- Set DB env vars (DB_HOST, DB_USER, etc.)
- Run any migrations or seed scripts if present (I did not detect migrations in search)

If you use Sequelize CLI or migrations, add relevant scripts in `package.json` (e.g. `sequelize db:migrate`).

## Project layout (high level)

- App.js — main Express application entrypoint
- package.json — dependencies and scripts (start uses nodemon)
- Procfile — `web:node app.js` (Heroku)
- routes/ — Express route handlers (e.g. viatura, inspecao, maquina, etc.)
- views/ — EJS templates (UI pages)
- assets/ — static CSS/JS/images (HTML5 UP theme assets are included)
- README.md — this file

## Testing

No automated tests detected in package.json. The `test` script currently exits with an error placeholder. Add test tooling (Jest/Mocha) and update `package.json` to include test scripts.
