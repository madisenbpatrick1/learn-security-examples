# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
    - Absence of authorization
        - the /update-role endpoint does not authenticate properly. A user can supply random data in the request and get access to different roles. 
    - Weak role verification
        - Checking the user.role is based only on the userId. This can be tampered with. Nothing is checking that the request is the same user or has the correct role. 
    
2. Briefly explain how a malicious attacker can exploit them.
    - A malicious attacker can tamper with the request body. The attacker can send a random userId and newRole. This would bypass security checks and allow malicious user into the database. 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
    - Session based authentication
        - using session middleware, makes sure that only authenticated users can get access to the protected routes. The session data is used to authenticate. 
    - Role based authentication
        - The server checks in the user is logged in and checks their role. The server now validates the users role before updating. 
    - Session cookies are protected and configured to be 'httpOnly' and 'samSite' strict. This helps mitigate CSRF 