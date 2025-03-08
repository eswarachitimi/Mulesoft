## XML or JSON threat protection – 

This will protect against the oversized XML or JSON payload

## Client ID enforcement – 

Authentication is need for proper use of an API, only client authorized can use the API and no one else

## SLA-based Rate Limiting – 

This is more need in case we want to monetize an API otherwise ignored e.g.

 > Free – 20 request per minute

 > Unlimited – 100K request per minute

## IP blacklisting – 

This can be used if we want to limit the consumption of an API to particular IPs e.g. IPs know for hacking etc.

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
