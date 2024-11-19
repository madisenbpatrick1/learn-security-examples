# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

   `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

   `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called **infodisclosure**. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

   `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

   ```
       http://localhost:3000/userinfo?username[$ne]=
   ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

   - Lack of access control to user information: The user has the ability to access internal database with a valid or invalid username. There is no check if it is a string or if it is validated.
   - NoSQL Injection capabilities: The route directly uses the user provided input. A user would be able to query to the MongoDB database with a different command.

2. Briefly explain how a malicious attacker can exploit them.

   - A malicious attacker can exploit the syntax by entering in a query. The query can bypass authentication by exploiting the NoSQL query syntax to match any user. The untrusted input can make it into the database and query.
   - The `/userinfo` route sends raw user data in the response. This could allow attackers to enumerate usernames or analyze the application's database schema.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
   - Input validation of Username
     - Checks the username query parameter is valid string
     - Rejects any unexpected formats
   - Input sanitization of Username
     - Sanitizes the username by removing non-alphanumeric characters.
     - This prevents the NoSQL injection by checking the parameter
