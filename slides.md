---
hideInToc: true
theme: seriph
---

# UberConf 2023
## July 17-21
### Matthew Pitts

---
hideInToc: true
layout: default
---

# Pick a Track

<Toc maxDepth="1"></Toc>

---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
transition: slide-left
---
# TL;DR :: Just give me the Cliff Notes!
<br />
<Toc mode="onlyCurrentTree" minDepth="2" maxDepth="2" />

---
level: 2
---
# Architecture
 - The fundamental goal of architecture is to **reduce the cost-of-change**
   - This may come in several contexts:
       - Developer famaliarity with a common design = reduced time to analyze existing code
       - Commonality in deployment infrastructure = reduced operational tasking
       - Code that doesn't need significant refactoring to implement "ABC" = reduced development time
       - etc.
 - Upfront design for future requirements is filled with pitfalls
 - If you have an architectural goal it should be **validated and/or testable**
   - Example: You want the system to be able to undergo the replacement of the storage backend without signficant refactoring
   - Write tests to validate the it can be done and/or prototype a second storage backend
   - Takeaway: If you're not willing to put the time into this upfront, then do you really need this requirement?
 - **Rapid feedback** should be applied even with architecture
   - **Develop tests** and/or a validation feedback mechanism into the project
   - ArchUnit

---
level: 2
---
# Microservices

> 80% of those claiming to be building microservices are not

## Cohesion
- We typically group things around some form of cohesion, but it has traditionally been around some aspect of the technology itself rather than the business
- Example: The traditional client-server model is clearly a technology-oriented cohesion
- Proper microservice design demands that we use the business domain as our **first** cohesion unit
  - Cohesion around technology can be applied but it is secondary to business cohesion

## What they are NOT
 - Neither "micro" nor "services"
 - The "micro" in *microservices* is akin to the "micro" in *microscope*
   - It's about the level of focus within, not an incidation of its overall size

---
level: 3
---
# Microservice Design Principles

- Build them for business agility (cohesion), not technology agility
- YAGNI(y) - You Aren't Gonna Need It (yet)
 - don't build it if you don't need it, yet
- start small and grow
- use *SOLID* principles
- never share source code; share binary only
  - favor encapulation and isoation over reuse
  - don't break every microservice by changing a single, shared library

## Deployable Units
 - The unit of deployment is what really defines our microservices
 - never recycle an in-use production instance of a microservice
 - use mulitple-instance, rolling-upgrade models for deployments

---
level: 3
---
# Microservice Caveats

- Requires additional infrastructural concerns
  - Instances running
  - Instances in-use
  - More automation
  - Additional Ops support

---
level: 2
---
# APIs

 - Take an API-first approach
 - Build and share a style guide
 - Design to a known specification (e.g. OpenAPI)
 - Use the spec to qualify the implementation
   - linting
 - Review and collaborate on the designed spec
 - Publish APIs as a catalog

---
level: 2
---
# Java

 - Newer language features
   - record
 - Functional programming models
 - Reactive programming
   - Spring and others

---
level: 2
---
# Soft Skills

## Decision Dials
 - We rarely make binary decisions - on or off
 - We decide within an analog range - a dial
 - Turning one dial might result in another dial changing or needing adjustment

## The Influential Engineer
#### Build a consensus
  - Ask "yes" questions 
#### When presenting between a large and a small option, give the larger option first
#### We tend to consider the effects of a loss more than the benefits of a gain
 - Discussing the potential losses of a decision direction might be more effective than discussing the gains of the other direction

---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
transition: slide-left
---
# Individual Sessions

<Toc mode="onlyCurrentTree" minDepth="2" maxDepth="2" />

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
transition: slide-left
---
# Designing Microservices: From Architecting to Data Modeling

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
level: 3
---

# Labs

```shell
git clone https://www.agiledeveloper.com/repos/git/uberconf23dm
```

 - userid: uberconf2023
 - password: westminstr

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---
level: 3
---

# Part 1: Architectural Patterns and Tenets of Microservices

- 80% of those claiming to be building MSs are really not

## Monoliths vs. distributed arch.
  - Is is about the unit of deployment; and not the environment of execution
  - Monoliths use a single unit of deployment; Dist Archs use multiple units of deployment

---
level: 4
---
# Cohesion
  - Like things are together; unlike things are apart
  - We want to minimize the frequency of change to a piece of code
  - Reduce the cost/time/effort; make change affordable
  - Context matters: there is no real/one cohesion due to different contexts
  - We always partition a system based on two diff criteria, but one is often more predominant
  - Technology-based and Domain-based partitioning
  - When designing monoliths we often focus on tech partitioning then domain
  - For MSs, we want the reverse; Domain partitioning should be first
  - Example: client-server monolith model is clearly a partition based on technology
  - Conways Law: Your application's design is a reflection of your organization's communication structure

