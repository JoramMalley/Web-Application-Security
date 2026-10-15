## What is web cache poisoning?

Web cache poisoning is an advanced technique whereby an attacker exploits the behavior of a web server and cache so that a harmful HTTP response is served to other users.

## Constructing a web cache poisoning attack

Constructing a basic web cache poisoning attack involves the following steps:
1. Identify and evaluate unkeyed inputs
2. Elicit/educe/send a harmful response from the back-end server
3. Get the response cached


# Portswigger Labs

## PACTITIONER LABS
## LAB 1 (WCP with an unkeyed header)
-->Check if the website is a cache oracle with a cache buster
	- check in the response for headers in the r
--> Identify the unkeyed input with param miner 
--> Use the unkeyed input header to poison the cache with a malicious server address

## LAB 2 (WCP with an unkeyed cookie)
-->Check if the website is a cache oracle with a cache buster
--> Identify the unkeyed input 
	- In this case was the cookie
--> use the unkeyed input to poison the cache
	- In this case was with a payload "-alert()-"

## LAB 3 (WCP with multiple headers)
--> Identify the unkeyed input 
	- In this case if found two headers `x-forwarded-scheme` and `x-forwarded-host` 
	- note that if you use param miner you can discover the first header but to get the second header then you have to use `x-forwarded-scheme` to discover the second header `x-forwarded-host` header
--> Use the unkeyed input to poison the cache 
	- For this case the cache poisoning should be done to the end point where js is being loaded so that it should be loaded with the malicious code from our exploit server

## LAB 4 (WCP using an unknown header)
--> Check if the website is a cache oracle and use a cache buster
--> Noted that the user-agent was keyed as well
--> Identify the unkeyed input 
	- In this case the unkeyed input was the `X-host` header 
--> Use the unkeyed input to poison the cache 
--> But the useragent is also a keyed input so when you poison the cache it only affects few individuals but there's an input in comment section which is html injectable so it can be injected `<img src='http://malicious-server.com/path/to/vulnerable.js'>`  

## LAB 5 (WCP via an unkeyed query string)
--> Check if the website is a cache oracle and use a cache buster
--> Identify the unkeyed input 
	- For this Lab the unkeyed query string was the `evil` which was getting reflected and through it a user perfom an XSS 
--> Use the unkeyed input to poison the cache  
	- Using the unkeyed query a user could poison the cache and perfom an XSS

## LAB 6 (WCP via an unkeyed query parameter)
--> Just like LAB 5

## LAB 7 (Parameter cloaking)
--> Check if the website is a cache oracle and use a cache buster
--> Identify the unkeyed input 
	- For this case the unkeyed input was `utm_content` query
--> Use the unkeyed input to poison the cache  
	- Poisoning this lab required an attacker to set the payload on a keyed input so the victim can not visit the link with the payload hence used a technique of # Parameter Cloaking to poison the cache by using ; as the separator instead of & so the cache server does'nt consider ; as the separator but the backend server considers it hence respond with a malicious responce which then get cached and served to everyone by the cache server.

## LAB 8 (WCP via a fat GET request)
--> Check if the website is a cache oracle and use a cache buster inorder to not affect live users
--> Identify the unkeyed input 
	- For this case the unkeyed input is throug a fat GET of `callback` 
--> Use the unkeyed input to poison the cache  
	- For this Lab poisoning the cache was straight foward.

## LAB 9 (URL normalization)
--> Check if the website is a cache oracle and use a cache buster inorder to not affect live users
--> Identify the unkeyed input 
	- For this case there were no any unkeyed input identified hence the web behaviour was use to poison the cache  
--> When the / was url decoded then the app would break and the error would be stored in the cache and served to the customers 

## EXPERT LABS

## LAB 10
--> Check if the website is a cache oracle and use a cache buster inorder to not affect live users
--> Identify the unkeyed input 
	- For this case the unkeyed input was `X-Forwarded-Host` which could inject a input in data which was used as host potion to load a json file
--> Use the unkeyed input to poison the cache   
	- For this case host a malicious server with the json file which has an xss payload whose url will be injected in the  `X-Forwarded-Host` which will later be executed when the website tries to load the json file from the injected url with the an xss payload.

## LAB 11
