
## **Data Fundamentals**

1. **Definition of Data**
    - Unorganized information processed to be meaningful
    - Includes: facts, numbers, symbols, images, perceptions
2. **Data Structures**
    - **Structured Data**
        - Highly organized, strict schema
        - Stored in tables (rows & columns)
        - Examples: Excel, SQL databases, online forms
    - **Unstructured Data**
        - No specific format, difficult to process
        - Examples: text files, media (images/audio/video), web pages, social media content
    - **Semi-Structured Data**
        - Partial organization, uses tags or hierarchy
        - Examples: JSON, XML, emails
3. **Data Sources**
    - Traditional databases
    - Flat files
    - XML datasets
    - Web scraping
    - Data streams & feeds
    - Social media
    - IoT sensors
4. **File Formats for Data Transfer**
    - **Delimited text files** → CSV, TSV
    - **Spreadsheets** → rows & columns, can export CSV
    - **Language files** → XML, JSON
5. **Data Repositories**
    - **Relational Databases (RDBMS)**
        - Structured data in related tables
        - Examples: IBM DB2, SQL Server, Oracle, MySQL
        - Uses: OLTP (day-to-day business operations)
        - Features: normalization, transactional integrity, concurrent access
    - **Non-Relational Databases**
        - Flexible, handle unstructured/semi-structured data
        - Examples: MongoDB, Cassandra, Redis
        - Document-oriented, key-value, columnar, graph
6. **OLAP Systems**
    - Focus: querying and analyzing large datasets
    - Includes: relational + non-relational DBs, data warehouses, data lakes, big data stores
    - Example: CRM data for sales projections
7. **OLAP vs OLTP**
    - **OLAP (Online Analytical Processing)**
        
        Online Analytical Processing is designed for **data analysis and decision-making** (Business Intelligence). It is not used to operate the business in real time, but rather to understand how the business is performing.
        
        - **Focus:** Reading large volumes of historical data to perform complex queries and aggregations.
        - **Priority:** Read speed and performance on large-scale queries.
        - **Structure:** Databases are **denormalized** (star or snowflake schemas), grouping information to make reads faster, even if it occupies more storage space. They typically live in a _Data Warehouse_.
        - **Real-world examples:**
            - Calculating the average sales of a store over the last 5 years, broken down by region.
            - Analyzing user behavior and retention over a quarter.
            - Generating end-of-month financial reports.
    - **OLTP (Online Transaction Processing)**
        
        Online Transaction Processing is designed for the **day-to-day operations** of an application or business. Its main goal is to process a large volume of short, fast transactions.
        
        - **Focus:** Constantly and safely inserting, updating, and deleting data (CRUD operations).
        - **Priority:** Write speed and data integrity. They use ACID properties (Atomicity, Consistency, Isolation, Durability) to ensure no transaction is left incomplete.
        - **Structure:** Databases are **highly normalized** (tables are split to avoid data redundancy and save space).
        - **Real-world examples:**
            - Making a transfer in your banking app.
            - Buying a product on Amazon and having inventory updated immediately.
            - Registering a new user on a platform.
8. **Conclusion**
    - Data types: structured, unstructured, semi-structured
    - Storage: relational DBs (OLTP), OLAP (analytics), non-relational DBs (flexibility)

---

## **Information and Data Models**

1. **Information Models**
    - Abstract representation of entities, properties, relationships, and functions.
    - High-level, conceptual, business-focused.
    - Used by stakeholders and analysts to define concepts and rules.
2. **Data Models**
    - Technical blueprint derived from information models.
    - Specifies schema: tables, columns, data types, indexes, relationships.
    - Ensures integrity via normalization, reduces redundancy.
    - Used by database designers and developers for implementation.
3. **Differences**
    - **Information models** → abstraction, broad business view, no storage details.
    - **Data models** → technical, storage/queries, concrete structures.
    - Flow: Information Model → Data Model → Database Implementation.
4. **Hierarchical Model**
    - Early physical implementation of information systems.
    - Tree-like structure, low abstraction.
    - Good for one-to-many, problematic for many-to-many → redundancy.
    - Historical importance, linked to initial database designs.
5. **Types of Data Models**
    - **Relational Model**
        - Stores data in tables.
        - Supports data independence (logical, physical, storage).
        - Advantages: simplicity, flexibility, ease of use.
    - **Entity-Relationship (ER) Model**
        - Conceptual representation of entities & attributes.
        - Uses ER diagrams (entities = rectangles, attributes = ovals).
        - Easy conversion to relational tables.
        - Example: library database → books, authors, borrowers.
6. **Key Concepts in Database Management**
    - **Logical Data Independence** → schema changes without affecting user access.
    - **Physical Data Independence** → internal reorganization without affecting apps.
    - **Physical Storage Independence** → moving/reorganizing storage without impact.

---

### 1. The Design Lifecycle (From Idea to Code)

These last three models represent the phases you go through when building a system, moving from the most abstract (business) to the most technical (code).

- **Information Model (IM) - The "What":** This is the business vision. There are no databases or code here, only human rules. The library director tells the analyst: _"We need to know what books we have, who wrote them, and which user has them on loan"_.
- **ER Model (ER) - The Map or "Bridge":** This is how we draw the Information Model so that technical teams can understand it. You use rectangles for **Entities** (Book, Author, User) and lines for **Relationships** (A user _borrows_ a book). It is a visual diagram to ensure nothing is missing before starting to code.
- **Data Model (DM) - The "How" (The Technical Blueprint):** This is where developers take the ER diagram and translate it into pure technology. They define that the "Books" table will have an `ID` column (integer) and a `Title` column (text of 100 characters), and create strict rules (Constraints and Foreign Keys) so the database does not accept errors.

### 2. Ways to Organize Data Internally

Once you have your technical blueprint (Data Model), you need a database system to build it. The two historical architectures:

- **Hierarchical Model (HM) - The Model of the Past:** Imagine the database as the folder system on your computer. You have a root folder (Author), and inside it you place files (their Books).
    - _The problem:_ It works well if a book has only one author (1 to N). But if a book was written by three different authors, the system collapses or forces you to save the same book three times in different folders (creating **redundancy**).
- **Relational Model (RM) - The Current Standard:** This is the model used almost everywhere today (SQL, databases like PostgreSQL or MySQL). Instead of folders, you use **independent tables** that relate to each other through identifiers (IDs).
    - _The advantage:_ A book exists only once in the "Books" table, and an author exists only once in the "Authors" table. If three authors wrote a book, you simply use an intermediate table to connect them. This eliminates redundancy and is the perfect foundation for **OLTP** (transactional) systems.

---

**Summary:** The _Information Model_ defines the business, the _ER Model_ draws it, the _Data Model_ translates it into technical rules, and all of this is built today using a _Relational Model_.

---

### 📦 Comparison Diagram

```
Abstraction ↑
[ Information Model ]  -> business rules, concepts
        ↓
[ Data Model ]        -> schema, DB blueprint
        ↓
[ Implementation ]    -> Hierarchical / Relational / ER
Abstraction ↓

```

---

## ERDs and Relationships types

---

### 🔑 Keywords / Concepts

- **ERD** → visual DB structure, entities ↔ relationships
- **Entities** → rectangles, people/objects/concepts, have attributes (ovals)
- **Relationship Sets** → diamond or line connecting entities
- **Crow’s Foot Notation** → visual symbols for relationship type & cardinality
- **Attributes** → properties of entities, connected to one entity
- **Relationship Types**:
    - **1:1** → one entity ↔ one entity
    - **1:N** → one entity ↔ many entities
    - **N:1** → many entities ↔ one entity
    - **N:M** → many entities ↔ many entities

---

### 📦 Diagrams (simplified)

**1:1**

```
[Book]───[Author]

```

**1:N / N:1 (crow’s foot)**

```
[Author] ──< [Book]   (one author writes many books)

```

**N:M (crow’s foot both sides)**

```
[Author] >──< [Book]   (many authors write many books)

```

**ERD components**

```
[Entity] (rectangle)
   |
   o-- Attribute (oval)

[Relationship] (diamond / line)
   |
Crow's foot → shows cardinality
```

![](assets/Pasted%20image%2020260503223331.png)



