# Web Architecture 101

[The article](https://engineering.videoblocks.com/web-architecture-101-a3224e126947).

## DNS 

Has been explained in one of the notes.

## Load Balancer

They’re the magic sauce that makes scaling horizontally possible. They route incoming requests to one of many application servers that are typically clones / mirror images of each other and send the response from the app server back to the client. Any one of them should process the request the same way so it’s just a matter of distributing the requests across the set of servers so none of them are overloaded.

### Horizontal vs Vertical Scaling 

Horizontal scaling means that you scale by adding more machines into your pool of resources whereas “vertical” scaling means that you scale by adding more power (e.g., CPU, RAM) to an existing machine.

In web development, you (almost) always want to scale horizontally because, to keep it simple, stuff breaks. Servers crash randomly. Networks degrade. Entire data centers occasionally go offline. Having more than one server allows you to plan for outages so that your application continues running. In other words, your app is “fault tolerant.” Secondly, horizontal scaling allows you to minimally couple different parts of your application backend (web server, database, service X, etc.) by having each of them run on different servers.

## Web Application Servers

They execute the core business logic that handles a user’s request and sends back HTML to the user’s browser. To do their job, they typically communicate with a variety of backend infrastructure such as databases, caching layers, job queues, search services, other microservices, data/logging queues, and more. As mentioned above, you typically have at least two and often times many more, plugged into a load balancer in order to process user requests.

You should know that app server implementations require choosing a specific language (Node.js, Ruby, PHP, Scala, Java, C# .NET, etc.) and a web MVC framework for that language (Express for Node.js, Ruby on Rails, Play for Scala, Laravel for PHP, etc.). 

## Database Servers

Every modern web application leverages one or more databases to store information. Additionally, each backend service may have it’s own database that’s isolated from the rest of the application.

## Caching Service 

A caching service provides a simple key/value data store that makes it possible to save and lookup information in close to O(1) time.
The two most widespread caching server technologies are Redis and Memcache.

## Job Queue & Servers

Job queues store a list of jobs that need to be run asynchronously. Job servers process jobs. They poll the job queue to determine if there’s work to do and if there is, they pop a job off the queue and execute it. 

## Full-text Search Service

Many if not most web apps support some sort of search feature where a user provides a text input (often called a “query”) and the app returns the most “relevant” results. The technology powering this functionality is typically referred to as “full-text search”, which leverages an inverted index to quickly look up documents that contain the query keywords.

## Content Delivery Network

CDN stands for “Content Delivery Network” and the technology provides a way of serving assets such as static HTML, CSS, Javascript, and images over the web much faster than serving them from a single origin server. It works by distributing the content across many “edge” servers around the world so that users end up downloading assets from the “edge” servers instead of the origin server.

## Cloud storage

“Cloud storage is a simple and scalable way to store, access, and share data over the Internet” according to AWS. You can use it to store and access more or less anything you’d store on a local file system with the benefits of being able to interact with it via a RESTful API over HTTP.
