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
   
   This file is susceptible to CSRF attacks for the following reasons:
   1. Setting the middleware httpOnly to false enables clients to access cookies
   2. The secret is hardcoded, meaning it can be read by the client.
   3. SameSite is set to false, meaning requests can be made from varying domains
   4. The request itself doesn't sanitize inputs, leaving vulnerabilities to injection and CSRF attacks
2. Briefly explain different ways in which vulnerability can be exploited. 
   
   Because HttpOnly is set to false, clients can grab the cookie through malicious document inputs.
In the example, this is done by taking advantage of unsanitized inputs to create a malicious form that steals the cookie.
Not having SameSite hardcoded means the attacker can make request across domains rather than from the main site, i.e. 
by redirecting users to feign web pages. Not hardcoding the secret will allow attackers to copy a client's signature. 
This is important because the secret is used to sign the session, so malicious access to the secret enables attackers to
make validated requests as the client.
3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**. 

   secure.ts fixed the aforementioned issues by requiring clients to pass secrets instead of hard-coding them,
setting httpOnly to true to prevent easy access to client cookies, and setting sameSite to true to prevent CSRF attacks.
It does not directly sanitize the inputs as described in the tampering section.
   