**Crow's foot → shows cardinality**
![](assets/Pasted%20image%2020260503223339.png)


---

## Data types

---

### 🔑 Keywords / Concepts

- **Data Type** → column constraint, controls type of data stored
- **Examples**:
    - Text → strings
    - Date → valid date format
    - Numeric → numbers
- **Varchar** → variable-length string, e.g., `Varchar(100)` → stores ≤100 chars, only uses space needed
    - Pros → efficient (space-saving), flexible (varying length strings)
    - Use → names, addresses, descriptions
- **Char** → fixed-length string → pads spaces if shorter than defined length
- **Numeric Types**:
    - **INT / SmallInt** → whole numbers, specific range
    - **Float** → approximate precision, fractional numbers
    - **Decimal** → exact precision, financial calculations
- **Date/Time Types** → date, time, datetime, timestamp → store temporal data
- **Binary / BLOB** → store images/files, non-textual sequences of bytes
- **Advantages of correct data types**:
    - Prevents invalid data
    - Accurate sorting and range queries
    - Enables numeric calculations (e.g., order totals)
    - Efficient storage and database performance

---

### 📦 Diagram (simplified)

```
[Book Table]
Columns:
Title       -> Varchar(100)
PublishDate -> Date
Pages       -> INT
CoverImage  -> BLOB

Notes:
Varchar → variable length, space-efficient
Char    → fixed length, pads spaces
Numeric → INT, FLOAT, DECIMAL depending on precision need
Date/Time → DATE, TIMESTAMP
Binary → BLOB

```

---

### ❓Questions that arise

- When to choose CHAR vs VARCHAR if string lengths are mostly uniform?
    
    If string lengths are **always** or **almost always** the same, **you should choose `CHAR`**.
    
    - **Why?** `VARCHAR` adds a small overhead of 1 or 2 extra bytes per record just to store how long the string is. `CHAR`, being fixed-length, does not need this overhead.
    - **The fragmentation problem:** If you use `VARCHAR` and update a record with a longer word than the previous one, the database engine might not have space in that memory block (page) and would have to move the entire row to a new location (a phenomenon known as _page split_ or _row migration_). This degrades performance. With `CHAR`, the space is already reserved from the start; an update simply overwrites the bytes without moving anything.
    - **Perfect use cases for `CHAR`:** Country codes (MX, US, ES), encrypted hashes (MD5, SHA-256), UUIDs, or single-letter status codes (M/F, Y/N).
- Float vs Decimal → trade-offs in performance vs precision?
    
    The fundamental difference lies in how the computer handles numbers at the binary level.
    
    - **Decimal (or Numeric): Exact Precision.**
        - **Pros:** What you store is **exactly** what you get. There are no strange rounding errors.
        - **Cons:** It takes up more disk space and mathematical calculations are slower because the database engine must process them through software, not directly in hardware.
        - **When to use it:** **Always** when handling money, financial transactions, or accounting.
    - **Float (or Real/Double): Approximate Precision (Floating Point).**
        - **Pros:** Calculations are incredibly fast because they use the processor's floating-point unit (FPU) (hardware). They can also store astronomically large or tiny numbers while taking up very little space.
        - **Cons:** They suffer from binary rounding errors (for example, `0.1 + 0.2` could result in `0.30000000000000004`).
        - **When to use it:** Scientific calculations, sensor telemetry (IoT), geographic coordinates, machine learning, or video games, where speed matters more than precision to the 15th decimal.
- How do BLOBs affect query performance in large tables?
    
    A `BLOB` (Binary Large Object) is used to store images, PDFs, or audio files directly in the database. Its impact on performance is usually **very negative** if not handled properly.
    
    - **The Cache and Table Scan problem:** Databases read information in blocks (typically 8KB). If you have small rows, hundreds of rows fit in a single block. If you put a 2MB file (a BLOB) in a row, you suddenly need many blocks for a single row. A `SELECT *` forces the hard drive to read gigabytes of useless data, ruining your server's memory cache.
    - **How DBMSs solve it:** Most modern engines do not store the BLOB in the same row (Off-Row storage). In the original row, they only store a "pointer" or invisible link that indicates where the actual file is located.
    - **Best practice:** As a data engineer, the modern golden rule is to **avoid storing files in the database**. It is much better to store the file in cloud storage (such as Amazon S3 or Google Cloud Storage) and store only the **URL** text in your database (using a `VARCHAR`).
- Variations of data types across DBMS (MySQL vs SQL Server vs Oracle)?
    
    | **Data Type** | **MySQL / PostgreSQL** | **SQL Server (Microsoft)** | **Oracle** |
    |---|---|---|---|
    | **Strings** | `VARCHAR` | `VARCHAR` / `NVARCHAR` (Use `N` if you need Unicode characters such as emojis or Chinese characters). | **`VARCHAR2`** (Never use `VARCHAR` in Oracle; it is a data type reserved for future use and is discouraged). |
    | **Date with Time** | `DATETIME` or `TIMESTAMP` | `DATETIME2` (The modern, recommended version over `DATETIME`). | `DATE` (In Oracle, the `DATE` type includes the time. If you need fractional seconds, use `TIMESTAMP`). |
    | **Booleans (True/False)** | `BOOLEAN` (Internally just an alias for `TINYINT(1)`). | `BIT` (Accepts 0, 1, or NULL). | Had no boolean for tables until version 23c. Historically, `NUMBER(1)` or `CHAR(1)` with 'Y' / 'N' is used. |
    | **Auto-increment** | `AUTO_INCREMENT` (MySQL) or `SERIAL` (PostgreSQL) | `IDENTITY(1,1)` | Uses `SEQUENCES` (independent objects that generate numbers, although recent versions added `IDENTITY`). |
    

---

---

## Relational Model Concepts

---

### 🔑 Keywords / Concepts

**Sets** → collection of unique elements, unordered

- Membership → `a ∈ A`
- Subset → `A ⊆ B`
- Union → `A ∪ B`
- Intersection → `A ∩ B`
- Difference → `A - B`
- Empty set → `{}`
- Power set → `P(A)`
- Universal set → `U`
- Disjoint sets → no elements in common
- Venn diagrams → visualize relationships

**Relations** → connections between set elements

- Binary relations → connect 2 elements
- Ordered pairs → `(a, b) ∈ A × B`

**Relation Properties**

- Reflexive → `aRa` (equality)
- Symmetric → `aRb ⇒ bRa` (siblings)
- Transitive → `aRb ∧ bRc ⇒ aRc` (less than)
- Antisymmetric → `aRb ∧ bRa ⇒ a=b` (≤ relation)

**Relational Model Components**

- Relation schema → structure
    - Relation name, attribute names & types
    - Example: Author(author_id CHAR, last_name VARCHAR, first_name VARCHAR, email VARCHAR, city VARCHAR, country CHAR)
- Relation instance → actual data (rows/tuples)

**Key Concepts**

- Degree → # of attributes / columns (6 in example)
- Cardinality → # of tuples / rows (5 in example)

---

### 📦 Diagram (simplified)

```
Sets:
A = {a1, a2, a3}
B = {b1, b2}
Operations: ∪, ∩, -, ⊆

Relations:
Binary: (3,5) less than
Ordered pairs: (author_id, name)

Relational Table:
Schema: Author(author_id CHAR, last_name VARCHAR, ...)
Instance:
Row1 | Row2 | Row3 | ...
Columns = attributes
Rows = tuples
Degree = #columns
Cardinality = #rows

```

---

---

### 🔑 Relations (Concrete Examples)

- A **relation** connects elements of one or more sets (tables in a DB).
- **Binary relation** → connects 2 elements. Example:
    - Set A: People → {Alice, Bob}
    - Set B: Books → {Book1, Book2}
    - Relation: “borrows” → {(Alice, Book1), (Bob, Book2)}
- **Ordered pair** → each relation has an order. Example: (Alice, Book1) ≠ (Book1, Alice)

**Summary:** Relation = “what connects to what” within sets, equivalent to rows in a table.

---

### 🔑 Relation Properties with Real-World Examples

1. **Reflexive**
    - Each element relates to itself.
    - Example: “is equal to” → Alice = Alice, Book1 = Book1
