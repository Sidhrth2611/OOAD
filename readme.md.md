# OOAD COMPLETE EXAM GUIDE - Simplest Approach

## START HERE: What is this subject about?
**Simple idea:** OOAD is about understanding a real-world problem, drawing it as classes and relationships, and then designing the software architecture to solve it.

**Main phases:**
1. **ANALYSIS** = Understanding what to build (WHAT)
2. **SYSTEM DESIGN** = Deciding how to build it (HOW)

---

# PART 1: OBJECT-ORIENTED ANALYSIS (OOA)

## Why do we do Analysis?
- Real-world problems are described in messy, vague language
- We need to convert this vague problem → **precise model**
- This model becomes the blueprint for design and implementation

## Key Concept: The Analysis Model has 3 parts
- **Class Model** = What things exist? (Classes & Relationships)
- **Interaction Model** = How do things talk to each other?
- **State Model** = How do things behave over time?

For exams: Usually Class Model is most important ✓

---

## DOMAIN MODEL = The Core of Analysis

**Domain Model = A precise picture of the real-world system**

### 9 Steps to Build a Domain Model (THIS IS IMPORTANT FOR EXAMS)

| Step | What to do | Key Point |
|------|-----------|-----------|
| 1. **Find Classes** | Look for nouns in problem description | Real-world entities only, not computer concepts |
| 2. **Prepare Data Dictionary** | Write 1-2 line definition of each class | Explains scope and boundaries |
| 3. **Find Associations** | Look for verbs/relationships between classes | Shows how classes connect |
| 4. **Find Attributes** | Add properties/data to each class | Properties of individual objects |
| 5. **Use Inheritance** | Group similar classes under parent class | Share common structure |
| 6. **Test Access Paths** | Can we navigate through the model to answer questions? | Check if model is complete |
| 7. **Iterate & Refine** | Fix problems, add missing pieces | Keep improving |
| 8. **Adjust Abstraction** | Simplify model by using more general concepts | Use patterns where possible |
| 9. **Group into Packages** | Organize classes into logical groups | Make model easier to understand |

---

## STEP 1: FIND CLASSES

### What IS a Class?
- Real-world entity (person, place, thing)
- Concept/abstraction (transaction, schedule, hierarchy)
- **NOT** computer concepts (linked list, pointer, loop)

### How to Find Classes?
1. **Look for NOUNS** in problem statement
   - Example: "Bank transfers money to Account" → Classes: **Bank, Money, Account**
2. **Don't be too picky at first** → write down all candidates
3. **Refine later** by removing bad ones

### Example: ATM System
**Problem:** "Design software for ATMs in banking network..."

**Candidate Classes found:**
- ATM, Bank, Account, Customer, CashCard, Transaction, Cashier, etc.

### Rules for KEEPING Good Classes (Filter Out Bad Ones)

#### 🚫 REMOVE IF:

1. **Redundant** - Two classes say the same thing
   - Keep the more descriptive name
   - Example: Customer vs User (in ATM) → Keep "Customer"

2. **Irrelevant** - Has nothing to do with problem
   - Example: "Apportioning Cost" in ATM software? NO
   - But "Transaction" in billing system? YES

3. **Vague** - Unclear or too broad
   - Example: "RecordkeepingProvision" → Too vague, handled by "Transaction"

4. **Actually an Attribute** - Describes a single object's property
   - Example: "Cash" should be attribute of Transaction, not class
   - But if independent importance exists → keep as class

5. **Actually an Operation/Action** - Not something we store/manipulate
   - Example: "PrintReceipt" is operation, not class
   - But "Receipt" (if stored/used) = class

6. **A Role, Not a Concept** - Name reflects role played, not intrinsic nature
   - Example: "Owner" is poor name for class in car factory → Use "Person" instead
   - Person can have roles: owner, driver, lessee

7. **Implementation Construct** - Computer-specific, not real-world
   - ❌ CPU, LinkedList, Array, Pointer, Thread
   - ✓ File, Database (these are real-world concepts too)

8. **Derived** - Can be calculated from other classes
   - Skip derived classes (or mark with "/" prefix if important)

---

## STEP 2: PREPARE DATA DICTIONARY

### What is it?
Dictionary that precisely defines each class with 2-3 sentences

