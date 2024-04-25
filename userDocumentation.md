User Documentation

Features

Core Features

Our core features consist of user signup, user login, adding a provider, admins editing/deleting a provider, searching through the provider table, sending users verification emails, ability to reset password, and an admin page to view users and change user roles.

User Signup

For user signup, the user clicks on the "signup" button in the top right of the home page. The user then inputs the required information. The user will then both be added to the user database and will recieve a verification email in the email they provided.

User Login

For user login, the user clicks on the "login" button in the top right of the home page and then inputs their username and password. The user is then allowed to access features available to logged in users (adding providers).

Adding a Provider

For adding a provider, the user first needs to be logged in. Then the user can click on the "Find Providers" button on the home page and then click the plus button in the bottom right of the "Find Providers" page, or the user can click on the "Add Providers" button on the home page. The user then needs to input the required information about the provider and once submitted will then be visible on the "Find Providers" page

Editing/Deleting a Provider

For editing a provider, the user must be logged in as an admin. To edit a provider the user can go to the "Find Providers" page, scroll all the way to the right, hit the edit button, and then input the desired edits. To delete a provider the user must go to the "Find Providers" page, scroll all the way to the right, and then click the delete button.

Searching Through the Provider Table

For searching through the provider table, the user needs to go to the "Find Providers" page, at the top of the page there is a search bar where the user can input what they want to search and then click the search button. After clicking the search button, after putting in their input, the provider table will list all the providers that contain the input.

Sending Verification Emails

For sending verification emails, once the user creates an account an email with a link to verify their account will be sent to the provided email.

Reseting Password

For reseting a users password, the user can navigate to the "login" page and click the forgot password. After inputing your username and email, an email will be sent to the users email with a link taking the user to the reset password page where they can then put in a new password.

Admin Page

For the admin page, the user must first be logged in as an admin and they then can edit the url from /home to /admin-page (if any other user goes to this url it will not show any users). On the admin page, the user can view all created users and can edit their roles by using the drop down arrow in the roles column. Admins can also delete users by using that drop down arrow or by click the "X" button on the far right side of each user.

External Resources

In Caregiver Connect we use two outside resources, GEOAPIFY and SENDGRID. We use GEOAPIFY when we add providers into the database to help insure that the address/location the user inputs for the provider is correct. We use SENDGRID for our emails with user verification and password resets.
