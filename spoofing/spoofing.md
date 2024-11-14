# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.

    The spoofing vulnerability in insecure.ts include the following:
        - Hard-coded secret value is vulnerable because a person can forge or guess the secret value.
        
        - Weak cookie security due to the httpONLY setting being set to false. THis makes the cookie accessible to the JavaScript. This allows for cross-site scripting. Also does not contain 'secure: true.

        - No CSRF Protection enabled to prevent malicious attackers from submitting unauthorized requests. 


2. Briefly explain different ways in which vulnerability can be exploited.
    Hard-coded value can be exploited by malicious attackers by predicting the secret and/or using brute force and guess. Once the attackers guesses the code it can be used to forge a session cookie.  

    cookie: {httpOnly: false} can be exploited by malicious attackers by injecting a script that could allow them to access the session cookie. If the attacker manages to steal the session cookie, the attacker can hijack the original user's sessions. Also they will be able to gain unauthorized access to different parts of the site. 

    No CSRF protection can be exploited by malicious attackers by creating a malicious website. When the website is accessed by the user, it can automatically sends POST requests. 


3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
- put the mitigations used in secure.ts here

    In secure.ts it addresses the spoofing vulnerabilities in insecure.ts. 
        1. The secret is not hard-coded and instead is provided from 'process.argv[2]'. This change makes the value less predictable and more secure. 
        2. Better cookie security with 'httpOnly: true' and 'sameSite: true'. Both of these changes prevent JS from accessing session cookies and protects against CSRF. 