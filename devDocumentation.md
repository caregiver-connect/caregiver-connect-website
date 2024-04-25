# Developer Documentation

## Installing and Deploying Caregiver Connect
Overview
Caregiver Connect is built on a scalable and easy-to-use infrastructure, allowing for easy installation, modification, and deployment. By leveraging containerization technologies, Caregiver Connect provides a simple platform for deploying Caregiver Connect applications and services.
Necessary Hardware/Software
The Caregiver Connect technology stack is designed to work on a single web-connected machine, whether a self-hosted server or a cloud-deployable host. Regardless of the hosting platform, please ensure that a secure and up-to-date version of your preferred operating system has been installed, along with Docker, Docker Compose, and all the necessary dependencies. This project also makes heavy use of the Geoapify and Sendgrid APIS, so API keys for both dependencies will need to be obtained. Following the installation of these dependencies, ensure that at least one port on the hosting machine is accessible, as this will be the port from which the front-end web pages are served. This requirement may be skipped via a reverse proxy, such as Nginx, following external guidance.
Installation
The installation and use of Caregiver Connect have been designed to be simple. To do so, simply clone the caregiver-connect repository (https://github.com/caregiver-connect/caregiver-connect) on the host machine. Then, the required environment variables must be assigned. To do this, create the file .env in the root directory of the project and copy the following environment variables format:
```
# DATABASE
POSTGRES_USER=
POSTGRES_PASSWORD=
POSTGRES_HOST_AUTH_METHOD=trust
POSTGRES_DB=

# BACKEND & SENDGRID
HOSTNAME=
SECRETKEY=
DB_SCHEMA=
DB_USER=
DB_PASSWORD=
DB_HOST=
SENDGRID_API_KEY=
GEOAPIFY_API_KEY=

# FRONTEND
TOKEN_SECRET=
```
Following each environment variable, define the intended value for the login information and provide the API keys for Sendgrid and Geoapify. For hosting on a local machine, set HOSTNAME equal to http://localhost. For hosting on a server, change localhost to the servers domain name.

Then, install docker and in the root directory, run docker compose up. This command should automatically pull the database, Postgres, Nginx, and openssl containers and build the front and back end before launching the complete stack. The stack can then be taken down with docker compose down.

To improve the ease of use and handle challenges with image rebuilds and relaunching the tech stack, several scripts have also been provided in the repository for easy execution of common functions. These scripts allow the stack to be launched, relaunched and closed using docker-launch.sh, docker-relauch.sh, and docker-close.sh.

Note: It seems that in most cases the first time the docker containers are brought up there is an error with the caregiver-backend container. Just take the containers down with docker compose down and bring them back up with docker compose up.

## External Dependency Notice:

As mentioned earlier, this application makes significant use of the Sendgrid and Geoapify APIs, and will not maintain complete function without these dependencies. Both offer limited free tiers of their APIs, which should allow for initial implementation and experimentation, but we suggest purchasing a more sufficient license to meet the request needs of the implemented application and to follow licensing rules and regulations in production.


# Modifying and Extending the Software
## Tech Stack
The front end uses the Vue framework with Ionic for UI components and themeing. The backend node.js server connects to the postgreSQL database using sequelize.

All dependencies are listed in the ./package.json, ./provider-nodejs/package.json section of this documentation. We also depend on the geoapify and sendgrid APIs as mentioned in the installation section.

## Modifying Existing Software
To modify different parts of the project look in the following files and directories:
```
Vue/Ionic Frontend: ./src
Backend NodeJS server: ./provider-nodejs
Docker Configuration: ./docker-compose.yml, ./docker-compose-postgres.yml (for postgres database container), ./Dockerfile (For frontend containter), ./provider-nodejs/Dockerfile (for backend nodejs container)
Styling
Utilize Ionic for UI components to keep styling consistent. The primary and secondary colors swap when changing to dark mode. The crimson color does not change.
```
## Testing
Most automated testing is done through a semaphore workflow, focusing on build testing. There is also the opportunity to expand on this testing in the future by adding a JWT containerized testing platform to the Semaphore workflow. The current build testing platform allows for independent build testing of both the front and back ends. This build testing involves creating a new container, installing all the necessary dependencies, building the project with npm, then installing the container and running it for a short period to ensure it is properly built without any errors. The build testing is also directly integrated with Github for continuous integration. Every commit is build-checked using the semaphore workflow and indicates whether or not the build has passed. Individual build workflows can be defined in the future for new branches or components simply by editing the semaphore workflow page.

Test cases are located in ./tests/testcases.md

## Bugs and Possible New Features
### Known bugs and security issues:

When the docker containers are created and ran for the first time, the nodejs backend server errors and fails.
Reseting a password hashes the password but the salting is different so the user cannot login again after the reset.
Sendgrid won't send emails to crimson.ua.edu emails (this may not be able to be fixed)
Building the application with Ionic build does not work.
Https is not implemented.
CSRF middleware does not work to protect against CSRF attacks.


### Possible features to add:

Adding an unverified edits table to allow users to edit/delete providers. Edits would then be approved or denied by the community and applied to the provider table after a certain number/ratio of approvals are recieved. This would require extensive edits to the database schema and creation of a new database table. Merge conflicts would also have to be resolved.

Automatic periodic backups of the database.

Automatic loading of the database from a backup/file.

Seperate services table with more details on the services a provider offers.

Ability to delete a user.

Ability for users to indicate when they use a provider or service and see the number of users that have used a provider or resource recently.

SMS messaging for phone number verification.

Emailing providers to encourage them to make edits/updates to their own information on services they provide.

Map with providers.
