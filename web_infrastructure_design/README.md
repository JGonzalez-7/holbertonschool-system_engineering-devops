# Web Infrastructure Design

This project explores the components, communication paths, benefits, and
limitations of several web infrastructure architectures. Each task is
represented by a Mermaid diagram for the fictional domain `www.foobar.com`.

## Learning Objectives

By completing this project, you should be able to explain:

- How DNS resolves a domain name to an IP address
- The roles of web servers, application servers, and databases
- How clients and servers communicate over a network
- Why load balancers are used and how traffic is distributed
- How primary-replica database clusters work
- The purpose of firewalls, HTTPS, SSL certificates, and monitoring
- Common single points of failure and strategies for scaling infrastructure

## Diagrams

| File | Architecture | Description |
| --- | --- | --- |
| [`0-simple_web_stack`](0-simple_web_stack) | Simple web stack | A single server runs Nginx, the application server, application files, and MySQL. |
| [`1-distributed_web_infrastructure`](1-distributed_web_infrastructure) | Distributed infrastructure | HAProxy distributes requests between two servers backed by a primary-replica MySQL setup. |
| [`2-secured_and_monitored_web_infrastructure`](2-secured_and_monitored_web_infrastructure) | Secured and monitored infrastructure | Adds firewalls, HTTPS/SSL termination, and monitoring clients to the distributed design. |
| [`3-scale_up`](3-scale_up) | Scaled infrastructure | Uses a load-balancer cluster and separates the web, application, and database layers onto dedicated servers. |

## Architecture Progression

### 0. Simple Web Stack

The first design hosts every service on one machine:

- Nginx receives web requests.
- The application server executes the application logic.
- The codebase provides the application files.
- MySQL stores persistent data.

This setup is straightforward but creates a single point of failure and makes
independent scaling or maintenance difficult.

### 1. Distributed Web Infrastructure

The second design introduces:

- HAProxy for round-robin load balancing
- Two application servers
- A MySQL primary database and replica

This improves capacity and availability, but the load balancer and database
primary can still become single points of failure.

### 2. Secured and Monitored Web Infrastructure

The third design adds:

- Firewalls to restrict incoming traffic
- An SSL certificate for encrypted HTTPS connections
- Monitoring clients that collect logs and performance metrics

These components improve security and observability. The design still needs
careful handling of SSL termination, database writes, and load-balancer
redundancy.

### 3. Scale Up

The final design separates services by responsibility:

- Two HAProxy instances provide load-balancer redundancy.
- Nginx runs on a dedicated web server.
- The application server and codebase run on a dedicated application server.
- MySQL runs on a dedicated database server.
- An additional server provides room for more capacity.

This separation allows each layer to be maintained and scaled more
independently.

## Viewing the Diagrams

The task files contain fenced Mermaid syntax. Open them in a Markdown viewer
with Mermaid support, or paste their contents into the
[Mermaid Live Editor](https://mermaid.live/).
