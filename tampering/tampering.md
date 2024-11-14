# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

    Potential tampering vulnerabilities include:
    1. Failure to reject code as input
        - Un-sanitized inputs in the /register route such as name 
    2. Allows attackers to tamper with cookies
        - Weak session validation allows attackers to potentially alter user value
    3. Using inputs in database queries without validation
        - inputs are not validated before using a database query


2. Briefly explain how a malicious attacker can exploit them.

    1. Failure to reject code as input allows for input tampering. Input tampering can allow a malicious attacker to inject code into the 'name' field. This code can be stored and executed in the session. 
    2. The code allows for attackers to tamper with cookies causing for sessions to be manipulated. Attackers are able to set the session.user to 'Admin'. Setting the user to 'Admin' allows the attacker to gain access to the sensitive session. The attacker can bypass any access control. 


3. Briefly explain why **secure.ts** does not have the same vulnerabilities?
    1. secure.ts includes input sanitization. The 'name' field is sanitized using the 'escapeHTML' function. This function is used to sanitize the input by escaping HTL special characters. Calling this function checks for any dangerous characters.
    2. secure.ts includes 'sameSite: 'strict''. This setting prevents client side access to the cookie. This secures and prevents the risk of cookie tampering 