---
level: 4
---
# Microservices are built around cohesion on the domain first, then the technology after
## #1 reason to build MS is to provide better business agility; if this is not the goal then the MS is not a good goal
## Traditional technology-based partitioning gives good response time to technology changes: ex an upgrade to Java across-the-board
## But, it makes changes based on business requirements slower
## Business agility should be the only real reason to justify the cost of MS development
## Domain-based partitioning means that changes to accommodate business needs are much quicker. But technology changes could be more difficult.
## However, localized goverance applied to MSs can keep technology changes more localized

# What are microservices NOT?
## Not arbitrarily small
## Neither micro, nor services
### The word "micro" in Microservices, is like the the word "micro" in "microscope"
#### It is not about the size of the thing being analyzed/modeled, it is about the focus: on the domain elements
## Does not force specific technology/language/framework
## not a project... a product
## not centrally governed
### Decentralized goverance on how the MSs are built
## "A system of applications that are loosely connected to collaborate to serve business needs"
## Autonomous development. Each MS team focuses on their own development plan with a lightweight target govered at a higher level

# Isolated deployments
## Tenet #1: We should never recycle an instance that is currently in production
## Two kinds of change: 1. bugfix/minor (no API change); 2. API change (new or existing)
## For #1 change release:
### New code is released on new MS instances with rolling takedowns of existing instances
### If there are issues, new instances are stopped and existing instances are kept
## For #2 change release:
### Release a completely new endpoint that clients can migrate to on their discresion
#### New URL or token routing to point to new instance
### Keep original instances online for some period of time and remove from service as usage drops
## This means more effort to manage instances and life-cycle; more observability, metrics, etc.


# Communication style
## Async or sync: up to the design; no intrinsic requirements
## Sync is sometimes easier to implement, but may require faster response/latency/etc
## Async may be better based on processing time or other external integrations
## If unsure, start with sync and willing to add async capability later if needed

# Transactions
## Distributed transactions are bad
### There is no one transaction to begin with
## We have technology based transactions (databases) and domain based transactions (business process)
## Typically a technology transaction needs to be extremely fast (milliseconds)
## Business transactions are typically very long (minutes, hours, days)
## Example: purchasing a ticket for a complex flight arrangement that involves a third party carrier might involve outside confirmations
### Have to stitch together several tech based transactions to build a single business transaction
## Requires one or both of ("Sagas"):
### Retries - reattempt the entire operation until all participant systems confirm
### Compensating transactions - revert back elements of the saga based on related failures
#### Ex: refund used frequent-flyer mileage for flights that could not be booked and confirmed
### A form of both: retrying for some period and then reversing/compenstating transactions if failures persist
## What about consistency
### Never ask your business ppl if consistency is important
### In most cases, the business does not really need strict or instant consistency
### If we put a lot of effort to achieve what we really do not need, we lose our ability to provide those things are truly essential
### CAP Theorem
### Most of the time eventual consistency is sufficient - so business transactions can be reconciled without technology transactions

# End comments/notes
## Business needs to provide more business people to the microservice build process to collaborate directly in the design

