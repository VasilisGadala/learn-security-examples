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

    The issue here is that the server does not safely handle the case where the user inputs an invalid id, meaning users can intentionally crash the server (DOS). Additionally, the server does not have any rate limiting, meaning users can spam requests to the server and crash it.
2. Briefly explain how a malicious attacker can exploit them.

    A malicious user can exploit this vulnerability by intentionally inputting an invalid id to crash the server. Additionally, they can send a large number of requests to the server to crash it.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?

    secure.ts adds try catch error handling handles the case where the user inputs an invalid id, meaning users cannot intentionally crash the server. It also adds rate limiting, meaning users cannot spam requests to the server and crash it. To provide further resilance, we could add a firewall or load balancer to prevent DOS attacks on the middleware layer.