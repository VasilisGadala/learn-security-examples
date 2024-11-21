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

    The main issue is that the server does not check if the user is an admin before updating the role, and allows any user to update the role of other users if they have access to the user's id. This is pretty limited because the server only allows admins to admin roles to be updated, however this allows users to remove permissions from admins.

2. Briefly explain how a malicious attacker can exploit them.

    A malicious attacker can exploit this vulnerability by sending a request to update the role of an admin user. Since there aren't many roles, this allows anyone to remove permissions from admins.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?

    secure.ts fixes this vulnerability by providing proper authorization checks before allowing the described updates. This is accomplished by checking the id in the user session, and preventing users from being able to use other STRIDE attacks to gain access to the session to steal admin permissions.