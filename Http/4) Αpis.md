# APIs

## What is an API
- **API (Application Programming Interface)** is a set of rules and protocols that define how software components communicate.
- Acts as a **contract** between applications, specifying how one program can use another's functionality.
- Enables **data exchange** and **integration** between different systems, services, and applications.

## Types of APIs

- **REST API (Representational State Transfer) ⭐**  
  - Most common today.  
  - **Stateless** architecture (doesn’t store previous interactions).  
  - Uses **JSON** for data transfer.  
  - Lightweight and suitable for **web and mobile apps**.  
  - Ideal for CRUD operations and simple service integration.  

- **GraphQL API ⭐**  
  - Retrieves **only the data you need** in a single request.  
  - Uses **JSON**.  
  - Flexible and efficient for modern applications.  
  - Good for apps with complex data models or multiple client types.  

- **gRPC API (Remote Procedure Call)**  
  - Supports **multiple programming languages**.  
  - Uses **Protocol Buffers** for communication.  
  - High performance for **microservices** and lightweight payloads.  
  - Suitable for internal service-to-service communication.  
  - Offers built-in support for **streaming data**.  

- **WebSocket API ⭐**  
  - Enables **bidirectional, event-driven communication**.  
  - Provides **persistent connections**.  
  - Ideal for applications requiring **low latency**, like chat, live updates, or gaming.  
  - Can be used alongside REST or GraphQL for real-time features.  


## API Use Cases

- **System Integration** – Connects disparate systems or services through a common interface.  
- **Software Development** – Developers access functionality of libraries/services without building from scratch.  
- **Mobile Applications** – Apps communicate with backend services to access data and complex functionality.  
- **Task Automation** – Scripts or programs call APIs to perform repetitive tasks automatically.
