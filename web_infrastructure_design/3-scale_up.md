```mermaid
graph TD
    User["User's Computer / Browser"] -->|Requests www.foobar.com| DNS["DNS Resolver"]

    DNS -->|Resolves to Load Balancer Cluster IP| LBCluster["HAProxy Load Balancer Cluster"]

    subgraph LBClusterBox["Load Balancer Cluster"]
        LB1["HAProxy Load Balancer 1"]
        LB2["HAProxy Load Balancer 2"]
    end

    LBCluster --> LBClusterBox

    LB1 -->|Forwards traffic| WebServer["Server 1: Web Server"]
    LB2 -->|Forwards traffic| WebServer

    LB1 -. Cluster failover .-> LB2

    subgraph WebServerBox["Server 1 - Web Layer"]
        Nginx["Web Server: Nginx"]
    end

    WebServer --> WebServerBox

    Nginx -->|Forwards dynamic requests| AppServer["Server 2: Application Server"]

    subgraph AppServerBox["Server 2 - Application Layer"]
        App["Application Server"]
        Code["Application Files / Codebase"]

        App -->|Uses| Code
    end

    AppServer --> AppServerBox

    App -->|Reads/Writes data| DBServer["Server 3: Database Server"]

    subgraph DBServerBox["Server 3 - Database Layer"]
        MySQL["MySQL Database"]
    end

    DBServer --> DBServerBox

    ExtraServer["Server 4: Extra Server"]
    ExtraServer -->|Can be used for more web, app, or database capacity| LBCluster
```