2. **Symmetric**
    - If A relates to B, then B relates to A.
    - Example: “is a sibling of” → If Alice is Bob's sibling, Bob is Alice's sibling
3. **Transitive**
    - If A relates to B and B relates to C, then A relates to C.
    - Example: “is less than” → If 3 < 5 and 5 < 7, then 3 < 7
4. **Antisymmetric**
    - If A relates to B and B relates to A → A = B
    - Example: “≤” → If 5 ≤ 7 and 7 ≤ 5, then 5 = 7

---

### 📦 Visual simple

```
Reflexive:        Alice → Alice
Symmetric:         Alice ↔ Bob
Transitive:        3 < 5 < 7  =>  3 < 7
Antisymmetric:     5 ≤ 7 && 7 ≤ 5  =>  5 = 7

```

---

---

## Data architecture

---

### 📌 Keywords / Concepts

- Deployment Topology → arrangement HW/SW/network
- Factors: scalability, performance, reliability, app nature
- Single-tier → all in one machine
- Two-tier → client (UI) + server (logic + DB)
- Three-tier → client (UI) + app server (logic) + DB server
- Cloud DB → remote, scalable, no local install, accessible anywhere

### 📦 Simple Diagrams

**Single-tier**

```
[UI + Logic + DB]

```

**Two-tier**

```
[Client(UI)] <--> [Server(DB + Logic)]

```

**Three-tier**

```
[Client(UI)] <--> [App Server(Logic)] <--> [DB Server]

```

**Cloud**

```
[Client] <--> [App Layer in Cloud] <--> [DB in Cloud]

```

### ❓ Questions that arise

- Why choose 2-tier over 3-tier if scalability is a concern?
- How is security different in Cloud vs on-prem 3-tier?

---

---

## **Distributed Architecture and Clustered Databases**

### **Topic: Distributed Database Architectures**

**Keywords / Concepts**

- **Why?** For critical or large-scale workloads needing **High Availability (HA)** and **scalability**.
- **What?** Clusters of interconnected machines that distribute processing and storage tasks.
- **Benefits:** Enhanced scalability, fault tolerance, and performance.

---

### **Topic: Architecture Types**

**Keywords / Concepts**

- **Shared Disk:**
    - Multiple servers, one **shared storage** pool.
    - All servers can access all data, allowing for parallel processing.
    - **Failure:** Clients are rerouted to another active server.
- **Shared Nothing:**
    - Each node is self-sufficient with its own CPU, memory, and disk.
    - Data is distributed across nodes using replication or partitioning.
    - **Failure:** Clients are rerouted to a replica or an alternative node.
- **Combination/Specialized:**
    - A hybrid approach that uses a mix of shared disk, shared nothing, and other techniques.

**Diagrams**

- **Shared Disk Architecture**
    
    ```python
    +----------+    +----------+    +----------+
    | Server 1 |    | Server 2 |    | Server N |
    | (CPU/Mem)|    | (CPU/Mem)|    | (CPU/Mem)|
    +----------+    +----------+    +----------+
         |             |               |
         '-----. V .-----'---------------'
               |
       +-----------------+
       |  SHARED STORAGE |
       |      (Disk)     |
       +-----------------+
    ```
    
- **Shared Nothing Architecture**
    
    ```python
    +-----------------+    +-----------------+    +-----------------+
    |      NODE 1     |    |      NODE 2     |    |      NODE N     |
    | (CPU/Mem/Disk)  |<-->| (CPU/Mem/Disk)  |<-->| (CPU/Mem/Disk)  |
    +-----------------+    +-----------------+    +-----------------+
    ```
    

---

### **Topic: Data Management & Optimization Techniques**

**Keywords / Concepts**

- **Database Replication:** 💿
    - Copying changes from a primary database to one or more replicas.
    - **Goal:** Distribute read workloads and provide failover capability.
    - **HA Replica:** High Availability. Replica is in the same location for local failures (hardware/software).
    - **DR Replica:** Disaster Recovery. Replica is in a different geographic location for site-wide disasters (fire, flood).
- **Database Partitioning & Sharding:** 分割
    - **Partitioning:** Splitting one large table into smaller logical pieces (e.g., sales data by year).
    - **Sharding:** Placing these partitions (called shards) onto separate nodes in a cluster.
    - **How it works:** Queries are processed in **parallel** across multiple shards, and the results are then combined.
    - **Goal:** Massively scale both read and write performance. It's excellent for huge datasets found in Data Warehousing and BI.

---

### **Questions**

- The video mentions "combination architectures" but gives no examples. What does a real-world hybrid of Shared Disk and Shared Nothing look like?
    
    ### ## Hybrid Architecture: The Best of Both Worlds 🔗
    
    A real-world hybrid of **Shared Disk** and **Shared Nothing** architecture is typically found in high-end, mission-critical database systems designed for both extreme local performance and disaster-proof reliability.
    
    The most common example is an **Oracle Real Application Clusters (RAC) database running on an Exadata machine, combined with Oracle Data Guard for disaster recovery.**
    
    Think of it like a major restaurant chain:
    
    - **The Shared Disk Part (The Local Restaurant):** At a single location (one datacenter), you have a massive, state-of-the-art kitchen (a high-performance **shared storage** system). Multiple chefs (database server **nodes**) work in this kitchen simultaneously. They can all access any ingredient (data) instantly. If one chef gets sick, another immediately takes over their station. This is **Oracle RAC**. It provides incredible local high availability and processing power because all nodes see the same data.
    - **The Shared Nothing Part (The Restaurant Chain):** The company has restaurants in different cities (geographically separate datacenters). Each restaurant is a self-contained unit with its own kitchen and ingredients. They are completely independent. If a fire burns down the New York restaurant, the company can redirect all business to the Chicago location. This is **Oracle Data Guard**, which **replicates** data between the two independent sites.
    
    The combination gives you the best of both worlds:
    
    1. **Local High Availability (Shared Disk):** If a single server node fails within your primary datacenter, another node takes over in seconds with no data loss because they all share the same disk.
    2. **Disaster Recovery (Shared Nothing):** If your entire primary datacenter is destroyed by a flood, you can fail over to your secondary datacenter hundreds of miles away and continue operating.
- In a sharded architecture, how does the database know which shard contains the data for a specific query? Is there a coordinator or routing layer that isn't mentioned?
    
    ### ## Shard Routing: The Database's Postal Service 🗺️
    
    A sharded architecture knows where to find data for a specific query by using a **Shard Key** and a **Routing Mechanism**. It's very similar to how a postal service uses a zip code to deliver mail.
    
    Here are the key components of the process:
    
    ### **1. The Shard Key 🔑**
    
    This is the most critical piece. It's a specific column in your data that the database uses to decide which shard the row belongs to. When you design the sharded database, you choose this key.
    
    - **Example:** For a `Users` table, the `UserID` is a perfect shard key. For an `Orders` table, `CustomerID` is often used.
    
    ### **2. The Partitioning Strategy (The Rule Book)**
    
    This is the rule that uses the shard key to assign a row to a shard. The two most common strategies are:
    
    - **Hash-based Sharding:** The database applies a hash function to the shard key value (e.g., `hash(UserID)`). The output of the hash determines which shard the data goes to. This distributes data very evenly but makes it hard to query for a range of keys (e.g., "get all users with IDs between 1000 and 2000").
    - **Range-based Sharding:** The database assigns data based on a range of the shard key. For example, Shard 1 gets UserIDs 1-1,000,000, Shard 2 gets 1,000,001-2,000,000, and so on. This is great for range queries but can create "hot spots" if one range is much more active than others.
    
    ### **3. The Routing Mechanism (The Mail Sorter)**
    
    This is the component that directs the query to the correct shard. It's not a single thing but can be implemented in a couple of ways:
    
    - **A Router/Proxy:** Your application sends its query to a lightweight proxy server (in MongoDB, this is called `mongos`). This router holds a map of which shard key ranges live on which shard. It inspects your query's `WHERE` clause for the shard key, determines the correct destination, and forwards the query to **only that shard**.
    - **A Smart Client:** In some systems, the database driver your application uses is "shard-aware." It periodically caches the shard map and can calculate where to send the query itself, sending it directly to the correct shard without needing a proxy.
    
    So, the full process is:
    
    1. Your application issues a query like `SELECT * FROM Users WHERE UserID = 54321;`.
    2. The router or smart client sees the shard key (`UserID`) and its value (`54321`).
    3. It applies the partitioning strategy (e.g., hashing `54321`) to determine the data lives on, say, **Shard 3**.
    4. The query is sent **only** to Shard 3, which finds the data and returns it. This avoids searching every shard and is why sharding is so efficient.

