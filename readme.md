# Advanced Distributed Systems, Enterprise Architecture and Cloud Computing — Model Answers

# SECTION A: QUESTION ONE — AGRIMART

## Question 1(a): Distributed Systems — Definition, Aspects, Advantages and Challenges (10 marks)

**Definition:** A distributed system is a collection of independent computers that appear to users as a single coherent system, communicating and coordinating by passing messages over a network.

**Hardware and software aspects**

- **Hardware:** The computers are autonomous. Each branch, warehouse and head-office server can operate independently.
- **Software:** Users perceive the distributed computers as one system. For example, a cashier interacts with one AgriMart system rather than separate branch, warehouse and head-office computers.

**Advantages over a centralised system**

1. **Economics:** Several smaller computers can provide better price-performance than one expensive mainframe, avoiding a costly mainframe upgrade.
2. **Speed:** Processing loads are distributed across multiple computers, reducing bottlenecks during busy periods such as month-end.
3. **Inherent distribution:** Processing can take place where the work occurs. Branches can process local sales while warehouses manage inventory.
4. **Reliability:** Failure of one computer need not stop the entire system. A branch can potentially continue operating if another branch's server fails.
5. **Incremental growth:** Capacity can be added gradually by installing servers for new branches or services rather than replacing the entire central system.

**Challenges in designing a distributed system**

| Challenge | Explanation | AgriMart example |
|---|---|---|
| Heterogeneity | Different hardware, operating systems, networks and programming languages must work together. | Linux, Windows, vendor-specific systems and mobile scanners. |
| Openness | Components must use well-defined interfaces and protocols to support interoperability and extension. | Integrating the planned online shopping service. |
| Security | Distributed resources require authentication, authorisation, encryption and protection against attacks. | Protecting customer records across many computers. |
| Scalability | The system must remain effective as users, resources and locations increase. | Adding branches and customers. |
| Failure handling | Computers, processes and network links may fail independently. | A branch loses its connection to head office. |
| Concurrency | Multiple processes may access and update the same resources simultaneously. | Several tills update the same stock record. |
| Transparency | Distribution should be hidden from users where practical. | Staff should experience one coherent AgriMart system. |
| Quality of Service (QoS) | The system must meet requirements for performance, reliability, availability and security. | Maintaining acceptable response times during month-end. |

A distributed system can improve cost, performance and reliability, but these benefits depend on appropriate architecture, coordination, security and failure-handling mechanisms.

## Question 1(b): Transparency, Openness, Scalability, Replication and Caching (10 marks)

**Transparency** means hiding the distributed nature of resources and processes so that users experience the system as coherent.

The main types of transparency are:

1. **Access transparency:** Hides differences in how local and remote resources are accessed.
2. **Location transparency:** Hides the physical location of a resource.
3. **Migration transparency:** Allows a resource to move without affecting how it is accessed.
4. **Relocation transparency:** Allows a resource to move while it is being used without disrupting access.
5. **Replication transparency:** Hides the existence of multiple copies of a resource.
6. **Concurrency transparency:** Allows several users to access shared resources safely.
7. **Failure transparency:** Hides failures and recovery where possible.
8. **Persistence transparency:** Hides whether a resource is in memory or on persistent storage.

At AgriMart, location transparency allows a branch to request stock information without knowing which warehouse server holds it. Concurrency transparency helps prevent simultaneous till transactions from corrupting stock records. Replication transparency allows staff to use price lists without needing to know how many copies exist.

Complete transparency is not always possible. For example, a slow server may be difficult to distinguish from a failed server, and attempts to hide every failure can increase cost and reduce performance.

**Openness** means that distributed services follow well-defined rules for syntax and semantics, enabling interoperability, portability and extension. Standard interfaces allow AgriMart's Linux, Windows, vendor-specific and mobile systems to communicate. They also make it easier to add the online shop without redesigning the entire system.

An open system should provide mechanisms that applications can use according to their requirements, rather than imposing inflexible policies.

**Three dimensions of scalability**

1. **Size scalability:** The system remains effective as the number of users, computers or resources increases. AgriMart must support additional branches, tills and customers.
2. **Geographical scalability:** The system remains effective when computers are separated by greater distances and network latency increases.
3. **Administrative scalability:** The system can operate across multiple administrative organisations or management domains.

**Four techniques for achieving scalability**