### Example (ATM):
```
Account: A single account at a bank. Transactions can be applied against it. 
Customer can hold multiple accounts (checking, savings, etc.)

CashCard: Card assigned to customer authorizing ATM access. Contains bank code 
and card number. One customer, but multiple physical copies for security.

Transaction: Single request for operations on a customer's account. Can include 
withdrawal, deposit, or query.
```

### Why important?
- Removes ambiguity
- Makes scope clear
- Helps identify if class is really needed

---

## STEP 3: FIND ASSOCIATIONS

### What IS an Association?
**Relationship/Connection between two classes**

Example: **Student enrolls-in Course** (Student ←→ Course)

### How to Find?
1. **Look for VERBS/VERB PHRASES** in problem
   - "Bank HOLDS Account" → Association
   - "ATM COMMUNICATES with CentralComputer" → Association

2. **Common association types:**
   - Physical location: NextTo, PartOf, ContainedIn
   - Action: Drives, Manages, WorksFor
   - Communication: TalksTo, Communicates
   - Ownership: Owns, Has

### ATM Example Associations:
- Bank **holds** Account
- Customer **has** CashCard
- CashCard **accesses** Account
- ATM **communicates with** CentralComputer
- Transaction **entered on** ATM
- Bank **is part of** Consortium

### Rules for KEEPING Good Associations (Filter Out Bad Ones)

#### 🚫 REMOVE IF:

1. **Between eliminated classes** - One class doesn't exist anymore
   - If you removed class X, remove associations with X

2. **Irrelevant or Implementation** - Outside problem domain
   - ❌ "System handles concurrent access" = implementation concept
   - ✓ "Bank holds Account" = real-world relationship

3. **Actually an Action/Event** - Transient, not permanent
   - ❌ "ATM accepts card" = temporary event during transaction
   - ✓ "Customer owns CashCard" = permanent relationship

4. **Ternary (3-way) Association** - Usually break into binary (2-way)
   - Example: "Professor teaches Course in Room"
   - Better: "Professor teaches Course" + "Course held in Room"

5. **Derived** - Can be calculated from other associations
   - Example: "Grandchild of" = derived from two "Parent of" associations
   - Mark with "/" if important: "/GrandchildOf"

### Multiplicity (How many? One or Many?)

**Notation:**
- **1** = exactly one
- **0..1** = zero or one (optional)
- **\*** or **0..*** = zero or more (many)
- **1..*** = one or more

**Example:**
- One Bank **holds** Many Accounts (1 → *)
- One Customer **owns** Zero-or-One CashCard (1 → 0..1)

**Important:** Multiplicity often changes during analysis, so don't worry too much!

---

## STEP 4: FIND ATTRIBUTES

### What IS an Attribute?
**Data property of individual object** (not relationship to another object)

Examples: name, birthdate, color, size, balance

### How to Find?
1. **Look for NOUNS + POSSESSIVE** (the ___ of the ___)
   - "the balance of the account" → Attribute: balance
   - "the color of the car" → Attribute: color

2. **Look for ADJECTIVES** (specific values)
   - red, blue, on, off, active, expired

3. **Use domain knowledge** - Not all in problem statement
   - For Bank: "Account has balance" = obvious

### Rules for KEEPING Good Attributes (Filter Out Bad Ones)

#### 🚫 REMOVE IF:

1. **Should be a Class** - Independent existence is important
   - ❌ "boss" as attribute of Employee → Should be separate Person class
   - ✓ "salary" as attribute of Employee

2. **Should be a Qualifier** - Value depends on context
   - ❌ "employeeNumber" for person with 2 jobs → Context-dependent
   - Better: Use qualified association "Company employs Person" with qualifier "employeeNumber"

3. **Should be a Qualifier** - Name selecting from set
   - ❌ "departmentName" attribute → Better as qualifier
   - Why: Department name is context-dependent (unique within company, not globally)

4. **Is just an Identifier** - Only purpose is to identify object
   - ❌ "transactionID" (internal implementation)
   - ✓ "accountCode" (customers see this in real world)

5. **Is on Association, Not Class** - Property of relationship
   - Example: "membershipDate" belongs to "Person-Club" association (many-to-many)
   - Because person can join multiple clubs on different dates

6. **Internal/Hidden** - Invisible from outside object
   - ❌ Whether database is up/down = internal state
   - ✓ Account balance = external property

7. **Too Minor** - Doesn't affect operations
   - Skip fine details, get important ones first

