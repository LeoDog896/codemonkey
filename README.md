# Code Monkey

For me and other people in my group: 
<ul>
  <li>Submission Form: <a href="https://docs.google.com/forms/d/e/1FAIpQLSeWqrl5Fv2bUUb8hKgddbWtL_wgjdhOrIMJ5EPcReuUGyQniA/viewform"> Google Pre-Proposal Form</a></li>
  <li>Shared Document: <a href="https://docs.google.com/document/d/1VxrSXIrScJ1PQG0PVCgcN-ZDyvmENHpNuVRCk0shqvc/edit">Google Document</a></li>
</ul>

## To Do List

### General
:white_check_mark: Create domain with SSL (codemonkey.tk)

:white_check_mark: Submit code from front end to back end without refreshing the page. Also send the backend information to the front end without refreshing the page. This will mostly be used for submitting code to the server to run and check against the reqirements.

:white_check_mark: Use session tokens stored in a cookie to authenticate users

### Front End

:white_check_mark: Create admin page

:x: Make admin page look pretty

:white_check_mark: Create login page

:x: Make login page pretty

:white_check_mark: Create default page

:x: Make default page look pretty

:x: Create register page

:x: Make register page look pretty

:x: Create a function to submit code to the backend

:x: Receive code execution details from the backend

:x: Create a page that recieves challenges and displays them to the user.

:x: Make page for each challenge look pretty

### Backend

:white_check_mark: Use tokens to authenticate users
<ul>
  <li>Should have an expiration date</li>
  <li>Should refresh every time a user reloads a page</li>
</ul>

:white_check_mark: Use json for formating data

:white_check_mark: Put the session token into a cookie instead of plainly in the HTML. Also means the cookie has to be accessed by the backend.

:x: Track course completion for each user

:x: Course completion should also be in a database file

:x: Store user information in a database instead of a text file

:white_check_mark: Use threading to remove inactive sessions every minute.

:white_check_mark: Accept code submit requests from the frontend

:white_check_mark: Execute code from the frontend

:white_check_mark: Send code back to the frontend

:x: Use threads to run code asynchronously and check if the code runs for too long, then kill the thread and notifiy the user.

:x: Do not allow users to create an account with an already existing username.

:x: Password restrictions for weak passwords

:x: Require emails for registration to prevent users from creating multiple accounts

:x: Add email verification

:x: Send emails to the users

:x: Track users by a unique id

## Functionality of Pages

### Login
<ol>
  <li>User enters login credentials</li>
  <li>Backend hashes the password five times, creates a session token, and an expiration date for the token.</li>
  <li>Token (and only the token) is sent back to the front end to be part of the front-end HTML through a cookie</li>
  <li>The user is sent to the challenges page</li>
</ol>

### Loading a Normal Webpage 
<ol>
  <li>Session token, and any other information is sent to back end</li>
  <li>Backend checks if token is expired. Yes -> require the user to log in. No -> Continue</li>
  <li>Determine the next page that needs to be loaded.</li>
  <li>Send information about the next page to the front end or redirect the user to the correct page</li>
</ol>

### Submitting Code
<ol>
  <li>Encode with base64 the user's code and challengename plus the challenge id and add it to a request along with the user's session token</li>
  <li>Send this data to the backend using ajax</li>
  <li>The backend checks if the recieved session token is valid. Yes -> continue; No -> Require the user to login.</li>
  <li>Decode the base64 encoded user code</li>
  <li>Check if the code contains any statements that allow code execution Examples would be "import os" to gain a remote shell to the server</li>
  <li>Run the code</li>
  <li>Check if the output matches the expected output Yes -> Mark it as correct; No -> Mark it as correct</li>
</ol>

## Database Layout

## Accounts

The Accounts database contains usernames, emails, hashed passwords, and admin status

Example table:
<table>
  <tr>
    <th>username</th>
    <th>email</th>
    <th>password</th>
    <th>admin</th>
  </tr>
  <tr>
    <td>Daniel</td>
    <td>daniel@codemonkey.tk</td>
    <td>30cd2f99101cdd52cc5fda1e996ee137</td>
    <td>True</td>
  </tr>
  <tr>
    <td>ChrisMz</td>
    <td>chrismz@codemonkey.tk</td>
    <td>7b3b4de00794a247cf8df8e6fbfe19bf</td>
    <td>False</td>
  </tr>
</table>

## Completion

This table will track course completion for each user

Example table:

<table>
  <tr>
    <th>username</th>
    <th>0001</th>
    <th>0002</th>
    <th>0003</th>
  </tr>
    <td>Daniel</td>
    <td>True</td>
    <td>False</td>
    <td>False</td>
  </tr>
    <td>ChrisMz</td>
    <td>False</td>
    <td>True</td>
    <td>True</td>
  </tr>
</table>