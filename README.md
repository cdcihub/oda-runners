# Federated ODA Workers

## Why Federated Workers?

Providing sufficient computing resources is difficult.

Hence:

**Our goal is to assist in expoloitation of technologies facilitating grows of federation of scientific analysis workflows.**

We provide:

* **frontend**: beutiful and familiar [frontend](https://www.astro.unige.ch/cdci/astrooda_/).
* **data caching**: some data will be cached directly on our storage, and hence re-used by all users.
* **knowledge base**: "open" RDF fact store, explaining relations and provenance of workflows and data. Used to search for relation between workflows and data.

## How do you take part?

* Simply **use our online analysis frontend or API**, leveraging the collective effort of the federation with just few clicks, tracking provenance of our platform.
* **Empower your requests with your own hardware**, computing selected (by you) and verified (by instrument expects whom you trust anyway) analysis workflows. The analysis will store the high-level products in shared provenance-based cache, accelerating similar workflows for the community. Community will see your contribution and will be grateful.
* **Join your own service - a remotely computable workflow** - register it in the Knowledge Base, and find that people will query it more often.

job token runner flow

security implications by case

issue flow

![Diagram](Diagram.png)

## Workflow Model

There is a large variety of methods of modelling (describing) workflows. Most notably, for our purposes: CWL, Yadage, Luigi, Airflow (the latter chosen by ESA).

All of them refelct general scheme, treating workflows as functions:

* each workflow is a computable function. 
* a workflow has inputs (dependencies, requirements). The inputs are subject to a type system. 
* workflows can be composed from other workflows, following function composition rules

We also consider that

* workflow requirements, such as workflow runner version or execution environment, can be understood as a special kind of inputs.

In addition, we leverage workflows as first-order data type, allowing:

* workflow can be an input to another workflow, allowing for example "mapping" or "factorizing" workflows.
* workflow can be an output of another workflow, allowing dynamic workflow composition

## Provenance?

benefits of provenance include:


## Security implications of distributed analysis
