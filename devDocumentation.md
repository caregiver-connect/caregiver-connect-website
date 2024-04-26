# Developer Documentation

## Installing and Deploying Caregiver Connect
### Overview
Caregiver Connect is built on a scalable and easy-to-use infrastructure, allowing easy installation, modification, and deployment. By leveraging containerization technologies, Caregiver Connect provides a simple platform for deploying Caregiver Connect applications and services.
### Necessary Hardware/Software
The Caregiver Connect technology stack is designed to work on a single web-connected machine, whether a self-hosted server or a cloud-deployable host. Regardless of the hosting platform, please ensure that a secure and up-to-date version of your preferred operating system has been installed, along with [Docker](https://www.docker.com/get-started/), Docker Compose, and all the necessary dependencies. This should be completed automatically. This project also makes heavy use of the [Geoapify](https://apidocs.geoapify.com/#docs) and [Sendgrid](https://sendgrid.com/en-us/solutions/email-api) APIS, so API keys for both dependencies will need to be obtained. Following the installation of these dependencies, ensure that at least one port on the hosting machine is accessible, as this will be the port from which the front-end web pages are served. Following external guidance, this requirement may be skipped via a reverse proxy, such as Nginx.

### Installation
The installation and use of Caregiver Connect have been designed to be simple. To do so, clone the caregiver-connect repository (https://github.com/caregiver-connect/caregiver-connect) on the host machine. To ensure that string variable errors are not present in the CORS setup, navigate to `caregiver-connect/provider-nodejs/server.js` and replace the URL in `var whitelist = ['http://cs495-spring2024-09.ua.edu']` with the IP or hostname of the server host. This is the only necessary code change for the application to function, as using an environment variable has yielded string-end issues with different operating systems. Then, the required environment variables must be assigned. To do this, create the file .env in the root directory of the project and copy the following environment variables format:
```yaml
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
Following each environment variable, define the intended value for the login information and provide the API keys for Sendgrid and Geoapify. For hosting on a local machine, set `HOSTNAME` equal to `http://localhost`. To host on a server, change localhost to the server's domain name.

Then, install Docker and run `docker compose up` in the root directory. This command should automatically pull the database, Postgres, Nginx, and OpenSSL containers and build the front and back end before launching the complete stack. The stack can then be taken down with `docker compose down`.

To improve the ease of use and handle challenges with image rebuilds and relaunching the tech stack, several scripts have also been provided in the repository for easy execution of common functions. These scripts allow the stack to be launched, relaunched and closed using `docker-launch.sh, docker-relauch.sh, and docker-close.sh`.

For security, a default admin user does not exist, and must be created in order to access the admin page and execute admin functions. On first initialization, a standard user, made through the signup page, must be converted to an admin account. To do this, launch the stack and using `docker exec -it postgres /bin/bash` enter the bash terminal of the postgres container. Then, after connecting to the container, use `psql -U postgres` to enter the postgres query terminal. Connect to the database containing the user table (defined by `POSTGRES_DB`) and using the following short SQL script, set a standard user to an admin user:
```sql
UPDATE user
SET role=admin
WHERE username='your-username'; 
```
Other queries may also be used to add, remove, or change other users, however, after initializing the first admin user, all future admin users can be added from the admin page.

Note: It seems that in most cases, the first time or initialization, the docker containers are brought up, and there is an error with the caregiver-backend container. Just take the containers down with `docker compose down` and bring them back up with `docker compose up` or use `docker-relaunch.sh`.

### External Dependency Notice
As mentioned, this application significantly uses the Sendgrid and Geoapify APIs and will not maintain complete function without these dependencies. Both offer limited free tiers of their APIs, which should allow for initial implementation and experimentation. Still, we suggest purchasing a more sufficient license to meet the request needs of the implemented application and to follow licensing rules and regulations in production.


## Modifying and Extending the Software
### Tech Stack
The front end uses the Vue framework with Ionic for UI components and themeing. The backend node.js server connects to the postgreSQL database using sequelize.

All dependencies are listed in the `./package.json, ./provider-nodejs/package.json` section of this documentation. We also depend on the geoapify and sendgrid APIs as mentioned in the installation section.

### Modifying Existing Software
To modify different parts of the project look in the following files and directories:

- Vue/Ionic Frontend and calls to backend APIs: `./src`
- Backend NodeJS server: `./provider-nodejs/server.js`
- API routes: `./provider-nodejs/app/routes`
- API controllers:` ./provider-nodejs/app/controllers`
- Database schemas for user and provider tables: `./provider-nodejs/app/models`
- Docker Configuration: ./docker-compose.yml,` ./docker-compose-postgres.yml` (for postgres database container), `./Dockerfile` (For frontend containter), `./provider-nodejs/Dockerfile` (for backend nodejs container)

#### Hard Coded Values
- pageSize in `./src/views/ProviderSearch.vue` and `./src/views/AdminPage.vue` controls the number of database entries shown on each page of the provider search and admin pages.
- The website hostname is hardcoded in the whitelist variable in `./provider-nodejs/server.js` that is then used for CORS options.
- The list of services that can be checked as offered by a provider is hard coded in `./src/views/AddProvider.vue` and `./src/views/EditProvider.vue` in the `allServices` dictionary in `data()`. To edit these, you can add a specific service to a service type within the `services_with_other` or `services_without_other` in `allServices`. To add a service type without an `other` checkbox, simply add it as a dictionary to the services_without_other object. To add a service type with an `other` checkbox, do the same with the services_with_other except be sure to add a key-value pair for `other_checked` and `specific`.
- The initial value for user roles is assigned in `./provider-nodejs/app/controllers/user.controller.js` when the user variable is created in the create function.
- The options for user roles is hardcoded in the `ion-popover` HTML element in `./src/views/AdminPage.vue`

### Styling
Utilize Ionic for UI components to keep styling consistent. The primary and secondary colors swap when changing to dark mode. The crimson color does not change. Themeing, as well as global CSS, is found in `./src/theme/variables.css`

### Testing
Most automated testing is done through a semaphore workflow, focusing on build testing. There is also the opportunity to expand on this testing by adding a JWT containerized testing platform to the Semaphore workflow. The current build testing platform allows for independent build testing of both the front and back ends. This build testing involves creating a new container, installing all the necessary dependencies, building the project with npm, then installing the container and running it for a short period to ensure it is properly built without any errors. The build testing is also directly integrated with Github for continuous integration. Every commit is build-checked using the semaphore workflow, indicating whether the build has passed. Individual build workflows can be defined in the future for new branches or components simply by editing the semaphore workflow page.

Test cases are located in `./tests/testcases.md`

### Bugs and Possible New Features
#### Known bugs and security issues:

- When the docker containers are created and ran for the first time, the nodejs backend server errors and fails.
- Reseting a password hashes the password but the salting is different so the user cannot login again after the reset.
- Sendgrid won't send emails to crimson.ua.edu emails (this may not be able to be fixed)
- Building the application with Ionic build does not work.
- Https is not implemented.
- CSRF middleware does not work to protect against Cross-Site Request Forgery attacks.


#### Possible features to add:

- Adding an unverified edits table allows users to edit/delete providers. The community would then approve or deny edits and apply them to the provider table after a certain number/ratio of approvals are received. This would require extensive edits to the database schema and the creation of a new database table. Merge conflicts would also have to be resolved.
- Automatic periodic backups of the database.
- Automatically load the database from a backup/file.
- Provide a separate services table with more details on the provider's services.
- Ability to delete a user.
- Ability for users to indicate when they use a provider or service and see the number of users that have used a provider or resource recently.
- SMS messaging for phone number verification.
- Emailing providers to encourage them to make edits/updates to their own information on their services.
- Map with providers.
