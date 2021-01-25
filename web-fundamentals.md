# Web Fundamentals

## How do we load websites?

    1. What request verb is used to retrieve page content?
        a. GET
    2. What port do web servers normally listen on?
        a. 80
    3. What's responsible for making websites look fancy?
        a. CSS

## More HTTP - Verbs and request formats

    1. What verb would be used for a login?
        a. POST
    2. What verb would be used to see your bank balance once you're logged in?
        a. GET
    3. Does the body of a GET request matter? Yea/Nay
        a. Nay - Server will likely ignore it.
    4. What's the status code for "I'm a teapot"?
        a. 418 - I'm a teapot - The server refuses the attempt to brew coffee with a teapot.
    5. What status code will you get if you need to authenticate to access some content, and you're unauthenticated?
        a. 401 - Unauthorized - Although the HTTP standard specifies "unauthorized", semantically this response means "unauthenticated". That is, the client must authenticate itself to get the requested response.

## Mini CTF

    1. What's the GET flag?
        a. thm{162520bec925bd7979e9ae65a725f99f} - I used the command 'curl http://ipaddress:8081/ctf/get'
    2. What's the POST flag?
        a. thm{3517c902e22def9c6e09b99a9040ba09} - I used the command 'curl -d "flag_please" -X POST http://ipaddress:8081/ctf/post
    3. What's the "Get a cookie" flag?
        a. thm{91b1ac2606f36b935f465558213d7ebd} - I used the command 'curl -c - http://ipaddress:8081/ctf/getcookie'
    4. What's the "Set a cookie" flag?
        a. thm{c10b5cb7546f359d19c747db2d0f47b3} - I used the command 'curl --cookie "flagpls=flagpls" http://ipaddress:8081/ctf/sendcookie
