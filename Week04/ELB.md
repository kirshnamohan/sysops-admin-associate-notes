# AWS - ELB (Elastic Load Balancer)

## ELB Characteristics

- Region wide load balancer
- Can be used internally or externally
- SSL termination and processing
- Cookie-based sticky session
- ELB EC2 health checks / AWS CloudWatch
- Integrates with Auto Scaling
- Integrates with Route 53

## ELB types

### Application Load Balancer
- Makes routing decisions at the application layer (layer 7, mostly using HTTP / HTTPS).
- Supports path based routing, and can route requests to one or more ports on each instance.
- Evaluates the listener rules in priority order to determine which rule to apply, and then select a target from target group using Round Robin.
- Support HTTP/2 and connection upgrades from HTTP to Websockets.

### Network Load Balancer

- Selects a target from the target group, for default, using a flow hash algorithm, based on protocol, source IP address, source port, destination IP address, destination port, and TCP sequence number.
- The TCP connections from a client have different source ports and sequence numbers, and can be routed to different targets.
- Each individual TCP connection is routed to a single target for the life of the connection.

### Classic Load Balancer

- Selects a registered instance using the round robin routing algorithm for TCP listeners and the least outstanding requests routing algorithm for HTTP and HTTPS listeners.
- Doesn't support HTTP/2.
- Automatically scales its request handling capacity in response to incoming application traffic.
- Layer 4 or Layer 7 Load Balancing.
- Only supports internet-facing load balancers scheme.

## ELB Features

### Routing (Application Load Balancer)
- *Content-based* routing, can route a request to a service based on the content of the request.
- *Host-based* routing, can route based on the *Host* field of the HTTP header, allowing to route to multiple domains from the same load balancer.
- *Path-based* routing, can route a client request based on the URL path of the HTTP header.

### Sticky sessions 
- Load Balancers support the ability to stick user sessions to specific EC2 instances using load balancer generated cookies. 
- Traffic will be routed to the same instances as the user continues to access your application.
- Stickiness is defined at a target group level.

### Load Balancer Scheme
- Must choose to make a internal load balancer, or an Internet-facing load balancer.
- The nodes of an Internet-facing load balancer have public IP addresses. The DNS name of an Internet-facing load balancer is publicly resolvable to the public IP addresses of the nodes. 
- The nodes of an internal load balancer have only private IP addresses. The DNS name of an internal load balancer is publicly resolvable to the private IP addresses of the nodes.
- Note that both Internet-facing and internal load balancers route requests to your targets using private IP addresses.
- Your targets do not need public IP addresses to receive requests from an internal or an Internet-facing load balancer.

### Connection draining 
- Load Balancer stops sending requests to instances that are de-registering or unhealthy, while keeping the existing connections open. 
- This enables the load balancer to complete in-flight requests made to instances that are de-registering or unhealthy.
- If your instances are part of an Auto Scaling group and connection draining is enabled for your load balancer, Auto Scaling waits for the in-flight requests to complete, or for the maximum timeout to expire, before terminating instances due to a scaling event or health check replacement
- Can specify a maximum time for the load balancer to keep connections alive before reporting the instance as de-registered.
- You can disable connection draining if you want your load balancer to immediately close connections to the instances that are de-registering or have become unhealthy.

### HTTP Connections
- Classic Load Balancers use pre-open connections but Application Load Balancers do not.
- Classic Load Balancers support the following protocols on front-end connections (client to load balancer): HTTP/0.9, HTTP/1.0, and HTTP/1.1.
- Application Load Balancers support the following protocols on front-end connections: HTTP/0.9, HTTP/1.0, HTTP/1.1, and HTTP/2.
- You can use HTTP/2 only with HTTPS listeners.
- Both Application Load Balancers and Classic Load Balancers use HTTP/1.1 on back-end connections (load balancer to registered target). 
- Keep-alive is supported on back-end connections by default.
- For Application Load Balancer, the host header contains the DNS name of the load balancer.
- For Classic Load Balancer, the host header contains the IP address of the load balancer node.

### HTTPS Support
- Supports HTTPS termination between the clients and the load balancer. 
- Load Balancers also offer management of SSL certificates through AWS Identity and Access Management (IAM) and AWS Certificate Manager for predefined security policies.

--
Voila! Badabing, badaboom would you take a look at that!
