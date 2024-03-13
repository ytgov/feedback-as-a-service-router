# YG feedback as a service router

API component to route feedback securely from websites hosted in the cloud to a final destination.

## Development

Before starting the API server, you need to create the appropriate .env file which can be done by running `cp src/api/.env.sample src/api/.env.development`. You must then set the appropriate values

To develop within this environment, you must have Node.js and NPM installed on your development machine. Open a terminal windows to `/src/api`, the API back-end can be started with: `npm run start:dev`.

## Understanding the environment variables

Environment variables should never be checked into the repository! 

- API_PORT=(the port the API will be listening on (doesn't have to match the docker port))
- SMTP_SERVER= (The host of your outgoing SMTP server.)
- SMTP_PORT=(SMTP Port)
- EMAIL_FROM=(The e-mail address that all e-mails will be from.)
- NAME_FROM= (The name that all e-mails will be from.)
- EMAIL_SUBJECT= (The  e-mail subject.)
- EMAIL_TO= (The e-mail address that all e-mails will be to.)
- EMAIL_DEFAULT= (the email to be sent to by default if the domain is not set as constant; don't forget to add this constant)
- {{domain}}={{email}}
  - i.e. dev-d-10-modules.pantheonsite.io=mariazel@bizont.ca

## Building the container image

`docker-compose -f docker-compose.production.yml up --build -d`

## Running the container in test or production

By default, the container will run in development mode, but following the step above, you can create the appropriate environment files for the instance you are targetting. Depending, the application will look for either `src/api/.env.test` or `src/api/.env` . To tell the API which instance to use, add the environment variable `NODE_ENV` to the docker run command like below.


`docker run -p 8080:3000 -e NODE_ENV=production --restart=on-failure feedback-as-a-service-router`