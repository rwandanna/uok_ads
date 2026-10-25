# Exam Coaching Guide: All Five Questions

**Advanced Distributed Systems · Enterprise Architecture · Cloud Computing**

Every sub-question (1a–5c) is coached in four steps: **(1) what the examiner wants, (2) concept breakdown, (3) variation survival guide, (4) model answer.** Lists are taken from **your lecturer's slides**, because the scenarios are written to trigger those exact lists.

---

## 0. Read first (3 minutes)

### 0.1 My verdict on your two drafts

- **Long draft:** thorough, well organised, honest about assumptions, with useful extras (stale-price example, cache privacy, downtime calculation, mistakes list). **But** it fills gaps with generic textbook lists instead of the lecturer's lists, and it misread Figure 2.
- **Short draft:** good compact structure and mostly sensible recommendations. **But** several answers are too thin for the marks, and a few are wrong against the slides (see the table).
- **Best use:** keep their structure and examples, but **replace the generic lists with the slide lists below.** Marks follow the lecturer's wording.

### 0.2 Where the drafts differ from the slides (use the right-hand column)

| Topic | Drafts say | Slides say (write this) |
| --- | --- | --- |
| **Four architectural questions (1e)** | Components / how connected / where placed / how coordinated | **(1) Entities that communicate, (2) Communication paradigm, (3) Roles and responsibilities, (4) Placement on physical infrastructure** |
| **Middleware service groups (1c, 5a)** | RPC, message queues, naming, transactions, web services | **Communication, Information system, Control, Security** (examples under each) |
| **SMP vs ASMP (1d)** | Short draft: master/slave CPUs | **SMP: all processors treated equally. ASMP: some processors reserved for special purposes** |
| **Node/network heterogeneity (1d)** | x86 vs ARM, endianness; or generic hardware/OS/language | **Node:** parallel systems, high-end PCs/servers, simple network computers, mobile computers. **Network:** local gigabit LANs, wireless, long-haul high-latency (POTS), wide-area switched megabit links |
| **Service contract (3c)** | WSDL, OpenAPI, schemas, SLAs | **Functional description; input requirements and output specifications; precondition; postcondition; error handling** |
| **Migration strategies (2c)** | Retain / retire / refactor | **Rehost (lift-and-shift), Re-platform, Repurchase, Rebuild/re-architect** |
| **SaaS shading (2b)** | Short draft shades Data as provider-managed | **You are always responsible for your data**: shade **Data** even under SaaS (add a one-line note) |
| **Figure 2 reading (2c)** | Long draft: demand 10–20, peak \~40 then 30 | **Your photo shows \~20 servers in most months, climbing from about August and reaching \~55–60 in Nov–Dec, against 60 installed** (check your own paper) |
| **Field sales architecture (4b)** | Long draft recommends server-centric | **Client-centric = better response time (but lacks security); server-centric = secure, no client software, but slower.** Field staff want the quickest response, so client-centric suits them, with security safeguards |
| **Cloud ERP and IP (4c)** | Long draft leans to leasing | Slides: cloud has a **conflict of interest** (provider may copy your application) and is **not suited to highly competitive industries where intellectual property is hard to protect** |

### 0.3 Rules that apply to every answer

1. **Marks ≈ number of distinct, explained points.** A 10-mark part needs about 8–10 points. About 1 mark per minute is a safe pace.
2. **Five-step answer formula:** **Define** (slide wording) → **List** the slide's items (numbered) → **Link** each to the scenario in one clause → **Trade-off** → **Recommend, justify, name the risk and its mitigation.**
3. **Scenarios mirror slide lists.** If a manager “fears it is costly, time-consuming, needs strong security, has inconsistent performance” (Q3), that **is** the slide's list of SOA drawbacks. Spot the echo, use the list.
4. **Recommendations:** pick **one** option, justify it with **two or three facts from the scenario**, and name the main risk of your choice. Either side can earn marks if justified.
5. **Diagrams:** draw boxes, label every box, show arrow direction, add a title. Never leave a requested diagram out.
6. **Choosing two from Q2–Q5:** Q2 (cloud, with a free-mark SLA calculation) and Q4 (ERP, with a table to copy) are the most list-driven. Choose the two where you recall the lists best.

---

# SECTION A: QUESTION ONE (AgriMart, 50 marks, compulsory)

**What the scenario is signalling:** six-hour mainframe outage (**reliability**), month-end slowness (**speed**), expensive upgrade (**economics**), new branches and online shop (**scalability, incremental growth**), mixed Linux/Windows/vendor OS/mobile (**heterogeneity, middleware**), “one single system” (**transparency**), price list and loyalty points out of step (**replication/caching inconsistency**), security worry, link failure (**failure handling**), client-server vs peer-to-peer (**architecture roles**).

---

## 1(a) Define; hardware and software aspects; advantages; challenges (10 marks)

### 1. What the examiner wants

- Definition + **two aspects** (hardware: autonomous computers; software: users see a single system).
- **Advantages over a centralised system:** economics, speed, inherent distribution, reliability, incremental growth.
- **Challenges:** the eight on the slides.
- Rough mark split (my estimate): definition 2, aspects 1–2, advantages 3, challenges 3–4.

### 2. Concept breakdown

- **Definition:** a collection of **independent computers that appear to users as a single coherent system**, coordinating **only by passing messages**.
- Each advantage answers one symptom in the story:

| Scenario symptom | Advantage |
| --- | --- |
| Larger mainframe “far more expensive” | **Economics:** many microprocessors give better price/performance |
| Tills slow at month-end | **Speed:** more total computing power, load spread across machines |
| 40 branches and 3 warehouses already spread out | **Inherent distribution:** a supermarket chain is naturally distributed |
| Mainframe fault stopped all 40 branches | **Reliability:** one machine failing does not stop the whole system |
| New branches and online shop; months to deliver a mainframe | **Incremental growth:** add capacity in small steps |

- Do not claim a DS is *automatically* cheaper or more reliable. These are **potential** benefits that depend on design (a point the long draft rightly stresses).

### 3. Variation survival guide

- “Over centralised” = **E-S-I-R-I** (Economics, Speed, Inherent distribution, Reliability, Incremental growth). “Over independent PCs” = **data sharing, resource sharing, communication, flexibility.**
- Challenges = **H-O-S-S-F-C-T-Q:** Heterogeneity, Openness, Security, Scalability, Failure handling, Concurrency, Transparency, QoS. Match each to a scenario clue (table in the model answer).
- Change the company (bank, hospital, university) and the structure stays the same: define, aspects, five advantages, eight challenges.

### 4. Model answer

**Definition.** A distributed system is a collection of independent computers that appear to users as a single coherent system, communicating and coordinating only by passing messages over a network.

**Aspects.** *Hardware:* the computers are **autonomous**: each branch, warehouse and head-office server runs independently. *Software:* users **think they are using one system**: a cashier sees one AgriMart system.

**Advantages over the mainframe.**

1. **Economics:** many microprocessors give better price/performance than one mainframe, so AgriMart avoids the costly upgrade.
2. **Speed:** total computing power is greater and load is shared, so month-end tills no longer queue behind one machine.
3. **Inherent distribution:** a chain of branches and warehouses is naturally distributed, so processing sits where the work happens.
4. **Reliability:** if one machine fails the rest continue, so a fault would not stop all 40 branches for six hours.
5. **Incremental growth:** capacity is added in small steps, such as a server for each new branch or the online shop.

**Challenges in design.**

| Challenge | Meaning | AgriMart link |
| --- | --- | --- |
| **Heterogeneity** | Different networks, OSs, hardware, languages | Linux, Windows, vendor OS, mobile scanners |
| **Openness** | Extensible; components by different programmers integrate | Adding the online shop later |
| **Security** | Encryption; denial-of-service threats | More computers hold sensitive data |
| **Scalability** | Cost of adding a user stays constant | New branches and customers |
| **Failure handling** | Any process, computer or link can fail independently | Branch-to-head-office link fails |
| **Concurrency** | Many simultaneous requests; resources must be safe | Many tills updating one stock record |
| **Transparency** | Hide distribution from programmers and users | “One single system” |
| **QoS** | Guarantee performance, security, reliability | Month-end response times |

---

## 1(b) Transparency, openness, scalability; dimensions, techniques; replication/caching problem (10 marks)

### 1. What the examiner wants

- Each goal defined **and** applied to AgriMart.
- Scalability: **three dimensions**, **four techniques**, and the **problem: inconsistency**, with AgriMart examples. Without examples you lose the application marks.

### 2. Concept breakdown

- **Transparency:** hiding that processes and resources are physically distributed. **Eight types:** Access, Location, Migration, Relocation, Replication, Concurrency, Failure, Persistence (**A-L-M-R-R-C-F-P**).
- **Openness:** services offered by **standard rules for syntax and meaning** (e.g., interfaces in an **IDL**); supports **portability** and **interoperability**; provides **mechanisms, not fixed policies** (a policy is a decision, such as how fresh cached data must be; a mechanism is the tool that lets each application choose).
- **Scalability, three dimensions:** **size** (users/processes), **geographical** (distance between nodes), **administrative** (number of administrative domains).
- **Four techniques:** **hiding communication latency**, **distribution** (partition data and work), **replication** (copies), **caching** (clients keep local copies).
- **The problem:** copies make changes inconsistent. Keeping all copies consistent needs **global synchronisation** on every change, which is impractical at scale. If the application can **tolerate some inconsistency**, synchronisation can be reduced; what is tolerable depends on the application.
- **Stale-price example (from the long draft):** head office changes a price from RWF 2,000 to RWF 2,200; a branch cache still holds 2,000 and briefly charges the old price. That is exactly AgriMart's pilot problem.

### 3. Variation survival guide

- Matching scenario actions to techniques: branch servers each run their own tills = **distribution**; price list copies = **replication**; cached customer records = **caching**; tills keep working without waiting for head office = **hiding latency**.
- Replication is *deliberate copies on other machines*; caching is *a client's local copy of recently used data*. Do not merge them.
- Template for the problem: *copies → one changes → others stale → global synchronisation needed → impractical → tolerate inconsistency where harmless, enforce prompt updates where harmful.*

### 4. Model answer

