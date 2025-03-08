## XML or JSON threat protection – 

This will protect against the oversized XML or JSON payload

> **Returned Status Codes**       _400 - Bad Request_

![image](https://github.com/user-attachments/assets/e8b6529d-c7dd-4cf6-b5f1-33dbea88260f)

![image](https://github.com/user-attachments/assets/3e9fac61-95ce-415f-84e4-36286c633d6e)


## Client ID enforcement – 

Authentication is need for proper use of an API, only client authorized can use the API and no one else

## SLA-based Rate Limiting – 

This is more need in case we want to monetize an API otherwise ignored e.g.

 > Free – 20 request per minute

 > Unlimited – 100K request per minute

## IP blacklisting & IP Whitelisting – 

![image](https://github.com/user-attachments/assets/b114ede0-b265-4997-a572-3172b4ae3d78)

##### IP Whitelisting:

- Definition: Grants access to a network or system only from a list of pre-approved IP addresses.
- Approach: Default-deny, meaning access is denied to all IPs unless explicitly allowed on the whitelist.
- Security: More secure as it restricts access to only known and trusted sources.
- Use Cases: Ensuring only specific devices or users can access a network, or allowing access to a server from a specific IP range.
- Example: Allowing only employees' home IPs to access a company's VPN.


##### IP Blacklisting:

- Definition:Blocks access to a network or system from a list of IP addresses identified as malicious or suspicious.
- Approach:Default-allow, meaning access is allowed to all IPs unless explicitly blocked on the blacklist.
- Security:Less secure as it relies on identifying and blocking known threats, which may not be comprehensive.
- Use Cases:Preventing spam emails from a known spam IP address, or blocking access to a website from a compromised IP.
- Example:Blocking a known botnet IP address from accessing a website. 

## Tokenization – 

To tokenize any element which can be sensitive e.g. credit cards etc.

## HTTP Caching – 

In case we think the response don’t change frequently and it’s ok to send the same response for particular request

## Cross-Origin resource sharing – 

is a standard mechanism that allows JavaScript XMLHttpRequest (XHR) calls executed in a web page to interact with resources from non-origin domains. CORS is a commonly implemented solution to the “same-origin policy” that is enforced by all browsers.

## Spike Control API – 

It will protect the system against burst requests

## Header removal or injection – 

Add remove HTTP header

## Message logging – 

Logs custom messages between policies and flow. the payload will be consumed by the policy if it’s a non-repeatable streams