---

## **Database Usage Patterns**

### **Topic: Database User Categories & Roles**

**Keywords / Concepts**

- **Data Engineers (DEs) & Database Administrators (DBAs):**
    - **Role:** Administration & Foundation.
    - **Focus:** Create/manage DB objects, access control, performance tuning.
- **Data Scientists (DS) & Business Analysts (BAs):**
    - **Role:** Analysis & Insight.
    - **Focus:** Reading data to find patterns, make predictions, and build reports.
- **Application Developers (Devs):**
    - **Role:** Application Building.
    - **Focus:** Create applications that read from and write to the database. They rarely access the DB directly.

---

### **Topic: Tools & Interfaces by User Type**

**Keywords / Concepts**

- **For DEs/DBAs:**
    - **GUIs:** Graphical tools for management (e.g., Oracle SQL Developer).
    - **CLIs:** Command-Line Interfaces for direct commands (`db2 create db`) or interactive shells (`sqlplus`).
    - **Admin APIs:** For programmatic/automated administrative tasks.
- **For DS/BAs:**
    - **DS/ML Tools:** Jupyter, R Studio, Zeppelin.
    - **BI/Reporting Tools:** Power BI, Tableau, Excel.
    - **Connection:** These tools connect via SQL interfaces, but often **abstract away** the SQL from the user.
- **For App Devs:**
    - **Languages:** Python, Java, C#, JavaScript, etc.
    - **Low-Level APIs:** JDBC, ODBC (the "traditional" way).
    - **ORM Frameworks:** Object-Relational Mapping (the "modern" way). Hides SQL complexity.
        - **Examples:** Hibernate (Java), Django (Python), ActiveRecord (Ruby), Sequelize (JavaScript).

**Diagrams**

- **User Access Patterns**
    
    ```python
    +-----------------+      +-----------------------+      +---------------+
    |   DEs / DBAs    |      |      DS / BAs         |      |    App Devs   |
    +-----------------+      +-----------------------+      +---------------+
            |                        |                            |
            V                        V                            V
    +-----------------+      +-----------------------+      +---------------+
    | GUIs, CLIs,     |      | BI Tools (Tableau),   |      | ORM Frameworks|
    | Admin APIs      |      | DS Tools (Jupyter)    |      | (Django, etc.)|
    +-----------------+      +-----------------------+      +---------------+
            |                        |                            |
            '-----------.------------'----------------------------'
                        V
                +----------------+
                |    DATABASE    |
                +----------------+
    ```
    

---

### **Questions**

- **What are JDBC, ODBC, and ORM?**
    
    JDBC, ODBC, and ORM are all tools and techniques that help applications communicate with databases, but they operate at different levels of abstraction.
    
    - **ODBC** is a universal translator for any language.1
    - **JDBC** is a specialized translator just for Java.2
    - **ORM** is like a personal assistant that handles all the translation for you automatically.3
    
    ---
    
    ### ## ODBC (Open Database Connectivity) 🔌
    
    **What it is:** ODBC is a universal **standard API** for accessing databases.4 Think of it as a "universal adapter plug." Its goal is to allow any application to talk to any database, regardless of the programming language or the database system, as long as you have the correct driver.5
    
    **How it works:** An application written in a language like C++, Python, or PHP makes a generic ODBC call.6 The ODBC Driver Manager on the operating system then routes that call to a specific driver made for the target database (e.g., a PostgreSQL ODBC driver).7
    
    - **Analogy:** You're an English speaker who wants to talk to people who speak Japanese, German, and Swahili. You hire a **universal translator (ODBC)** who knows how to connect with specialized local translators (the drivers) for each language (database).8
    
    ---
    
    ### ## JDBC (Java Database Connectivity) ☕
    
    **What it is:** JDBC is the standard API specifically for **Java applications** to connect to databases.9 While Java can use a "bridge" to talk to ODBC, JDBC is the native, more direct, and generally more efficient way for Java code to do it.
    
    **How it works:** A Java application uses the JDBC API to load a specific JDBC driver for its target database (e.g., a MySQL JDBC driver).10 The connection is then more direct than the ODBC multi-step process.
    
    - **Analogy:** You're a Java speaker. Instead of hiring a universal translator, you hire a **specialist firm (JDBC)** that provides native-speaking translators for Japanese, German, and Swahili. The communication is more direct and fluent because it's tailored to your native language (Java).
    
    ---
    
    ### ## ORM (Object-Relational Mapping) 🤖
    
    **What it is:** ORM is not a driver or a direct connection API; it's a **programming technique** implemented by frameworks that creates a high-level abstraction layer.11 It automatically "maps" the data from a relational database table into an object in your programming language (like a `User` class in Python or Java).12
    
    **How it works:** Instead of writing SQL queries, the developer interacts with objects in their native language.13 The ORM framework then generates the necessary SQL in the background and executes it using JDBC or ODBC.14
    
    - **You write:** `user.name = "Alice"; user.save();`
    - **The ORM generates and runs:** `UPDATE users SET name = 'Alice' WHERE id = 123;`
    - **Analogy:** You don't want to bother learning Japanese, German, or Swahili at all. You hire a **personal assistant (the ORM)**. You just tell the assistant in English, "Save this contact information." The assistant figures out which language to speak (SQL dialect), writes the message perfectly, and handles the entire conversation for you.
    
    Popular ORM frameworks include **Hibernate** (Java), **Django's ORM** (Python), and **ActiveRecord** (Ruby on Rails).
    
    ---
    
    ### ## Comparison Table
    
    |Feature|ODBC|JDBC|ORM|
    |---|---|---|---|
    |**What it is**|A universal API standard|A Java-specific API standard|A programming technique/framework|
    |**Primary Language**|Language-independent|**Java**|Language-dependent (e.g., Python, Java)|
    |**Level of Abstraction**|Low-level (you write SQL)|Low-level (you write SQL)|**High-level** (you manipulate objects)|
    |**Analogy**|Universal Translator|Java-Native Translator|Personal Assistant|
    

---

## **Introduction to Relational Database Offerings**

### **Topic: History of Relational Databases (RDBMS)**

**Keywords / Concepts**

- A brief timeline of key developments in relational database history.

**Diagrams**

- **RDBMS Timeline**
    
    ```python
    1960s: IBM Sabre -> First recognizable relational system.
      |
    1970s: Codd's 12 Rules, Chen's ER Model -> The theoretical foundation.
      |
    1980s: IBM DB2, SQL Standard -> Commercialization and standardization.
      |
    1990s: Client-server tools (Oracle Dev, Access) -> Widespread adoption.
      |
    2000s: MySQL, PostgreSQL -> The rise of open source.
      |
    2010s: Amazon RDS, Azure SQL -> The rise of the cloud.
    ```
    

---

### **Topic: Commercial vs. Open-Source Databases**

**Keywords / Concepts**

- **Commercial DBs:** 💰
    - **Model:** Licensed, proprietary software.
    - **Why use?** Perceived reliability, comprehensive features, and dedicated support.
    - **Examples:** Oracle, Microsoft SQL Server, IBM DB2.1
- **Open-Source DBs:** 🌐
    - **Model:** Free and publicly available source code.
    - **Principles:** Users can view, modify, and distribute the code. Fosters collaboration.
    - **Examples:** MySQL, PostgreSQL, SQLite.2
- **Popularity Trend (DB-Engines):**
    - Open-source popularity is overtaking commercial.
    - 2013: Open source accounted for 35.5% of popularity.
    - 2023: Open source grew to 55.3%.

---

### **Topic: Cloud Databases**

**Keywords / Concepts**