**Transparency** hides the physical distribution of processes and resources. Examples: *access* (Linux and Windows data formats hidden), *location* (a branch queries stock without knowing which warehouse server holds it), *replication* (copies of the price list hidden), *concurrency* (two tills update one stock record safely), *failure* (a failed server's recovery hidden); the others are migration, relocation and persistence. Limits: failures cannot be fully hidden because a slow server cannot be told from a failed one, and full transparency costs performance.

**Openness** means services follow standard rules for syntax and semantics, such as IDL interfaces. Well-defined interfaces let AgriMart's Linux, Windows, vendor-specific and mobile systems interoperate, keep applications portable, and allow the online shop to be added without redesign. The system should provide mechanisms (such as per-item caching policies) rather than fixed policies.

**Scalability dimensions.** *Size:* more tills, customers and branches beyond 40. *Geographical:* branches linked over the Internet across long distances. *Administrative:* head office, regional warehouses and any partner organisations under different management.

**Techniques.** (1) *Hiding latency:* tills complete sales locally instead of waiting for head office. (2) *Distribution:* each branch server handles its own tills and stock. (3) *Replication:* copies of the price list at every branch. (4) *Caching:* branches keep recently used customer records.

**The problem.** Replication and caching create several copies, so changing one makes the others inconsistent. In the pilot, a head-office price change left some branches charging the old price, and loyalty points differed between two branches. Keeping every copy consistent requires global synchronisation on each update, which is practically impossible at scale. AgriMart should tolerate short lags where harmless and enforce prompt updates where errors cost money or trust, for example a single authoritative record for loyalty points and quick propagation (or short expiry) for prices. What is tolerable depends on the application.

---

## 1(c) NOS vs DOS vs middleware; middleware categories; client-server vs P2P (10 marks)

### 1. What the examiner wants

- Three software concepts compared on stated criteria.
- **Four middleware service categories with one example each** (communication, information system, control, security).
- Client-server vs P2P compared, ideally with an AgriMart choice.

### 2. Concept breakdown

- **NOS:** each computer has its **own OS** with networking; nodes work **independently** (may run different OSs); services tied to individual nodes (ftp, telnet, WWW); **file-oriented**.
- **DOS:** the OS on each computer **knows about the others**; services **transparently distributed**. Hard on multicomputers because **memory is not shared**: no simple global communication, synchronisation or central resource management. **Very few exist** (e.g., Amoeba).
- **Middleware:** a layer **between OS and applications**; OSs **need not be the same or know each other**; connects existing systems, which is why AgriMart needs it.
- The slide lists only the comparison **criteria** (transparency, same OS?, copies of OS, communication basis, resource management, scalability, openness). The cell values below are reasoned from the slide descriptions.

### 3. Variation survival guide

- Use fixed rows for any three-way comparison: **OS per node, awareness of others, transparency, communication basis, resource management.**
- Middleware services = **C-I-C-S** (Communication, Information system, Control, Security). Add an example from the scenario.
- Client-server vs P2P: compare **roles, control, resource provision, example.** If asked to choose, justify with the scenario.

### 4. Model answer

| Criterion | Network OS | Distributed OS | Middleware |
| --- | --- | --- | --- |
| OS on each node | Own OS, may differ | OS knows the others | Local OSs need not be the same or know each other |
| Transparency | Low | High | High (transparently distributed services) |
| Communication basis | Mostly shared files | Messages (no shared memory) | Model-specific communication services |
| Resource management | Per node | Global, hard to build | Per node, with services layered on top |
| Practicality | Common | Very few exist | Integrates existing systems |

AgriMart should use **middleware**, because its Linux, Windows and vendor-specific machines must keep their own operating systems.

**Middleware service categories.**

1. **Communication:** remote procedure calls, remote method invocation, message queuing, event notification. *Example:* a message queue carries a branch's reorder request to a warehouse.
2. **Information system:** naming, directory and location services, persistent storage, caching and replication. *Example:* a naming service finds the nearest inventory server.
3. **Control:** distributed transactions, code migration. *Example:* a distributed transaction updates branch and warehouse stock together.
4. **Security:** authentication and authorisation, encryption, auditing. *Example:* authentication limits access to the loyalty database.

|  | Client-server | Peer-to-peer |
| --- | --- | --- |
| Roles | Distinct: clients request, servers manage shared resources (a server may itself be a client) | Similar roles; peers equally privileged |
| Control | Servers central to each service | **No central coordination** |
| Resources | Held by servers | Each peer shares part of its processing, storage and bandwidth |
| AgriMart | Branches ask dedicated warehouse servers for stock | Branches and warehouses share stock data as equals |

**Recommendation:** client-server for authoritative stock and prices (clear ownership, easier control and audit); P2P only for optional sharing where no single authority is needed.

---

## 1(d) Multiprocessor; SMP vs ASMP; shared memory vs message passing; heterogeneity (10 marks)

### 1. What the examiner wants

- Multiprocessor defined; SMP and ASMP contrasted **as on the slides**; the two communication architectures compared; **node and network heterogeneity** categorised, ideally mapped to AgriMart.

### 2. Concept breakdown

- **Multiprocessor:** a computer system with **two or more processing units sharing main memory and peripherals**, processing programs simultaneously. (A **multicomputer** has separate computers with **private memory** using messages.)
- **SMP:** all processors **treated equally**. **ASMP:** some processors are **reserved for special purposes**.

|  | Message passing | Shared memory |
| --- | --- | --- |
| Address space | Separate for each processor | Shared |
| Communication | Messages; local message-queue memories | Memory reads and writes |
| Notes | Designs focus on costly non-local operations | Easy on small machines; **lower latency** |

- Distinguishing features of hardware designs: **private vs shared memory** and **bus vs switched** interconnection.
- **Heterogeneity in a network of computers:** node heterogeneity (**parallel systems, high-end PCs and servers, simple network computers, mobile computers**) and network heterogeneity (**local gigabit LANs, wireless, long-haul high-latency POTS connections, wide-area switched megabit links**). An ideal DS **hides** these differences.

### 3. Variation survival guide

- Memory comparisons: always use rows **address space, communication method, latency, suitability.**
- Heterogeneity: split into **nodes** and **networks**, then place each machine and link in the scenario into a slide category.
- Do not call a set of branch servers a multiprocessor: a multiprocessor **shares memory**.

### 4. Model answer

A **multiprocessor** is a computer system with two or more processing units sharing main memory and peripherals so that programs are processed simultaneously. In **SMP** all processors are treated equally; in **ASMP** some processors are reserved for special purposes.

In **shared-memory** architecture processors share one address space and communicate by reading and writing memory: easy on small machines and lower latency. In **message-passing** architecture each processor has its own address space and communicates by explicit messages, with local message-queue memories, and designs focus on the costly non-local operations. AgriMart's separate branch servers are a message-passing (multicomputer) arrangement.

**Heterogeneity at AgriMart.** *Nodes:* high-end servers (head-office Linux servers), PCs (branch Windows PCs), older vendor-specific warehouse machines (simple computers), and mobile computers (handheld scanners). *Networks:* local high-speed LANs inside branches, wireless links for handhelds, and wide-area links with higher latency between branches, warehouses and head office. The distributed system should hide these differences from users.

---

## 1(e) Four architectural questions; communication paradigms; caching service (10 marks)

### 1. What the examiner wants

- The **four questions stated correctly**, three paradigms with sub-types, and the caching workflow.

### 2. Concept breakdown

**The four questions (E-C-R-P):**

1. What are the **entities** that communicate? (processes; nodes in sensor networks; threads as endpoints; objects and components as abstractions)
2. **How** do they communicate: which **communication paradigm**?
3. What **roles and responsibilities** do they have? (client-server, peer-to-peer)
4. How are they **mapped onto the physical infrastructure** (placement)?

**Communication paradigms:**

- **Inter-process communication:** message-passing primitives and direct use of Internet-protocol APIs (**socket programming**).
- **Remote invocation:** two-way exchange calling a remote operation: **request-reply protocols** (basis of client-server), **RPC** (call a procedure in another process as if local), **RMI** (the same for distributed objects). Sender and receiver are directly linked.
- **Indirect communication:** the sender need not know the receiver (**space uncoupling**) and they need not exist at the same time (**time uncoupling**). ⚠ The slide misprints this as “time coupling”; write *time uncoupling*.

**Caching service:** a cache is a store of **recently used data objects closer to the client** than the objects themselves. New objects replace old ones. On a request the service **checks for an up-to-date copy**; if it has none it **fetches** one. Caches may be **in each client** or in a **shared proxy server**.

### 3. Variation survival guide

- “State the key questions” is pure recall: memorise **E-C-R-P**.
- Paradigms: three headings, each with definition → sub-types → key feature → scenario example.
- Caching: always give **request → check for up-to-date copy → hit (serve) or miss (fetch, store, replace old) → where it sits → benefit and the freshness problem.**

### 4. Model answer

**Four key questions:** (1) which **entities** communicate; (2) which **communication paradigm** they use; (3) what **roles and responsibilities** they have (client, server, peer); (4) how they are **placed on the physical infrastructure**.

**Paradigms.** *Inter-process communication* is low-level message passing and socket programming, for example a branch process sending a stock query to a warehouse over a socket. *Remote invocation* is a two-way exchange: request-reply protocols support client-server computing, RPC calls a procedure in a remote process as if local, and RMI does the same for distributed objects; for example a till calls a remote get-price procedure. *Indirect communication* uncouples sender and receiver in space and time; for example head office posts a price update that branches collect when they are online.

**Caching service.** A cache holds recently used data objects closer to the client. When a request arrives, the caching service checks for an up-to-date copy. If one exists (a hit) it is returned without contacting the server; otherwise (a miss) the object is fetched, stored, and replaces an older object. Caches sit in each client or in a shared proxy server. At AgriMart a branch cache holding the price list avoids a remote request for every scan, cutting response time and traffic, but it must be refreshed or it will serve stale prices.

---

# SECTION B: Answer ANY TWO (25 marks each)

---

# QUESTION TWO: MedConnect Health (cloud computing)

**Scenario signals:** equipment bought up front and 25 IT staff (**CAPEX, in-house cost**); year-end spike of 2–3× and idle servers (**elasticity, cloud bursting**); developers wait months (**agility, on-demand self-service**); managers think cloud is “a new technology” (**cloud is a service model**); email tools / mobile-app platform / rented virtual servers (**SaaS / PaaS / IaaS**); patient data must stay under company control (**private/hybrid**); legacy proprietary billing (**migration strategy**); 99.5% SLA and 97.8% pilot (**calculation**); platform works only with its own tools (**vendor lock-in**); CFO on costs (**CAPEX → OPEX**).

---

## 2(a) Cloud diagram; NIST definition; two characteristics (7 marks)

### 1. What the examiner wants

- A **labelled diagram**: front end, Internet, back end.
- The **NIST definition** (close to word-for-word).
- **Two** of the five characteristics, each **defined and applied**.

### 2. Concept breakdown

- **Cloud computing (simple):** on-demand delivery of servers, storage, databases and applications **as services over the Internet**, hosted in large provider data centers, with implementation details hidden.
- **NIST definition:** *a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources (networks, servers, storage, applications, services) that can be rapidly provisioned and released with minimal management effort or service provider interaction.*
- **Misconception in the scenario:** cloud is **not a technology**; it is a **business/service model** that relies on enabling technologies such as **virtualization**. A service counts as cloud when it shows the **five characteristics**: on-demand self-service, broad network access, resource pooling, rapid elasticity, measured service (**O-B-R-R-M**).

```
 FRONT END                     INTERNET                     BACK END (cloud)
+-----------------+         +-------------+         +---------------------------+
| Clinic staff    |         |             |         | Servers | Storage | Network |
| browsers, apps, | <-----> |  Internet   | <-----> | Databases | Applications    |
| mobile devices  |         |             |         | Management + metering     |
+-----------------+         +-------------+         +---------------------------+
```

### 3. Variation survival guide

- If asked for **any two** characteristics, pick the two that match the scenario; the story usually names them (months waiting for servers = **on-demand self-service**; peak season = **rapid elasticity**; CFO billing = **measured service**).
- Use the **define → mechanism → scenario** pattern for each.

### 4. Model answer

Cloud computing is a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources that can be rapidly provisioned and released with minimal management effort or service provider interaction. It is a service model, not a technology: virtualization and similar technologies enable it.

In the diagram, the **front end** is the clinic user with a browser or app; the **Internet** carries requests and replies; the **back end** is the provider's servers, storage and networks that run the service.

**On-demand self-service:** the customer provisions resources automatically **without human interaction** with the provider. MedConnect's developers could create test servers themselves in minutes instead of waiting months for hardware.

**Rapid elasticity:** resources are **provisioned or released to match demand**. During the year-end claims period MedConnect adds virtual servers, then terminates them when demand falls, so it stops paying for idle capacity.

---

## 2(b) Stack shading; public vs private vs hybrid; recommendation (8 marks)

### 1. What the examiner wants

- **Figure 1 completed correctly** for four columns.
- Comparison of three deployment models.
- A **justified recommendation** for MedConnect (law, billing legacy, mobile app, email).

### 2. Concept breakdown

**Service models:** **SaaS** = ready-to-use applications (end users); **PaaS** = platform to build and deploy apps (developers; high lock-in risk); **IaaS** = processing, storage, networks (system administrators; the base layer). **Rule of thumb:** *the higher the service model, the less the customer manages, but the data is always the customer's responsibility.*

**Figure 1 (■ = shade, customer-managed; □ = provider-managed, leave blank):**

| Layer | On-premise | IaaS | PaaS | SaaS |
| --- | --- | --- | --- | --- |
| Data | ■ | ■ | ■ | ■ |
| Applications | ■ | ■ | ■ | □ |
| Runtime | ■ | ■ | □ | □ |
| Middleware | ■ | ■ | □ | □ |
| OS | ■ | ■ | □ | □ |
| Virtualization | ■ | □ | □ | □ |
| Servers | ■ | □ | □ | □ |
| Storage | ■ | □ | □ | □ |
| Networking | ■ | □ | □ | □ |

**⚠ Note on SaaS Data:** the lecturer says you are always responsible for your data, so shade **Data** under SaaS and add a one-line note. Some textbooks leave SaaS fully provider-managed; if your marker's scheme does, your note shows you understand why.

**Deployment models:**

|  | Public | Private | Hybrid |
| --- | --- | --- | --- |
| Used by | General public | One organization | Public + private bridged |
| Run | CSP premises, multitenant | Organization on-premise, or third party off-premise | Separate clouds linked for data/application portability |
| Strength | Cheapest (metered), huge scalability | Control of data location and security | Better fit to business needs |
| Weakness | No control of data location (regulatory concern) | Needs in-house skills; limited scalability; costly | Harder to manage |

### 3. Variation survival guide

- **Recommendation formula:** requirement → option → benefit → risk → mitigation (from the long draft, which is good).
- Slides' rule of thumb: **startups → public; SMEs → hybrid; large enterprises → private;** keep **mission-critical, regulated and legacy/proprietary** apps private; put **non-critical** apps (email/collaboration, dev/test) in the public cloud.

### 4. Model answer

*(Draw the Figure 1 table above with ■ shading.)* Under **IaaS** the customer manages data, applications, runtime, middleware and OS; under **PaaS** only data and applications; under **SaaS** the provider runs the application, but the customer remains responsible for its data.

A **public cloud** serves the general public from the provider's premises: cheapest and highly scalable, but with no control over data location. A **private cloud** serves one organization: more control over data and security, but needs in-house skills, costs more and scales less. A **hybrid cloud** bridges the two: better alignment to business needs but harder to manage.

**Recommendation: hybrid.** (1) Patient records must stay under MedConnect's control, so they stay in the **private** environment. (2) The legacy billing application is mission-critical and proprietary, so it also stays private for now. (3) Email and collaboration (non-critical) move to **SaaS**; the mobile app uses **PaaS**; extra capacity uses **IaaS** or bursting for peaks. The main risk is management complexity, reduced by clear responsibilities, monitoring and consistent security policy.

---

## 2(c) Figure 2, cloud bursting, drivers, SLA calculation, migration, lock-in (10 marks)

### 1. What the examiner wants

- **Interpret Figure 2** and **sketch bursting**.
- **One cost driver + one agility driver.**
- **SLA credit** (the free-mark calculation) and **purpose of an SLA.**
- **Migration strategy with justification** and **vendor lock-in risk.**

### 2. Concept breakdown

**Reading Figure 2 (from your photo; check your own paper):** installed capacity is a flat line at **60 servers**. Demand sits around **20** in most months, starts climbing around **August–September**, and reaches about **55–60 in Nov–Dec**. So capacity is sized for the **peak**, leaving about two-thirds idle for most of the year.

**Cloud bursting:** run applications in the **private** cloud; when demand exceeds local capacity, the **public cloud absorbs the burst**. Slide example: a tax-preparation firm with 2–3× volume in tax season sizes for the **typical** load and bursts at peak.

```
Servers
 60 |                                      ..XXXX   <- burst to PUBLIC cloud
 50 |                                   ..XXXXXX
 40 |                                .XXXXXXXXXX
 30 |------------------------ private baseline (own servers) --------
 20 |####  ####  ####  ####  ####  ####  ####  ####  ####  ####
  0 +----------------------------------------------------------
     Jan   Mar   May   Jul   Sep  Oct   Nov   Dec
```

**Caveat (from the long draft, useful):** patient data must stay under company control, so burst only workloads and data that are allowed to leave (for example anonymised or non-sensitive processing), not the sensitive records themselves.

**Drivers:** *cost driver:* **economies of scale** and the shift **CAPEX → OPEX** (no upfront hardware; pay only for what you use). *Agility driver:* **scalability and elasticity, faster time to market** (dev/test environments in minutes, global access for other regions, more focus on core business).

**SLA:** a **contract between customer and CSP** stating **uptime** and performance, with **compensation (money or service credits)** if unmet. **Credit bands:** 99.0% to <99.5% → **10%**; 95.0% to <99.0% → **30%**; <95.0% → **100%**.

**Calculation (show formula, substitution, result):**

- Pilot uptime = **97.8%**. Find the band: 95.0% ≤ 97.8% < 99.0% → **30% service credit.**
- Downtime in a 30-day month: hours = 30 × 24 = **720**; downtime = (1 − 0.978) × 720 = 0.022 × 720 = **15.84 hours**.
- Promised downtime allowance at 99.5%: 0.005 × 720 = **3.6 hours**, so the pilot missed the target by about 12.2 hours.
- State the assumption: the 30% applies to the eligible monthly charge for that service.

**Migration strategies (low to high effort):** **Rehost** (lift-and-shift into IaaS, fastest, no optimisation) → **Re-platform** (optimise without changing core architecture) → **Repurchase** (switch to SaaS) → **Rebuild** (re-architect, most expensive).

**Vendor lock-in:** reliance on proprietary technology that makes switching hard and costly. The slide notes **PaaS has high lock-in risk**; leaders reduce it by supporting **standard/open languages**. **Multi-cloud** (more than one vendor) gives best-fit services and avoids lock-in but adds management complexity.

### 3. Variation survival guide

- **SLA with different numbers:** locate the band first, then state the credit, then (if asked) compute downtime = (1 − uptime) × hours in month. Months: 28 days = 672 h, 30 = 720 h, 31 = 744 h.
- **Migration choice rule:** legacy + mission-critical + “do not disturb” → **rehost** (fastest, least change) or **keep private**; modern app that needs scale → **re-platform/rebuild**; commodity software (email, CRM, HR) → **repurchase**.
- Always pair the strategy with its **downside** (rehost = no optimisation, benefits of cloud not fully used).

### 4. Model answer

**Figure 2** shows 60 servers installed all year while demand is about 20 for most months and rises to about 55–60 only in November–December, so capacity is sized for the peak and sits idle for most of the year. **Cloud bursting** fixes this: MedConnect keeps a baseline (about 20–30 servers) in its private environment and, when demand crosses that line, temporarily rents public-cloud capacity (the shaded burst area in the sketch), releasing it afterwards. Only workloads and data allowed to leave the private environment should burst.

**Cost driver:** economies of scale and the shift from CAPEX to OPEX: no upfront purchase of 60 servers, paying only for what is used. **Agility driver:** elasticity and faster time to market: developers get test environments in minutes instead of months, enabling the mobile app and other regions.

**SLA and credit.** An SLA is a contract stating the uptime and performance the provider supports and the compensation if it fails. The pilot server was up 97.8%, which lies in the 95.0%–<99.0% band, so MedConnect receives a **30% service credit**. (Downtime = 0.022 × 720 h = 15.84 h, against a 3.6 h allowance at 99.5%.)

**Billing system.** I recommend **rehosting** (lift-and-shift) the billing system, into the private/hybrid environment first. It is a proprietary, mission-critical legacy application that management does not want disturbed; rehosting is the fastest strategy and changes no architecture. Its weakness is that it does not optimise for the cloud, so MedConnect can later **re-platform** parts (for example move its database to a managed service). **Repurchase** or **rebuild** would be slow, costly and risky now.

**Vendor lock-in.** The development platform works only with the provider's tools, so moving later would mean rewriting. Mitigate by using standard/open languages, keeping data in portable formats, negotiating exit terms, and considering a second provider (multi-cloud) while accepting the extra management complexity.

---

# QUESTION THREE: SwiftTrade Distributors (silos, three-tier ERP, SOA)

**Scenario signals:** organised by function with managers at three levels (**horizontal and vertical silos, POSDCORB, hierarchy**); clerk cannot see warehouse stock, accounting re-types data, no real-time information (**silo information systems are inefficient, inaccurate, expensive**); cross-functional order-fulfilment teams (**matrix structure**); browser + application servers + central database (**three-tier**); expensive and complex (**three-tier limitation**); keep the old inventory system as services (**SOA**); fears of cost, time, security, inconsistent performance (**the slide's SOA drawbacks**).

---

## 3(a) POSDCORB functional model; hierarchical model; cross-functional matrix (7 marks)

### 1. What the examiner wants

- **Two drawings** (functional/POSDCORB model; hierarchical model) and an explanation of how a **cross-functional matrix** breaks silos.
- POSDCORB spelled out in full and linked to **departments**.

### 2. Teach me: the functional model (POSDCORB)

**What it is:** **Luther Gulick** (late 1930s) described the work of management as seven functions: **P**lanning, **O**rganizing, **S**taffing, **D**irecting, **Co**ordinating, **R**eporting, **B**udgeting. Organizations grouped people by these specialised functions (control, management, supervision, administration), which produced departments such as **Accounting** and **Human Resources**. These are the **horizontal silos**.

**In simple words:** a company is cut into slices by specialty; each slice has its own manager, staff and computer system. Good for specialisation and responsibility, bad for sharing information.

**Why it exists:** as organizations grow they break work into smaller units so staff can manage complexity and specialise, which raises productivity.

```
FUNCTIONAL MODEL (horizontal silos, POSDCORB)

                 +---------------------------+
                 |       ORGANIZATION        |
                 +-------------+-------------+
          +----------+--------+--------+-----------+
          |          |                 |           |
     +--------+ +-----------+   +-----------+ +--------+
     | Sales  | |Procurement|   | Warehouse | |Account-| ... HR
     |        | |           |   |           | |ing     |
     +--------+ +-----------+   +-----------+ +--------+
   Each department performs: Planning, Organizing, Staffing,
   Directing, Coordinating, Reporting, Budgeting for its own area
```

**Hierarchical model (vertical silos, by level):**

```
+--------------------------------------------+
| TOP MANAGEMENT (CEO / President)           |  strategic: long-term strategy
+--------------------------------------------+
| MIDDLE MANAGEMENT                          |  tactical: policy, carry out strategy
+--------------------------------------------+
| LOWER MANAGEMENT / SUPERVISORS             |  operational: day-to-day operations
+--------------------------------------------+
```

**Cross-functional matrix (breaks silos):** a **cross-functional (matrix) structure** adds **processes that cut across departments** (for example order fulfilment), staffed by people from several departments who **share information at any level**.

```
                 Sales   Warehouse   Accounting   Procurement
Order fulfilment   X        X           X
Procurement cycle                        X            X
   (each row is a process team drawing people from several departments)
```

### 3. Variation survival guide

- **Drawing questions:** title the diagram, label every box, add a one-line caption saying what it shows.
- Link every drawing to the scenario: sales clerk cannot see stock = **missing information flow between horizontal silos**; CEO / middle managers / supervisors = **vertical levels**.
- Silo system problems (slide): **inefficient, inaccurate, expensive; bottlenecks; information not in real time.**

### 4. Model answer

The **functional model** divides an organization into departments based on Gulick's POSDCORB functions (planning, organizing, staffing, directing, coordinating, reporting, budgeting): SwiftTrade's sales, procurement, warehouse, accounting and HR are horizontal silos. The **hierarchical model** divides roles by level: the chief executive plans long-term strategy, middle managers handle tactical issues and policy, and supervisors run day-to-day operations.

A **cross-functional matrix structure** breaks the functional silos by opening information flows between departments: for example an **order-fulfilment team** with people from sales, warehouse and accounting share the same information. The sales clerk can see stock before promising goods, warehouse data flows to invoicing without re-typing, and managers get information in real time. SwiftTrade must define who owns each process to avoid conflicting reporting lines.

---

## 3(b) Three-tier ERP architecture; role of each tier; benefits and limitation (8 marks)

### 1. What the examiner wants

- A **labelled three-tier diagram**, the **role of each tier**, **two benefits and one limitation.**

### 2. Teach me: three-tier ERP architecture

**What it is:** the ERP is organised in **layers (tiers)** to **manage complexity and provide scalability and flexibility.** The **three-layer architecture** is described as the most reliable, flexible and scalable, and the most common today: **web servers, application servers, database servers.**

**In simple words:** like a restaurant: customers sit in the dining room (web tier), the kitchen follows the recipes (application tier), and the store room keeps ingredients (data tier). Customers never go into the store room.

**How a request flows (SwiftTrade order check):**

1. A retailer opens the **browser** and requests stock availability. (web tier)
2. The request reaches the **application server**, which applies business rules and reporting logic. (application tier)
3. The application server reads or updates the **central database**. (data tier)
4. The answer returns up the same path to the browser.

```
   Users: sales staff, retailers (web browser)
                    |
+-----------------------------------------------+
| TIER 1  WEB TIER                              |  web portal: access and analyse
|         (browser, web servers)                |  information through a browser
+-----------------------------------------------+
                    |
+-----------------------------------------------+
| TIER 2  APPLICATION TIER                      |  business processes + reporting;
|         (application servers)                 |  shields users from ERP internals
+-----------------------------------------------+
                    |
+-----------------------------------------------+
| TIER 3  DATA TIER                             |  structure of ALL organizational
|         (central database)                    |  data and their relationships
+-----------------------------------------------+
```

**Roles (memorise):**

| Tier | Role |
| --- | --- |
| **Web tier** | Presentation and access: users reach the ERP through a **web portal/browser**; sends requests, shows results |
| **Application tier** | Runs the **business processes and reporting**; **shields users from ERP internals** |
| **Data tier** | Holds the **structure of all organizational data and relationships** (the central database) |

**Benefits (slide list of six, S-R-F-M-R-S):** **Scalability** (easy to add, change or remove applications), **Reliability** (multiple levels of redundancy), **Flexibility** (partitioning is simple), **Maintainability** (lower support cost), **Reusability** (reusable components), **Security** (IT staff have more control). **Limitation:** can be **very expensive and complex.**

**Also in the slides:** web access is often called a **fourth tier** (web services tier + web browser tier). In practice vendors such as SAP and PeopleSoft are web-based so many users can reach ERP over the Web.

### 3. Variation survival guide

- Pick the two benefits **most relevant to the scenario** (SwiftTrade grows and wants to keep old systems: **scalability, flexibility**) and give one reason each.
- The limitation is already in the story: managers “worry it will be expensive and complex.” Quote the slide limitation, then add one mitigation (phased rollout, skilled staff, careful budgeting).
- Never draw the database at the top. Flow is **user → web → application → data.**

### 4. Model answer

*(Draw the three-tier diagram above.)* SwiftTrade's ERP has three tiers. The **web tier** lets staff and retailers reach the ERP through a browser portal. The **application tier** runs the business processes and reporting on application servers and shields users from the ERP's internal workings. The **data tier** is the central database that holds the structure of all company data and its relationships.

**Benefits.** (1) *Scalability:* when order volume grows, SwiftTrade can add or change application servers without redesigning the whole system. (2) *Flexibility/reusability:* partitioning is simple and components can be reused, so modules such as inventory and finance can be added or changed independently. (Also: reliability through redundancy, maintainability, security.)

**Limitation.** It can be **very expensive and complex** to buy, build and maintain; SwiftTrade should phase the rollout and budget for skilled support.

---

## 3(c) SOA: consumer, provider, messages; contract; benefits, drawbacks; recommendation (10 marks)

### 1. What the examiner wants

- From the **figure**: **consumer, provider, request and reply.**
- The **five elements of the contract.**
- **Two benefits, two drawbacks**, and a **justified recommendation.**

### 2. Concept breakdown

- **SOA** breaks the business tier into smaller, distinct **services** that together support an ERP module. **Any service consumer can exchange messages with any service provider**, from any device, OS or language.
- It is a development model based on a **contract between consumer (client) and provider (server).**

```
+------------------+      REQUEST       +-------------------------------+
| SERVICE CONSUMER | -----------------> | SERVICE PROVIDER              |
| (sales / ERP     |                    | (legacy inventory system      |
|  application)    | <----------------- |  exposed as a service)        |
+------------------+       REPLY        +-------------------------------+
                 (the exchange is “the Service”)
```

- **Contract (5 elements):** (1) **functional description** of the service; (2) **input requirements and output specifications**; (3) **precondition** (state before the service can be called); (4) **postcondition** (state after it runs); (5) **error handling.**
- **Benefits (any two, explained):** works across **heterogeneous platforms**; **location independence** of business logic; **loose coupling**; **leverages existing investments**; **lower hardware/maintenance cost**; **composite applications**; **more reliable**; meets customer demand faster; less reliance on custom development.
- **Drawbacks (slide list):** **costly and time-consuming**; needs **complex firewalls** and **sophisticated security**; **inconsistent performance**; needs **enterprise-level focus**.
- **Web services** (how SOA is often built): interfaces that let applications interact **only by sending and receiving messages**, using open XML-based standards **WSDL, UDDI, SOAP**.

### 3. Variation survival guide

- The scenario's three fears (costly and time-consuming; strong security between services; inconsistent performance) **are** the slide's drawbacks. Use the slide wording, then add a mitigation for each.
- Consumer/provider roles belong to an **interaction**, not permanent labels: the same system can be both.
- Recommendation template: **adopt, but in phases**, starting with the highest-value service (stock availability), with contracts, security, monitoring.

### 4. Model answer

**Figure 1.** The **consumer** is the application that needs a function, such as SwiftTrade's sales or ERP module. The **provider** is the legacy inventory system exposing its functions as services. The consumer sends a **request** message (for example “stock level of product X”) and the provider returns a **reply** (the quantity, or an error).

**Contract elements:** functional description; input requirements and output specifications; precondition; postcondition; error handling.

**Benefits.** (1) *Leverages existing investments:* the old inventory system is wrapped as a service, not thrown away. (2) *Heterogeneous platforms/loose coupling:* other applications call it regardless of operating system or language.

**Drawbacks.** (1) *Costly and time-consuming* to design and build services. (2) *Needs complex firewalls and sophisticated security* between services, and *performance can be inconsistent.*

**Recommendation: adopt SOA in phases.** SwiftTrade wants to keep the old inventory system while integrating a new ERP; SOA lets it do that without a full replacement. Start with a stock-availability service, agree its contract, secure it, monitor performance, then extend. If budget or security skills are lacking, delay rather than rush.

---

# QUESTION FOUR: BrightStitch Garments (ERP architecture, access layers, cloud ERP)

**Scenario signals:** departments on spreadsheets, stand-alone packages and paper (**silos**); ERP with a **functional side and a system side** (**two components of ESA**); three vendors and a table (**copy Table 1 exactly**); Java-enabled browser, intranet + Internet, interface layer, secure connection, application software layer (**the layered Info.Net architecture**); field staff want fastest response, IT manager wants processing on servers (**client-centric vs server-centric**); lease as a service, monthly subscription, security, outside vendor, provider copying design ideas (**cloud benefits and drawbacks, conflict of interest, IP**).

---

## 4(a) Two components of ESA; ERP module diagram; Table 1 modules (7 marks)

### 1. What the examiner wants

- **Two components** named and explained: **functional** and **system.**
- A **labelled diagram of typical ERP modules.**
- **Accurate copying** of the procurement and accounting modules for the three vendors from Table 1. Do not substitute other product names.

### 2. Teach me: ERP system and modules

**What ERP is:** **integrated, multi-module application software** that serves **several business functions** across the organization, with **business rules** that embed best practice. Main vendors: **SAP, Oracle/PeopleSoft, Microsoft Dynamics.**

**Two components of Enterprise Systems Architecture (ESA):**

- **Functional:** the **ERP modules that support business functions** (accounting, human resources, procurement, fulfilment, and so on).
- **System:** the ERP **architecture viewed through its hardware, software and networking components.**

**Typical ERP modules (Figure 3-2 content):**

```
                         +-----------------------------+
                         |     ERP  (shared database)  |
                         +--------------+--------------+
   +------------+------------+---------+---------+-------------+-----------+
   |            |            |         |         |             |           |
+--------+ +----------+ +----------+ +---------+ +---------+ +--------+ +-----------+
|Produc- | |Purchasing| |Inventory | |Sales &  | |Finance  | | Human  | |Miscellan- |
|tion    | |          | |management| |marketing| |         | |resource| |eous       |
+--------+ +----------+ +----------+ +---------+ +---------+ +--------+ +-----------+
                                                        (BI, self-service, project mgmt, e-commerce)
```

**What each module does (slides):**

- **Production:** plans and optimises manufacturing capacity, parts, components and materials using historical data and sales forecasts.
- **Purchasing:** streamlines procurement of raw materials and supplies.
- **Inventory management:** keeps the right stock level in the warehouse.
- **Sales and marketing:** order placement, scheduling, shipping, invoicing.
- **Finance:** gathers data from departments and produces financial reports.
- **Human resource:** streamlines management of people.
- **Miscellaneous:** business intelligence, self-service, project management, e-commerce.

**Table 1 (vendor modules; this is what the question asks for):**

| Function | SAP | Oracle/PeopleSoft | Microsoft Dynamics |
| --- | --- | --- | --- |
| Sales | Sales and Distribution, Sales Opportunity | Marketing and Sales, Supply Chain Management | Retail POS, Field Service Management |
| **Procurement** | **Purchasing, Supplier Relationship Management** | **Procurement and Supplier Relationship Management** | **Supply Chain Management** |
| Production | MRP, Product Life Cycle Management | Manufacturing | Manufacturing |
| **Accounting** | **Financial Accounting** | **Financial Management** | **Financial Management** |

### 3. Variation survival guide

- If the question asks for **sales** or **production** instead, read the other rows of the table; the question always supplies it. **Copy exactly; do not add modules from memory.**
- Two components memory line: **“What it does” (functional) and “what it runs on” (system).**
- Diagram marks come from **labels**: put the ERP core/database in the middle and name every module.

### 4. Model answer

Enterprise systems architecture has two components. The **functional** component is the set of ERP modules that support business functions such as procurement, production, accounting and human resources. The **system** component is the ERP architecture seen through its hardware, software and networking components, which supply the platform for the modules.

*(Draw the module diagram: ERP core with Production, Purchasing, Inventory, Sales and marketing, Finance, Human resource and Miscellaneous (BI, self-service).)* The modules share one integrated database so a transaction entered in one is available to the others.

From Table 1: **procurement** is **Purchasing and Supplier Relationship Management** in SAP, **Procurement and Supplier Relationship Management** in Oracle/PeopleSoft, and **Supply Chain Management** in Microsoft Dynamics. **Accounting** is **Financial Accounting** in SAP and **Financial Management** in both Oracle/PeopleSoft and Microsoft Dynamics.

---

## 4(b) Layered access architecture; how the connection is established; server- vs client-centric (8 marks)

### 1. What the examiner wants

- A **labelled layered diagram** of how a user reaches the ERP.
- The **connection steps in order.**
- A **comparison** of server-centric and client-centric architectures and a **recommendation for the field sales staff.**

### 2. Teach me: the layered ERP access architecture

**What it is:** the layered (Info.Net-style) ERP architecture generalises functional layers so it can change as technology changes. The user's PC reaches the server through browser, network and interface layers.

**How the connection is established (the steps in the scenario):**

1. The user has a **Java-enabled web browser** on a PC.
2. The PC is connected to the **intranet and Internet** so it can reach the ERP server.
3. The browser connects to the **interface layer (Java Virtual Machine layer)**, which sets up a **secure SSL connection.**
4. The user then talks to the server through the **applications software layer (ASL)**, which runs the ERP functions against the database.

```
+------------------------------------------+
| USER PC  (factory / head office / laptop)|
| Java-enabled web browser                 |
+---------------------+--------------------+
                      |  intranet / Internet
+---------------------v--------------------+
| INTERFACE LAYER  (Java Virtual Machine)  |
| sets up secure SSL connection            |
+---------------------+--------------------+
                      |
+---------------------v--------------------+
| APPLICATIONS SOFTWARE LAYER (ASL)        |
| ERP business logic, modules              |
+---------------------+--------------------+
                      |
+---------------------v--------------------+
| ERP SERVER + DATABASE                    |
+------------------------------------------+
```

**Server-centric vs client-centric (slide statements):**

|  | Server-centric | Client-centric |
| --- | --- | --- |
| Where processing happens | Mostly on the **server** | More on the **user's computer** |
| Strength | **No complex, expensive client software; secure** user access | **Better response time** |
| Weakness | **Slower** | **Lacks security** |
| Administration | Centralised, easy updates | Software on every client |

### 3. Variation survival guide

- **Match the user group to the criterion they care about:** field staff want **speed** (client-centric); head-office and factory staff want **security and simple administration** (server-centric).
- Always state the **cost** of your choice and a **mitigation**: client-centric security risk → encryption (SSL), limited local data, strong authentication, remote wipe of laptops; slow-link speed risk for server-centric → lightweight pages, fewer round trips.
- If the paper asks for “which suits X”, give **one clear choice**, then say the other groups can differ.

### 4. Model answer

*(Draw the layered diagram above.)* A BrightStitch user opens a **Java-enabled browser** on a PC connected to the **intranet and Internet**. The browser first connects to the **interface layer**, which sets up a **secure (SSL) connection**; the user then talks to the server through the **applications software layer**, which executes the ERP functions and accesses the database.

In a **server-centric** architecture most processing is on the server: **no complex, expensive client software and secure access**, but **slower**. In a **client-centric** architecture more processing is on the user's computer: **better response time**, but it **lacks security**.

**Recommendation for field sales staff: client-centric.** They work on laptops over slow mobile connections and want the quickest response, and local processing reduces the number of slow network round-trips. The security weakness is managed with SSL encryption, strong authentication and keeping sensitive data on the server. Factory and head-office users, on fast networks, can use the server-centric design the IT manager prefers.

---

## 4(c) Cloud-based ERP diagram; benefits and drawbacks; lease or buy (10 marks)

### 1. What the examiner wants

- A **labelled diagram**: users, Internet, provider.
- **Three benefits** and **two drawbacks**, each tied to BrightStitch.
- An **evaluation with a clear recommendation** and reasons.

### 2. Teach me: cloud-based ERP service

**What it is:** **cloud computing** here means software provided **as a service over the Internet, securely, by a provider on a monthly or yearly lease.** Companies **save money by replacing per-seat licensed software**; some providers also let you build and host your own applications. It suits organisations that do **not** want to buy, install and maintain software or worry about data storage security. **Risk:** reliance on an **external vendor** for reliability, security and continuity.

```
 BRIGHTSTITCH USERS                                   CLOUD ERP PROVIDER
+----------------------+                         +---------------------------+
| Factory PCs          |                         | Hosted ERP application    |
| Head-office PCs      | <--- INTERNET --------> | (production, purchasing,  |
| Field-sales laptops  |    (secure link)        |  finance, HR, sales)      |
+----------------------+                         | ERP database, backups,    |
   pay a monthly subscription                    | security, operations      |
                                                 +---------------------------+
```

**Benefits (slide list):**

| Benefit | In simple words |
| --- | --- |
| Pay a **subscription**, not licences and upgrades | Lower **capital and operating** expenses |
| Access from **anywhere** with Internet | Field staff reach the same system |
| **Nothing to install**; **no maintenance fees** | Provider runs and updates it |
| **Dynamic scalability** on demand | Add users or capacity when needed |

**Drawbacks (slide list):**

| Drawback | Meaning for BrightStitch |
| --- | --- |
| **Data security** and **vulnerability** | Company data sits with a third party |
| **Conflict of interest** | The provider could **copy your application** or build a similar product from your design ideas |
| **Not suited to highly competitive industries** where **intellectual property (IP)** is hard to protect | BrightStitch calls its design ideas a key competitive asset |
| Reliance on an **outside vendor** for reliability and continuity | An outage or provider failure stops the business |

### 3. Variation survival guide

- **Decision rule:** if the story says IP or confidentiality is the competitive asset, the slides push you to **in-house/private**; if it stresses cost and speed with no sensitive IP, **SaaS** wins. Either is accepted when justified; the **un-justified** answer is the one that loses marks.
- Always give **both sides**: one reason for your choice, one reason the alternative is tempting, and the **condition** under which you would switch.
- Evaluation checklist: cost, control and IP, security, availability/continuity, scalability, skills.

### 4. Model answer

*(Draw the cloud ERP diagram.)* BrightStitch's factory, head-office and field users reach an ERP hosted by the provider over the Internet; the provider runs the application, database, backups and security, and BrightStitch pays a monthly subscription.

**Three benefits:** (1) a **subscription instead of per-user licences and upgrades**, lowering capital and operating expense; (2) **access from anywhere with an Internet connection**, helping field sales staff; (3) **nothing to install, no maintenance fees, and dynamic scalability**, so BrightStitch needs fewer IT staff and can add users on demand.

**Two drawbacks:** (1) **data security and vulnerability**: company data sits with an outside party; (2) **conflict of interest and IP risk**: the provider could copy the application or build a similar product from BrightStitch's design ideas, and the slides note cloud is **not suited to highly competitive industries** where IP is hard to protect. There is also reliance on the vendor for reliability and continuity.

**Evaluation and recommendation.** Leasing offers clear savings and easy access, but BrightStitch itself calls its design ideas a **key competitive asset**, and a garment maker competes on design. I therefore recommend **buying and running the ERP in-house** (private), at least for modules holding design and production know-how, while non-sensitive functions such as email or HR could still use cloud services. I would switch to leasing only if the provider accepted strong IP and confidentiality terms, continuity guarantees and an exit clause.

---

# QUESTION FIVE: EduNet University (middleware, hardware, caching, architecture)

**Scenario signals:** different systems on Linux, Windows, macOS, Android and separate logins (**heterogeneity, security/authentication service**); “one coherent system” without replacing machines (**middleware**); shared-memory vs private-memory designs on a bus or switch (**Figure 1, multiprocessor vs multicomputer**); thousands requesting the same pages and congested links (**caching, proxy server**); departments sharing datasets without a central server (**P2P**); whole platform client-server or P2P (**recommendation**).

---

## 5(a) Layered structure on three machines; role of middleware; two service categories (7 marks)

### 1. What the examiner wants

- A **labelled diagram**: three machines, each with the layers, joined by a network.
- The **role of middleware.**
- **Two service categories with an example each.**

### 2. Teach me: the layered structure of a distributed system

**What it is:** every host (computer) has the same stack, bottom to top: **hardware → network operating system → middleware → application components.** The hosts are joined by a **network**. **Middleware is the layer that turns a set of networked computers into a distributed system**: without it you only have a network of separate machines.

**In simple words:** the OS on each machine stays as it is (Linux, Windows, macOS). Middleware sits on top and speaks a common language, so applications on different machines can talk to each other as if on one system.

```
   MACHINE 1             MACHINE 2             MACHINE 3
+----------------+   +----------------+   +----------------+
| Application    |   | Application    |   | Application    |
| components     |   | components     |   | components     |
+----------------+   +----------------+   +----------------+
| MIDDLEWARE     |   | MIDDLEWARE     |   | MIDDLEWARE     |   <- common services
+----------------+   +----------------+   +----------------+
| Network OS     |   | Network OS     |   | Network OS     |   <- may differ
| (e.g. Linux)   |   | (e.g. Windows) |   | (e.g. macOS)   |
+----------------+   +----------------+   +----------------+
| Hardware       |   | Hardware       |   | Hardware       |
+-------+--------+   +-------+--------+   +-------+--------+
        |                    |                    |
========+====================+====================+========  NETWORK
```

**Role of middleware (slides):** software **between the operating system and applications** that connects components or enterprise applications across a network. The OS on each computer **need not be the same and need not know about the others**; services are **transparently distributed.** It exists because integrating many networked applications using only primitive NOS-level services was too hard: it supports **federated information systems** (combine different databases, one view), **enterprise-wide Internet services**, **transactions across databases** and **extensibility**, and it must work on **existing operating systems.**

**Four service groups:**

| Group | Examples |
| --- | --- |
| **Communication** | Remote procedure calls, remote-object method invocation, message queuing, event notification |
| **Information system** | Naming, directory and location services, persistent storage, **caching and replication** |
| **Control** | Distributed transaction processing, code migration |
| **Security** | **Authentication and authorization**, encryption, auditing |

### 3. Variation survival guide

- Name the **two categories** that match the story: EduNet's “log in separately to each system” points to **security (authentication and authorization, i.e. single sign-on)**; “data does not move easily” points to **communication** or **information-system (naming, directory)** services.
- Draw **identical** layers on each machine, and show the **network** line joining them.
- Do not draw middleware as one central box: it exists on **every** machine and cooperates across the network.

### 4. Model answer

*(Draw the three-machine diagram above.)* Each machine has hardware, a network operating system, a middleware layer and application components; the machines are connected by a network.

**Role of middleware.** Middleware sits between the operating system and the applications and connects components across the network. The operating systems on the machines need not be the same and need not know about each other, so EduNet can keep its Linux registry, Windows library catalogue and mixed staff devices while applications see one coherent system, without replacing every system.

**Two service categories.** (1) **Security services:** authentication and authorization, so a user logs in once and is recognised across systems, solving the separate-login complaint. (2) **Communication services:** remote procedure calls or message queuing, so the registry, library and finance applications exchange data. (Others: information-system services such as naming and directory; control services such as distributed transactions.)

---

## 5(b) Figure 1: distinguishing features; multiprocessor or multicomputer; shared memory vs message passing (8 marks)

### 1. What the examiner wants

- The **two distinguishing features**: **private vs shared memory** and **bus-based vs switched** interconnection.
- **Classification** of all four designs.
- A **comparison** of the two communication architectures.

### 2. Concept breakdown

**Reading the figure:** columns = memory type (**shared | private**); rows = interconnection (**bus-based | switch-based**). P = processor, M = memory.

| Figure position | Memory | Interconnect | Classification | How processors communicate |
| --- | --- | --- | --- | --- |
| Top-left | Shared | Bus | **Multiprocessor** | Read/write shared memory |
| Bottom-left | Shared | Switch | **Multiprocessor** | Read/write shared memory through the switch |
| Top-right | Private | Bus | **Multicomputer** | Messages over the bus |
| Bottom-right | Private | Switch | **Multicomputer** | Messages through the switch |

- **Multiprocessor:** two or more processing units **sharing main memory** and peripherals. **Multicomputer:** separate computers with **their own memory**, communicating by messages.
- **Bus:** one shared communication path; simple but contention rises with more processors. **Switch:** several paths at once; more parallelism, more complexity. *(Reasoned explanation \[Added\]; the slides name the two features but give little detail.)*

|  | Shared memory | Message passing |
| --- | --- | --- |
| Address space | **Shared** | **Separate** for each processor |
| Communication | Memory **reads and writes** | **Messages**; local message-queue memories |
| Latency | **Lower** | Higher for non-local operations |
| Fits | Small machines, easy to program | Multicomputers and networks; designs focus on the costly non-local operations |
| Watch-out | Needs synchronisation | Needs explicit send/receive handling |

### 3. Variation survival guide

- Classify by **memory**, not by interconnect: shared = multiprocessor; private = multicomputer. Bus or switch only changes **speed and contention.**
- Start your answer by naming the **two axes**; the examiner is looking for exactly that sentence.
- For a different figure (different drawing), repeat the process: identify memory, identify links, then classify.

### 4. Model answer

The four designs differ in two features: **memory** (shared or private) and **interconnection** (bus-based or switch-based). The two shared-memory designs, one on a bus and one through a switch, are **multiprocessors**: their processors share main memory and communicate by reading and writing it. The two private-memory designs, one on a bus and one through a switch, are **multicomputers**: each processor has its own memory and communication is by messages.

In **shared memory** all processors use one address space, so data exchange is simple and latency is lower, but access must be synchronised and the bus can become a bottleneck. In **message passing** each processor has its own address space and exchanges explicit messages, with the costly operations being non-local ones; it scales across separate machines but has higher communication overhead. EduNet's research office should pick shared memory for tightly coupled number-crunching on one machine and message passing for many separate machines.

---

## 5(c) Client-server vs P2P diagrams; proxy-cache operation; architecture recommendation (10 marks)

### 1. What the examiner wants

- **Two diagrams** (client-server; peer-to-peer).
- How a **proxy-server cache** works.
- A **justified recommendation** for the learning platform (with the research-data case handled separately).

### 2. Concept breakdown

```
 CLIENT-SERVER                          PEER-TO-PEER

 [Client]  [Client]  [Client]           [Peer] <----> [Peer]
     \        |        /                  ^   \        /   ^
      \       |       /                   |    \      /    |
       +-----[SERVER]-----+               v     v    v     v
   server manages shared                 [Peer] <----> [Peer]
   resources (may itself be            all peers equal, no central
   a client of other servers)          coordination
```

**Caching (slides):** a **cache** is a store of **recently used data objects closer to the client** than the objects themselves. **New objects replace old ones.** When a client requests an object, the caching service **first checks for an up-to-date copy**; if none, it **fetches one.** Caches may be **in each client** or in a **shared proxy server.**

```
 Student (campus A) --request--> [PROXY CACHE] --hit--> copy returned (fast, no inter-campus traffic)
                                      |
                                     miss
                                      v
                        [CENTRAL LEARNING SERVER] --object--> stored in proxy, replaces old object
```

**Benefits:** less traffic on the congested inter-campus links, faster responses, less load on central servers. **Risk:** **stale copies**, so use expiry/revalidation, and do **not cache private or personalised content** (results, submissions) in a shared cache (a useful point from the long draft).

### 3. Variation survival guide

- **Choose by need:** authority and control (official notes, quizzes, results) → **client-server**; direct sharing without a central point (research datasets) → **P2P.** A **hybrid** is a valid recommendation.
- Always mention **what is cached** (static, frequently requested pages, lecture notes) and **what is not** (private data).
- If asked how the same idea reduces congestion, quote the mechanism: **repeat requests are served locally, so fewer cross-campus transfers.**

### 4. Model answer

*(Draw both diagrams.)* In the **client-server model** clients request services from servers that manage shared resources; a server may itself be a client of other servers, for example a Web server. In the **peer-to-peer model** all processes play similar roles and cooperate as equals with no client/server distinction and no central coordination.

**Proxy-cache operation.** A campus proxy server sits between students and the central web servers and holds recently used objects, such as popular lecture notes. When a student requests a page, the cache checks for an up-to-date copy. If it has one (hit), it serves it locally; otherwise (miss) it fetches the object from the central server, stores it, and replaces an older object. At exam time thousands of students request the same pages, so most requests are served locally, which relieves the congested inter-campus links and the central servers. Copies must be refreshed so students do not see outdated notes, and private data must not be cached in the shared proxy.

**Recommendation.** Build the **learning platform as client-server with proxy caches at each campus.** The university needs one authoritative source for lecture notes, quizzes, accounts and results, with controlled access and a simple way to update content, and the proxies fix the congestion problem. Use **peer-to-peer only for the departments' research datasets**, where direct sharing without a central server is an advantage and no single official version is needed. The risk of the client-server choice is a central bottleneck and single point of failure, reduced by redundant servers and caching.

---

# APPENDIX A: Internet of Things (IoT) study notes

**⚠ Source note:** IoT does **not** appear in the six chapters you uploaded, so everything in this appendix is **general textbook knowledge \[Added\]**, not your lecturer's wording. Terms and layer names vary between textbooks, so if you have IoT slides, use their headings and keep these as explanations.

## A1. What IoT is

**IoT** is a network of **physical objects (“things”) with embedded sensors, software and connectivity** that **collect and exchange data** over the Internet or other networks, so that they can be monitored and controlled with little or no human effort. **Case:** AgriMart fits fridges with temperature sensors; readings flow to the cloud; an alert goes to the manager when a fridge warms above a limit, and the compressor can be switched automatically.

## A2. Characteristics of IoT

| Characteristic | Meaning | Example |
| --- | --- | --- |
| **Connectivity** | Things connect to networks and to each other | Sensor reports over Wi-Fi |
| **Sensing / actuation** | Detect the environment and act on it | Temperature sensor; relay switches a pump |
| **Intelligence / analytics** | Data is processed to give decisions and predictions | Predict fridge failure |
| **Unique identity** | Each thing is identifiable (ID, address) | Device ID / MAC / IP |
| **Heterogeneity** | Many device types, protocols, platforms interwork | Sensors from different vendors |
| **Scalability** | Billions of devices; system must grow | New branches add thousands of sensors |
| **Dynamic, self-adapting** | Devices join, leave, move and change state | Mobile scanners connect and disconnect |
| **Interoperability** | Standard protocols let different systems exchange data | MQTT, HTTP, CoAP |
| **Limited resources** | Small devices have low power, memory and processing | Battery sensors |
| **Security and privacy needs** | Many endpoints = larger attack surface; sensitive data | Encryption, authentication |
| **Enormous data (big data)** | Constant streams of readings | Time-series storage |

**Memory aid:** **C-S-I-I-H-S-D-I-L-S-D** is too long; remember **“Connect, Sense, Identify, Interoperate, Scale, Secure, Analyse.”**

## A3. Physical vs virtual capabilities

**Physical capabilities** are what the **hardware** can do in the real world; **virtual capabilities** are what the **software/digital representation** can do.

|  | **Physical (the “thing”)** | **Virtual (its digital counterpart)** |
| --- | --- | --- |
| Exists as | Real device: sensor, actuator, tag, machine | Software representation: digital identity, data model, **digital twin**, service |
| Capabilities | **Sense** the environment; **actuate** (move, switch, heat); **compute** locally (microcontroller); **communicate** (radio); **store** small data; powered by battery or mains | **Identify** (unique ID); **store and process** data at scale; **analyse and predict**; **expose services/APIs**; **simulate and monitor** remotely; **compose** with other services; **access control and logging** |
| Limits | Low power, memory, range; can fail physically | Depends on network and platform; can lag behind the real state |
| Example | A fridge with a temperature sensor and relay | Cloud record of that fridge with history, rules and an alert service |

**In simple words:** the physical part touches the world; the virtual part is its **mirror in the cloud**, where data is stored, analysed and offered as a service.

## A4. How IoT works (five steps)

1. **Sense / collect:** sensors measure a quantity (temperature, motion, location).
2. **Process locally:** the device's microcontroller converts the signal to digital data, filters it and may decide locally (edge processing).
3. **Connect / transmit:** data is sent through a **gateway** or directly using Wi-Fi, cellular, Bluetooth, LoRa or Ethernet, with protocols such as MQTT or HTTP.
4. **Process and store in the cloud (or edge server):** platform stores data, applies rules and analytics (including machine learning).
5. **Act and present:** results go to **dashboards/apps**, and commands go back to **actuators**, closing the loop. Repeat.

```
[Sensors] -> [Device MCU] -> [Gateway / network] -> [Cloud platform: store + analyse]
    ^                                                          |
    |                                                          v
[Actuators] <------------ commands <------------ [Apps / dashboards / rules]
```

## A5. IoT architecture

**Three-layer model (the basic exam answer):**

```
+---------------------------------------------------------+
| APPLICATION LAYER   smart home, smart farm, healthcare, |
|                     dashboards, user services            |
+---------------------------------------------------------+
| NETWORK LAYER       gateways, Wi-Fi, cellular, Bluetooth,|
|                     LoRa; protocols (MQTT, HTTP, CoAP, IP)|
+---------------------------------------------------------+
| PERCEPTION LAYER    sensors, actuators, RFID, devices     |
+---------------------------------------------------------+
```

**Five-layer model (when more detail is asked):**

| Layer | Role |
| --- | --- |
| **Perception (device)** | Sensors, actuators, tags: sense and act |
| **Network (transport)** | Moves data: gateways and communication technologies |
| **Processing (middleware)** | Storage, analytics, device management, cloud/edge platforms |
| **Application** | Services for users: apps, dashboards |
| **Business** | Business models, policies, decisions, privacy, management |

**Where cloud and edge fit:** *edge/fog* processing near devices reduces delay and bandwidth; *cloud* gives large storage and analytics. **Security** applies to every layer.

## A6. General diagram of an IoT device

```
                  +--------------------------------------------+
   ENVIRONMENT    |               IoT DEVICE (node)            |
                  |                                            |
  physical   ---> | [ SENSOR(S) ] --> [ ADC / signal conditioning ]
  quantity        |                          |                 |
                  |                          v                 |
                  |  [ MICROCONTROLLER / PROCESSOR ] <--> [ MEMORY ]
                  |          |   firmware / embedded OS        |
                  |          v                                 |
  action     <--- | [ ACTUATOR(S) ] (relay, motor, valve, LED) |
                  |          |                                 |
                  |          v                                 |
                  |  [ COMMUNICATION MODULE ] -- antenna --> network / gateway
                  |                                            |
                  |  [ POWER SUPPLY: battery, solar, mains ]   |
                  +--------------------------------------------+
```

**Components:** **sensors** (input), **actuators** (output), **processor/microcontroller** (decides), **memory** (firmware and data), **communication module** (Wi-Fi/cellular/Bluetooth/LoRa), **power supply**, **firmware** (software on the device), and optionally a **user interface**.

## A7. Types of sensors

| Sensor type | Measures | Example use |
| --- | --- | --- |
| **Temperature** (thermistor, thermocouple) | Heat | Cold chain, smart thermostat |
| **Humidity** | Moisture in air | Greenhouses, storage |
| **Pressure** | Gas/liquid pressure | Weather, tyres, pipelines |
| **Proximity / ultrasonic / infrared** | Nearby object or distance | Parking, obstacle detection |
| **Light (LDR, photodiode)** | Light level | Street lights, screen brightness |
| **Motion (PIR)** | Movement of people | Security lights, alarms |
| **Accelerometer / gyroscope** | Acceleration, tilt, rotation | Phones, wearables, vehicles |
| **Gas / smoke** | Gas concentration, fire | Safety alarms, air quality |
| **Level** | Liquid level | Water tanks, fuel |
| **Flow** | Fluid flow rate | Water meters, irrigation |
| **Image (camera)** | Pictures/video | Surveillance, checkout counting |
| **Sound (microphone)** | Noise, voice | Voice assistants |
| **GPS / location** | Position | Fleet tracking |
| **Magnetic / Hall effect** | Magnetic field | Door sensors, speed |
| **Biometric / heart-rate** | Body signals | Health wearables |
| **Touch / force** | Contact, pressure by touch | Screens, smart tills |

**Two ways to classify:** *analog vs digital* output; *active* (needs external power or sends a signal, e.g., ultrasonic) vs *passive* (reacts to the environment, e.g., thermistor); also by the physical quantity measured (table above).

## A8. Cellular vs Wi-Fi for IoT

| Feature | **Cellular (LTE-M, NB-IoT, 4G/5G)** | **Wi-Fi (IEEE 802.11)** |
| --- | --- | --- |
| Coverage / range | **Wide area** (kilometres, operator network) | **Short range** (tens of metres per access point) |
| Infrastructure | **Operator's network**; no private network to build | You install and manage **access points** |
| Mobility | **Excellent**: works on the move (vehicles, trackers) | Poor: tied to access-point coverage |
| Data rate | LTE-M/4G/5G high-to-medium; NB-IoT low | **High** (good for video, large data) |
| Power use | NB-IoT/LTE-M can be **low-power**; 4G/5G more | **Higher**, a weakness for battery devices |
| Cost | **Recurring subscription/SIM fees**; modules costlier | Cheap hardware; **no per-device data fees** |
| Security | Strong SIM-based authentication, operator-managed | Depends on correct setup (WPA2/WPA3) and passwords |
| Deployment | Works anywhere with coverage; simple for remote sites | Best inside buildings, campuses, homes |
| Typical use | Smart meters, asset/vehicle tracking, remote farms, ATMs | Smart homes, retail stores, offices, cameras |

**Which to choose (rule):** *fixed, indoors, plenty of power, lots of data* → **Wi-Fi**. *Remote, mobile or spread-out, battery-powered, small data* → **cellular** (LTE-M or NB-IoT). *Long range, very low power, own gateway* → LoRa/LPWAN (mention as an alternative). **Example:** AgriMart's in-store handheld scanners and shelf sensors use **Wi-Fi**; its delivery trucks and remote warehouse generators use **cellular**.

---

# APPENDIX B: Last-5-minutes sheet for the five questions

- **Q1:** DS = independent computers, one coherent system, messages. Advantages **E-S-I-R-I**. Challenges **H-O-S-S-F-C-T-Q**. Transparency **A-L-M-R-R-C-F-P**. Scalability: 3 dimensions (size, geographical, administrative), 4 techniques (hide latency, distribution, replication, caching), problem = **inconsistency**. Middleware groups **Communication, Information system, Control, Security**. Four questions **E-C-R-P**. Paradigms: IPC, remote invocation (request-reply, RPC, RMI), indirect (space + time uncoupling). SMP = all equal; ASMP = some reserved. Shared memory (lower latency) vs message passing (separate address spaces).
- **Q2:** NIST 5 (**O-B-R-R-M**), 4 deployment (public, private, hybrid, community), 3 service (SaaS, PaaS, IaaS). Shade: IaaS customer = data to OS; PaaS = data + apps; SaaS = data. SLA bands **10 / 30 / 100%**; 97.8% → **30%**; downtime 15.84 h (30-day month). Migration **rehost → re-platform → repurchase → rebuild**. PaaS = lock-in risk.
- **Q3:** POSDCORB = Planning, Organizing, Staffing, Directing, Coordinating, Reporting, Budgeting (horizontal silos); hierarchy = strategic / tactical / operational; matrix = cross-functional processes. Three tiers: web, application, data. Benefits **S-R-F-M-R-S**; limitation = expensive and complex. SOA contract: functional description, input/output, precondition, postcondition, error handling. SOA drawbacks: costly/time-consuming, complex security, inconsistent performance.
- **Q4:** ESA = functional (modules) + system (hardware/software/network). Table 1: procurement and accounting rows. Layered: browser → interface layer (SSL) → applications software layer → server. Server-centric: secure, no client software, slower. Client-centric: faster, less secure. Cloud ERP: subscription, anywhere, nothing to install, scalable; drawbacks: security, conflict of interest/IP, vendor reliance.
- **Q5:** Layers per host: hardware, network OS, middleware, components. Figure 1: memory (shared/private) × interconnect (bus/switch); shared = multiprocessor; private = multicomputer. Proxy cache: check for up-to-date copy → hit serves, miss fetches and stores. Recommend client-server + proxy caches; P2P for research datasets.

---

# APPENDIX C: Chapter 1 deep dive (the seven topics on the Contents slide)

**Source:** Chapter\_1\_1.pptx. I compared it slide by slide with your earlier Chapter\_1.pptx: **all 59 slides are identical**, so nothing new was added, but this appendix explains these seven topics in more depth and in exam-answer form.

**About “I know for sure it is asked”:** I cannot know the real paper. What I can say: your paper's Question 1 (50 marks, compulsory) is built almost entirely from this chapter: **1(a)** introduction, advantages, challenges; **1(b)** goals; **1(c)** software concepts and client-server vs P2P; **1(d)** hardware concepts; **1(e)** architecture models and caching. So these topics are **the highest-probability material you have.**

**⚠ Heads-up:** the Contents slide lists seven headings, but the chapter also contains **Hardware concepts (slides 25–29)** and **Software concepts (slides 30–39)** under unnumbered/“6.” headings. They are **not on the Contents slide, yet Q1(c) and Q1(d) test them.** They are covered in Q1(c) and Q1(d) above; do not skip them.

**How each topic is taught below:** *What it is → In simple words → How it works → Why it matters → Example → Exam angle.*

---

## C1. Introduction (slides 3–8)

**What it is.** The chapter's starting point: what a distributed system (DS) is and what it is made of.

**In simple words.** Many separate computers, joined by a network, **cooperate** so well that the user feels they are using **one computer**.

**The definitions on the slides (learn at least two):**

1. A collection of **independent entities that cooperate to solve a problem that cannot be individually solved.**
2. A collection of **mostly autonomous processors communicating over a communication network.**
3. Hardware or software components at networked computers that **communicate and coordinate their actions only by passing messages.**
4. A collection of **independent computers that appear to its users as a single coherent system.**

**Distributed computing (the activity):** a single program is **split into parts that run at the same time on multiple computers**, communicating over a network.

**Two aspects (very likely asked):** **Hardware:** the computers are **autonomous.** **Software:** users **think they are dealing with a single system.**

**How it is built (ingredients, slides 7–8):** each **host** has the same stack. **Without middleware** it is just networked computers; **with middleware** it is a distributed system.

```
+---------------------------+      +---------------------------+
| Component-1 ... Component-n|      | Component-1 ... Component-n|
+---------------------------+      +---------------------------+
| MIDDLEWARE                |      | MIDDLEWARE                |
+---------------------------+      +---------------------------+
| Network OS                |      | Network OS                |
+---------------------------+      +---------------------------+
| Hardware                  |      | Hardware                  |
+------------+--------------+      +-------------+-------------+
          Host-1  ==============NETWORK============  Host-n
```

**Why it matters.** Slide 3 gives the motivation: a growing need for **more information usage and access regardless of where it is located**, plus the **spread of the Internet and the “global village”.** Slide 5 adds that **a parallel computer is implicitly a distributed system.**

**Examples (slide 5):** a **network of workstations**; a **distributed manufacturing system** (automated assembly line); a **network of branch-office computers.**

**Case study: a university's three campuses.** *Situation:* students register from Kigali, Huye or Musanze. *Concept:* DS. *Steps:* each campus server is autonomous (hardware aspect); servers coordinate by messages; the student sees one registration system (software aspect); if one server fails the others continue. *Lesson:* independence + cooperation + single-system illusion.

**Exam angle.** “Define a DS” → give definition 4, then add: independent computers, network, message passing, and the two aspects. Mention **middleware** to show you know what makes it a DS.

**⚠ Slide 3 wording is garbled** (the “crash of a computer” test). Learn the idea: *a DS keeps working for you when one machine fails.*

---

## C2. Why distributed computing? (slides 3, 9, 10 and the advantages)

**What it is.** The reasons organisations and researchers choose distributed or parallel computing instead of one big machine.

**In simple words.** One machine eventually becomes too slow, too expensive, too risky (single point of failure) or too far from the users. Several cooperating machines solve all four.

**Reasons you can draw from the slides (use these as five numbered points):**

1. **Need for access to information wherever it is:** more information use and accessibility regardless of location (slide 3).
2. **The Internet and global village** make distributed computing a **widely deployed, practical tool** (slide 3).
3. **Some problems cannot be solved by one entity alone** (definition 1, slide 4).
4. **Better price/performance and total power than mainframes**, with **incremental growth** (slide 11).
5. **Hardware trend:** after **instruction-level parallelism (ILP) in the 1990s**, **multi-core parallel systems are going to outperform mainstream ones** (slides 9–10).

**But the slides also list open difficulties (a good “discuss” point):** how to **use a large number of processors simultaneously**; how to **write parallel programs easily and efficiently**; **what software support is needed**; **analysing and optimising parallel programs is still hard**; how to **debug concurrent programs.**

**Example.** AgriMart (Q1): the mainframe is expensive to upgrade, slows at month-end and fails completely when it breaks. Distributing the work addresses cost, speed and failure.

**Exam angle.** “Why distributed computing?” is answered by **motivations (1–5) + the advantages (C3)**; end with one sentence on the difficulties. **⚠** Slides 9 and 10 are fragmentary (slide 9 has only the ILP heading), so rely on slides 3 and 11 for substance.

---

## C3. Advantages and disadvantages of a DS (slides 11–13)

**A. Over centralised systems (E-S-I-R-I):**

| Advantage | What it means | How to explain / example |
| --- | --- | --- |
| **Economics** | A collection of microprocessors gives **better price/performance** than a mainframe | Many cheap servers beat one very expensive mainframe |
| **Speed** | May have **more total computing power** than a mainframe; **enhanced performance through load distributing** | Slide example: **10,000 CPU chips × 50 MIPS = 500,000 MIPS** |
| **Inherent distribution** | Some applications are **naturally distributed** | A **supermarket chain** |
| **Reliability** | If one machine crashes **the system as a whole can still survive**; **higher availability, improved reliability** | One branch server fails, others trade on |
| **Incremental growth** | Computing power added in **small increments** (modular expandability) | Add a server per new branch |

Another driving force: the **huge number of PCs** and the need to **collaborate and share information.**

**B. Over independent PCs:**

| Advantage | Meaning |
| --- | --- |
| **Data sharing** | Many users access a **common distributed database** |
| **Resource sharing** | Share **expensive peripherals** (colour printers) |
| **Communication** | Better human-to-human communication: **email, chat** |
| **Flexibility** | **Spread the workload** over available machines |

**C. Disadvantages (3):**

| Disadvantage | Meaning / example |
| --- | --- |
| **Software** | **Difficult to develop** software for distributed systems (concurrency, failures, consistency) |
| **Network** | **Saturation** (network overloaded) and **lossy transmissions** (messages lost) |
| **Security** | **Easy access also applies to secret data**: more entry points |

**Calculation (possible):** total power = number of CPUs × speed of each. 10,000 × 50 MIPS = **500,000 MIPS.**

**Exam angle.** Always give **name + one-line meaning + scenario link**. For “discuss”, finish with a balance sentence: advantages are **potential** and depend on good design, while disadvantages can be reduced with good middleware, replication and security measures.

---

## C4. Goals of a DS (slides 14–21)

**What it is.** The main goal is to **let users access and share resources** while achieving **three goals: Transparency, Openness, Scalability.**

### Goal 1: Transparency

**In simple words:** the user should not need to know that the system is spread over many computers. **Eight types (slide 15):**

| Type | Hides | Easy example |
| --- | --- | --- |
| **Access** | Differences in **data representation and invocation** | A Windows PC and a Linux server exchange data without the user noticing |
| **Location** | **Where** the object is | You open a file without knowing which server holds it |
| **Migration** | That the object **moves** (hidden from the object) | A service moved to another server |
| **Relocation** | That the system **moves an object while a client is using it** (hidden from the client) | A live session continues after the server moves |
| **Replication** | That **copies** exist | A mirrored website |
| **Concurrency** | The **coordination** of simultaneous use | Two tills update stock safely |
| **Failure** | That something **failed and recovered** | A backup server takes over |
| **Persistence** | That an object may be stored in **memory or on disk** (“passivated”) | A record is fetched from disk as if in memory |

**Why full transparency is not possible (slide 16, 3 reasons):** (1) users may be on **different continents**: distribution is obvious; (2) **completely hiding failures is impossible**: you **cannot distinguish a slow computer from a failing one**, and you **can never be sure a server performed an operation before a crash**; (3) **full transparency costs performance** (e.g., keeping **Web caches exactly up to date** with the master copy; **immediately flushing writes to disk** for fault tolerance).

### Goal 2: Openness

An **open DS** can interact with services from other open systems **regardless of the underlying environment**. It should: **conform to well-defined interfaces**, **support portability**, **interoperate easily.** Interfaces are specified with an **interface definition language (IDL).** The challenge: make the DS independent of **heterogeneity of hardware, platforms and languages.** **Implementing openness:** support **different policies** chosen by applications and users (how consistent must cached data be? what may downloaded code do? how to adjust QoS when bandwidth varies? how secret must communication be?). **Ideally the DS provides only mechanisms:** dynamic caching policies per item, different trust levels for mobile code, adjustable QoS per stream, different encryption algorithms.

### Goal 3: Scalability

**Three dimensions:** **size** (users/processes), **geographical** (maximum distance between nodes), **administrative** (number of administrative domains). **Most systems handle only size**, the “(non)solution” being powerful servers; **today's challenge is geographical and administrative scalability.** **Four techniques:** **hiding communication latency**, **distribution** (partition data and computation: DNS, WWW, Java applets), **replication** (copies: replicated file servers/databases, mirrored websites), **caching** (local copies: web caches, file caching). **The scaling problem:** multiple copies lead to **inconsistencies**; keeping them consistent needs **global synchronisation on every change**, which makes **large-scale solutions practically impossible**; if inconsistency can be **tolerated**, global synchronisation can be reduced, and **tolerance depends on the application.**

**Example (campus portal):** a timetable cached on two phones. Lecturer changes it; one phone still shows the old version until refreshed. Forcing all phones to update instantly would slow everyone.

**Exam angle.** Expect “Explain the goals of a DS”, “discuss transparency and its limits”, or “scalability: dimensions, techniques and the problem.” Use **definition → types/dimensions → example → limit/problem.**

---

## C5. DS challenges (slides 22–24)

**What it is.** The eight difficulties designers must overcome (**H-O-S-S-F-C-T-Q**), then the eight false assumptions.

| # | Challenge | Meaning | Typical way it is handled |
| --- | --- | --- | --- |
| 1 | **Heterogeneity** | Different **networks, OSs, hardware, languages** | Middleware, standard protocols |
| 2 | **Openness** | DS should be **extensible**; integrating components by **different programmers** is hard | Published, standard interfaces |
| 3 | **Security** | **Encryption** protects shared resources and secrets in transit; **DoS attacks** remain a problem | Encryption, authentication, firewalls |
| 4 | **Scalability** | Scalable if **the cost of adding a user is a constant amount of resources** | Distribution, replication, caching |
| 5 | **Failure handling** | **Any process, computer or network may fail independently**; each component must be aware of failure modes | Redundancy, recovery, timeouts |
| 6 | **Concurrency** | Many users send **concurrent requests**; each resource must be **safe** concurrently | Locks, transactions |
| 7 | **Transparency** | Make aspects of distribution **invisible to the application programmer** | Middleware abstractions |
| 8 | **Quality of Service (QoS)** | Access is not enough; **guarantee performance, security, reliability** | Resource management, monitoring |

**False assumptions (8 fallacies):** the network is **reliable**; **secure**; **homogeneous**; the **topology does not change**; **latency is zero**; **bandwidth is infinite**; **transport cost is zero**; **there is one administrator.** Each is **false** and each causes real bugs.

**⚠ Overlap:** openness, scalability and transparency are both **goals** and **challenges**. In an answer, treat goals as *what you want* and challenges as *what makes it hard*.

**Exam angle.** “Describe the challenges…” → list all eight with one line each and one scenario link for at least two. If the paper gives a scenario, quote its symptoms next to each challenge.

---

## C6. DS architectural model (slides 40–53)

**What it is.** The **architecture** of a system is its **structure in terms of separately specified components and their interrelationships.** The goal is that the structure meets **present and likely future demands**, like the architecture of a building.

**The four questions (E-C-R-P) that structure everything:**

| # | Question | Answer in the slides |
| --- | --- | --- |
| 1 | **Entities:** what communicates? | **Processes** (supplemented by **threads**, the real endpoints); **nodes** in sensor networks; **objects** (to encourage OO); **components** (like objects, accessed through interfaces) |
| 2 | **Communication paradigm:** how? | **Inter-process communication**, **remote invocation**, **indirect communication** |
| 3 | **Roles and responsibilities:** who does what? | **Client-server** and **peer-to-peer** |
| 4 | **Placement:** how mapped onto physical infrastructure? | Needs **strong application knowledge; few universal guidelines.** Strategies: **services on multiple servers**, **caching**, **mobile code**, **mobile agents** |

**Communication paradigms in depth:**

- **Inter-process communication:** message-passing primitives and **direct use of Internet-protocol APIs (socket programming).**
- **Remote invocation:** a **two-way exchange** that calls a remote operation. **Request-reply protocols** support client-server computing; **RPC** calls procedures in remote processes **as if local**; **RMI** is RPC for **distributed objects.** Sender and receiver are **directly linked**, with senders explicitly directing invocations.
- **Indirect communication:** senders **need not know who they send to (space uncoupling)**; senders and receivers **need not exist at the same time (time uncoupling).** **⚠ Slide 46 says “time coupling”; this is a misprint, write time uncoupling.**

**Placement strategies:**

1. **A service provided by multiple servers:** several server processes on separate hosts cooperate to provide one service.
2. **Caching:** a **cache** stores **recently used data objects closer to a client** than the objects themselves. **New objects replace old ones**; the **caching service first checks the cache** and supplies the object **if an up-to-date copy exists**; **otherwise an up-to-date copy is fetched.** Caches may be **with each client** or in a **shared proxy server.**
3. **Mobile code:** code **downloaded** to run locally when accessing a service (the Web: some sites need additional code in the browser).
4. **Mobile agents:** **a running program (code and data) that travels from computer to computer carrying out a task on someone's behalf (e.g., collecting information) and eventually returns with results.**

**Example.** A university web portal: entities = browser and web server processes; paradigm = request-reply; roles = client-server; placement = proxy cache at each campus.

**Exam angle.** “State the four questions” is **pure recall**. “Explain the communication paradigms” needs **three headings with sub-types.** “Describe how a caching service works” needs the **three steps** (check, serve if up to date, otherwise fetch and store).

---

## C7. Types of distributed systems (slides 54–58)

**What it is.** By how nodes are arranged, a DS is **client/server** or **peer-to-peer.**

**Client-server model (slides 55–56):**

- **Servers** provide services around a **shared resource:** file systems, databases, implementation repositories; shared linked documents (Web, video-on-demand); shared applications; shared distributed objects.
- **Clients** give remote access to services: a **programming interface that turns local service calls into request/reply messages**; simple devices (**barcode readers, teller machines, hand-held phones**); computers with their own interface for a specific service; computers with an integrated interface for related services (**compound documents**).
- **Application layering** (slide 56) is a diagram I could not read. **\[Added\]** The usual three levels are **user interface, processing (application logic), and data**, which can be split between clients and servers.

**Peer-to-peer model (slides 57–58):** a distributed application architecture that **partitions tasks or workloads between peers.** Peers are **equally privileged, equipotent participants**, forming a **network of nodes.** Peers **make a portion of their resources (processing power, disk storage, network bandwidth) directly available to others without central coordination by servers or stable hosts.**

|  | Client-server | Peer-to-peer |
| --- | --- | --- |
| Roles | **Distinct**: clients request, servers provide | **Equal**: each peer both uses and provides |
| Control | Servers manage shared resources (central) | **No central coordination** |
| Resources | Held by servers | Contributed by every peer |
| Strength | Easy to manage, secure, authoritative data | Resilient, spreads load, no single point of failure |
| Weakness | Server can be a **bottleneck / single point of failure** | **Harder to coordinate, search, secure and keep consistent** **\[Added reasoning\]** |
| Example | **Web server** and browsers; ATM and bank server | File sharing among peers **\[Added\]** |

**Exam angle.** Usually **“compare client-server and P2P, with diagrams”** and often **“which would you choose?”** Draw both diagrams, compare on **roles, control, resources, strengths, weaknesses**, and justify the choice with the scenario (authoritative stock and prices → client-server; direct sharing of large datasets → P2P).

---

## C8. Quick-fire question bank for Chapter 1 (practice, then check the skeleton)

| # | Likely question | Answer skeleton |
| --- | --- | --- |
| 1 | Define a DS and give its two aspects | Definition 4 + independent computers, network, messages; hardware = autonomous; software = single system |
| 2 | Why use distributed computing? | Five motivations in C2 + advantages + one difficulty |
| 3 | Advantages of DS over centralised systems | E-S-I-R-I, each with a one-line meaning and example (10,000 × 50 MIPS) |
| 4 | Disadvantages of DS | Software, network (saturation, lossy), security (easy access to secrets) |
| 5 | Explain transparency; list types; discuss limits | Definition, 8 types, 3 limits |
| 6 | Explain openness | Standard rules for syntax/semantics (IDL), interfaces, portability, interoperability; mechanisms not policies |
| 7 | Explain scalability | 3 dimensions, 4 techniques, inconsistency problem, tolerate inconsistency |
| 8 | Describe the challenges of a DS | The eight, with one line each |
| 9 | List the false assumptions | Eight fallacies |
| 10 | State the four architectural questions and explain paradigms | E-C-R-P; IPC, remote invocation (request-reply, RPC, RMI), indirect |
| 11 | How does a caching service work? | Check cache → up-to-date copy served; otherwise fetch, store, replace old; client or proxy |
| 12 | Compare client-server and P2P | Table in C7 + scenario choice |

**Two-minute self-test (cover the answers):**

1. What are the two aspects of a DS? *(hardware: autonomous computers; software: single-system view)*
2. Name the five advantages over centralised systems. *(E-S-I-R-I)*
3. Which transparency hides movement while the client is using the object? *(relocation)*
4. What are the three scalability dimensions? *(size, geographical, administrative)*
5. What problem do replication and caching cause? *(inconsistency, needs global synchronisation)*
6. Name the four architectural questions. *(entities, communication paradigm, roles/responsibilities, placement)*
7. Which communication paradigm is two-way and directly linked? *(remote invocation: request-reply, RPC, RMI)*
8. What is a mobile agent? *(program with code and data that travels between computers and returns with results)*