8. **Discordant** - Completely different from other attributes
   - Example: Attributes {name, balance, color} don't fit together
   - Problem: Class mixes unrelated concepts → Split into 2 classes

9. **Boolean** - Reconsider as enumeration
   - ❌ isActive (true/false)
   - ✓ status (Active, Inactive, Suspended)

### Attributes on Associations

**Attribute can belong to relationship, not just objects**

Example:
```
Person ←→ Club

Attribute on Association: membershipDate
Why? Because:
- Same person joins different clubs on different dates
- Attribute depends on WHICH person joined WHICH club
```

---

## STEP 5: USE INHERITANCE (Generalization & Specialization)

### What IS Inheritance?
**Parent-Child relationship** - Child inherits attributes/methods from Parent

### Two Directions:

#### Bottom-Up (Generalization)
Look for **similar classes** → Create parent class

**Example:**
```
Before:          After:
CheckingAccount  Account (parent)
SavingsAccount   /
                 CheckingAccount (child)
                 SavingsAccount (child)
```

**How to find:** Look for classes with common attributes/relationships

#### Top-Down (Specialization)
Start with general class → Find **specific types**

**Example:**
```
Before:      After:
Car          Car (parent)
/            /
             SedanCar
             SUVCar
             SportsCar
```

**How to find:** Look for adjectives on class names (pop-up menu, slide-out menu, etc.)

### Rules for Good Inheritance

1. **Don't force it** - If doesn't fit naturally, it's wrong generalization
2. **Use real-world taxonomy** - Prefer real-world categories
3. **Avoid excessive detail** - Don't create subclass for every variant
4. **Avoid multiple inheritance unless necessary** - Too complex

### Mark Derived Classes
When showing inheritance, mark derived specializations with "/" prefix:

```
Person
/Manager (derived - actually just Person with special attribute)
```

---

## STEP 6: TEST ACCESS PATHS

### What Does This Mean?
**Can we navigate through the model to answer likely questions?**

### Example Questions (ATM):
- Q: "Given a cash card, find all accounts it can access?"
- Q: "Given a customer, find all their accounts?"
- Q: "Given a transaction, find which bank approved it?"

For each question, can we draw a path through associations to get answer?

### What This Checks:
- ✓ Missing associations
- ✓ Missing classes
- ✓ Wrong multiplicity values

---

## STEP 7: ITERATE & REFINE

### It's NEVER right first time!
Keep improving the model by:

1. **Look for missing classes** - Signs:
   - Asymmetry (class A connects many ways, but class B connects only one way)
   - Mixed attributes (class mixing unrelated properties)
   - Difficulty fitting into inheritance

2. **Look for redundant elements** - Remove:
   - Duplicate associations (same relationship twice)
   - Derived associations (can be calculated)
   - Unnecessary subclasses

3. **Split confusing classes** - If class has "split personality":
   - Example: CashCard = both "authorization" AND "physical card"
   - Solution: Split into CardAuthorization + CashCard

---

## STEP 8: SHIFT ABSTRACTION LEVEL

### Idea: Use More General Concepts (Patterns)

**Example Problem:**
```
IndividualContributor
Supervisor
Manager

All have: phone, address, etc.
Only difference: who they report to
```

**Bad Model:** 3 separate classes + shared superclass = BLOATED

**Good Model:** Single Person class + association "manager" (self-referential)
```
Person
 └─ has boss: Person (optional)
 └─ employeeType: {Individual, Supervisor, Manager}
```

**Why better:**
- Simpler model
- If new level added (VP Manager), model doesn't change - just add data
- Reusable pattern for any hierarchy

### Use Patterns
**Pattern = proven solution to common problem**

Examples:
- Management hierarchy (boss-worker relationship)
- Guardian object (for resource control)
- Transaction handling

When you recognize a pattern → Use it immediately!

---

## STEP 9: GROUP INTO PACKAGES

### What IS a Package?
**Group of related classes** for organization

### Why?
- Makes large models easier to view
- Shows semantic grouping (classes in same package more related)
- Reduces visual clutter

### How to Group?
1. **Find cut points** - Classes connecting otherwise separate groups
   - These become bridges between packages

2. **Common theme** - Classes doing similar things

### ATM Example:
```
PACKAGES:
- Tellers: Cashier, CashierStation, ATM, EntryStation
- Accounts: Account, Transaction, CashCard, CardAuthorization, Customer
- Banks: Bank, Consortium
```

---

