# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicious user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
    - Lack of authentication and logs vulnerable to tampering
        - The route allows for a user to retrieve all messages with authentication. This makes the route vulnerable to data breach attacks. 
    - Uncaught Errors 
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
    - Added authentication
        - authentication mechanism to ensure that only authorized users can access sensitive information.
    - Middleware functions
        - Middleware logs all requests and actions. This provides accountability and traceability. The log entry also includes a timestamp with each log. 
    - Error logger/handling middleware
        - The middleware captures errors and logs them to the server log while sending an error message. 

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
    - Middleware design pattern is used
        - This chains multiple middleware functions together. Each of these middleware functions are responsible for a different concern. 
        - bodyParser is used to handle input parsing and log incoming requests
        - authentication is used to ensure only authenticated users can perform specific actions. 
        - Error handling is used to handle errors and logs them