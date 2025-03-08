## XML or JSON threat protection – 

This will protect against the oversized XML or JSON payload

> **Returned Status Codes**       _400 - Bad Request_

![image](https://github.com/user-attachments/assets/e8b6529d-c7dd-4cf6-b5f1-33dbea88260f)

![image](https://github.com/user-attachments/assets/3e9fac61-95ce-415f-84e4-36286c633d6e)

## HTTP Basic Authentication - Simple :

Basic authentication is simple and most widely used authentication mechanism in HTTP based services or APIs. The client sends HTTP requests with the Authorization HTTP header that contains the word Basic word followed by a space and a base64-encoded string username:password .

For example, to authorize as username/password the client would send below HTTP header

> Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=

![image](https://github.com/user-attachments/assets/81e834cc-fd43-4082-8abe-69bc40f71297)

## HTTP Basic Authentication -SLA :

![image](https://github.com/user-attachments/assets/d6e1c752-47ad-4be3-98c7-0828dec61bfe)

![image](https://github.com/user-attachments/assets/7003c6b0-0daa-41f8-babe-161778e36852)


## Client ID enforcement – 

Authentication is need for proper use of an API, only client authorized can use the API and no one else -

![image](https://github.com/user-attachments/assets/b5eef96f-efb9-4f4d-94f3-f54390cf45d5)

![image](https://github.com/user-attachments/assets/6cdbf7ac-ef0a-437f-8526-a0aaaa853eed)

![image](https://github.com/user-attachments/assets/20f5efdf-a681-4a2c-bd3b-0864ac9bb6b3)

![image](https://github.com/user-attachments/assets/41ebbc33-96c1-465c-b472-8ed59c8996f2)

Click on create and request Access. It will give you credentials to access this API. Save these credentials.

![image](https://github.com/user-attachments/assets/9b72b8e3-db8c-4f5e-b643-e7aefb8e90a7)


## SLA-based Rate Limiting – 

This is more need in case we want to monetize an API otherwise ignored e.g.

 > Free – 20 request per minute

 > Unlimited – 100K request per minute

![image](https://github.com/user-attachments/assets/a672def3-6819-4fab-89a4-5c609af98756)

![image](https://github.com/user-attachments/assets/a871bb4c-548d-4ff3-b983-f7cb6e7074a0)

![image](https://github.com/user-attachments/assets/e61989f8-8d29-4d62-a052-b0dd20e09e17)

## IP blacklisting & IP Whitelisting – 

![image](https://github.com/user-attachments/assets/b114ede0-b265-4997-a572-3172b4ae3d78)

##### IP Whitelisting:

- Definition: Grants access to a network or system only from a list of pre-approved IP addresses.
- Approach: Default-deny, meaning access is denied to all IPs unless explicitly allowed on the whitelist.
- Security: More secure as it restricts access to only known and trusted sources.
- Use Cases: Ensuring only specific devices or users can access a network, or allowing access to a server from a specific IP range.
- Example: Allowing only employees' home IPs to access a company's VPN.

![image](https://github.com/user-attachments/assets/5bfffe28-7ebd-4338-a394-918a4b1ffd31)


##### IP Blacklisting:

- Definition:Blocks access to a network or system from a list of IP addresses identified as malicious or suspicious.
- Approach:Default-allow, meaning access is allowed to all IPs unless explicitly blocked on the blacklist.
- Security:Less secure as it relies on identifying and blocking known threats, which may not be comprehensive.
- Use Cases:Preventing spam emails from a known spam IP address, or blocking access to a website from a compromised IP.
- Example:Blocking a known botnet IP address from accessing a website. 

![image](https://github.com/user-attachments/assets/1d2e2051-72af-411a-b594-f154395580f3)

## Tokenization – 

Tokenization is the process of masking a value or piece of information that can be considered sensitive data into a token that can be mapped back to its original value using detokenization concepts. If your API contains sensitive data, the tokenization policy is a highly effective way to protect it.

The data is displayed in the same format as the original value, but its actual value is not revealed initially. This policy is designed to work only for Anypoint Runtime Fabric deployments.

Tokenization minimizes the risk of matching the sensitive data to the original value, in case a third party accesses the data. For example, you can use this policy to hide credit card numbers, personally identifiable information (PII), protected health information (PHI), and similar sensitive data.

## HTTP Caching – 

HTTP Caching policy creates a caching space to store the response of different request. So if same request come then it will not go back to end system to retrieve the same information instead it will the response from caching.

HTTP Caching policy is used for those APIs whose response will not change for a long/substantial time. E.g. In an organization Employee details are least likely to change in a day and if we cache the employee information for a day and use that to send the response then it can improve the throughput time and reduce the load from the end system. After a day new information is fetched for the employee and stored in cache.

![image](https://github.com/user-attachments/assets/f5553b09-2bf4-4506-8b00-72c508bdeace)

- HTTP Caching Key – Uniquely define the key for the request. E.g. Employee id for employee request. Should be a dataweave expresion
- Maximum Cache Entries – no of entries (request key – response payload) to cache
- Entry Time To Live (in Seconds) – cached time after which a new details is fetched or actual mule flow will be called
- Distributed – True in case we are using cluster or multiple workers
- Persistent – True in case we want to persist cache data in case of runtime restart

![image](https://github.com/user-attachments/assets/8ee2baf1-43f1-4842-832c-5eeb20a6a896)

- Follow HTTP Caching directives – to add proper HTTP headers in response to tell client we are using caching
- Invalidation Header – to specify in case we don’t want cache result
- Condition Request Caching Expression – based on which caching will be used so if condition is true then only use caching e.g. storing the result in cache and reuse in case we get the same request
- Condition Response Caching Expression – based on which caching will be used so if condition is true then only use caching e.g. storing the result in cache and reuse in case we get the same request

## Cross-Origin resource sharing – 

It is a standard mechanism that allows JavaScript XMLHttpRequest (XHR) calls executed in a web page to interact with resources from non-origin domains. CORS is a commonly implemented solution to the “same-origin policy” that is enforced by all browsers.

Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.

There are some situations when we need to enable CORS at the Mule application side so that UI applications like React JS and Angular JS can integrate exposed APIs. 

## Spike Control API – 

It will protect the system against burst requests.

Spike Control policy limit or restrict the number of request an API can accept in a defined window of time. It doesn’t reject the requests when the number exceed in defined window of time and the policy allows requests to be queued for later reprocessing without closing the connection to the client.

- Number of Reqs – Maximum quota allowed per time window.
- Time Period – window of time
- Delay Time in Milliseconds – Amount of time request will be delayed before retrying (delaying is a CPU intensive process).
- Delay Attempts – The maximum number of times the policy will try to process the request if there is no quota available (delaying is a CPU intensive process).
- Queuing Limit – The maximum number of concurrent requests that can be waiting
- Expose header – Spike Control related headers will be passed back to caller.

These headers are:

```
x-ratelimit-remaining – remaining hits in a window of time
x-ratelimit-limit – max limit in a window of time
x-ratelimit-reset – window of time in milliseconds
 ```

![image](https://github.com/user-attachments/assets/90679cda-880b-468e-808a-f921b7897a6a)

## Header removal or injection – 

Add (or) remove HTTP header.

API Manager supports policies for removing HTTP headers from a request or response. The policies take effect before sending the request or response. The Header Removal policy performs the following actions:

> Prevents receipt of one or more specified headers sent from the client to the backend service.

> Prevents inclusion of one or more specified headers in a response from the backend service to the client.

- Inbound Header Map – header key in String or Regex
- Outbound Header Map – header key in String or Regex

![image](https://github.com/user-attachments/assets/d2ae697d-1be4-4002-9714-8e7c0a84a4d5)

## Message logging – 

Message Logging policy is used to logs custom message between policy and flow. We can log information related to request or response. This comes quite handy in case where we want to capture request/response related logs for debugging without changing the code in mule application.

![image](https://github.com/user-attachments/assets/3c038d40-d35c-46be-8399-856e53e826e3)

## OAuth 2.0 -

> https://mulesy.com/z-oauth-2-0-implementation-using-mule-oauth2-provider-in-mule-4/