1. **Hiding communication latency:** Perform local or asynchronous processing so users do not need to wait for every remote operation. Branches can process local sales without contacting head office for every action.
2. **Distribution:** Divide data and processing across several computers. Each branch server can handle local transactions.
3. **Replication:** Maintain copies of data on multiple computers. AgriMart can replicate price lists to branches to reduce remote access.
4. **Caching:** Store recently used data close to the client. Branches can cache frequently accessed customer records to reduce latency and network traffic.

**The problem introduced by replication and caching**

Replication and caching create multiple copies of data. When one copy changes, other copies may become stale, producing inconsistency.

For example, head office changes an item's price from RWF 2,000 to RWF 2,200, but a branch cache still contains the old price. That branch may temporarily charge RWF 2,000. Similarly, loyalty points may differ between branches.

Keeping all copies perfectly consistent requires coordination and synchronisation, which can increase network traffic, latency and system complexity. At large scale, synchronising every copy immediately may be impractical.

AgriMart should apply consistency controls according to the importance of the data. Loyalty points should use an authoritative record and reliable update coordination. Prices should propagate quickly, with suitable cache-expiry or invalidation rules. Temporary inconsistency may be acceptable for some information but not for data that directly affects financial transactions.

## Question 1(c): Network Operating Systems, Distributed Operating Systems, Middleware, and Communication Models (10 marks)

### Comparison of Network Operating Systems, Distributed Operating Systems and Middleware

| Criterion | Network Operating System (NOS) | Distributed Operating System (DOS) | Middleware |
|---|---|---|---|
| Operating systems | Each computer has its own operating system, which may differ from others. | The operating systems cooperate and are aware of other computers in the system. | Existing operating systems need not be identical or know about each other. |
| Transparency | Users may need to know which machine provides a resource. | Aims to present distributed resources as a unified system. | Provides common services that hide selected distribution details. |
| Communication | Commonly uses network services and file-oriented access. | Coordinates communication among distributed computers. | Provides communication services appropriate to the middleware model. |
| Resource management | Resources are often managed on individual computers. | Aims for coordinated or global resource management. | Adds common services while retaining the existing operating systems. |
| Practical use | Common in networked environments. | More difficult to implement and less common. | Useful for integrating heterogeneous existing systems. |

AgriMart should use **middleware** because its Linux, Windows and vendor-specific computers must communicate without replacing their operating systems.

### Four categories of middleware services

1. **Communication services:** Enable processes to exchange information using remote procedure calls (RPC), remote method invocation (RMI), message queues and event notification.  
   *Example:* A message queue delivers a branch's reorder request to the appropriate warehouse.

2. **Information-system services:** Provide naming, directory, location, persistent-storage, caching and replication services.  
   *Example:* A naming service helps a branch locate an inventory server.

3. **Control services:** Coordinate activities through services such as distributed transactions and code migration.  
   *Example:* A distributed transaction coordinates related inventory updates.

4. **Security services:** Provide authentication, authorisation, encryption and auditing.  
   *Example:* Authentication and authorisation restrict access to AgriMart's loyalty database.

### Client-server versus peer-to-peer

| Criterion | Client-server | Peer-to-peer (P2P) |
|---|---|---|
| Roles | Clients request services; servers provide and manage shared resources. | Peers perform similar roles and can both request and provide resources. |
| Control | Servers provide defined points of control for their services. | No central coordination is required by the basic model. |
| Resources | Shared resources are commonly managed by servers. | Resources such as processing power, storage and bandwidth are contributed by peers. |
| Management | Easier to establish central authority, access control and auditing. | Coordination, consistency and governance can be more difficult. |
| AgriMart example | Branches request authoritative stock information from warehouse servers. | Branches and warehouses share stock data as peers. |

**Recommendation:** AgriMart should use client-server architecture for authoritative stock and pricing because ownership, access control and auditing are easier to manage. Peer-to-peer communication may be useful for optional sharing where central authority is unnecessary.

## Question 1(d): Multiprocessors, SMP, ASMP, Shared Memory, Message Passing and Heterogeneity (10 marks)

A **multiprocessor** is a computer system with two or more processing units that share main memory and peripherals and can process programs simultaneously. A **multicomputer**, by contrast, consists of separate computers with private memories that communicate through messages.

**Symmetric multiprocessing (SMP)** treats all processors equally. **Asymmetric multiprocessing (ASMP)** reserves some processors for specific purposes or assigns them different roles.

