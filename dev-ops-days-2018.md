# DevOps Days 2018

## Keynote

Kolton Adrus - Gremlin Inc.

Arrested Development Podcast

--HOW large is our DB

How to get in front of issues?
Chaos Engeneering - experiment w/ dicipline, Before things go wrong

Availability Theory
- Failure when restoring a database
- When you cause failure, is an alert sent
- Use Chaos to practice failure
- Gamesay - What could go wrong - how to measure the failure and impact
- Can I test in one host, or one container. How is the failure handled

## Kubernetes Test Drive

Rob Rich

Slides: robrich.org/slides/kubernetes-test-drive

March - AZGiveCamp

Orchestration engine - givine a cluster of machines, allow the orchestrator to make the decision where they run.

Physical Layer:
KubeCtl
...

Installing Kubernetes.... dont do it   (kubeadm) its not that bad but it is involved

Private = mesosphere, OpenStack, CloudFoundry

Docker also does some - just gets you running with K8S
Minikube - single node cluster - does less magic but exposes the pieces

### Elements

Pods - work details, 
deploy - scale and restart, 
service - route inbound traffic

Yaml File
* apiVersion
* Kind
* metadata
* spec

Pods are wrapped by deployments

Service - is in another file, will route traffic. the yml file will determine how the service is configures


Look at persistent Volumes, which are for storage

`kubectl` UI - Pipe analytics to ELK stack

Questions:
* What are the implications of running a (FROM) ubuntu and redhat
* on prem k8s
* firewall ports

-----
- Look at "On-prem turn key" installs on the K8S website
- Use CI system to exec `kubectl` commands from the source controlled 
- look at 'Helm' for semi-CI

On-Premises turnkey cloud solutions
https://kubernetes.io/docs/setup/pick-right-solution/#on-premises-turnkey-cloud-solutions


## Orchestrating Serverless with Step Functions

Matt Williams

Technovalgelist.com

Serverless - Faas - Functions as a Service
Usually Trigger based
Should respect single responsible principle

How do we orchestrate functions? 
(Kinesis as traffic cop)
github.com/Nordstrom/hello-retail

AWS Step functions 
- is a statemachine
- It has transitions that coordinate the work

Tasks, 
Choices - route/switch
Succeeed/Fail - based on result 
Pass - 
Wait for a timestamp or result or period of time
Parallel

Can use the serverless frameworks - utility to create lambda functions and other resources

sf.technovangelist.com

**Look at what ServerlessFramework work for on-prem solutions**

Open source, Kubernetes-native Serverless Framework
https://fission.io/


## DevOps should Marry Graph Databases

Mark Gunnels
Tabula Rasa Healthcare

Enable DevOps success by Modeling

1) Reduce org silos
1) Accept failure as normal
1) Impelement gradual challenges
1) Leverage tooling and automation
1) Measure everything

Move from get stuff done to -> Get stuff done well

Large data sets are fater to traverse with graph than with relational 

Neo4j is one, but there are several of them now.

Property Graphs - 
Node - can have unique properties. (Apps, queues, topics)
Relationship - a connection between two nodes, and a direction (of message)

`MATCH` like a where stmt

Graph databases are easy to translate a model to it.

Extracting Topology from RabbitMQ is easy

'miner' - GO http api - builds the whole topology of a rest service, whats available

Create a node for an app, then if its producing or consuming from a service
Once created, we can create 

graphenedb.com - UI for nodes

Once you have your system modeled, you can talk about what happens when one item goes down

'cf-alert' - looks for app crashes (cloud foundry)
 - This can provide you with automated 

 Book: "Your Code as a Crime Scene"

"centrality" graph algo - which apps need the most monitoring


-----------

Video: Mark Richardson - How to scale based on queue depth - Algo

Referal: Mark Gunnels

-----------


## Lunch

DevOpsTopologies website - shows organizations topologies

Molecule - framework to test the configuration of your setup

Guilds - "Software Quality" guild


## Database DevOps with Containers

Rob Richardson

robrich.org/slides/database-devops-with-containers

Goals: Relaibility, consistency, cost

Anything we do a lot, we want to automate.

With databases this gets weird.

With apps, the critical part is code.
With DBs, the important part it the data in PROD.

Nightly backups, used to restor agains pre-prod.
Take it a next step. Then automate all the way back to test, then dev.

Sanitize, ananomise, shrin, migrate to latest version it.