- **What:** A database service built and accessed through a cloud platform (DBaaS).
- **Trend:** Popularity has more than doubled in the past decade.
- **Prediction:** 80% of all databases will be deployed on or migrated to a cloud platform by 2025.
- **Why the Growth?**
    - Driven by the Software as a Service (SaaS) model.
    - Provides enhanced scalability for large data volumes.
    - Offers built-in data backup and disaster recovery solutions.
- **Examples:** Amazon DynamoDB, Azure Cosmos DB, Google BigQuery.

---

### **Questions**

- The video's "Top 10 Relational Databases" list from DB-Engines includes NoSQL databases like MongoDB, Redis, and Elasticsearch. Why are they included in a relational list? Does this suggest the overall database market popularity is more relevant than strict categorization?
- With the prediction that 80% of databases will be in the cloud by 2025, what are the primary reasons a company might choose to keep its database on-premises instead of migrating?

---

## **Db2**

### **Topic: What is Db2?**

**Keywords / Concepts**

- **IBM Db2:** Relational Database Management System (RDBMS) since 1983.
- **History:** Started on IBM mainframes, evolved to a single cross-platform codebase (Linux, Unix, Windows).
- **Today:** A full suite of data management products for on-premises and cloud.
- **Key Features:**
    - **AI-Powered:** Uses machine learning for query optimization.
    - **Column Store:** Improves analytics performance by querying specific columns instead of entire tables.
    - **Data Skipping:** Automatically avoids processing data not needed for a query.
    - **Common SQL Engine:** Write a query once, and it will work across the Db2 family.
    - **Replication (HADR):** The core of its High Availability and Disaster Recovery solution.

---

### **Topic: The Db2 Product Family**

**Keywords / Concepts**

- **Db2 Database:** The core on-premises RDBMS, optimized for transactional workloads (OLTP).
- **Db2 Warehouse:** An on-premises data warehouse built for analytics, using Massively Parallel Processing (MPP).
- **Db2 on Cloud:** A fully managed cloud version of Db2 Database.
- **Db2 Warehouse on Cloud:** A fully managed, elastic cloud version of Db2 Warehouse.
- **Db2 Big SQL:** An SQL-on-Hadoop engine for querying diverse data sources (HDFS, NoSQL, etc.).
- **Db2 for z/OS:** The flagship database for IBM Z mainframes.
- **IBM Cloud Pak for Data:** An integrated data & AI platform that runs on containers (Red Hat OpenShift) and can connect to any data source, including the full Db2 family.

---

### **Topic: High Availability & Scalability**

**Keywords / Concepts**

- **HADR (High Availability Disaster Recovery):**
    - Replicates changes from a **primary** database to multiple **standby** servers.
    - If the primary fails, a standby is automatically promoted to become the new primary, and clients are redirected.
- **Db2 Warehouse Scalability (Partitioning):**
    - Data is split across partitions on different data nodes.
    - **Scale Up:** Add a node, and the system automatically rebalances the data and workloads.
    - **Scale Down:** Remove a node to reduce capacity and cost.

**Diagrams**

- **HADR Failover Flow**
    
    ```python
    // Normal Operation
    Client ---> [Primary DB] --(replicates changes)--> [Standby DB 1]
                                                   +--> [Standby DB 2]
    
    // After Failure of Primary
    Client ---> [New Primary (was Standby 1)] --(replicates)--> [Standby DB 2]
    ```
    

---

### **Questions**

- The video mentions Db2 Warehouse uses "database partitioning" for scaling, while the previous video talked about "sharding." These concepts sound functionally identical (splitting data across servers for parallel processing). Is "partitioning" just IBM's terminology for sharding, or is there a technical difference?
- How does the "Common SQL Engine" handle differences in data sources for a product like Db2 Big SQL, which can query NoSQL and object stores? Does it translate the standard SQL into the native query language for those sources?

---

## MySQL

### **Topic: What is MySQL?**

**Keywords / Concepts**

- **MySQL:** An object-relational database management system (ORDBMS).
- **Known for:** Reliability, scalability, and ease of use.
- **History:** Created by MySQL AB -> acquired by Sun Microsystems -> acquired by **Oracle**. Its popularity surged with the **LAMP stack** (Linux, Apache, MySQL, PHP).
- **Licensing:** Dual license model.
    - **GNU GPL:** The open-source version. This has led to popular forks like **MariaDB**.
    - **Commercial:** For embedding MySQL in proprietary applications.
- **Data Support:** Primarily relational, but also supports **JSON**.

---

### **Topic: Storage Engines**

**Keywords / Concepts**

- **Storage Engine:** The underlying component that handles the data operations (read, write, store) for a table. Different engines offer different features.
    - **InnoDB:**
        - **Default** engine. A good all-rounder.
        - **Features:** Transactions (ACID compliance), **row-level locking** (good for multi-user read/write), foreign key constraints.
    - **MyISAM:**
        - **Best for:** Read-heavy workloads with few updates (e.g., data warehousing).
        - **Limitation:** Uses **table-level locking**, which can be slow for mixed read/write workloads.
    - **NDB (Network DataBase):**
        - **Purpose-built for:** **MySQL Cluster**.
        - **Focus:** High availability and redundancy.

---

### **Topic: High Availability (HA) & Clustering**

**Keywords / Concepts**

- **Replication:**
    - Copying data from a source database to one or more replicas.
    - **Benefits:** Spreads read load for **scalability** and allows for failover for **availability**.
- **Clustering Option 1: InnoDB Group Replication**
    - **Setup:** One primary (read-write) server and multiple secondary servers.
    - **Coordination:** `MySQL Router` load balances client connections and handles failover by redirecting traffic to an available server.
- **Clustering Option 2: MySQL Cluster Edition**
    - **Setup:** Uses the **NDB** engine. Separates compute from storage.
    - **Components:** Multiple `MySQL Server Nodes` (for processing queries) access a set of shared `Data Nodes` (which store data, often in memory).
    - **Benefit:** Highly available and scalable architecture.

**Diagrams**

- **InnoDB Group Replication**
    
    ```python
    +-----------------+
    |  Client App     |
    +-----------------+
            |
            V
    +-----------------+
    |  MySQL Router   |--+-- (Redirects traffic)
    +-----------------+  |
      |       |        |
      V       V        V
    +-------+ +-------+ +-------+
    | Primary | | Secondary | | Secondary |
    | (R/W)   | |  (R)    | |  (R)    |
    +-------+ +-------+ +-------+
    (InnoDB Nodes with Group Replication)
    ```
    
- **MySQL Cluster (NDB)**
    
    ```python
    +-----------------+      +-----------------+
    |  Client App     |      |  Client App     |
    +-----------------+      +-----------------+
            |                      |
            V                      V
    +-----------------+      +-----------------+
    | MySQL Server Node |      | MySQL Server Node |
    |   (Compute)     |      |   (Compute)     |
    +-----------------+      +-----------------+
            |                      |
            '---------. V .--------'
                      |
    +-------------+   +-------------+
    | Data Node 1 |<->| Data Node 2 |
    |  (Storage)  |   |  (Storage)  |
    +-------------+   +-------------+
    (NDB Storage Engine)
    ```
    

---

### **Questions**

- What is the practical difference between standard **Replication** and **InnoDB Group Replication**? Does Group Replication offer more advanced features like automatic primary election or multi-primary capabilities that simple replication lacks?
- The video mentions MySQL Cluster (NDB) data nodes are "usually stored in memory." Does this make it an in-memory database by default? How does it ensure data durability if a data node reboots or fails?

---

## **PostgreSQL**

---

### **Topic: What is PostgreSQL?**

**Keywords / Concepts**

- **PostgreSQL (Postgres):** A free, open-source, **object-relational** database management system (ORDBMS).
- **History:** Evolved from the POSTGRES project at the University of California, Berkeley.
- **Key Differentiator (Object-Relational):** Supports object-oriented concepts like **inheritance** and **overloading**, allowing for database object reuse and simpler designs.
- **Ecosystem:**
    - Part of the **LAPP** stack (Linux, Apache, PostgreSQL, PHP).
    - Highly **extensible**, with popular add-ons like **PostGIS** for geographic and spatial data.
