## Caching

Caching is the term for storing reusable responses in order to make subsequent requests faster.

Caching is a buffering technique that stores frequently-queried data in a temporary memory to allow retrieval without having to request the data repeatedly from the original data source, reducing the trips to the original data source and in turn, improving the response time. 

You can use a Cache scope to reduce the processing load on the Mule instance and to increase the speed of message processing within a flow. It is particularly effective for these tasks:

- Processing repeated requests for the same information.
- Processing requests for information that involve large repeatable streams.
  
Mule runtime engine (Mule) offers customizable strategies, such as the `Cache scope` & the `HTTP Caching API Gateway policy`, to enable cache according to your needs. Both strategies help applications that constantly request the same data by reducing the processing load, especially network interactions with a remote host.


### Debug Cache Scope

You can debug the cache logs by adding AyncLogger in log4j file under logger tab -

`<AsyncLogger name=”com.mulesoft.mule.runtime.cache” level=”DEBUG”/>`

### Filters

Instead of processing all message payloads that it receives, the Cache scope can exclude specific payloads from the Cache scope flow based on an DataWeave expression.

### Notes

- Cache scope will not cache target variable, it will cache only payload.
- The cache scope caches repeatable streams only. By default, all streams are repeatable unless configured to be non-repeatable.
- For Cache scope, consider a production environment in which the default in-memory caching consumes all of your memory resources. To avoid this consumption, use an object-store caching configuration with well-defined storage and expiry policies.
- Identifying key aspects of your data such as when to use cache and which cache strategy to follow, helps you to improve processing performance.
