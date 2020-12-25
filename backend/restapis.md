__REpresentational State Transfer (REST)__ → architectural style for designing loosely coupled applications over HTTP, first presented by Roy Fielding. It has 6 guiding constraints, which must be satisfied for an interface to be considered RESTful.

#### Uniform interface
- We **must** follow religiously the API interface we define for API consumers to access resources inside the system.
- A resource in the system should only have one logical URI, and provide a way to fetch related or additional data **(HATEOAS)**. A resource shouldn't be too large.
- Synonymize a resource with a web page.
- Resource representations across the system should follow specific guidelines, *e.g.* naming conventions, JSON.

> “Once a developer becomes familiar with one of your APIs, he should be able to follow a similar approach for other APIs.”

#### Client-server
- The client and server application **must** be able to evolve separately without any dependency on each other.
- A client should know only resources URIs.

> “Servers and clients may also be replaced and developed independently, as long as the interface between them is not altered.”

#### Stateless
- Make all client-server interactions stateless. Treat every request as new.
- Each request from the client should contain all the information necessary to service the request - including authentication and authorization details.

> ”No client context shalll be stored on the server between requests. The client is responsible for managing the state of the application.”

#### Cacheable
- Caching shall be applied to resources when applicable. Caching can be implemented on the server or client-side.
- These resources **must** declare themselves cacheable.

> “Well-managed caching partically or completely eliminates some client-server interactions, further improving scalability and preformance.

#### Layered system
- A client cannot ordinarily tell whether it is connected directly to the end server or an intermediary along the way.

#### Code on demand (optional)
- When we need to, we are free to return executable code to support a part of our appliation, *e.g.* returning an UI widget rendering code.

## REST Resource Naming
__Resource__ → primary data representation in REST, addressed via **Uniform Resource Identifiers (URIs)**. It can be a singleton, *e.g.* customer, or a collection, *e.g.* customers. We can identify *customers* collection resource using the  URI `/customers`, while a single *customer* using `/customers/{customerId}`.

When resources are named well, an API is intuitive and easy to use.
- __Use nouns to represent resources__ → a resource is a thing, therefore use nouns. We can also divide **resource archetypes** into four categories:
    1. __document__ → singular concept akin to an object instance or database record. Use singular name to denote it. *e.g.* `http://api.example.com/user-management/users/{id}`.
    2. __collection__ → server-managed directory of resources. They choose what it wants to contain and the URIs of each contained resource. Use plural names. *e.g.* `http://api.example.com/user-management/users`
    3. __store__ → client-managed resource repository. It lets an API client put recourses in, get them back out, and decide when to delete them. The URI is first choren by a client when it was initirally put into the store. *e.g.* `http://api.example.com/song-management/users/{id}/playlists`
    4. __controller__ → models a procedural concept. They are like executable functions, with parameters and return values. Use verbs. *e.g.* `http://api.example.com/song-management/users/{id}/playlist/play`
- __Consistency is key__ → creates low ambiguily, and high readability and maintainability. An example is: forward slash (`/`)  to indicate hierarchical relationships, no trailing forward slash (`/`), hyphens (`-`) to improve readability, no underscores, use lowercase letters, and no file extensions.
- __Never use CRUD function names in URIs__ → URIs should be used to uniquely identify resources, whilst HTTP request methods should be used to indicate which CRUD function is performed.
- __Use query component to filter URI collection__ → enable sorting, filtering, and pagination capabilities in resource collection API, and pass the input parameters as query paramenters. *e.g.* `http://api.example.com/device-management/managed-devices?region=USA`.

## HATEOAS Driven REST APIs
__Hypermedia as The Engine of Application State (HATEOAS)__ → constraint of the REST application architectures. It allows the client to dynamically navigate to the appropriate resources by traversing the hypermedia links.

__Hypermedia__ → any content that contains links to other forms of media such as images, movies, and text.

A REST client hits an initial API URI and uses the server-provided links to dynamically discover available actions and access the resources it needs. The advantages of this are the state is driven by the hypermedia, the client needs no prior knowledge of the service, and the clients no longer have to hard code the URI structures for various resources.
```json
{
  "department": 10,
  "departmentName": "Administration",
  "locationId": 1700,
  "managerId": 200,
  "links": [
    {
      "href": "10/employees",
      "rel": "employees",
      "type": "GET"
    }
  ]
}
```
There's no universally accepted format for representing links between two resources in JSON. Each REST framework provides it's own way of creating the HATEOAS links.

## Security Essentials
Security should be an integral part of any development project. A certain thing is that RESTful APIs should be stateless - so request authentication/authorization should not depend on cookies or sessions. Each API request should come with some sort authentication credentials which must be validated on the server for every request.

Some best practices to secure a REST API are:
- Keep it simple;
- Always use HTTPS;
- Use password hashes, passwords must always be hashed to protect the system;
- Never expose information on URLs;
- Consider OAauth;
- Consider adding timestamp in request, comparing the current timestamp to the request one. This prevents very basic replay attacks from people who are trying to brute force our system without changing the timestamp. We can use a HTTP custom header;
- Input parameter validation.

# Keywords
__Aplication state__ → server-side data which the servers store to identify incoming client requests, their previous interaction details, and current context information. **REST statelessness means being free on application state.**

__Resource state__ → the current sate of a resource on a server at any point of time. Is what we get as a response from the server. We can refer to it as resource representation.

# Sources
[REST API Tutorial](https://restfulapi.net/)