---
level: 3
---
# Part 2: Design Principles and practices
## Extensibility: The ability for us to design in a way that a pice of code is able to accommodate a reasonable change in requirements without much change to the code.
### The holy grail of software development
### Slippery slope: a lot of complexity has been introduced in the name of extensibility
### Extensibility requires really good anticipation: if we anticipate well, we end up with extensibility. But if we anticipate poorly, we end up with unncessary complexity.
#### The code we already have makes it harder to introduce more code/change (crowded train)
## Every team has 3 kinds of ppl:
### 1. those who know the domain really well, but nothing about software design
### 2. those who know the software design really well, but nothing about the domain
### 3. those who know both really well
### Group 3 is the best for anticipation; groups 1 and 2 have to collaborate much more
## Saying code is extensible is a misnomer and too board to actually define
## It should not be accounted for until it is truly required
## Reuse
### Grady Booch: "Use before you reuse"
### For something to be usable it has to be specific, for something to be reusable it has to be generic
### Reuse increases coupling
### It is never a good idea to reuse source code
### Favor binary reuse, but do so lightly. 
### Do not compromise on autonymous development and isolated deployment for the sake of reuse. It is not a matter of one being useful and the other not, it is prioritizing which is more important.
## SOLID Prinicples
## Single Responsiblity Principle
### A single "reason to change" principle - e.g. cohesion
### Microservices rely on very high cohesion, but domain-based rather than technology-based
## YAGNI(y)
### You Aren't Gonna Need It (yet)
### Don't do something until you definitely know you need it
### Collides with Extensibility which says to design for something that you do not yet know about
### Use YAGNI for microservices... postpone some piece of work until it is known to be needed
## DRY
### Don't Repeat Yourself
### Every piece of knowledge should have a single, unambiguous, authoritative source of representation
### Single Source of Truth
### Minimize duplication of effort, not just duplicate of code
### Caveat: If we remoe duplication, we increase coupling and potentially reduce encapsulation
### Place higher importance on encapsulation, autonomy, isolation over DRY
### Focus on business agility over reducing duplication
### Do not remove duplication in part that really do not deserve sharing
## Coupling around data formats, not specific technology solutions
### E.g. JSON model vs. JMS message queue
## Encapsulation
### #1 priority in microservice design
### Example: database behind a microservice should never be shared; it should be encapsulated behind the service
### If you lose encapsulation (e.g. by sharing the database) you lose autonomy and isolation
### Create distributed datamodels with hidden data and shared data.
### Export data, not the database
### Isolation: do not embed your microservice within a container; instead embed your container within your microservice
### We place precedence on encapsulation over duplication. Minimize duplication, but not at the degradation of encapsulation
## Developer productivity; deployment autonomy; 

## Design approach
### Focus on relevant details
### Remove or postpone details that look extraneous
### Prototype early and often
### Create and share common models through collaboration
### use a common language for the domain
### Don't call the same thing by different names in different contexts/layers
### It's about the domain you're focusing on
### Decouple domain objects for software technology related operations (e.g. synchronized keyword in business code)
### Avoid spreading business logic between layers
### Layers: UI, Application, Domain, Infrastructure

--- #7
level: 3
---
# Part 3: Data Modeling
## Eric Evans: Domain Driven Design
## Focus on the domain; bounded context
## Do not create a universal data model
### They lack encapsulation: a change to the model affects everything
## Create a distributed domain model with shared and hidden context
## Do not create a unified data model
## Don't prevent inconsistency, instead deal with it effectively as a business process
## Each MS has its own representation of data (encapsulation)
### We don't care how another MS models the same data internally
## Data exchange format is what is common
## Remove associations that are not essential to the model
## prefer aggregation over composition
## Entities
### Defined by its domain identity (not something specific to storage like PK)
### Identity should be unique even in a distributed system
## Value Objects
### used to describe aspects of a domain unrelated to specific identity (e.g. business card)
### Does not have identity
### Immutable as they represent a set of details rather than an identifiable entity
### Can be readily shared or copied 
## Services
### Represent activities or (stateless) actions that do not fit into entity or value objects
### Identify domain services vs application services
## Aggregates, factories, repositories
### aggregate
#### Cluster of ojects treated as a unit for data change
#### Has root to pull-in the other records to aggregate, but references are hidden
## Honor encapsulation, cohesion and delineate clear boundaries
## Focus on Figuring out the bounded context
### Start with nothing and start including what you need instead of starting with everything and then excluding
### Live with less rather than suffer with more
### What is shared, what is hidden and what is transient

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
transition: slide-left
---
# Know your Java?
## Venkat Subramaniam

---
level: 3
---
# Exercises

<Toc mode="onlyCurrentTree" minDepth="4" />

---
level: 4
---
# List#remove overload and override
```java
Collection<Integer> items = new ArrayList<Integer>(List.of(1, 2, 3));
List<Integer> items = new ArrayList<Integer>(List.of(1, 2, 3));

items.remove(1) // functions differently based on items being Collection or List
List#remove(int index)
List#remove(T object) // an overload and an override at the same time
```
---
level: 4
---
# Type inference

```java
Collection<Integer> numbers = new ArrayList<Integer>(List.of(1, 2, 3));
var numbers = new ArrayList<Integer>(List.of(1, 2, 3));
// type inference treats numbers as an ArrayList vs. something more generic like Collection
numbers.remove(1); // removes by index instead of object identity
```
- creates the same problem as the override+overload problem before

---
level: 4
---
# Arrays.asList()

```java
List<Integer> numbers = Arrays.asList(1, 2, 3);
numbers.add(4); // is not supported
numbers.set(2, 2); // is allowed
```

- Question the use of #asList
- Use the #of methods instead
  - They create proper immutable collection type

```java
List.of
Set.of
Map.of
```

- Immutability brings a lot of benefits