# PART 2: SYSTEM DESIGN

## What is System Design?
**Planning HOW to build the system** (high-level architecture)

### 11 Key Decisions in System Design:

| Decision | What? | Why? |
|----------|-------|------|
| 1. **Performance Estimate** | Can system be built in time/budget? | Check feasibility |
| 2. **Reuse Plan** | Use existing code/patterns/frameworks? | Save time/money |
| 3. **Subsystems** | Divide system into major pieces | Manage complexity |
| 4. **Concurrency** | What runs in parallel? | Better performance |
| 5. **Hardware Allocation** | Which code on which computer? | Physical distribution |
| 6. **Data Storage** | Use files or database? | Access & reliability |
| 7. **Global Resources** | Control shared resources | Prevent conflicts |
| 8. **Control Strategy** | Procedure-driven or event-driven? | Program organization |
| 9. **Boundary Conditions** | Handle start/stop/failures | Robustness |
| 10. **Trade-offs** | Speed vs Memory? Quality vs Cost? | Set priorities |
| 11. **Architectural Style** | Layers vs Partitions vs Hybrid? | System structure |

---

## 1. PERFORMANCE ESTIMATE ("Back of Envelope" Calculation)

### Idea: Quick rough estimate to check feasibility

### Process:
1. **Estimate transaction volume** (per second/minute/hour)
2. **Estimate time per transaction** (CPU time)
3. **Multiply** to get CPU load
4. **Check if reasonable** with available hardware

### ATM Example:
```
40 bank branches
+ ~40 supermarket ATMs (same number outside banks)
= 80 total ATMs

Half busy at peak times = 40 ATMs busy
Each transaction ~1 minute
→ ~40 transactions/minute = ~1 transaction/second

Conclusion: Modern CPU easily handles 1 transaction/second
(Not a performance bottleneck!)
```

### Key: Don't need precision, just "ballpark" estimate!

---

## 2. REUSE PLAN

### Types of Reuse:

#### 2.1 Libraries
**Collection of classes** for common tasks

Example: String library, Math library, Container library

**Challenges when combining multiple libraries:**
- Argument validation (collective vs individual?)
- Error handling (return codes vs exceptions?)
- Control paradigms (event-driven vs procedure-driven?)
- Memory management (garbage collection strategies differ)
- Name collisions (classes with same name?)

**Solution:** Often must wrap/adapt libraries to work together

#### 2.2 Frameworks
**Skeletal program** that you complete for your specific problem

Example: Web framework (Flask, Django), GUI framework (Qt)

**How it works:**
- Framework provides structure + flow of control
- You fill in specific behavior for your app
- Often includes class libraries too

#### 2.3 Patterns
**Proven solution to general problem**

Examples:
- Model-View-Controller (MVC)
- Observer pattern
- Singleton pattern
- Management hierarchy pattern

**Benefit:** No need to reinvent - just apply proven pattern

---

## 3. BREAKING INTO SUBSYSTEMS

### What IS a Subsystem?
**Major chunk of system** (group of classes with common theme)

Examples:
- File system (operating system)
- Renderer subsystem (graphics system)
- Physics subsystem (game engine)

### Subsystem Interface
- **Defines** what subsystem does
- **Hides** internal implementation
- **Other subsystems** talk through interface only

### Two Types of Relationships:

#### 3.1 Client-Server
```
Client calls Server
→ Server does work
→ Server returns result
→ Control back to Client
```
**Advantage:** Simple, one-way communication
**Use:** Whenever possible

#### 3.2 Peer-to-Peer
```
Subsystem A calls Subsystem B
Subsystem B calls back Subsystem A
(Two-way calls)
```
**Disadvantage:** Complex, can have cycles, hard to understand
**Avoid:** If possible use Client-Server instead

### System Size
- Most systems have **3-7 top-level subsystems** (not 20+!)
- Each subsystem can be divided into smaller subsystems

---

## 3.1 LAYERS (Horizontal Architecture)

### Idea: Stack of layers, each built on previous

### Example:
```
┌─────────────────────┐
│   Application UI    │ ← Top: What users see
├─────────────────────┤
│  Graphics Engine    │
├─────────────────────┤
│  Operating System   │
├─────────────────────┤
│  Hardware           │ ← Bottom: Physical resources
└─────────────────────┘
```

