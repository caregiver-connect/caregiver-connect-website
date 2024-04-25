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

External Dependency Notice
As mentioned earlier, this application makes significant use of the Sendgrid and Geoapify APIs, and will not maintain complete function without these dependencies. Both offer limited free tiers of their APIs, which should allow for initial implementation and experimentation, but we suggest purchasing a more sufficient license to meet the request needs of the implemented application and to follow licensing rules and regulations in production.