### Shared-memory versus message-passing architectures

| Criterion | Shared memory | Message passing |
|---|---|---|
| Address space | Processors share an address space. | Each processor has its own address space. |
| Communication | Processors communicate through memory reads and writes. | Processors exchange explicit messages. |
| Coordination | Shared data requires synchronisation to prevent conflicts. | Coordination is performed through message exchanges and protocols. |
| Latency | Often lower on a small, tightly coupled machine. | Communication overhead can be higher, particularly for remote operations. |
| Scalability | Contention for shared memory or interconnects may limit growth. | Can scale across separate computers but requires more communication management. |

AgriMart's separate branch and warehouse servers form a multicomputer arrangement and communicate through messages rather than sharing one physical memory space.

**Heterogeneity at AgriMart**

- **Node heterogeneity:** The system contains high-end servers at head office, Windows PCs in branches, older vendor-specific warehouse computers and mobile barcode scanners.
- **Network heterogeneity:** It may include high-speed local-area networks inside branches, wireless links for handheld devices and wide-area Internet connections with greater latency between branches, warehouses and head office.

Middleware and standard communication protocols help hide these differences so that the heterogeneous components can work together.

## Question 1(e): Architectural Questions, Communication Paradigms and Caching (10 marks)

### Four key architectural questions

1. **Which entities communicate?** These may be processes, nodes, threads, objects or components.
2. **How do they communicate?** The architecture must specify the communication paradigm.
3. **What are their roles and responsibilities?** For example, an entity may act as a client, server or peer.
4. **How are they placed on the physical infrastructure?** The design must determine which computers host the entities and how those computers connect.

### Communication paradigms

**1. Inter-process communication (IPC)**

IPC is communication between processes through message-passing primitives or network interfaces such as sockets. For example, a branch process sends a stock query to a warehouse server through a network socket.

**2. Remote invocation**

Remote invocation allows a process to request an operation from another process across a network. It commonly uses a request-reply exchange.

- **Request-reply protocols:** A client sends a request and receives a response.
- **Remote procedure call (RPC):** Allows a process to invoke a procedure in another process using an interface that resembles a local procedure call.
- **Remote method invocation (RMI):** Provides similar functionality for methods of distributed objects.

For example, a till invokes a remote `getPrice` operation to retrieve the current price of an item.

**3. Indirect communication**

Indirect communication allows senders and receivers to communicate without directly addressing one another. It can provide:

- **Space uncoupling:** The sender does not need to know the receiver's identity or location.
- **Time uncoupling:** The sender and receiver do not need to be active at the same time.

For example, head office publishes a price-update message to a messaging service, and branches receive it when they are connected.

### How a caching service works

A cache stores recently used data objects closer to the client than the original server.

1. A client requests a data object.
2. The cache checks whether it contains a valid, up-to-date copy.
3. On a **cache hit**, the cache returns the object without contacting the original server.
4. On a **cache miss**, the cache fetches the object from the original server.
5. The fetched object is stored in the cache, potentially replacing an older object.
6. The cache must use suitable expiry, validation or invalidation rules to prevent stale data from being served.

A cache may be located on each client or in a shared proxy server. At AgriMart, caching a price list at each branch reduces remote requests and improves response time. However, the cache must be refreshed when prices change.

# SECTION B: QUESTION TWO — MEDCONNECT HEALTH

## Question 2(a): Cloud Computing, Architecture Diagram and Characteristics (7 marks)

Cloud computing is a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources—such as networks, servers, storage, applications and services—that can be rapidly provisioned and released with minimal management effort or service-provider interaction.

Cloud computing is a **service and business model enabled by technologies such as virtualisation**, rather than simply a new technology.

### Cloud computing architecture

```text
                 FRONT END
          +----------------------+
          | Clinic staff         |
          | Browsers and apps    |
          | Computers and phones |
          +----------+-----------+
                     |
                     | Requests and responses
                     v
               +-----------+
               | Internet  |
               +-----+-----+
                     |
                     v
                  BACK END
       +-----------------------------+
       | Cloud provider               |
       | +-----------+ +------------+ |
       | | Servers   | | Storage    | |
       | +-----------+ +------------+ |
       | | Databases | | Applications| |
       | +-----------+ +------------+ |
       | Resource management/metering |
       +-----------------------------+