### Rules for Layers:
- **One-way knowledge** - Top knows about bottom, bottom doesn't know about top
- **Client-server flow** - Upper layer uses lower layer services
- **Each layer** has its own classes/operations

### Closed vs Open Architecture:

#### Closed Layers
```
Layer N only uses Layer N-1
(Most information hiding)
```
✓ **Good:** Easy to modify, change only affects one layer above
✗ **Bad:** Inefficient (must call through each layer)

#### Open Layers
```
Layer N can use any lower layer
(Less information hiding)
```
✓ **Good:** More efficient
✗ **Bad:** Changes affect multiple layers

---

## 3.2 PARTITIONS (Vertical Architecture)

### Idea: Divide system into independent pieces (like departments)

### Example:
```
COMPILER SYSTEM:
┌──────────┬─────────┬──────────┬─────────┐
│ Lexical  │ Syntax  │ Semantic │ Code    │
│ Analysis │ Analysis│ Analysis │ Gen     │
└──────────┴─────────┴──────────┴─────────┘
```

### Characteristics:
- **Peer relationships** (not strict hierarchy)
- **Similar abstraction level** (unlike layers)
- **Data flows** through partitions

### Difference from Layers:
- **Layers** = levels of abstraction (high-level → low-level)
- **Partitions** = independent services (all same level)

---

## 3.3 COMBINING LAYERS + PARTITIONS

### Real systems often mix both:

**Example: Graphics Application**
```
┌─────────────────────────────────────┐
│  Application UI                     │ LAYER
├───────┬──────────┬──────────────────┤
│ Input │ Render   │ Physics Engine   │ PARTITIONS
│ Mgmt  │          │                  │
├───────┴──────────┴──────────────────┤
│  Operating System                   │ LAYER
├─────────────────────────────────────┤
│  Hardware                           │ LAYER
└─────────────────────────────────────┘
```

### ATM Example Architecture:
```
        ATM Stations (3+ instances)
                  ↓
    ┌─────────────────────────┐
    │  Consortium Computer    │ (router/hub)
    │  (Central routing)      │
    └─────────────────────────┘
         ↓       ↓       ↓
    Bank A   Bank B   Bank C
    Computers Computers Computers

TOPOLOGY: Star (all go through center)
```

---

## 4. IDENTIFYING INHERENT CONCURRENCY

### What is Concurrency?
**Multiple things happening at same time** (independently)

### How to Find?
Look at state diagrams:
- **Two objects concurrent?** If they receive events at same time without interacting
- Example: Airplane engine + wing controls run in parallel

### Thread of Control
**Path of execution through state diagrams**

- One "thread" = one sequential execution path
- Multiple threads = concurrent execution

### ATM Example:
```
While Bank is verifying account →  ATM is idle (waiting)
While ATM shows menu →  Bank is idle (waiting)

Can these happen simultaneously? 
YES, if one ATM machine = one CPU + separate bank computer = another CPU

Can they happen simultaneously if single CPU?
YES, via task switching by Operating System (simulated concurrency)
```

---

## 5. ALLOCATING HARDWARE

### 5.1 Estimate Performance Needs
- Transaction volume × Time per transaction = CPU load
- Choose hardware that can handle peak load

### 5.2 Hardware vs Software Trade-off
- **Use hardware if:**
  - Existing hardware does exactly what you need (cheaper)
  - Performance impossible in software
- **Use software if:**
  - More flexible
  - Easier to maintain

### 5.3 Allocate Tasks to Processors

**Reasons to put code on specific hardware:**

1. **Logistics** - Must be physically located there
   - Example: ATM has its own CPU (located in store)

2. **Communication Limits** - Data flow too high for network bandwidth
   - Example: High-speed graphics device needs local processor

3. **Computation Limits** - Single CPU can't handle computation
   - Example: Parallel processing requires multiple CPUs

### 5.4 Physical Connectivity
**How are hardware units connected?**

Types of topology:
- **Star** - All connect to center (like ATM consortium computer)
- **Pipeline** - Data flows linearly (like compiler)
- **Tree** - Hierarchical connections
- **Mesh** - Fully connected (complex, rarely used)

**ATM Topology:**
```
        (Central)
           ↑↓
    ┌──────┼──────┐
    ↓      ↓      ↓
  Bank1  Bank2  Bank3
```
= STAR topology

---

## 6. DATA STORAGE

### Three Options:

#### Option 1: Data Structures (In Memory)
- **Use for:** Temporary data during processing
- ✓ Fast access
- ✗ Lost when program ends