```java
List<Integer> numbers1 = List.of(1, 2, 3);
List<Integer> copy = List.copyOf(numbers1);

copy == numbers1; // copyOf detects immutability and returns the same reference
```

---
level: 4
---
# forEach and add

```java
List<String> names = List.of("Dory", "Gill", "Bruce", "Nemo", "Darla", "Marlin", "Jacques");
List<String> inUppercase = new ArrayList<>();

names.stream().map(String::toUpperCase).forEach(name -> inUppercase.add(name));
System.out.println(names.size());
System.out.println(inUppercase.size());
```

- What's wrong with this?
- It runs, but is it OK?

<v-clicks depth="2">

- The pipeline is not 'pure': it has side effects outside of the pipeline
- It has shared mutablity, which we want to avoid
- Changing above to use #parallelStream() introduces concurrency issues
  - Very difficult to detect and debug

</v-clicks>

---
level: 5
---
# forEach and add :: What's the better way?

```java
List<String> names = List.of("Dory", "Gill", "Bruce", "Nemo", "Darla", "Marlin", "Jacques");
List<String> inUppercase = names.stream().map(String::toUpperCase).toList(); // java 16
// java8: #collect(toList()) would create a mutable list which is less desireable
// java9: #collect(toUnmodifiableList())
System.out.println(names.size());
System.out.println(inUppercase.size());
```

- works fine with #parallelStream() because there is no shared mutability
- toList() is a safe, terminal operation on the stream

--- 
level: 4
---
# stream and mutablilty

```kotlin
val numbers = listOf(1, 2, 3)
var factor = 2
val result = numbers.map { it * factor }
factor = 0
result.forEach(::println)
```

- what is the output?
- "2, 4, 6"
- the corresponding code in java produces: "0, 0, 0"
- functional programming relies on lazy evaluation for efficiency and performance
- lazy evaluation relies on immutability and purity of functions for correctness

## Two rules for purity
#. a pure function does not modify anything in a way the change can be seen outside
#. a pure function does not depend on anything that may change from the outside

---
level: 4
---
# stream's parallel vs. sequential

```java
List.of(1, 2, 3).stream()
  .parallel()
  .map(number -> transform(number))
  .sequential()
  .forEach(number -> print(number))
```

- Does #transform run parallel or sequential?
- Does #print run parallel or sequential?
- Hint: the stream evaluates laziy...

<div v-click>
# They both run sequentially b/c that is the last call preference and the stream is evaluated lazily
</div>

---
level: 4
---
# constructor and virtual

<v-clicks depth="2">

- DO NOT do anything significant in the constructors
  - DO NOT call other methods
  - DO NOT create other objects
  - DO NOT create threads
- DO write factory methods to do complex construction logic
  
</v-clicks>

---
level: 4
---
# final and virtual

```java
public class Sample {
  // f1 can be overridden in a derived class, f2 can not
  public void f1() {}
  public final void f2() {}
}

public static void main(String[] args) {
  var sample = new Sample();
  sample.f1(); //invokevirtual
  sample.f2(); //?
}
```

- how is f2 invoked within the JVM at runtime?
- 'final' is a compile-time only feature
- runtime method invocation is still done virtually in the JVM

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Agile Architecture
## Kirk Knoernschild

### Contents
<Toc mode="onlyCurrentTree" minDepth="3" maxDepth="3" />

---
level: 3
---
# Why do we do architecture?
    - scalability
    - security
    - maintainability

## Who needs an Architect by Martin Fowler

---
level: 3
---
# Architecture's Goals
 - "Architecture represents the significant decisions where significance is measured by cost of change"
 - Grady Booch
 - A primary goal is to make future changes most cost efficient

## Complexity
 - loc doubles every 7 years
 - 50% of development time is spent understanding code
 - 90% of software cost is maintenance and evolution

## Lehman's Law
 - As a system evolves, its complexity increases 
  
## Gall's Law
 - A complex system that works is invariably found to have evolved from a simple system that worked. A complex system designed from scratch never works and cannot be patched up to make it work. You have to start over, beginning with a working simple system.

---
level: 3
---
# When We Do Architecture

## Between requirements and design
 - We often try to specify solutions to problems that require knowledge we currently do not possess.
 - This is about our ability to predict future needs, which is difficult at best
 - In many cases our attempts to design to reduce future cost-of-change turn into unnecessary complexity and don't actually facilitate future growth

## The core tenet of agile is to get rapid feedback so that we can respond to change

---
level: 3
---
# So how do we change?

<div v-click>

## Define what the goals of the architecture are...
 - Example: We want to be able to swap-out the graphical fronted without significant modification to the backend

