# Initial thoughts regarding the application

This application is for educational and practice purposes. I want to learn Golang, React and MongoDB.

---
## Functionalities 

* User based
* There must be able to create several todo-lists.
* Maybe divide them into categories? Work-related, School-related, Personal etc. Colors to distinct between the different categories?
* Optional reminder for the todo-tasks? 
* Email notification for missing todo-tasks


* Further work
  * Share todo-lists between users?
  * Grocery shopping lists?

---
## Frontend 

React is a strong contender, maybe Svelte?

---
## Backend 

Golang will be used for the backend.

### Routing and handling HTTP requests

We will be using gin(https://github.com/gin-gonic) for routing and HTTP requests. The Gin Framework will help to reduce the boilerplate code and is very efficient in building scalable API's

> go get github.com/gin-gonic

### **Database**

I want to explore NoSQL databases, so in this case i will be using the MongoDB.

### **Authentication**

Authentication will be done with JWT(JSON Web Token).

Using a persistence layer to store the JWT metadata. This enables us to invalidate the JWT token the very second the user logs out, thereby improving security.

* Lets use Redis - Redis is a key-value storage, therefore keys needs to be unique, we will therefore use *uuid* as the key and the userid as the value.

Need two packages: github.com/twinj/uuid && github.com/go-redis/redis/v7

#### JWT

JWT is comprised of three parts:

* Header - The type of token and signing algorithm used. The type of token can be "JWT" and the signing algorithm can either be HMAC or SHA256
* Payload - Contains the claims. These claims include application specific data(userid, username...), token expiration time(exp), issuer(iss), subject(sub), and so on
* Signature - The encoded header, encoded payload and a secret you provide are used to create the signature

Website: https://www.jwt.to - Let's you verify tokens

Production grade: Store JWT in a HttpOnly cookie.
---
### Tips from reddit when developing the backend
> Source: https://www.reddit.com/r/golang/comments/8opi9r/what_are_some_projects_that_will_help_in_getting/

Build a real world "production" REST or gRPC API:

* Scalable, must be able to run more than one instance.

* Dockerized, runnable on minikube.

* Unit tested, must be able to run "go test ./..." directly from clone.

* Integration tested, recommend docker-compose.

* OpenAPI/Swagger (or similar for gRPC) documented.

* dep vendored, but using the standard library often, instead of piling on dependencies.

* Authenticated and Authorized via apikeys and/or user accounts.

* Built and tested via CI: Travis, CircleCi, etc. Recommend Makefile for task documentation.

* Flag & ENV config, API keys, ports, dev mode, etc.

* "why" comments, not "what" or "how" which should be clear through func/variable names and godoc comments.

* Use of Context to limit request time.

* Leveled JSON logging, logrus or similar.

* Postgres/MySQL, sqlx or an ORM.

* Redis/memcache for scalable caching.

* Datadog, New Relic, AppDynamics, etc for monitoring and statistics.

* Well documented README.md with separate sections for API user and service developer audiences. Maybe even include graphviz or mermaidJS UML diagrams.

* Clean git history with structured commits and useful messages. No merge master commits.

* Passing go fmt, go lint, or better, go-metalinter in the CI.

Show me that, or even half of it, on Github/Gitlab with some open source contributions and I'd be arguing to hire you. Note: I'm not saying this is required to be hired.

Edit: Formatting and links.

* https://peter.bourgon.org/go-for-industrial-programming/

* https://blog.csnet.me/blog/building-a-go-api-grpc-rest-and-openapi-swagger.1/

EditEdit: You do not need all of this just to get a junior level job. Many developers will not get to all of this at first, especially since when needing to balance time/resources vs shipping. Long term, it should all be there for a production system.