#### Option 2: Files
- **Use for:** Permanent storage, sequential data
- ✓ Simple, portable
- ✗ Low-level (must write lots of code)
- ✗ Formats vary by OS

#### Option 3: Database
- **Use for:** Complex queries, multiple users accessing same data
- ✓ High-level (built-in query language)
- ✓ Handles locking, recovery, caching
- ✓ Works on all platforms
- ✗ More complex interface
- ✗ Slower than files for simple access

### Types of Databases:

#### Relational DBMS (RDBMS)
- **Use for:** Most applications (financial, business, etc.)
- Example: Oracle, PostgreSQL, MySQL
- **Why:** Mature, reliable, ubiquitous

#### Object-Oriented DBMS (OO-DBMS)
- **Use for:** Specialized apps (multimedia, CAD, embedded systems)
- Example: db4o, ObjectDB
- **Why:** Stores objects directly (not tables)

### ATM Example:
```
ATM: Might use either RDBMS or OO-DBMS
Bank Computer: Definitely RDBMS (standard financial apps)
```

---

## 7. GLOBAL RESOURCES

### What ARE Global Resources?
**Shared by entire system** - Need coordination to prevent conflicts

### Types:

1. **Physical Units** - Processors, printers, network links
2. **Space** - Disk space, screen, buttons
3. **Logical Names** - Object IDs, filenames, class names
4. **Shared Data** - Database

### How to Manage?

#### Solution 1: Guardian Object
**Special object that owns resource** - All access goes through it

```
All tasks → Guardian Object → Shared Resource

Advantage: Centralized control
Disadvantage: Slower (must always request access)
```

#### Solution 2: Locks
**Tokens that grant temporary access**

```
Task 1: Get lock from Guardian
        Use resource directly
        Release lock

Task 2: Wait for lock
        Get lock from Guardian
        Use resource directly
        Release lock

Advantage: Faster (no middleman after getting lock)
Disadvantage: Must trust all tasks to follow lock protocol
```

### ATM Example:
```
GLOBAL RESOURCE: Bank Codes
- Must be unique within consortium
- Guardian Object: Consortium (controls allocation)
- All ATMs & Bank Computers request bank code through Consortium

GLOBAL RESOURCE: Account Numbers
- Must be unique within bank
- Guardian Object: Bank (controls allocation)
```

---

## 8. CONTROL STRATEGY (How does code execute?)

### 8.1 PROCEDURE-DRIVEN CONTROL
"Program drives everything"

```
Procedure A:
  Make request for input
  Wait for input ← BLOCKS HERE until input arrives
  Process input
  Return
```

**Characteristics:**
- Control lives in program code
- Program requests input and waits
- Uses stack to remember where program is

**Pros:** Easy with normal languages (C++, Java)
**Cons:** Hard for systems with many independent events

**Use when:** Simple, sequential operations

#### Example (Bad):
```
ATM Procedure-Driven:
1. Ask "Enter card"
2. WAIT for card
3. Ask "Enter PIN"
4. WAIT for PIN
5. Check balance
6. etc.

Problem: Can't do anything else while waiting!
```

---

### 8.2 EVENT-DRIVEN CONTROL
"Events drive program" (via callback)

```
Dispatcher (provided by framework):
  Loop forever:
    Wait for event
    Find procedure attached to event
    Call procedure
    Procedure returns → Dispatcher continues

Your code (callback procedures):
  Listen for events
  When event occurs, do something
  Return immediately
```

**Characteristics:**
- Control lives in dispatcher/monitor
- Your code responds to events
- Program doesn't wait for anything

**Pros:** Responsive, flexible, good for user interfaces
**Cons:** Slightly harder to implement

**Use when:** Responsive UI, many independent events

#### Example (Good):
```
ATM Event-Driven:
- "Card inserted" event → Handle card input
- "PIN entered" event → Check PIN
- "Withdrawal requested" event → Process withdrawal
- Can handle multiple cards/requests at same time
```

---

### 8.3 CONCURRENT CONTROL
"Multiple tasks run in parallel" (true concurrency on multiple CPUs, or simulated on one)

```
Task 1: Running ← CPU A
Task 2: Running ← CPU B
Task 3: Waiting for input
Task 4: Running ← CPU C
```

**Characteristics:**
- Each object = separate task
- Tasks can actually run in parallel
- OS handles scheduling

