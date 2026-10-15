## What is the HTTP Host header?

The HTTP Host header is a mandatory request header as of HTTP/1.1. It specifies the domain name that the client wants to access. For example, when a user visits `https://portswigger.net/web-security`, their browser will compose a request containing a Host header as follows:

`GET /web-security HTTP/1.1 Host: portswigger.net`

In some cases, such as when the request has been forwarded by an intermediary system, the Host value may be altered before it reaches the intended back-end component.

# Portswigger Labs

## PACTITIONER LABS

## LAB 1 (Basic password reset poisoning)
--> First check how the normal fuction for password reset work 
	- For this lab a user was sent a link with token to set the new password
--> Then changed the host header to see the link which is being sent then you will observe that the reset link is sent with the host name you used in the host header
--> Use the exploit server provided as the hostname and reset the carlos user password which will send a reset link to his email.
--> If the user carlos clicks the link with our malicious domain then the event is getting logged in our server where we can extract the token and use it to reset carlos password.

## LAB 2 (Host header authentication bypass)
--> When bruteforced the directories discovered that there is an end point `/admin`  which returned the response that its accessible only to admins
--> From there i intercepted the request and changed to host header to localhost and was able to access `/admin`

## LAB 3 (Web cache poisoning via ambiguous requests)
--> Check if the website is a cache oracle with a cache buster
	- check in the response for headers like `Cache-Control: max-age=30| Age: 0| X-Cache: miss`
--> Identify the unkeyed input 
	- For this case was `Host`
--> Use the unkeyed input header to poison the cache with a malicious server domain
	- For this case the input was reflected inside a `<script>` tag which was loading the js file so we hosted our own js file with malicious content which when server executed.

## LAB 4 (Routing-based SSRF)
--> This Lab involved a server side request forgery(SSRF) attack in which a the `/admin` endpoint was accessible only when the host was changed to an internal IP which was `192.168.0.75`

## LAB 5 (SSRF via flawed request parsing)
--> This Lab involve a server side request forgery(SSRF) as well where if take the url and paste after GET ie.(GET `url`) then the web behave differently and when you change host header then you get `504 Gateway Timeout` and if you bruteforce the internal IP `192.168.0.$$` then you get redirected to the admin panel /admin.

## LAB 6 (Host validation bypass via connection state attack)
--> This Lab involve two vulnerbilities 
	- SSRF
	- RACE condition

--> If you change the host name then you get a redirection to the original url but there is race condition where there is a small window for time to check and time to use where the server checks the data in the request and when the server uses the data in the server and this can be used to exploit race condition vulnerbility where by you send one valid request with the parameter `Connection: keep-alive` and another request with the host header set to internal ip (192.168.0.1) then you will be redirected to /admin where also you will be able to access the /admin and be able to delete the user carlos.

## LAB 7 (# Password reset poisoning via dangling markup)
--> 