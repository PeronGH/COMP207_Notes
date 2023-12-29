### Introduction to Distributed Databases

#### I. Background and Motivation
- **Scenario:** Expansion of a store chain (e.g., CS-DOR) across multiple locations.
- **Need:** Each site has its database for local information, while a central office manages broader data.
- **Goal:** Seamless query execution across different sites without specifying data location.

#### II. Concept of Distributed Databases
- **Definition:** A collection of multiple logically interrelated databases distributed over a computer network.
- **Characteristics:**
  - Consists of various nodes or sites connected by network links.
  - Each node represents a physical location of data storage.
  - Network links allow communication between nodes.

#### III. Examples of Distributed Databases
- **Organizations:** Large companies with branches or different sub-companies.
- **Capacity Issues:** Handling extensive data transactions exceeding the capability of a single computer.
- **Legal Compliance:** GDPR in Europe requires data about Europeans to be stored within Europe.

#### IV. Advantages of Distributed Databases
1. **Workload Balancing:** Distributes database queries across multiple computers.
2. **Scalability:** Easier to add more computers than upgrading existing hardware.
3. **User Throughput:** Handles more user requests simultaneously.
4. **Data Safety:** Geographic distribution reduces risks of data loss due to local disasters.

#### V. Formal Definition
- **Distributed Database:** Collection of interrelated databases distributed over a network.
- **Network Structure:** Comprises nodes (data storage sites) linked by network connections.

#### VI. Advantages of Distributed Databases
1. **Improved Performance:** Reduces computation time, disk access, and communication costs.
2. **Ease of Scalability:** Adding new computers increases capacity and performance.
3. **Resilience:** Multiple nodes provide backup, reducing risk of complete system failure.

#### VII. Key Takeaway
- **Essential Concept:** Understanding the distributed nature of databases, where data is stored across various networked sites, each contributing to a larger, interconnected database system.

### Fragmentation, Replication, and Transparency in Distributed Databases

#### I. Introduction
- **Transparency:** Hiding unnecessary details from the user.
- **Focus:** Fragmentation and replication as key examples of transparency.

#### II. Fragmentation Transparency
- **Horizontal Fragmentation (Sharding):** Dividing a table into rows and storing them at different sites. The original table can be reconstructed by taking the union of these fragments.
- **Vertical Fragmentation:** Dividing a table into columns and storing them at different sites. The original table can be reconstructed via a natural join of these fragments.
- **Combination:** Both horizontal and vertical fragmentation can be combined for more complex distributions.
- **User's Perspective:** The user sees the complete relation without needing to know about the fragmentation.

#### III. Examples of Fragmentation
- **Horizontal Fragmentation Example:** The 'transaction' relation in a store database is split across different locations like Liverpool, Manchester, and London.
- **Vertical Fragmentation Example:** A relation with attributes like 'name', 'transaction ID', 'customer ID', and 'price' is split so that the central site holds 'name' and 'price', while each site stores 'transaction ID' and 'customer ID'.

#### IV. Replication Transparency (Redundancy)
- **Purpose:** Improves resilience in case of system failures and enhances efficiency.
- **Example:** Storing parts of a database at multiple sites allows query execution even if one site fails.
- **Full Replication:** Every site stores a full copy of the entire database, allowing fast queries but slow updates.
- **No Replication:** Each fragment is stored uniquely at one site, leading to fast updates but potential issues with query execution during failures.
- **Partial Replication:** A middle ground between full and no replication.
- **User's Perspective:** Users are unaware of the replication status of data.

#### V. Other Types of Transparency
- **Location Transparency:** Users are unaware of where the data is physically stored.
- **Naming Transparency:** Ensures consistent naming conventions across different sites.

#### VI. Summary
- Fragmentation and replication are crucial aspects of distributed databases that maintain transparency for users. These mechanisms enable efficient data management and retrieval without burdening users with the underlying complexities of data distribution and storage.

### Transaction Management in Distributed Databases

#### I. Introduction
- **Context:** Challenges in transaction management within distributed databases.
- **Focus:** Concurrency control and recovery mechanisms.

