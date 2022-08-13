# Execute an Azure function with an HTTP request

## What is an HTTP trigger?

An HTTP trigger is a trigger that executes a function when it receives an HTTP request. HTTP triggers have many capabilities and customizations, including

- Provide authorized access by supplying keys.
- Restrict which HTTP verbs are supported.
- Return data back to the caller.
- Receive data through query string parameters or through the request body.
- Support URL route templates to modify the function URL.

## What is an HTTP trigger Authorization level?

There are three Authorization levels:

- ```Function``` levels are "key" based. To send an HTTP request, you must supply a key for authentication. 
- ```Anonymous``` level means that there's no authentication required. We use this level in our exercise.
- ```Admin``` levels are "key" based. To send an HTTP request, you must supply a key for authentication. 

## How to invoke an HTTP trigger
To invoke an HTTP trigger, you send an HTTP request to the URL for your function. To get this URL, go to the code page for your function and select the ``Get function URL`` link.