</div>

<div v-click>

## ... And build a system to provide rapid feedback of the goal being satisfied
 - Even if this means building a second UI
 - What is the point of defining the goal if you're not willing to do the work to prove it works

</div>

---
level: 3
---
# Three Pillars of Software Architecture

## Social
 - The architects themselves
## Process
 - The act of architecting
## Structure
 - The resulting architecture

## Take aways
- When we make the decision is equally as important as the descision we make!
- Architects should be getting rapid feedback even when making design decisions.

---
level: 3
---
# Going forward, what do we do?

## Test/validate early - both design and function
## Move architectural decisions to the right until they are testable/validatable
## Strong feedback loop between developers and architects
## Architecture exists at every level
### The layer at which architecture stops is where design rot can start
## Must create a shared understanding between developers and architects
### Architect at every layer


---
level: 3
---
# Start with Simple

## The architecture you believe you have is not always what you have
## Documenting the architecture is obsolete
## Source code is the design
## Validate the architecture: prove it works; write tests
## Use tools to generate visualizations
### jaranalyzer
## Generate your documentation
## Unit of release *IS* the unit of reuse
## Give yourself feedback
### Visualizations
### Test cases

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Asynchronous Programming in Java using Virtual Threads
## Venkat Subramaniam

### Contents
<Toc mode="onlyCurrentTree" minDepth="3" maxDepth="3" />

---
level: 3
---
# Threading
 - Virtual threads came out in java 20
 - Threading itself has been in java since the beginning
 - Several innovations since

## Parallel vs. Concurrent
 - Walk and talk in parallel
 - Talk and drink can not be done simultaneously

## Parallel vs. Asynchronous
 - Asynchronous boils down to non-blocking
 - Non-blocking: a thread does not have to block waiting for something that takes time to execute
 - Example: making coffee... you don't wait (block) for the coffee to brew; you do something else

---
level: 3
---
# Threads
 - Threads are lightweight, but this is relative
 - How many threads can/should you create?
 - Depends on the amount of memory and CPU cores
 - $numThreads <= \dfrac{numCores}{1 - blockingFactor}$
 - Blocking factor is how much your thread-work will be blocking vs. actually using CPU
   - E.g. something computationally intensive will have a blocking factor of 0
   - A blocking factor of 0.5 means numThreads can equal double the cores


---
level: 3
---
# Multi-threading, eh?
 - Sequential execution
   - You're doing sequential execution if you're happy!
 - Existing programming model: threads tied to tasks (for the most part)
 - What if a task is going to take some time?
 - Just add more threads (??)

---
level: 3
---
# Example

```java
public class Sample {
  public static doWork() {
    Thread.sleep(5000);
  }

  public static main(String[] args) {
    for (int i = 0; i < 10; i++) {
      new Thread(Sample::doWork).start();
    }
  }
}
```

- We're tying the work to threads
- This will be fine for 10s or 100s of threads
- this won't scale to 10s of 1000s of threads
- Analogy: Threads in java are like a waiter in a restaurant that is focused on one table only at a time

---
level: 3
---
# Continuations
## Subroutines: the execution of an anonymous function... input+output and done
## Coroutines: Coordinating routines

```kotlin
import kotlinx.coroutines.*
suspend fun task1() { 
  yield()
}

suspend fun task2() {
  yield()
}

runBlocking {
  launch { task1() }
  launch { task2() }
}
```

- a good system is where you reap the benefits of continuation/threading without complexity in the code

---
level: 3
---
# VirtualThreads of Java
- Super lightweight threads
- managed by the JVM, not the OS 
  - Traditional Thread mapped directly to a native OS thread
- VirtualThread maps down to a *career thread*
  - The mapping is one-to-many where a single career thread will be maintained and used to execute many VirtualThread
  - Allows for a pool of career threads to service the whole JVM

```java
public class Sample {
  public static doWork() {
    Thread.sleep(5000);
  }

  public static main(String[] args) {
    for (int i = 0; i < 100000; i++) {
      Thread.startVirtualThread(Sample::doWork);
    }
  }
}
```

---
level: 3
---
# Taking it further

## In the past, the stucture of sequential imperative style code was very different from the structure of parallel imperative style code.
## Start in java 8, the structure of sequential functional style code is the same as the structure of parallel functional style code - thanks to Streams
## Staring java 8 the structure of synchronous functional style code is the same as the structure of asynchronous functional style code - thanks to CompletableFuture
## Functional style is great as long as the functions are pure and you really don't have to deal with a lot of nested exceptions.
## Starting java 20, the structure of synchronous imperative style code is the same as the structure of asynchronous imperative style code - thanks to Virtual threads.