Then in dev, how does a developer he needs to install sql server, restore, etc!

So each dev needs a sandbox environment to work in so devs dont step on each others toes.

#### 

* Backup database
Copy the .bak into container
Copy the sql script into the container

then start the service, run script and kill sql engine

Run the SQL script, which cleans up the data and database. Shring the data size, truncate log file, change user.

Then create new container with dev data (so prod data doesnt accidentally bleed over.)
Then start up the container with the dev database


---- 
When we do this backup every day, then we 

## Intro to Designing Systems and Processes

Slides: https://docs.google.com/presentation/d/e/2PACX-1vSRUFm2uASxkkgCPewMcdr5PtmRe-s-8zEjowo56p7sCnuE-rWuSWcoJLcTtLlmuPLQQJ2Y0HEdBWV8/pub?start=false&loop=false&delayms=3000&slide=id.g430a7e7c0c_2_409

What to change, what to change to, how to cause the change - "Goldratt books"

listen -> explore -> think -> write it down (repeat)

Structure, connection, people, capability, cost

1) Define the problem 

-Loving the problem, Not your solution (Ash Maurya)

How do we solve this problem right now? 
-Map out the system
-System diagem, plus process flow. Make illustrations accessible to many peoples
*Describe* the existing system

Observer work being done. Listen to people.
Study the "Exception process" - where has the existing process broken down, whenre have people filled in gaps

2) Describe the problem space
People, problem statement, ...

In 1-3 sentances, describe the problem.

Design: Expected benefits - (protect customers and improve cycle times)
Desing: Context and Major Requirements

2) Develop and Evaluate the problem

How can we simplify the problem.
How can we 'unload' people? (people make the system resilient, fill in the gaps) - provide tools, remove tedius tasks
How can we maximize flow? Reduce variation, automate, where is re-work

Optmiise Processes for your KPIs

"Directed System Design"
-KPIs - time to resolution, 

**Create sequence or data flow diagrams for top 3 use cases**


System should give information and control

Design monitoring points
* Learn about problems before customers
* Understand health of components all the way down

Done is Better than Perfect
Better is Better than Perfect

QA for Designs 
- Find defects during reviews
- Implement Prototypes - find failures here (choose tools that cannot be deployed to prod(rest mock tool))
-Architecture DR

Robust and Resilient systems are not build by accident.

See tweet for link #DevOpsDaysPHX

## :Leveraging Go to Build a Functions as a Service

Brina Downs

FaaS
Hashicorp - Nomad - possibly

Core components
* FreeBSD Jails - segment execution
* ZFS
* Go

FreeBSD - OS, server majority of internet traffic. Native support of ZFS and DTrace
Jail - OS virtualization,
**ZFS - stable file system, has snapshots, instant cloning**
  (This is super interesting)

CURL into endpoint, pass a json data payload 
1) with a pointer to the function name
2) 

Request to API
API checks cache for function
If function missing get from repo, then build
if exists use
then pass binary to jail
execute in jail
return 


FAAS Compoenents
IP Management - VNET can be used (cant use DHCP)
API 
- need a health check (/health)
- need a function endpoint : POST /api/v1/function
-Jail option 
-- get jails, functions, etc as endpoints

github://briandowns/sky-island

BSD Meetup


### Keynote

Service Mesh

Christian Posta - Chief Architect Redhat
Istio contributor - Istio in Action (book - MEAP)

Thread Bulkheading??

Look at Netflix service libraries, what they do and why theyre valuable
Hystrix, Zuul, Ribbon, Eureka, etc

If you go with a library approach, you have to pick a language(prevent some)

Instead what is the way to extract away: Contanerize

 heterogenus architectures
 use proxy to handle the concerns
 proxy lives with the service to handle all application traffic

Service mesh - decentralized network infrastructure between services
each service is deployed with a proxy

App goes through proxy for all network requests.
Proxy handles all load balancing, encripting traffic, telemetry, authroization/policies
Control plane handles config, telemetry and distributed tracing, service discovery

* Linkerd - part of CNCF(JVM) - fat (linkerd2 built in Rust)
* Consul - started as service discovery - have added concusl connect, establish mutual TLS and policy
    -Consul agent is in charge of managing proxies
* Istio - large backing (1.0 - understand what it is but wait a bit before putting it into production)

EnvoyProxy
Linkerd
Istio-Tutorial