- **Data Support:**
    - Standard RDBMS features (keys, transactions, views).
    - **NoSQL-like features:** Supports **JSON** and **HSTORE** (a key-value data type).

---

### **Topic: High Availability & Scalability**

**Keywords / Concepts**

- **Partitioning:** Splitting one large table into multiple smaller sections to improve query performance.
- **Sharding:** Storing horizontal partitions across multiple remote servers to distribute the data load.
- **Replication (Built-in):**
    - **Synchronous (2-node):** A change must be written to both the primary and the replica before the transaction is confirmed. Guarantees zero data loss on failover.
    - **Asynchronous (Multi-node):** A primary node sends changes to multiple read-only replicas but doesn't wait for confirmation. This is faster and scales read workloads effectively.
- **Replication (Commercial Add-ons):**
    - **Multi-Master:** Tools like EDB PostgreSQL Replication Server allow multiple read/write databases to replicate changes with each other, providing high availability for write-intensive applications.

**Diagrams**

- **Synchronous Replication (2-Node)**
    
    ```python
    Client ----------------> [ Primary (R/W) ]
        ^                      |
        | (Waits for ACK)      V (Commit must succeed here first)
        '-------------------- [ Replica (R) ]
    ```
    
- **Asynchronous Replication (Multi-Node)**
    
    ```python
    Client ---> [ Master (R/W) ] --+--> [ Read Replica 1 ]
                (Commits immediately) |--> [ Read Replica 2 ]
                                    +--> [ Read Replica N ]
    ```
    
- **Multi-Master Replication (Commercial)**
    
    ```python
    Client A --> [ Master 1 (R/W) ] <----> [ Master 2 (R/W) ] <-- Client B
                       ^                       ^
                      |         (Replicate all changes)         |
                      '-----------------------'
    ```
    

---

### **Questions**

- The video defines "partitioning" as splitting a table and "sharding" as storing those splits on different servers. In many other database systems, these terms are used interchangeably. Is this a strict definition unique to Postgres, or just a way of explaining the process in two distinct steps?
- For the commercial **multi-master** replication, how are write conflicts handled? If two users update the same record on two different master nodes simultaneously, what is the conflict resolution strategy?

---

## Advanced Relational Model Concepts

### **Topic: Core Concepts**

**Keywords / Concepts**

- **Functional Dependency (FD):** ➡️
    - A **one-to-one** relationship between attributes.
    - One value (determinant) uniquely finds another value (dependent).
    - **Notation:** `X -> Y`
    - **Example:** `EmployeeID -> EmployeeName` (Knowing the ID gets you exactly one name).
    - **Purpose:** Data integrity, consistency, and is the foundation of **database normalization**.
- **Multi-Valued Dependency (MVD):** ➡️➡️
    - A **one-to-many** relationship between attributes.
    - One value (determinant) finds a _set_ of possible values for another attribute, typically in separate rows.
    - **Notation:** `X ->> Y`
    - **Example:** `EmployeeID ->> ProjectID` (Knowing the ID gets you a list of all projects that employee works on).
    - **Purpose:** To properly structure and maintain integrity in many-to-many relationships.
- **Candidate Key (CK):** 🔑
    - A set of attributes that **uniquely identifies** each row in a table.
    - **Properties:**
        - **Uniqueness:** The key's value combination must be unique for every row.
        - **Minimality:** No attribute can be removed from the key without losing its uniqueness.
    - **Purpose:** Enforces data integrity (prevents duplicate rows) and improves query performance through indexing. A table can have multiple candidate keys.

---

### **Topic: Practical Scenario Analysis**

**Keywords / Concepts**

- **Table:** `(EmployeeID, ProjectID, EmployeeName, ProjectName, Department)`
- **Dependencies Found:**
    - **FD:** `EmployeeID -> EmployeeName`
    - **FD:** `ProjectID -> ProjectName`
    - **MVD:** `EmployeeID ->> ProjectID`
    - **FD:** The text implies `{EmployeeID, ProjectID} -> Department`.
- **Candidate Key Found:**
    - The combination `{EmployeeID, ProjectID}` is the candidate key because it is the minimal set of attributes that uniquely identifies each row in the example table.

**Diagrams**

- **Scenario Dependencies**
    
    ```python
          +------------+       +---------------+
          | EmployeeID |------>| EmployeeName  |
          +------------+       +---------------+
               |
               V (MVD)
          +------------+       +---------------+
          | ProjectID  |------>| ProjectName   |
          +------------+       +---------------+
               |
               V
          +------------+
          | Department |
          +------------+
    
    // Candidate Key for the table
    CK = {EmployeeID, ProjectID}
    ```
    

---

---


---



---

# Module 2
## Types of SQL Statements

### **Topic: The Two Main Categories of SQL**

**Keywords / Concepts**

- **Data Definition Language (DDL):** 🏗️
    - **Purpose:** Manages the **structure** of database objects (like tables).
    - **Analogy:** The **blueprint** of a house. Used to build, modify, or demolish the structure itself.
- **Data Manipulation Language (DML):** 🛋️
    - **Purpose:** Manages the **data** _inside_ the tables.
    - **Analogy:** The **furniture** inside the house. Used to add, view, change, or remove the contents.
    - **Acronym:** **CRUD** (Create, Read, Update, Delete).

---

### **Topic: DDL vs. DML Commands**

**Keywords / Concepts**

- **DDL Commands:**
    - `CREATE`: Builds a new table.
    - `ALTER`: Modifies a table's structure (e.g., add/remove a column).
    - `TRUNCATE`: Deletes all data from a table _very quickly_, but keeps the empty table structure.
    - `DROP`: Deletes an entire table, structure and all.
- **DML Commands:**
    - `INSERT`: Adds new rows of data (Create).
    - `SELECT`: Retrieves rows of data (Read).
    - `UPDATE`: Modifies data in existing rows (Update).
    - `DELETE`: Removes specific rows from a table (Delete).

**Diagrams**

- **DDL vs. DML Analogy**
    
    ```python
    +-------------------------------------------+
    |             DATABASE (The House)          |
    |                                           |
    |  +-------------------------------------+  |
    |  | DDL: Manages the Table's STRUCTURE  |  |
    |  | (The Blueprint: CREATE, ALTER, DROP)|  |
    |  +-------------------------------------+  |
    |  |       TABLE (The Room)              |  |
    |  |-------------------------------------|  |
    |  | DML: Manages the DATA inside        |  |
    |  | (The Furniture: INSERT, SELECT,     |  |
    |  |  UPDATE, DELETE)                    |  |
    |  | [Row 1]                             |  |
    |  | [Row 2]                             |  |
    |  +-------------------------------------+  |
    +-------------------------------------------+
    ```
    

---

### **Questions**

- The video puts `TRUNCATE` in DDL and `DELETE` in DML. Both remove data, so what's the practical difference between `TRUNCATE TABLE my_table;` and `DELETE FROM my_table;`?
	- DELETE: 
		- Deletes data row by row. The engine reads each line before removing it.
		- WHERE clause: You can filter what to delete
		- ROLLBACK: you can safely issue a rollback within a transaction
	- TRUNCATE: 
		- Removes data by deallocating the memory pages that store the table.
		- It's very fast
		- Cannot be undone.

- Are DDL and DML the only categories of SQL statements? What about commands for managing permissions (like `GRANT`) or for controlling transactions (like `COMMIT` and `ROLLBACK`)?
	- Although DDL and DML are the most frequently mentioned. SQL is traditionally divided into five sublanguages or categories to organize all of its commands: 
		- - **1. DDL (Data Definition Language):**
    
		    - Used to define or modify the database structure (tables, indexes, views).
		        
		    - _Commands:_ `CREATE`, `ALTER`, `DROP`, `TRUNCATE`.
        
		- **2. DML (Data Manipulation Language):**
		
				 Used to add, modify, or delete the data _inside_ those structures.
					
				- _Commands:_ `INSERT`, `UPDATE`, `DELETE`.
        
	- **3. DQL (Data Query Language):**
	    
	    - Used exclusively to query information. Many authors group it under DML, but formally it is its own category.
	        
	    - _Commands:_ `SELECT`.
	        
	- **4. DCL (Data Control Language):**
	    
	    - Handles security, managing who has access to what data.
	        
	    - _Commands:_ **`GRANT`** (give permissions) and **`REVOKE`** (remove permissions).
	        
	- **5. TCL (Transaction Control Language):**
	    
	    - Manages the changes made by DML commands. It ensures operations complete successfully or are reverted if there's an error, keeping the database in a consistent state.
	        
	    - _Commands:_ **`COMMIT`** (save changes permanently), **`ROLLBACK`** (undo changes of the current transaction), and **`SAVEPOINT`** (create a temporary restore point).