---
level: 3
---
# Summary
## Where to use?

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Practical AI Tools For Java Developers
## Ken Kousen

<Toc mode="onlyCurrentTree" minDepth="3" maxDepth="3" />

---
level: 3
---
# ChatGPT
 - OpenAI
 - Largely owned by Microsoft
 - Large plugin ecosystem, but no quality control

## Code interpreter
 - Allows for the submission of data and generates code to load and correlate the data

## Links
 - openai-cookbook

## Models
 - GPT 3.5
 - GPT 4
 - DALL-E
 - Whisper

## Limitations
 - can not read files from local filesystem
 - can not read files from a URI

## Demo
 - Walked through using ChatGPT to convert a block of gradle groovy DSL to kotlin
  
---
level: 3
---
# Google Bard

---
level: 3
---
# Other tools

## Claude
 - https://claude.ai

## Whisper
 - MacWhisper
  
## Descript
 - Transcribes video
 - Edits to the text transcription can be transposed into the video
 - Has video edits to do standard cleanup/improvements
 - Can train on your voice and then overdub from text

---
level: 3
---
# Canva and Midjourney

## Walked through an example of using AI in Canva to generate a presentation and added in an image generated in MidJourney

---
level: 3
---
# AI Assistant in JetBrains IDEA
 - just introduced
 - very little documentation
 - trains itself on your own github repository
 - suggests code completion using AI
 - can explain code via selection menu
 - Generate documentation
 - named suggestions
 - commit message generation

---
level: 3
---

# GitHub AI

---
level: 2
---
# Keynote: Technical Debt (Codescene)
- Software developers spend 23-42% of their work week dealing with technical dpte and bad code
- There is a statistically signifcant correlation b/t software
- Research finds that developers are frequently fores to introduce new Technical Debt in order to deliver new features

# The laws of software evolution

## Continuing change: a system must be continually adapted for it becomes progressively less satisfactory
 - feedback loop is quick - we deliver a new feature and people are happy
  
## Increasing complexity
 - feedback loop is slow and thus we don't respond to it well
    
# Hyperbolic Discounting

- There's never enough time to do something right, but there's always enough time to do things over and over again.

# Developer unhappiness
 - Stuck in problem-solving
 - Time pressure
 - Work with bad code

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Conway's Game of Life :: Functional Programming

## Design Exercise

- My initial tests help me to design the skin
- Later tests help me to design the guts

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# API Design First: Succeeding with API Goverance
## Travis Gosselin

<Toc mode="onlyCurrentTree" minDepth="3" maxDepth="3" />

---
level: 3
---
# Developer Experience

## The activity of studying, improving and optimizing how developers get their work done.

- "Developers work in rainforests, not planned gardens"
- Developer Experience is a direct reflection of the APIs they have to use
- Over 90% of developers use APIs
- Developers spend 30% of their time coding APIs (the largest single chunk of their time)
  
---
level: 3
---
# API-First Approach

An API-first approach means that [...] your APIs are treaed as "first-class citizens". That everyting about a project revolves around the idea that the end product will be consumed by client applications.

## API Goverance

We want teams/developers to move rapidly (think autobahn). However, complete autonomy and no guardrails/speed limits means accidents.

### Modern analogy: the traffic circle. 
 - Designed to create a free-flowing, low-speed environment

### Goverance with a lowercase 'g'
 - Alignment
 - Enablement
 - Collaboration
 - Guidance

Think "stewardship" instead of Goverance

---
level: 3
---
# Pillars

- API Standards
- API Design
- API Development
- API Publishing

Standardization continues to be the top API technology challenge

---
level: 3
---
# Style Guide
- URL structure
- Path params vs. query params
- Collections (roots, pagination)
- Serialization
  - Quantities
  - Dates
  - Durations
- Request & Response
  - HTTP codes
  - Headers
  - Verbs
- Errors
  - Error responses
  - Schema
  - Required fields
- Naming
  - Reused names

---
level: 4
---
# Style Guide Best Practices

- less is more; don't write a book
- not implementation specific
- living document; let the guide itself evolve
- goldilocks use cases
  - good to not over-burden certain standards
  - can be used to give examples within specific implementation details without dictating them
- align to existing standard
  - rfc2119
- examples always
- don't build from scratch - plaglurize from other style guides
  - paypal
  - cisco devnet
  - apisytlebook.com
  - github.com/spscommerce/sps-api-standards
- consider the automate-ability of the style-guide itself

---
level: 4
---
# Who builds this guide?

