# SSL, TLS, HTTPS and SSH
__SSL and TLS__ → protocols that encrypt your data sent across a network. SSL in the older version renamed in 1999 to TLS. We are currently on TLS 1.3.

__HTTPS__ → is HTTP wrapped in TLS. However TLS is not specific to HTTP only.

__SSH__ → cryptographic protocol. Used to securely execute commands on a remote server. Designed as a secure replacement for telnet, rsh or rlogin.

# HTTP Protocol
__Hypertext Transfer Protocol (HTTP)__ → stateless, application-layer protocol. Allows for communication between a variety of hosts and clients, assuming very litle about a particular system. It doesn't keep a state between different message exchanges. The communication usually takes place over TCP/IP, the default port being **80**.

Communication between a host and a client occurs via a **request/response pair**.
![communication between host and client diagram](https://miro.medium.com/max/929/1*0w3tMXm7jr174bqOprcdOg.png "HTTP and Websockets: Understanding the capabilities of today’s web communication technologies – Medium")

The current HTTP version is **HTTP/2**.

## URLs
At the heart of web communications is the request message sent via **Uniform Resource Locators (URLs)**. They take the format of `protocol://hostname:port/resource-path?query`. An example is:
```
http://www.domain.com:1234/path/to/resource?a=b&x=y
```

The default protocols is `http` or `https` (for secure communications), and the default port is `80`, but one can be set explicitly.

## HTTP Verbs
__HTTP verbs__ → action that should be performed on the host. The most popular verbs are:
- __GET__ → *fetch* an existing resource. URL contains the necessary information.
- __POST__ → *create* a new resource. Usually carries a payload with the specified data.
- __PUT__ → *update* an existing resource. Can also contain a payload.
- __DELETE__ → *delete* an existing resource.

`PUT` and `DELETE` can be considered specilized versions of the `POST` verb, and may be packaged as it with the payload containing the exact action.

Some less popular verbs are:
- __HEAD__ → similar to `GET`, but without the message body. Used to retrieve the server headers.
- __TRACE__ → used to reteive the hops that a requset takes to round trip from the server. Can be used for diagnostic purposes.
- __OPTIONS__ → used to retrieve the server capabilities. Can be used to modify the request on the client based on what the server can support.

## Status Codes
__Status codes__ → sent in the server response together with the message payload, tells the client how to interpret the server response.

Different number ranges have a different type:
Code | | Name | Description
--- | --- | --- | ---
__1xx__ | | Informational Messages | tells the client to continue sending the remainder of the request, or ignore if it has already sent it
__2xx__ | | Successful | the request was successfully processed
| | `200` | `OK` | the resource is sent in the message body
| | `202` | `Accepted` | the request may not include the resource in the response. Useful for async processing on the server side
| | `204` | `No Content` | no message body in the response
| | `205` | `Reset Content` | indicates to the client to reset its document view
| | `206` | `Partial Content` | the response only contains partial content. Additonal headers indicate the exact range and content expiration information
__3xx__ | | Redirection | requires the client to take additional information. *e.g.* jumping to different URL
| | `301` | `Moved Permanently` | the resource is now located at a new URL
| | `303` | `See Other` | the resource is temporily located at a new URL
| | `304` | `Not Modified` | the resource has not changed and the client should use its cached copy. Relies on the client sedning `ETag` (Enttity Tag).
__4xx__ | | Client Error | the server thinks that the client is at fault
| | `404` | `Not Found` | the resource is invalid and does not exist on the server
| | `400` | `Bad Request` | the request was malformed
| | `401` | `Unathorized` | request requires authentication. The client can repeat the request with the `Authorization` header.
| | `403` | `Forbidden` | server had denied access to the resource
| | `405` | `Method Not Allowed` | invalid or non-supported HTTP verb used
| | `409` | `Conflict` | the client is trying to modify a resource that is newer than the client's timestamp. Often seen in collaborative edits on a resource
__5xx__ | | Server Error | server failure while pocessing the request
| | `500` | `Internal Server Error`
| | `501` | `Not Implemented` | the server doesn't yet support the requested functionality
| | `503` | `Service Unavailabe` | could happen if an internal system or the server has failed or the server is overloaded. Typically, the server won't even respond and the request will timeout.

## Request and Response Message Formats
The HTTP specification states that a request or response message has to follow a generic structure:
```
Request-Line|Status-Line
*(<message-header>)
CRLF
[<message-body>]
```
The `message-header` can contain one of more headers, and is composed by:
```
Field-Name ':' Field-Value
```
The `message-body` may contain the complete data, or data in chunkes if `Transfer-Encoding: chunked` is used.

### Message Headers
#### General Headers
- `Cache-Control`
- `Connectin`
- `Date` → used to timestamp the request/response message.
- `Pragma` → considered a custom header. May be used to include implementation-specific headers.
- `Trailer`
- `Transfer-Encoding` → generally used to break the response into smaller parts, with the `chunked` value.
- `Upgrade` → used to switch protocols.
- `Via` → used in a TRACE message, and updated by all intermittent proxies and gateways.
- `Warning`

#### Resquest Specific Headers
They act as modifiers of the request message.
- `Accept`
- `Accept-Charset`
- `Accept-Encoding`
- `Accept-Language`
- `Authorization`
- `Expect`
- `From`
- `Host` → mandatory since HTTP/1.1.
- `If-Math`
- `If-Modified-Since`
- `If-None-Match`
- `If-Range`
- `If-Unmodified-Since`
- `Max-Forwards`
- `Proxy-Authorization`
- `Range`
- `Referer`
- `TE`
- `User-Agent`

#### Response Specific Headers
- `Accept-Ranges`
- `Age` → time in seconds since the message was generated on the server.
- `ETag` → MD5 hash of the entity. Uesd to check for modifications.
- `Location` → used when sending a redirection. Contains the new URL.
- `Proxy-Authenticate`
- `Retry-After`
- `Server` → indentifies the server generating the message.
- `Vary`
- `WWW-Authenticate`

#### Entity Headers
May be used to provide meta-information about the content (message body).
- `Allow`
- `Content-Encoding`
- `Content-Language`
- `Content-Length`
- `Content-MD5`
- `Content-Range`
- `Content-Type`
- `Expires` → indicates a timestamp of when the entity expires.
- `Last-Modified` → indicates the last modification timestamp for the entity.

Custom headers can also be created and sent by the client. They will be treated as entity headers by the HTTP protocol.

## Request Format
It has the same generic structure as above, with the `Status-Line` being composed by `Method URI HTTP-Version CRLF`. The method simply is an HTTP verb.

A typical request message might look like:
```
GET /articles/http-basics HTTP/1.1
Host: www.articles.com
Connection: keep-alive
Cache-Control: no-cache
Pragma: no-cache
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```

## Response Format
The `Response-Line` is composed by `HTTP-Version Status-Code Reason-Phrase CRLF`. The Status-Code and the Reason-Phrase are simply the HTTP status codes like `200 OK`.

A example of a nofitication that the requested resource has permanently moved is:
```
HTTP/1.1 301 Moved Permanently
Server: Apache/2.4.37 (Red Hat)
Content-Type: text/html; charset=utf-8
Date: Thu, 06 Dec 2018 17:33:08 GMT
Location: https://developer.mozilla.org/
Keep-Alive: timeout=15, max=98
Accept-Ranges: bytes
Via: Moz-Cache-zlb05
Connection: Keep-Alive
Content-Length: 325


<!DOCTYPE html...> // site-costomized page
```

## Typical HTTP session
A typical HTTP session consists of three phases:
1. The client establishes a TCP connection.
2. The client sends its request, and waits for the answer.
3. The server processes the request, sends back its answer, providing a status code and the appropriate data.\
As of HTTP/1.1 the connection is not closed after this phase, allowing the 2nd and 3rd phases to be performed any number of times.

> __Note:__ The client-server model does not allow the server to send data unless it was explicitly requested. Various methods were developed to work around this. *e.g.* WebSockets API

# Sources
[Roadmap.sh](https://roadmap.sh/)\
[HTTP: The Protocol Every Web Developer Must Know - Part 1 – envatotuts+](https://code.tutsplus.com/tutorials/http-the-protocol-every-web-developer-must-know-part-1--net-31177)\
[A typical HTTP session – MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Session)