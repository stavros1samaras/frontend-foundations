# Load Balancers

## What is a Load Balancer? ⭐
- A **load balancer** distributes incoming network traffic across multiple servers.  
- Goals:
  - **Reliability & High Availability** – prevents single server overload, keeps services online.  
  - **Performance Optimization** – routes requests to the least loaded or nearest server.  
  - **Security** – helps protect against DDoS attacks and can enforce TLS encryption.  
  - **Session Persistence** – ensures users are directed to the same server for consistent experience.  
  - **Fault Tolerance** – if one server fails, traffic is automatically routed to healthy servers.  
- Operates at **OSI Layer 7** for HTTP traffic (can also operate at Layer 4 for TCP/UDP).

## Load Balancing Algorithms
- **Round Robin** – requests distributed sequentially across servers.  
- **Least Connections** – directs traffic to the server with the fewest active connections.  
- **IP Hash** – routes request based on client IP address.  
- **Weighted Distribution** – assigns traffic according to server capacity.  
- **Additional Notes:** Algorithms can be combined or customized depending on traffic patterns and server capabilities.

## Additional Features of Modern Load Balancers
- **SSL/TLS Termination** – decrypts incoming HTTPS traffic to reduce server load.  
- **Health Checks** – continuously monitors server status and removes unhealthy servers from rotation.  
- **Content-Based Routing** – directs requests based on URL path, headers, or cookies.  
- **Caching & Compression** – some load balancers can cache responses or compress content to improve performance.

## Key Takeaways
- Load balancers **improve scalability, performance, availability, and security** of web services.  
- Can use **various algorithms** to distribute traffic efficiently.  
- Critical component in **real-world production environments** with multiple web servers.  
- Modern load balancers provide **advanced features** like SSL termination, health checks, and content routing.