- you
- other collaborators and advocates
- real users

---
level: 4
---
# Real-world release

- Nobody cares
- They will not read it
- Teams will agree it's a good thing and still not follow it
- It takes time

## Greenfield
 - obvious place to start using the guide
 - test it and feedback-loop with team

## Brownfield

---
level: 3
---
# Automating your Styleguide

- EX: Everyone should use RFC7807 for 4xx/5xx error responses
  - spectral can be used to define an automated evaluation

---
level: 3
---
# API Design

- produce a spec: e.g. openapi.yml
- The spec should be the defined, upfront contract of the API
- Review the spec as a collaboration
  - Is it the right thing to do
  - Steward the API as a team
  - Is the styleguide being applied? Automation?

---
level: 3
---
# People

- avoid design by committee
  - review together, don't design together
- use a standard design language - e.g. openapi
- focus on the hard things: the domain and workflows
- avoid requiring in-depth openapi knowledge
  - familiar but not experts

---
level: 3
---
# Real-world practices/tools

 - OpenAPI Domains
   - Hosted in a common place
 - IDE integrations with spectral linting
   - VSCode
   - IntelliJ
 - CI/CD integration
 - TypeSpec
   - microsoft.github.io/typespec

---
level: 3
---
# Development

- openapi spec can be directly used with mocking tools
  - stoplight prism

## Validation
 - linting the openapi spec
 - does not recommend from-code generated spec files
 - but it could be used to compare designed spec, vs. actual spec
 - docker run optnapitools/openapi-diff:latest design.yml generated.yml --fail-on-changed

---
level: 3
---
# Publishing

- Central
- Discoverable
- Developer Portal

## Documentation/Tools

 - Poor or inccurate documentation is worse than no documentation
 - Stripe
 - Stoplight
 - SwaggerHub

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Unleashing Deploy Velocity with Feature Flags