## Creating tables

### **Topic: Pre-Creation Checklist**

**Keywords / Concepts**

- Before writing any code, you need a plan.
- **1. Location:** Choose a **schema** to logically organize your table.
- **2. Details:** Collect the table name, all column names, and their specific **data types**.
- **3. Constraints:** Decide for each column if it can contain duplicate values or if it will allow `NULL` values.
- **4. Reference:** Use the **Entity Relationship Diagram (ERD)** from the database design phase as your guide.

---

### **Topic: Methods for Creating Tables**

**Keywords / Concepts**

- **Visual Interfaces (UIs):** 🖱️
    - **What:** Graphical tools that are user-friendly, especially for beginners or occasional tasks.
    - **Examples:** Db2 on Cloud console, phpMyAdmin (for MySQL), pgAdmin (for PostgreSQL).
- **SQL Statements:** 📜
    - **What:** Using the `CREATE TABLE` DDL statement.
    - **Benefit:** Can be saved in a script file to easily and repeatedly create multiple tables.
- **APIs (Application Programming Interfaces):** ⚙️
    - **What:** Programmatic interfaces for automated creation and management.
    - **Benefit:** Offers the most control and is best for automation tasks.

---

**Diagrams**

- **Table Creation Flow**
    
    ```python
    +-----------------+      +-----------------+      +-----------------+
    |   DESIGN (ERD)  |----->| GATHER DETAILS  |----->|  CHOOSE METHOD  |
    | (The Blueprint) |      | (Cols, Types)   |      | (UI, SQL, API)  |
    +-----------------+      +-----------------+      +-----------------+
                                                            |
                                                            V
                                                    +-----------------+
                                                    |  CREATE TABLE   |
                                                    +-----------------+
                                                            |
                                                            V
                                                    +-----------------+
                                                    | MODIFY & MANAGE |
                                                    +-----------------+
    ```
    

---

### **Questions**

- The video gives a NoSQL example (MongoDB with pymongo) for using an API to create tables. In a relational context, what would be a more common example of using an administrative API for this purpose instead of just running a `CREATE TABLE` script?

## CREATE TABLES Statement

### **Topic: The `CREATE TABLE` Statement**

**Keywords / Concepts**

- **`CREATE TABLE`:** The fundamental **DDL** (Data Definition Language) statement used to create a new table (entity) in a database.
- **Process:** The statement defines the table's name and specifies the columns (attributes) it will contain.
- **Column Definition:** Each column requires a **name**, a **data type**, and can have optional **constraints**.

---

### **Topic: Column Data Types & Constraints**

**Keywords / Concepts**

- **Data Types (Examples):**
    - **`CHAR(n)`:** A **fixed-length** character string. `CHAR(2)` will always occupy 2 characters of space, even if you only store "A".
    - **`VARCHAR(n)`:** A **variable-length** character string. `VARCHAR(24)` will occupy only the space needed for the actual text, up to a maximum of 24 characters.
- **Constraints:**
    - **`PRIMARY KEY`:** A constraint that uniquely identifies each row in a table. It automatically enforces uniqueness.
    - **`NOT NULL`:** A constraint that ensures a column cannot have an empty or `NULL` value.

**Diagrams**

- **Basic `CREATE TABLE`**
    
    ```sql
    CREATE TABLE mexican_states (
        state_id CHAR(3)       PRIMARY KEY NOT NULL,
        name     VARCHAR(40)   NOT NULL
    );
    ```
    
- **Practical Example (Author Table)**
    
    ```sql
    CREATE TABLE Author (
        Author_ID  CHAR(2)       PRIMARY KEY NOT NULL,
        Lastname   VARCHAR(15)   NOT NULL,
        Firstname  VARCHAR(15)   NOT NULL,
        Email      VARCHAR(40),
        City       VARCHAR(15),
        Country    CHAR(2)
    );
    ```
    

---

### **Questions**

- In the example, `Author_ID` is defined as `PRIMARY KEY NOT NULL`. Is the `NOT NULL` part redundant? Doesn't a column defined as a `PRIMARY KEY` already prevent `NULL` values by definition?
- The video only mentions character-based data types (`CHAR`, `VARCHAR`). What are the common data types for storing numbers (like integers or decimals) and dates?
- The `Author_ID` is a `CHAR(2)`. Does this mean the user has to manually create and assign a unique two-letter code for every new author? Can the database generate a unique ID automatically?

## **ALTER, DROP, and Truncate Tables**

---

### **Topic: The Three DDL Statements for Modification & Deletion**

**Keywords / Concepts**

- **`ALTER TABLE`:** 🔧
    - **Purpose:** Modifies the **structure** of an _existing_ table.
    - **Analogy:** Renovating a house (adding a room, changing a window, knocking down a wall).
- **`DROP TABLE`:** 💣
    - **Purpose:** Deletes an **entire table**, including its structure and all of its data.
    - **Analogy:** Demolishing the entire house.
- **`TRUNCATE TABLE`:** 🗑️
    - **Purpose:** Deletes all **data** from a table but keeps the table's empty structure.
    - **Analogy:** Completely emptying a house of all its furniture but leaving the building intact. It's faster than removing items one by one (`DELETE`).

---

### **Topic: `ALTER TABLE` Actions**

**Keywords / Concepts**

- `ALTER TABLE` is a versatile statement with different clauses for different actions.
- **`ADD COLUMN`:** Adds a new column to a table.
- **`ALTER COLUMN`:** Modifies an existing column's properties, such as its data type.
    - **Warning:** Changing a data type can fail if the existing data is not compatible with the new type (e.g., changing text "abc" to a number).
- **`DROP COLUMN`:** Removes a column from a table.

**Diagrams**

- **Common Syntax Examples**SQL
    
    ```sql
    - Add a new column
    ALTER TABLE Author ADD COLUMN telephone_number BIGINT;
    -- Modify a column's data type
    ALTER TABLE Author ALTER COLUMN telephone_number SET DATA TYPE CHAR(20);
    -- Remove a column
    ALTER TABLE Author DROP COLUMN telephone_number;
    -- Delete the entire table
    DROP TABLE Author;
    -- Empty the table of all data
    TRUNCATE TABLE Author IMMEDIATE;
    ```
    

---

### **Questions**

- The syntax shown is `TRUNCATE TABLE ... IMMEDIATE`. Is the `IMMEDIATE` keyword standard across all SQL databases, or is it specific to certain dialects like IBM Db2?
    
    - No, the `IMMEDIATE` keyword is **not standard SQL**. It's specific to certain database dialects, most notably **IBM Db2**. In most other popular database systems like **PostgreSQL**, **MySQL**, and **SQL Server**, the standard syntax is simply:
        
        ```sql
        TRUNCATE TABLE table_name;
        ```
        
- What happens if you use `ALTER COLUMN` to reduce the size of a data type (e.g., from `CHAR(20)` to `CHAR(10)`) when there is existing data longer than 10 characters? Will the statement fail, or will the data be automatically shortened (truncated)?
    
    - In most database systems, the `ALTER TABLE` statement will **fail with an error** to prevent accidental data loss.
- Since `DROP TABLE` is so destructive, do most database systems provide a safety net, like a recycle bin, to recover a dropped table, or is it permanently gone once the command is executed?
    
    - Some do, but many do not. You should **always treat `DROP TABLE` as a permanent and destructive action**.

## **Data Movement Utilities**

### **Topic: Why Move Data?**

**Keywords / Concepts**

- **Initial Population:** Filling a new database or table with its first set of data.
- **Cloning:** Creating duplicate databases for development or testing.
- **Disaster Recovery:** Creating snapshots (backups) to restore from in case of failure.
- **Data Integration:** Generating a new table or adding data to an existing table from an external file (e.g., a CSV).