**Use when:** Multiple CPUs available, or truly independent subsystems

**ATM Example:**
```
Consortium Computer (handles many ATMs):
- Task for ATM1
- Task for ATM2
- Task for ATM3
- Task for Bank1
- Task for Bank2
(All might run on multiple CPUs)
```

---

## 8.4 COMPARISON TABLE

| Control Type | Flow | Best For | Language Support |
|---|---|---|---|
| Procedure-Driven | Program → Input | Simple sequential | All languages (natural fit) |
| Event-Driven | Event → Callback | User interfaces | Most languages (with framework) |
| Concurrent | Multiple tasks | Multi-CPU systems | Special languages/OS support |

**ATM Recommendation:** Event-driven for station (responsive UI)

---

## 9. HANDLING BOUNDARY CONDITIONS

### Three Phases:

### 9.1 INITIALIZATION
**System starting up** (Nothing running yet)

What must happen:
- Load configuration data
- Initialize global variables
- Create core objects
- Start tasks
- Set up communication channels

**Challenges:**
- Independent objects must not get too far ahead/behind each other
- Some functionality not available during init (limited mode)

### 9.2 TERMINATION
**System shutting down** (Controlled stop)

What must happen:
- Release external resources (files, network, hardware)
- Save important data
- Notify other tasks of shutdown
- Clean exit

**Usually simpler than initialization**

### 9.3 FAILURE
**System crashing** (Unplanned stop)

Types:
- User error (wrong input)
- Resource exhaustion (disk full)
- External problem (network down)
- Software bug (impossible inconsistency)

What good system does:
- Detect problem gracefully
- Save as much state/data as possible
- Print diagnostic info for debugging
- Exit cleanly (not corrupt remaining system)

**Good design** = plan for failures rather than hope they don't happen

---

# SUMMARY: Key Points for Exam

## ANALYSIS (What to build):

✓ **Domain Model = Foundation**
- 9 steps to build it
- Start with classes, add associations, add attributes
- Refine through inheritance
- Test that model is complete
- Organize into packages

✓ **Three aspects of Objects:**
- Static structure (class model) ← Most important
- Interactions (interaction model)
- Life cycles (state model)

✓ **Class Model Construction:**
- Find classes (real-world entities only)
- Filter out bad classes (redundant, vague, implementation constructs, etc.)
- Find relationships (associations with multiplicity)
- Add attributes (properties of objects)
- Organize with inheritance
- Test access paths
- Iterate and refine

---

## SYSTEM DESIGN (How to build it):

✓ **11 Key Decisions:**
1. Estimate performance
2. Reuse plan (libraries, frameworks, patterns)
3. Break into subsystems
4. Identify concurrency
5. Allocate to hardware
6. Choose data storage
7. Manage global resources
8. Choose control strategy (procedure/event/concurrent)
9. Handle boundary conditions
10. Set trade-off priorities
11. Select architectural style

✓ **Architecture Patterns:**
- Layers (horizontal) = levels of abstraction
- Partitions (vertical) = independent services
- Combinations of both

✓ **Control Strategies:**
- Procedure-Driven: Program controls; wait for input
- Event-Driven: Events trigger callbacks; responsive
- Concurrent: Multiple tasks in parallel

---

# EXAM QUESTION TYPES & ANSWERS

## 2-Mark Questions (Definition/Concept)

**Q: What is domain analysis?**
A: Domain analysis is the process of understanding the real-world problem and building a precise model of it, independent of implementation details.

**Q: What's the difference between layer and partition?**
A: Layers are horizontal (levels of abstraction, one-way dependency); Partitions are vertical (independent services, same abstraction level).

**Q: What is a guardian object?**
A: A special object that owns and controls access to a shared global resource, preventing conflicts in concurrent access.

**Q: Distinguish association from attribute.**
A: Attribute is a property of individual object (name, balance); Association is a relationship between two objects (Customer owns Account).

---

## 5-Mark Questions (Explain/Describe)

**Q: Explain the 9 steps to construct a domain class model.**
A:
1. Find classes - Identify real-world entities (nouns)
2. Prepare data dictionary - Write definitions for each class
3. Find associations - Identify relationships (verbs)
4. Find attributes - Add properties to objects
5. Use inheritance - Group similar classes under parent
6. Test access paths - Verify model completeness
7. Iterate & refine - Fix problems, add missing elements
8. Shift abstraction - Use more general concepts
9. Group into packages - Organize classes logically

