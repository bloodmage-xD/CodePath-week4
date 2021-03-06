# CodePath-week4
Week 4 Project: Forgery, Theft, and Hijacking Prevention
Due: unspecified at 11:59pm

Overview: Implement defensive measures to protect an application against Cross-Site Scripting, SQL Injection, Cross-Site Request Forgery, Session Hijacking, and Session Fixation.

Walkthrough:  This video will walk through the setup, show you how to run the penetration tests, and briefly outline the code you will need to implement or improve.

Submitting Assignments: Submitted through Github, check out the Submitting Assignments page for more details.

Be sure to include a README containing a GIF walkthrough of your app and list of completed stories.
Use this README template in order to have a complete README.
Assets: The following assets may be helpful in completing this assignment.

 Assignment 4 Starting Database
 Assignment 4 Starting Code
User Stories:

User stories are a way to describe the features of a web application from the user's point of view. It will be up to you to create the database and code to make each feature works correctly for the user.

The following user stories must be completed:

1. Test for vulnerabilities
Test code has been included in the project in "pen_tests". Go to "pen_tests/index.php" to see a list of tests. Run all three tests. Notice that the application is currently vulnerable to three types of attack. (You will run these tests again at the end of the assignment.) (Tips)

2. Configure sessions.
Notice that "private/initialize.php" already includes session_start(). However, it has not been configured. You should configure sessions to prevent Cross-Site Scripting and Session Hijacking. (Tips)

Only allow session IDs to come from cookies
Expire after one day
Use cookies which are marked as HttpOnly
3. Login page.
Notice that "public/staff/login.php" and "private/auth_functions.php" already include much of the code needed for allowing a user to login to the staff area. You should complete it by adding: (Tips)

An error message for when the username is not found
An error message for when the username is found but the password does not match
After a successful login, store the user's ID in the session data (as "user_id").
After a successful login, store the user's last login time in the session data (as "last_login").
Regenerate the session ID at the appropriate point to prevent Session Fixation.
4. Require login to access staff area pages
The function require_login() is defined in "private/auth_functions.php". It can be added to any page which requires a login to access its content. (Tips)

Add a login requirement to almost all staff area pages. Determine which two pages do not need to require a login.
require_login() includes a call to determine if last_login_is_recent() but the function does not have proper code. Write code which will only consider a request as being "recent" if the user's last login was less than 1 day ago.
5. Logout page.
Notice that "public/staff/logout.php" and "private/auth_functions.php" already include much of the code needed for allowing a user to login to the staff area. You should complete it by adding code to destroy the user's session file after logging out. (Tips)

6. Add CSRF protections to the state forms.
The forms in "public/staff/states/" are new.php and edit.php. Add CSRF tokens to these forms and compare them against the stored version of the token before accepting the form. (Tips)

Only process forms data sent by POST requests. (This is already the case unless you change it.)
Confirm that the referer sent in the requests is from the same domain as the host.
Create a CSRF token.
Store the CSRF token in the user's session.
Add the same CSRF token to the login form as a hidden input.
When submitted, confirm that session and form tokens match.
If the tokens do not match, you can should show a simple error message which says "Error: invalid request" and exits.
Make sure that legitimate use of the states/new.php and states/edit.php pages by a logged-in user still works as expected.
7. Ensure the application is not vulnerable to XSS attacks. (Tips)

8. Ensure the application is not vulnerable to SQL Injection attacks. (Tips)

9. Run all tests from Objective 1 again and confirm that your application is no longer vulnerable to any test.

The following advanced user stories are optional:

Bonus Objective 1: Objective #4 (requiring login on staff pages) has a major security weakness because it does not follow one of the fundamental security principals. Identify the principal and write a short description of how the code could be modified to be more secure. Include your answer in the README file that accompanies your assignment submission.

Bonus Objective 2: Add CSRF tokens and protections to all of the forms in the staff directory (new, edit, delete). Make sure the request is the same domain and that the CSRF token is valid.

Bonus Objective 3: Add code so that CSRF tokens will only be considered valid for 10 minutes after creation.

Bonus Objective 4: Only consider a session valid if the user-agent string matches the value used when the user last logged in successfully.

Advanced Objective: Create two new pages called "public/set_secret_cookie.php" and "public/get_secret_cookie.php". The first page will set a cookie with the name "scrt" and the value "I have a secret to tell.". Before storing the cookie, you need to both encrypt it and sign it. You can use any (two-way) encryption algorithm you prefer. When the second page loads, it should read the cookie with the name "scrt", and then—if it is signed correctly—decrypt it. If it is not signed correctly then it should display an error message and skip decryption altogether.
