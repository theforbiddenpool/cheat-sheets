__REpresentational State Transfer (REST)__ → architectural style for designing loosely coupled applications over HTTP, first presented by Roy Fielding. It has 6 guiding constraints, which must be satisfied for an interface to be considered RESTful.

### Uniform interface
- We **must** follow religiously the API interface we define for API consumers to access resources inside the system.
- A resource in the system should only have one logical URI, and provide a way to fetch related or additional data **(HATEOAS)**. A resource shouldn't be too large.
- Synonymize a resource with a web page.
- Resource representations across the system should follow specific guidelines, *e.g.* naming conventions, JSON.

> “Once a developer becomes familiar with one of your APIs, he should be able to follow a similar approach for other APIs.”

### Client-server
- The client and server application **must** be able to evolve separately without any dependency on each other.
- A client should know only resources URIs.

> “Servers and clients may also be replaced and developed independently, as long as the interface between them is not altered.”

### Stateless
- Make all client-server interactions stateless. Treat every request as new.
- Each request from the client should contain all the information necessary to service the request - including authentication and authorization details.

> ”No client context shalll be stored on the server between requests. The client is responsible for managing the state of the application.”

### Cacheable
- Caching shall be applied to resources when applicable. Caching can be implemented on the server or client-side.
- These resources **must** declare themselves cacheable.

> “Well-managed caching partically or completely eliminates some client-server interactions, further improving scalability and preformance.

### Layered system
- A client cannot ordinarily tell whether it is connected directly to the end server or an intermediary along the way.

### Code on demand (optional)
- When we need to, we are free to return executable code to support a part of our appliation, *e.g.* returning an UI widget rendering code.

# Resources
[REST API Tutorial](https://restfulapi.net/rest-architectural-constraints/)
