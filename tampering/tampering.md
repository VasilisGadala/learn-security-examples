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
   
   The main vulnerability is that there are unsanitized inputs, meaning a malicious user can inject a script to manipulate the web page. In general injecting code can be used to make dangerous queries to the server.

2. Briefly explain how a malicious attacker can exploit them.

   In this example, a malicious user can inject a script that changes the HMTL
   produced when returning to the home page after submitting the form. This just redirects to Google to exemplify an XSS attack, but an attacker could make this redirect to a malicious site that mimics the main site to steal the user's credentials.
   
3. Briefly explain why **secure.ts** does not have the same vulnerabilties?

   secure.ts sanitizes the inputs, meaning the user cannot inject a script to manipulate the web page.
   