[Slides](https://nfjs.nyc3.digitaloceanspaces.com/slides/2023/travis_gosselin1/297299_Deploy.Velocity.Feature.Flags-Travis.Gosselin.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20230720T170137Z&X-Amz-SignedHeaders=host&X-Amz-Expires=259200&X-Amz-Credential=J3JF7GRGCUE4RUGX2JAP%2F20230720%2Fnyc3%2Fs3%2Faws4_request&X-Amz-Signature=99c52f0981c209afe8eed455cb3421e022ad8ae3928aa732b8cf03e9aebdcb45)

# flexibility with feature flags
 - trunk-based development
 - shorter, simpler branches
 - ship faster
 - rollback features without deployment
 - development team can release code as a separate cycle from features being enabled
   - business can enable the feature as a separate schedule from development releases

---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Reactive Spring APIs
## Craig Walls
 - www.habuma.com
 - craig@habuma.com
 - https://github.com/habuma/nfjs-samples/NFJS-UberConf-2023

<br />

<Toc mode="onlyCurrentTree" minDepth="3" maxDepth="3" />

---
level: 3
---
# Spring's Reactive Story

- leverages *Project Reactor*, but supports *RxJava*
- covers web, persistence, security, integration, etc.

## Spring MVC -> Spring WebFlux

- don't have to know alot about reactive programming to start using

## Reactive vs. Imperative
 - Imperative is how we think... do this, then that, loop on this, etc.
 - Imperative is typically written in the order it happens
 - Reactive style is more functional
 - Reactive is non-blocking, details of threading are hidden
 - Reactive typically allows for more efficient usage of threads

---
level: 3
---
# Examples

## Simple endpoints

```java
    @GetMapping("/hello")
    public Mono<String> hello() {
        return Mono.just("Hello world");
    }

    @GetMapping("/counter")
    public Flux<Long> counter() {
        return Flux.interval(Duration.ofSeconds(1));
    }
```
- Rest Controllers can return Flux types to allow for he generation of the objects in that Flux to be created in a reactive way (in another thread)
---
level: 3
---
## Reactive database access

 - the same concepts extend to Spring Data Repository types with supported backend databases
  
```java

    public interface BookRepository extends ReactiveCrudRepository<Book, Long> {
    }

    @GetMapping("/books")
    public Flux<Book> books() {
        return repository.findAll();
    }

    @PostMapping("/books")
    public Mono<Book> save(@RequestBody Book book)
    {
        return repository.save(book);
    }

```

---
level: 3
---
# RSocket

```java
@Controller
public class RSocketExampleController {
    @MessageMapping("hello/{name}")
    public Mono<String> helloTo(@DestinationVariable("name") String name) {
        return Mono.just("Hello");
    }
}
```

---
level: 3
---
# Other tools/links

- Spring Cloud Streams
- 
---
level: 2
---
# Spring Reactive Persistence

## Spring Data has reactive support for:
  - R2DBC
  - MongoDB
  - Cassandra
  - Redis
  - Couchbase
  - etc

---
level: 3
---
# Gradle dependencies

```groovy
    implementation 'org.springframework.boot:spring-boot-starter-webflux'
    implementation 'org.springframework.boot:spring-boot-starter-data-r2dbc'
    implementation 'com.h2database:h2:2.1.214'
    implementation 'io.r2dbc:r2dbc-h2:1.0.0.RELEASE'
    implementation 'io.projectreactor.netty:reactor-netty:1.1.5'
    implementation 'org.springframework.boot:spring-boot-starter-rsocket:3.0.4'
    implementation 'org.springframework.boot:spring-boot-starter-data-mongodb-reactive:3.0.4'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    testImplementation 'io.projectreactor:reactor-test'
```

---
level: 3
---
# Projecting database data unto other types

```java

public interface SimpleBook {
    String getIsbn();

    String getTitle();

    // We can use a bean-style evaluation syntax for deriving this field value at runtime from the target object - in this case Book
    @Value("#{target.author.split(' ')[0]}")
    String getAuthorFirstName();

    @Value("#{target.author.split(' ')[1]}") 
    String getAuthorLastName();
}

// And this repository method WORKs even though our db-table is mapped to Book instead of SimpleBook
Flux<SimpleBook> findSimpleBookByIsbn(String isbn);

```


---
level: 2
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Influential Engineer: Overcoming Resistence to Change
## Michael Carducci
### michael@mago.co
[Slides](https://nfjs.nyc3.digitaloceanspaces.com/slides/2023/michael_carducci/297305_Change%20Agent%202.0.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20230721T150241Z&X-Amz-SignedHeaders=host&X-Amz-Expires=259199&X-Amz-Credential=J3JF7GRGCUE4RUGX2JAP%2F20230721%2Fnyc3%2Fs3%2Faws4_request&X-Amz-Signature=30ba42f6bd8375a40b442b2f89214cdfc829a8a2c54e87c24de54aa608d3e1d3)
<br />

#### There is a science to persuasion

>15% of one's financial success is due to one's technical knowledge, and 85% is due to human engineering and the ability to lead people

---
level: 3
---
# Questions we want to answer

- Given two options should you present the more costly or the lest costly first?
- Is it better to tell management what they will save or what they will lose?
- If you have a new piece of information, when should you mention it is new?
- If your idea has both strenths and weaknesses, when should you present the weaknesses?
- If someone praises you what is the most effective thing you can do after you have said "thank you"?
- If you want someone to cooperate with you, what is the single most productive thing you can do before you try to influence them?

---
level: 3
---
# You Act First

## Law of recroprocity
 - I am obligated to give back to you the form of behavior that you first give to me.

### Is it ethical?

 - Future obligation for repayment of favors gives a group a tremendous competitive advantage.

---
level: 3
---
# Don't fumble this

> Thank you

> No problem

You fumbled!

### Better response:
> Absolutely! I know that if the situation were reversed, you'd do the same for me.

---
level: 3
---
# Reciprocity works in negotiations too

> I'm gonna need you to work this weekend


> Of course. I know it’s important that this gets done, and I’m happy to help; I’m sure if I ever needed something I could count on you too!
> I will just plan to take some comp time sometime to get the time back

## Always start with the larger request

---
level: 3
---
# Case Study
## Engineer wants a hardware upgrade...

- asks for a huge workstation and is turned down
- walks away
- returns and asks for a solid-state harddrive
- psychologically this is considered a separate request
- so the engineer is turned down again
  
> If you retreat from the situation, you lose, if you retreat in the situation, you win.

---
level: 3
---
# Building Consensus - Pro Tips

- get the other preson saying "yes" immediately
- probing questions establishing a consensus

> It's better if we're more productive, right?
> 
> Yes
> 
> And if we're losing time waiting for our computer to do stuff, that's a bad thing right?
> 
> Yes

#### This can be dangerous, or unethical depending on how it is used

---
level: 3
---
# Consensus Pro Tips

### We are driven by scarcity
  - You need to explain what it is aout this that they can't get anywhere else.
  - Managers weigh information about potential loses more than potential gains.

### Dramatize your Ideas
  - scarity works with information too
  
### Consensus power
### Listen; don't contradict
### Consistency
  - write it down
### Appeal to nobler principles
### Authority
  - You are the expert!

---
level: 3
---
# Videos to watch

