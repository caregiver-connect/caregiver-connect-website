
<h1 align="center">Our Goals</h1>
&nbsp;&nbsp;&nbsp;&nbsp; Our goal with Caregiver Connect is to create a service that would allow dementia patients and their caregivers the ability to search for caregiving services around them in the state of Alabama. We also would like to allow the community 
to be able to post any services that they find to Caregiver Connect.


<h2 align="center">Presentation and Code</h2>
[Click to view code.](https://github.com/caregiver-connect/caregiver-connect)

[Sprint 1 Presentation.](https://docs.google.com/presentation/d/1_thqBdY25fl19qdwpz-_1uIeUIzq8nOBMN4Q-_7fEos/edit?usp=sharing)
[Sprint 2 Presentation.](https://docs.google.com/presentation/d/1YA5GQ_Ipm-DqST1Csk8MmjwrnBMqo-BcD-LRmM81E3c/edit?usp=sharing)


<h2 align="center">Documentation</h2>
<h3>Installing and Deploying Caregiver Connect</h3>
<h4 align ="center">Overview</h4>
Caregiver Connect is built on a scalable and easy-to-use infrastructure, allowing for easy installation, modification, and deployment. By leveraging containerization technologies, Caregiver Connect provides a simple platform for deploying Caregiver Connect applications and services.
<h4 align ="center">Necessary Hardware/Software</h4>
The Caregiver Connect technology stack is designed to work on a single web-connected machine, whether a self-hosted server or a cloud-deployable host. Regardless of the hosting platform, please ensure that a secure and up-to-date version of Linux has been installed, along with Docker, Docker Compose, and all the necessary dependencies. This project also makes heavy use of the Geoapify and Sendgrid APIS, so API keys for both dependencies will need to be obtained. Following the installation of these dependencies, ensure that at least one port on the hosting machine is accessible, as this will be the port from which the front-end web pages are served. This requirement may be skipped via a reverse proxy, such as Nginx, following external guidance.

<h4 align ="center">Installation</h4>

The installation and use of Caregiver Connect have been designed to be simple. To do so, simply clone the caregiver-connect repository (https://github.com/caregiver-connect/caregiver-connect) on the host machine.
Then, the required environment variables must be assigned. To do this, create the file `.env` in the root directory of the project and copy the following environment variables format:

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

Following each environment variable, define the intended value for the login information and provide the API keys for Sendgrid and Geoapify.

Then, [install docker](https://docs.docker.com/get-docker/) and in the root directory, run `docker compose up`. This command should automatically pull the database, Postgres, Nginx, and openssl containers and build the front and back end before launching the complete stack. The stack can then be taken down with `docker compose down`.

To improve the ease of use and handle challenges with image rebuilds and relaunching the tech stack, several scripts have also been provided in the repository for easy execution of common functions. These scripts allow the stack to be launched, relaunched and closed using `docker-launch.sh`, `docker-relauch.sh`, and `docker-close.sh`.

Note: It seems that in most cases the first time the docker containers are brought up there is an error with the caregiver-backend container. Just take the containers down with `docker compose down` and bring them back up with `docker compose up`.

<h4 align ="center">External Dependency Notice</h4>
As mentioned earlier, this application makes significant use of the Sendgrid and Geoapify APIs, and will not maintain complete function without these dependencies. Both offer limited free tiers of their APIs, which should allow for initial implementation and experimentation, but we suggest purchasing a more sufficient license to meet the request needs of the implemented application and to follow licensing rules and regulations in production.
  
<h3>Features</h3>
<h4 align ="center">Core Features</h4>
<p> Our core features consist of user signup, user login, adding a provider, admins editing/deleting a provider, searching through the provider table, sending users verification emails, ability to reset password, and an admin page to view users and change user roles.</p>
<h5 align ="center">User Signup</h5>
<p>For user signup, the user clicks on the "signup" button in the top right of the home page. The user then inputs the required information. The user will then both be added to the user database and will recieve a verification email in the email they provided.</p>
<h5 align ="center">User Login</h5>
<p>For user login, the user clicks on the "login" button in the top right of the home page and then inputs their username and password. The user is then allowed to access features available to logged in users (adding providers).</p>
<h5 align ="center">Adding a Provider</h5>
<p>For adding a provider, the user first needs to be logged in. Then the user can click on the "Find Providers" button on the home page and then click the plus button in the bottom right of the "Find Providers" page, or the user can click on the "Add Providers" button on the home page. The user then needs to input the required information about the provider and once submitted will then be visible on the "Find Providers" page</p>

<h3>Modifying and Extending the Software</h3>
<h4 align="center">Tech Stack</h4>
<p>The front end uses the Vue framework with Ionic for UI components and themeing. The backend node.js server connects to the postgreSQL database using sequelize.</p>
<p>All dependencies are listed in the package.json or the Features->External Resources section of this documentation.</p>

<h3>FAQs</h3>


<h2 align="center">About Us</h2>

<h3 align="center">Logan Ladnier</h3>
<p align="center">I am a senior studying Computer Science and Math with a minor in Electrical Engineering. I will also be graduating with a Masters in Computer Science. My interests include software engineering and embedded systems engineering. I can be contacted at lcladnier@crimson.ua.edu</p>

<h3 align="center">Brent Christian</h3>
<p align="center">I am a senior studying math and computer science as well as working on my master's degree in CS through AMP.</p>

<h3 align="center">Mithul Nallaka</h3>
<p align="center">Hello! I'm Mithul and I'm a senior studying Computer Science and Biochemistry on the Pre-Med track. I'm looking forward to using technology to shape the future of healthcare.</p>

<h3 align="center">Jacob Curren</h3>
<p align="center">I am a senior studying Computer Science. I will be graduating this semester with a bachelor's degree. I can be contacted at jwcurren@crimson.ua.edu</p>