#### II. Concurrency Control
- **Using Locks:** Ensuring ACID properties (isolation and consistency) through locks.
- **Centralized Lock Management:** One computer manages all locks, leading to potential system bottlenecks or failures.
- **Decentralized Lock Management:** Multiple computers each manage different items, reducing bottlenecks but complicating lock requests.
- **Backup Systems:** To address failure of the central lock manager, backup systems can be implemented.
- **Voting System for Locks:** Each site with a data copy votes to grant a global lock, enhancing distribution but increasing communication overhead.

#### III. Recovery in Distributed Databases
- **Transactions in Distributed DBs:** Global transactions span multiple sites, requiring coordination for atomicity and durability.
- **Issues with Node Failures:** Failures during transactions can lead to uncertainty about the state of the transaction.

#### IV. Distributed Commit Protocols
- **Two-Phase Commit Protocol:**
  - **Phase 1:** Coordinating node asks if nodes are ready to commit. Nodes respond with readiness or abort.
  - **Phase 2:** Based on responses, the coordinator instructs to either commit or abort.
  - **Logging:** All actions are logged to ensure atomicity and durability.
- **Three-Phase Commit Protocol:**
  - **Introduction:** Addresses a specific failure scenario in the two-phase commit.
  - **Phase 2a (Prepare to Commit):** Nodes enter a preparatory state before committing.
  - **Phase 2b (Commit/Abort):** Final commit or abort instructions are sent.
  - **Advantage:** Addresses the dilemma of uncertain state in two-phase commit.

#### V. Summary
- **Concurrency Control in Distributed DBs:** Balancing between centralized and decentralized lock management, and introducing voting mechanisms.
- **Recovery Protocols:** Implementing two-phase and three-phase commit protocols to ensure consistent and reliable transaction management across distributed systems. 
- **Complexity:** Managing transactions in distributed databases introduces additional layers of complexity, requiring robust protocols for coordination and recovery.

### Query Processing in Distributed Database Management Systems

#### I. Overview
- **Objective:** Addressing challenges in query processing within distributed databases.
- **Focus:** Efficient execution of joins in a distributed environment using semi-joins.

#### II. Distributed Database Query Challenges
- **Scenario:** A query initiated at one site may require data from another site.
- **Problem:** Network communication between sites is slower compared to local data access.
- **Priority:** Minimize data transfer between sites to reduce query processing time.

#### III. Naive Approach to Distributed Joins
- **Example:** Joining two relations, R (at Site A) and S (at Site B).
- **Naive Method:** Site B requests the entire relation R from Site A for processing.
- **Issue:** High network cost due to the transfer of the entire relation R.

#### IV. Optimizing with Semi-Joins
- **Left Semi-Join:** Reduces the amount of data transferred by sending only necessary rows.
- **Procedure:**
  1. **Projection:** Site B sends a projection of common attributes in S to Site A.
  2. **Computation at Site A:** Calculates R's left semi-join with the received projection.
  3. **Transfer to Site B:** Only the relevant part of R (after semi-join) is sent to Site B.

#### V. Semi-Join Example
- **Database Example:** Film and Theater databases at different sites.
- **Goal:** Find films showing in Liverpool on a specific date.
- **Process:**
  1. **Site B's Projection:** Send relevant theater data (titles, dates) to Site A.
  2. **Site A's Computation:** Perform left semi-join on films with the received data.
  3. **Reduced Data Transfer:** Only send the result of the semi-join back to Site B.

#### VI. Communication Cost Analysis
- **Assumptions:** Number of movies, bytes per tuple, and number of movies in the query.
- **Cost with Semi-Join:** Significantly lower data transfer compared to the naive approach.
- **Comparison:** 40,000 bytes (with semi-join) vs. 10 million bytes (naive approach).

#### VII. Summary
- **Key Takeaway:** Semi-joins significantly reduce data transfer in distributed query processing.
- **Advantage:** Efficient execution of queries by minimizing network communication.
- **Recommendation:** Consider semi-joins for optimizing distributed database queries. 

#### VIII. Additional Information
- **MapReduce:** An optional topic bridging distributed databases and NoSQL databases.
- **NoSQL Databases:** The next topic in the course, exploring non-relational database systems.