---

### **Topic: Data Movement Methods**

**Keywords / Concepts**

- **Backup & Restore:** 💾
    - **Scope:** The **entire database** (all objects, data, schemas, security, etc.).
    - **Process:** `Backup` creates a full copy in a file; `Restore` recreates the database from that file.
    - **Use Case:** Primarily for **disaster recovery** and creating complete clones for dev/test environments.
- **Import & Export:** ↔️
    - **Scope:** A **single table** or the result of a query.
    - **Process:** `Import` reads a file and runs `INSERT` statements. `Export` saves table data to a file.
    - **Use Case:** Moving data for a specific table between different systems or applications.
- **Load:** 🚀
    - **Scope:** A **single table**, but designed for high performance.
    - **Process:** Bypasses SQL `INSERT` statements and writes data directly to the database pages. It may also bypass database logging.
    - **Trade-off:** To gain speed, it **does not** perform referential or table constraint checking. The data is assumed to be clean.
    - **Use Case:** Populating very large tables where performance is critical.

---

### **Topic: Common File Formats**

**Keywords / Concepts**

- **DEL (Delimited):** Uses a special character (like a comma) to separate column values. The most common example is **CSV**.
- **ASC (Non-delimited ASCII):** A flat text file where data is aligned in fixed-width columns.
- **PC/IXF:** A structured format, often specific to a database manager (like Db2), for efficient data exchange within that system.
- **JSON:** A popular format for web services and semi-structured data.

### Diagrams
#### Comparison of Data Movement Methods

| Method         | Scope           | Key Feature                                     | Best For                        |
| :------------- | :-------------- | :---------------------------------------------- | :------------------------------ |
| Backup/Restore | Entire Database | Creates an exact, complete copy.                | Disaster Recovery, Full Clones. |
| Import/Export  | Single Table    | Flexible, runs SQL INSERTs, checks constraints. | General-purpose data exchange.  |
| Load           | Single Table    | Extremely fast, bypasses SQL and constraints.   | Populating huge tables quickly. |

---

### **Questions**

#### 1. What happens when the Load utility encounters "dirty" data?

It neither completely fails nor leaves the database silently inconsistent. Instead, it uses a very clever middle-ground approach: **it loads the data but puts the table into a "quarantine" state.**

Because the `LOAD` utility's primary goal is raw speed, it completely ignores constraints (like Foreign Keys or Check constraints) while writing the data to disk. If dirty data is loaded:

- **The load succeeds:** The operation finishes, and the data is physically in the table.
    
- **The table is locked (Check Pending):** The database engine knows constraints were bypassed. To prevent users from querying inconsistent data, it immediately flags the table and puts it into a state often called **"Check Pending"** (or similar, depending on the specific database engine).
    
- **The resolution:** In this state, the table is usually locked for normal reading and writing. The administrator must manually run a secondary command (like `SET INTEGRITY` in Db2) to check the newly loaded data against the constraints. During this phase, any "dirty" rows that violate the foreign key are usually stripped out and moved to a separate "exception table," and the main table is finally unlocked for public use.
    

#### 2. Does PC/IXF being "preferred" imply it's a proprietary binary format?

**Exactly right.** Your assumption is 100% correct.

**PC/IXF** (Integration Exchange Format) is a highly structured, proprietary binary format developed by IBM, primarily used for its Db2 database system.

Here is why it differs from universal formats like CSV or JSON, and why a database engine might "prefer" it:

- **It contains metadata:** Unlike a CSV file, which only contains raw comma-separated text, a PC/IXF file contains both the actual data _and_ the structural definition of the table (the DDL). If you export a table to PC/IXF and import it onto a completely different server, the database can automatically recreate the table with the exact correct column types, lengths, and data.
    
- **It preserves exact data types:** In a CSV, a number is just text. In PC/IXF, a packed decimal or a binary object is preserved in its native machine format, meaning the database doesn't have to waste CPU cycles translating text into binary data when reading it.
    
- **The tradeoff:** As you noted, the major downside is interoperability. You cannot open a PC/IXF file in Notepad, Python, or Excel to quickly check the data. It is meant for machine-to-machine communication within the IBM ecosystem, whereas CSV and JSON are universal languages meant for sharing across different platforms.

---

## **Database Hierarchy and Schema Objects**

---

### **Topic: The RDBMS Hierarchy**

**Keywords / Concepts**

- **Instance:** The top-level logical boundary. A running copy of the database software on a server. An instance can contain multiple databases and has its own configuration and memory.
- **Isolation:** Multiple instances can exist on one physical server but remain completely isolated. In the cloud, an instance refers to a specific running copy of a service.
- **Database:** A unique entity within an instance with its own name, system catalog, and configuration files. Designed for organized data storage.
- **Relational Model:** Focuses on establishing relationships between tables to improve data integrity and reduce redundant data.

---

### **Topic: Schemas — Logical Organization**

**Keywords / Concepts**

- **Schema:** A logical grouping of database objects. Think of it as a folder within a database used to organize tables, views, and triggers.
- **Namespace / Name Qualifier:** Schemas prevent name conflicts. You can have two tables named `Sales` in different schemas (e.g., `Internal.Sales` vs. `External.Sales`).
- **Implicit vs. Explicit Assignment:**
    - **Explicit:** You specify the schema name when creating an object (`CREATE TABLE MySchema.MyTable...`).
    - **Implicit:** If you omit the schema name, the database assigns the object to your **Default Schema** (usually your username).
- **System Schema:** A specialized schema that holds the "brain" of the database (metadata, user permissions, index details, and partition information).

---

### **Topic: Common Database Objects**

**Keywords / Concepts**

- **Tables:** The basic logical structures consisting of rows and columns.
- **Constraints:** Rules enforced on data to ensure accuracy (e.g., "Employee ID must be unique").
- **Indexes:** Sets of pointers that speed up data retrieval and ensure uniqueness.
- **Views:** "Virtual" tables. They represent data from one or more tables but do not store data themselves; they are essentially saved queries.
- **Aliases:** Alternative, simpler names used to reference complex objects.
- **Partitioning:** Splitting large tables into smaller, manageable logical pieces to enhance performance in big data scenarios (Data Warehousing).
- **DDL (Data Definition Language):** The subset of SQL commands used to manage these objects, primarily `CREATE`, `ALTER`, and `DROP`.

---

### **Questions**

- **How does a View differ from a Table in terms of storage?**

    A Table stores data permanently on disk. A View is a logical representation — a "virtual" table that does not require permanent storage for its rows. It generates data dynamically by running a query on the underlying base tables.

- **The "Schema-Database Paradox": How does the hierarchy change between MySQL and PostgreSQL?**

    The video implies a strict hierarchy (Instance > Database > Schema). However, **MySQL** treats `SCHEMA` and `DATABASE` as interchangeable synonyms — creating a schema is literally creating a database. In contrast, **PostgreSQL** and **SQL Server** follow the strict hierarchy, where one database contains multiple schemas. This "flattened" hierarchy in MySQL is important for developers moving between platforms.

- **Security Boundaries: How do Senior DBAs use Schemas to implement the "Principle of Least Privilege"?**

    The most critical professional use of Schemas is **Access Control**. Permissions are granted at the **Schema level** — not at the table level (too tedious) or database level (too risky). A DBA might create a `Reporting` schema with `READ-ONLY` access for analysts, while keeping the `Core_App` schema restricted to the application's service account.

- **The "Serverless" Shift: What happens to the "Instance" in Cloud-Native architectures like BigQuery or Snowflake?**

    In **Cloud-Native/Serverless** databases, the "Instance" layer is abstracted away — the provider manages hardware and performance automatically. The modern Database Engineer focuses almost entirely on the **Schema and Object layers**, as Instance administration becomes a managed service.

- **Structural Performance: Why choose Partitioning over creating separate Tables for each month?**

    **Partitioning** allows the database to treat data as a single logical table while enabling the **Query Optimizer** to perform "Partition Pruning" — automatically ignoring data slices not needed by a query, without requiring complex `UNION` queries. This keeps the Schema clean while providing the performance of smaller datasets.
