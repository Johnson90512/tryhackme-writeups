# Burp Suite

## Overview of Features

    1. Which tool in Burp Suite can we use to perform a 'diff' on responses and other pieces of data?
        a. Comparer -Comparer as you might have guessed is a tool we can use to compare different responses or other pieces of data such as site maps or proxy histories (awesome for access control issue testing). This is very similar to the Linux tool diff.
    2. What tool could we use to analyze randomness in different pieces of data such as password reset tokens?
        a. Sequencer - Analyzes the 'randomness' present in parts of the web app which are intended to be unpredictable. This is commonly used for testing session cookies.
    3. Which tool can we use to set the scope of our project?
        a. Target - How we set the scope of our project. We can also use this to effectively create a site map of the application we are testing.
    4. While only available in the premium versions of Burp Suite, which tool can we use to automatically identify different vulnerabilities in the application we are examining?
        a. Scanner - Automated web vulnerability scanner that can highlight areas of the application for further manual investigation or possible exploitation with another section of Burp. This feature, while not in the community edition of Burp Suite, is still a key facet of performing a web application test.
    5. Encoding or decoding data can be particularly useful when examining URL parameters or protections on a form, which tool allows us to do just that?
        a. Decoder - As the name suggests, Decoder is a tool that allows us to perform various transforms on pieces of data. These transforms vary from decoding/encoding to various bases or URL encoding.
    6. Which tool allows us to redirect our web traffic into Burp for further examination?
        a. Proxy - What allows us to funnel traffic through Burp Suite for further analysis.
    7. Simple in concept but powerful in execution, which tool allows us to reissue requests?
        a. Repeater - Allows us to 'repeat' requests that have previously been made with or without modification. Often used in a precursor step to fuzzing with the aforementioned Intruder.
    8. With four modes, which tool in Burp can we use for a variety of purposes such as field fuzzing?
        a. Intruder -  Incredibly powerful tool for everything from field fuzzing to credential stuffing and more.
    9. Last but certainly not least, which tool allows us to modify Burp Suite via the addition of extensions?
        a. Extender - Similar to adding mods to a game like Minecraft, Extender allows us to add components such as tool integrations, additional scan definitions, and more!

## Proxy

    1. By default, the Burp Suite proxy listens on only one interface. What is it? Use the format of IP:PORT
        a. 127.0.0.1:8080
    2. Take a look at the actions, which shortcut allows us to forward the request to Repeater?
        a. Ctrl-R
    3. How about if we wanted to forward our request to Intruder?
        a. Ctrl-I
    4. What is the name of the first section wherein general web requests (GET/POST) are saved?
        a. HTTP History - Subtab under Proxy.
    5.These are commonly used in collaborate application which require real-time updates (Google Docs is an excellent example here).
        a. Websockets History.
    6. Here we can apply further fine-grained rules to define which requests we would like to intercept. Perhaps the most useful out of the default rules is our only AND rule. What is it's match type?
        a. URL
    7. How about it's 'Relationship'?
        a. Is in target scope.

## Target Definition

    1. What do we call this representation of the collective web application?
        a. site map
    2. What is the term for browsing the application as a normal user prior to examining it further?
        a. happy path
    3. Which poisoning issue arises when an application behind a cache process input that is not included in the cache key?
        a. Web Cache Poisoning.

## Puttin' it on Repeat[er]

    1. Try logging in with invalid credentials. What error is generated when login fails?
        a. Invalid email or password.
    2. Now that we've sent the request to Repeater, let's try adjusting the request such that we are sending a single quote (') as both the email and password. What error is generated from this request?
        a. sqlite_error
    3. What field do we have to modify in order to submit a zero-star review?
        a. rating - Make a post, and find the post in HTTP history. Once you find it in history, send it to repeater and change the rating to 0 and send it.

## Help! There's and Intruder!

    1. Which attack type allows us to select multiple payload sets (one per position) and iterate through them simultaneously?
        a. Pitchfork
    2.  How about the attack type which allows us to use one payload set in every single position we've selected simultaneously? 
        a. Battering Ram
    3. Which attack type allows us to select multiple payload sets (one per position) and iterate through all possible combinations?
        a. Cluster Bomb
    4. Perhaps the most commonly used, which attack type allows us to cycle through our payload set, putting the next available payload in each position in turn?
        a. Sniper
    5. Finally, click 'Start attack'. What is the first payload that returns a 200 status code, showing that we have successfully bypassed authentication?
        a. a' or 1=1--

## As it turns out the machines are better at math than us

    1. Parse through the results. What is the effective estimated entropy measured in?
        a. bits
    2. In order to find the usable bits of entropy we often have to make some adjustments to have a normalized dataset. What item is converted in this process?
        a. token - tis is on the Bit-Level analysis tab and sub tab Bit Conversion.

## Decoder and Comparer

    1. What character does the %20 in the request we copied into Decoder decode as?
        a. space
    2. Similar to CyberChef, Decoder also has a 'Magic' mode where it will automatically attempt to decode the input it is provided. What is this mode called? 
        a. Smart Decode
    3. What can we load into Comparer to see differences in what various user roles can access? This is very useful to check for access control issues.
        a. Site Maps - Found this by reading the help/question mark
    4.Comparer can perform a diff against two different metrics, which one allows us to examine the data loaded in as-is rather than breaking it down into bytes?
        a. Words - This comparison tokenizes each item of data based on whitespace delimiters, and identifies the token-level edits required to transform the first item into the second.
