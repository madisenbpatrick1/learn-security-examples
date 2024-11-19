# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
    - Lack of rate limiting
        - The route to authenticate user does not impose any restrictions on the number of requests a client can send to the server. Sending high volume requests to the server could result in a DoS attack. 
    - Un-validated parameters and no error handling 


2. Briefly explain how a malicious attacker can exploit them.
    - A malicious attacker could flood the network with requests to the /userinfo endpoint. This would exhaust resources like CPU and would crash or become unresponsive. 


3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
    - Rate limiting
        -A RateLimit is added to limit each IP address to request to every 5 seconds. This prevents the attacker from flooding the server with requests. 
    - Sanitizing input parameters for User 
    - Better Error Handling
        - `try-catch` block around the database query to handle unexpected errors