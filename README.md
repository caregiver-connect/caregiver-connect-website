
<h1 align="center">Our Goals</h1>
&nbsp;&nbsp;&nbsp;&nbsp; Our goal with Caregiver Connect is to create a service that would allow dementia patients and their caregivers the ability to search for caregiving services around them in the state of Alabama. We also would like to allow the community 
to post any services that they find on Caregiver Connect.


<h2 align="center">Presentation and Code</h2>
[Click to view code.](https://github.com/caregiver-connect/caregiver-connect)

[Sprint 1 Presentation.](https://docs.google.com/presentation/d/1_thqBdY25fl19qdwpz-_1uIeUIzq8nOBMN4Q-_7fEos/edit?usp=sharing)
[Sprint 2 Presentation.](https://docs.google.com/presentation/d/1YA5GQ_Ipm-DqST1Csk8MmjwrnBMqo-BcD-LRmM81E3c/edit?usp=sharing)
[Sprint 3 Presentation.](https://docs.google.com/presentation/d/1t7bWfc4SZc868H2hnkXAJyKo34jM_cEnY0eT2WhSIRk/edit#slide=id.g2cf2a67421e_0_25).

<h2 align="center">Full Demo Video</h2>
[Click to view video.](https://youtu.be/kU1p5HSiwIo)


<h2 align="center">Documentation</h2>
<h3>Installing and Deploying Caregiver Connect</h3>
<h4 align ="center">Overview</h4>
Caregiver Connect is built on a scalable and easy-to-use infrastructure, allowing for easy installation, modification, and deployment. By leveraging containerization technologies, Caregiver Connect provides a simple platform for deploying Caregiver Connect applications and services.
<h4 align ="center">Necessary Hardware/Software</h4>
The Caregiver Connect technology stack is designed to work on a single web-connected machine, whether a self-hosted server or a cloud-deployable host. Regardless of the hosting platform, please ensure that a secure and up-to-date version of your preferred operating system has been installed, along with Docker, Docker Compose, and all the necessary dependencies. This should be completed automatically. This project also makes heavy use of the <a href="https://apidocs.geoapify.com/#docs">Geoapify</a> and <a href="https://docs.sendgrid.com/for-developers/sending-email/api-getting-started">Sendgrid</a> APIS, so API keys for both dependencies will need to be obtained. Following the installation of these dependencies, ensure that at least one port on the hosting machine is accessible, as this will be the port from which the front-end web pages are served. Following external guidance, this requirement may be skipped via a reverse proxy, such as <a href="https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/"> Nginx.</a>


<h4 align ="center">Installation</h4>

The installation and use of Caregiver Connect have been designed to be simple. To do so, clone the caregiver-connect repository (https://github.com/caregiver-connect/caregiver-connect) on the host machine.
To ensure that string variable errors are not present in the CORS setup, navigate to `caregiver-connect/provider-nodejs/server.js` and replace the URL in `var whitelist = ['http://cs495-spring2024-09.ua.edu']` with the IP or hostname of the server host. This is the only necessary code change for the application to function, as using an environment variable has yielded string-end issues with different operating systems.
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

Following each environment variable, define the intended value for the login information and provide the API keys for Sendgrid and Geoapify. For hosting on a local machine, set `HOSTNAME` equal to `http://localhost`. To host on a server, change localhost to the server's domain name.

Then, [install docker](https://docs.docker.com/get-docker/) and in the root directory, run `docker compose up`. This command should automatically pull the database, Postgres, Nginx, and openssl containers and build the front and back end before launching the complete stack. The stack can then be taken down with `docker compose down`.

To improve the ease of use and handle challenges with image rebuilds and relaunching the tech stack, several scripts have also been provided in the repository for easy execution of common functions. These scripts allow the stack to be launched, relaunched, and closed using `docker-launch.sh`, `docker-relauch.sh`, and `docker-close.sh`.

Note: It seems that in most cases, the first time or initialization, the docker containers are brought up, and there is an error with the caregiver-backend container. Just take the containers down with `docker compose down` and bring them back up with `docker compose up` or use `docker-relaunch.sh`.

<h4 align ="center">External Dependency Notice</h4>
As mentioned, this application makes significant use of the Sendgrid and Geoapify APIs and will not maintain complete function without these dependencies. Both offer limited free tiers of their APIs, which should allow for initial implementation and experimentation, but we suggest purchasing a more sufficient license to meet the request needs of the implemented application and to follow licensing rules and regulations in production.
  
<h3>Features</h3>
<h4 align ="center">Core Features</h4>
<p> Our core features consist of user signup, user login, adding a provider, admins editing/deleting a provider, searching through the provider table, sending users verification emails, the ability to reset passwords, and an admin page to view users and change user roles.</p>
<h5 align ="center">User Signup</h5>
<p>For user signup, the user clicks on the "signup" button in the top right of the home page. The user then inputs the required information. The user will then both be added to the user database and will receive a verification email in the email they provided.</p>
<h5 align ="center">User Login</h5>
<p>For user login, the user clicks on the "login" button in the top right of the home page and then inputs their username and password. The user can then access features available to logged-in users (adding providers).</p>
<h5 align ="center">Adding a Provider</h5>
<p>For adding a provider, the user must first log in. Then, the user can click on the "Find Providers" button on the home page and then click the plus button in the bottom right of the "Find Providers" page, or the user can click on the "Add Providers" button on the home page. The user then needs to input the required information about the provider, and once submitted, it will then be visible on the "Find Providers" page</p>
<h5 align ="center">Editing/Deleting a Provider</h5>
<p> the user must be logged in as an admin for editing a provider. To edit a provider, the user can go to the "Find Providers" page, scroll to the right, hit the edit button, and then input the desired edits. To delete a provider, the user must go to the "Find Providers" page, scroll to the right, and then click the delete button.</p>
<h5 align ="center">Searching Through the Provider Table</h5>
<p>For searching through the provider table, the user needs to go to the "Find Providers" page; at the top of the page, there is a search bar where the user can input what they want to search and then click the search button. After clicking the search button and putting in their input, the provider table will list all the providers that contain the input.</p>
<h5 align ="center">Sending Verification Emails</h5>
<p>For sending verification emails, once the user creates an account, an email with a link to verify their account will be sent to the provided email.</p>
<h5 align ="center">Reseting Password</h5>
<p>For resetting a user's password, the user can navigate to the "login" page and click the forgot password. After inputting your username and email, an email will be sent to the user's email with a link to the reset password page, where they can put in a new password.</p>
<h5 align ="center">Admin Page</h5>
<p>For the admin page, the user must first be logged in as an admin, and they then can edit the URL from /home to /admin-page (if any other user goes to this URL, it will not show any users). On the admin page, the user can view all created users and can edit their roles by using the drop-down arrow in the roles column. Admins can also delete users by using that drop-down arrow or by clicking the "X" button on the far right side of each user.</p>
<h4 align ="center">External Resources</h4>
<p>In Caregiver Connect, we use two outside resources, GEOAPIFY and SENDGRID. We use GEOAPIFY when we add providers to the database to help ensure that the address/location the user inputs for the provider is correct. We use SENDGRID for our emails to verify user credentials and reset passwords.</p>

<h3>Modifying and Extending the Software</h3>
<h4 align="center">Tech Stack</h4>
<p>The front end uses the Vue framework with Ionic for UI components and themes. The backend node.js server connects to the PostgreSQL database using sequelize.</p>
<p>All dependencies are listed in the ./package.json, ./provider-nodejs/package.json or the Features->External Resources section of this documentation.</p>

<h4 align="center">Modifying Existing Software</h4>
<p>To modify different parts of the project, look in the following files and directories:</p>
<ul>
  <li>Vue/Ionic Frontend: ./src</li>
  <li>Backend NodeJS server: ./provider-nodejs</li>
  <li>Docker Configuration: ./docker-compose.yml, ./docker-compose-postgres.yml (for postgres database container), ./Dockerfile (For frontend containter), ./provider-nodejs/Dockerfile (for backend nodejs container)</li>
</ul>

<h4 align="center">Styling</h4>
<p>Utilize Ionic for UI components to keep styling consistent. The primary and secondary colors swap when changing to dark mode. The crimson color does not change.</p>

<h4 align="center">Testing</h4>
<p>Most automated testing is done through a semaphore workflow, focusing on build testing. There is also the opportunity to expand on this testing in the future by adding a JWT containerized testing platform to the Semaphore workflow. The current build testing platform allows for independent build testing of both the front and back ends. This build testing involves creating a new container, installing all the necessary dependencies, building the project with npm, then installing the container and running it for a short period to ensure it is properly built without any errors. The build testing is also directly integrated with Github for continuous integration. Every commit is build-checked using the semaphore workflow, indicating whether the build has passed. Individual build workflows can be defined in the future for new branches or components simply by editing the semaphore workflow page.</p>
<p>Test cases are located in ./tests/testcases.md</p>

<h4 align="center">Bugs and Possible New Features</h4>
<p>Known bugs and security issues:</p>
<ul>
  <li>When the docker containers are created and run for the first time, the Node-JS backend server errors and fails.</li>
  <li> Resetting a password hashes the password, but the salting is different, so the user cannot log in again after the reset.</li>
  <li>Sendgrid won't send emails to crimson.ua.edu emails (this may not be able to be fixed)</li>
  <li>Building the application with Ionic build does not work.</li>
  <li>Https is not implemented.</li>
  <li>CSRF middleware does not work to protect against CSRF attacks.</li>
</ul>
<p>Possible features to add:</p>
<ul>
  <li>Adding an unverified edits table to allow users to edit/delete providers. Edits would then be approved or denied by the community and applied to the provider table after receiving a certain number/ratio of approvals. This would require extensive edits to the database schema and the creation of a new database table. Merge conflicts would also have to be resolved.</li>
  <li>Automatic periodic backups of the database.</li>
  <li>Automatic loading of the database from a backup/file.</li>
  <li> Separate services table with more details on the provider's services.</li>
  <li>Ability to delete a user.</li>
  <li>Ability for users to indicate when they use a provider or service and see the number of users that have used a provider or resource recently.</li>
  <li>SMS messaging for phone number verification.</li>
  <li>Emailing providers to encourage them to make edits/updates to their own information on services they provide.</li>
  <li>Map with providers.</li>
</ul>

<h3>FAQs</h3>
<ul>
  <li><b>Q:</b> Do I need to make an account to use the website? <br> <b>A:</b> An account is only required if you want to add providers to the website and become a contribuer. You can find providers near you by clicking the "Find Providers" button on the homepage. </li>
  <li><b>Q:</b> What if I need to make an edit to a provider I have added? <br> <b>A:</b> Editing privileges are only given to admins, and they will moderate the website.</li>
  <li><b>Q</b>: Who is this website made for? <br> <b>A:</b> This website is made to assist senior citizens and dementia patients with finding caregivers near them. People who want to contribute can add any caregivers they know, even themselves, to the website.</li>
 <li><b>Q</b>: How do I know if the information is correct? <br> <b>A:</b> Admins will moderate the website and scan for entries with incorrect information.</li>
  <li><b>Q</b>: How do I access the admin page? <br> <b>A:</b> Currently, there is no button to navigate to the admin page. However, you can still access it by using the URL http://cs495-spring2024-09.ua.edu/admin-page</li>
</ul>


<h2 align="center">About Us</h2>

<h3 align="center">Logan Ladnier</h3>
<p align="center">I am a senior studying Computer Science and Math with a minor in Electrical Engineering. I will also be graduating with a Masters in Computer Science. My interests include software engineering and embedded systems engineering. I can be contacted at lcladnier@crimson.ua.edu</p>

<h3 align="center">Brent Christian</h3>
<p align="center">I am a senior studying math and computer science as well as working on my master's degree in CS through AMP.</p>

<h3 align="center">Mithul Nallaka</h3>
<p align="center">Hello! I'm Mithul and I'm a senior studying Computer Science and Biochemistry on the Pre-Med track. I'm looking forward to using technology to shape the future of healthcare.</p>

<h3 align="center">Jacob Curren</h3>
<p align="center">I am a senior studying Computer Science. I will be graduating this semester with a bachelor's degree. I can be contacted at jwcurren@crimson.ua.edu</p>