**Q: Explain how to filter/eliminate bad classes during class model construction.**
A:
- Remove redundant classes (keep most descriptive name)
- Remove irrelevant classes (unrelated to problem)
- Remove vague classes (unclear boundaries)
- Remove attributes (properties of objects, not classes)
- Remove operations (actions, not persistent concepts)
- Remove implementation constructs (linked lists, pointers)
- Reconsider roles (use Person, not Owner)
- Remove derived classes (can be computed from others)

**Q: Explain the three control strategies in system design with pros/cons.**
A:
- Procedure-Driven: Program waits for input. Pro: Easy to implement. Con: Unresponsive.
- Event-Driven: Events trigger callbacks. Pro: Responsive, flexible. Con: Slightly complex.
- Concurrent: Multiple independent tasks. Pro: Parallel execution. Con: Complex coordination.

**Q: Explain layers vs partitions with diagrams.**
A:
LAYERS (Horizontal):
```
┌─────────────┐
│ Application │ (top, high-level)
├─────────────┤
│  Middleware │
├─────────────┤
│   OS/HW     │ (bottom, low-level)
└─────────────┘
Knowledge: Top knows bottom, bottom doesn't know top
Relationship: Client-server (upper uses lower)
```

PARTITIONS (Vertical):
```
┌────┬────┬────┬────┐
│ A  │ B  │ C  │ D  │
└────┴────┴────┴────┘
All same abstraction level
Peer relationship (knowledge mutual)
```

---

## DRAW DIAGRAMS Questions

**Q: Draw domain model for ATM system (simplified).**
```
         ┌─────────────────┐
         │   Consortium    │
         └────────┬────────┘
                  │ owns
                  ↓
         ┌─────────────────┐
    ┌───→│  CentralComputer│←────────────────┐
    │    └─────────────────┘                │
    │                                        │
    │    ┌──────────────┐              ┌────────────┐
    │    │     Bank     │              │    ATM     │
    │    └──────────────┘              └────────────┘
    │           │ holds                      │
    │           ↓                            │
    │    ┌──────────────┐                    │
    │    │   Account    │←───────────────────┘
    │    └──────────────┘      accesses
    │
    └─────────── communicates

Attributes:
- Account: accountNumber, balance, type
- Customer: name, id
- Transaction: amount, date, type
```

**Q: Draw architecture of ATM system (subsystems).**
```
    ┌─────────────────┐
    │  ATM Stations   │◄─────────────┐
    │ (3+ instances)  │              │ "station code"
    └────────┬────────┘              │
             │                       │
             │                       │ "bank code"
             ↓                       │
    ┌─────────────────────┐          │
    │  Consortium         │──────────┘
    │  Computer(Central)  │
    │  (Routing Hub)      │
    └─────┬───┬───┬───────┘
          │   │   │
    ┌─────↓─┐ │   │ ┌──────┐
    │Bank A │ │   │ │Bank C│
    │Comp   │ │   │ └──────┘
    └───────┘ │   │
              │   │ ┌──────┐
              │   │ │Bank B│
              │   │ │Comp  │
              │   └─┼──────┘
              │     │
              └─────┘

TOPOLOGY: Star (all ATMs/Banks go through Consortium)
```

---

# QUICK CHECKLIST FOR EXAM

## Before Exam:

- [ ] Memorize 9 steps of domain model construction
- [ ] Know how to filter classes (8 criteria)
- [ ] Know how to filter associations (5 criteria)
- [ ] Know how to filter attributes (9 criteria)
- [ ] Understand inheritance (bottom-up vs top-down)
- [ ] Know 3 control strategies and when to use
- [ ] Know difference: layer vs partition
- [ ] Know 11 decisions in system design
- [ ] Understand ATM example thoroughly

## During Exam:

✓ For short (2M) questions: Define + 1-2 key points
✓ For long (5M) questions: Explain process + give examples
✓ For diagrams: Draw class relationships + label clearly
✓ Always use ATM example if unsure

---

**GOOD LUCK! 🎓**

Remember: Your teacher wants to see if you UNDERSTAND, not just memorize.
- For 5M questions: Explain WHY we do things, not just WHAT we do
- Use examples to prove understanding
- Connect concepts together (e.g., why inheritance before attributes)

This guide covers everything in your Misc.pdf in simplest possible way! 📚