# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.

    The vulerability is that the server performs logging after the fail case where a user or name is null. This means that a malicious user can send a request with a a null user or message, and then repudiate the request by saying they never sent the request.
2. Briefly explain why the vulnerability is addressed in __secure.ts__.

    secure.ts addresses this vulnerability by performing logging in the middleware, before the request is processed. This way, the server can properly log the user before the error would have been thrown, and the user cannot repudiate the request.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?

    This uses the chain of responsibility pattern, where each middleware function has a chance to handle the request or pass it on to the next handler in the chain. This enables the middleware to separate concerns, and perform logging before the request is processed, then pass the request on to the next handler and perform additional logic.
