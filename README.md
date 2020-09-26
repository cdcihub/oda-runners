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
* **Empower your requests with your own hardware**, computing selected (by you) and verified (by instrument expects whom you trust anyway) analysis workflows. The analysis will store the high-level products in shared provenance-based cache, accelerating similar workflows for the community. **Community will see your contribution, will be grateful, and requested to acknowledge it**.
* **Join your own service - a remotely computable workflow** - register it in the Knowledge Base, and find that people will query it more often.
* Perhaps even **join your computing resources to provide spare computing power to other users**, **community will be very grateful and requested to acknowlage your contribution**

## Ways of connecting a federated resource

### Anonymous (Job Token) runner

### Job runners

### Session runners

### User runners

### Group runners

security implications by case

issue flow

![Diagram](Diagram.png)


## Credits

we loose uniqueness credits by providing the capacity to reduce data with a click of a button

compute contributors loose credit since their resources are leveraged for common good without clear attribution

## Layering data storage (cache)

## Dealing with exceptions

## Considerations of resource optimization: network vs store vs compute

* Analysis Exceptions
* Unhandled Exceptions

## Scheduling to the data: worker capacities

## Communicating Distributed Workflows

* *How do we organize communication in the federation, e.g. between the platform and the workers?*

It would be preferable to use a popular languages, interfaces to describe tasks (workflows) and data.  Unfortunately, there is not a universal format. 
Instead, a large variety of methods of modelling (describing) workflows. Most notably, for our purposes: CWL, Yadage, Luigi, Airflow (the latter chosen by ESA).
CWL comes close to being a universal langauge.

All of them reflect general scheme, treating workflows as functions:

* each workflow is a computable function. 
* a workflow has inputs (dependencies, requirements). The inputs are subject to a type system. 
* workflows can be composed from other workflows, following function composition rules

We also consider that

* workflow requirements, such as workflow runner version or execution environment, can be understood as a special kind of inputs.

In addition, we leverage workflows as first-order data type, allowing:

* workflow can be an input to another workflow, allowing for example "mapping" or "factorizing" workflows.
* workflow can be an output of another workflow, allowing dynamic workflow composition

Dynamic workflow composition is vital for expressing the workflows conciesly. In particular, it can be used to compose the workflow from a set of relations, described in modules, by merging graphs. 

Finally, we use RDF:

* each workflow is identified by an URI (resolvable)
* RDF relations are used to describe the workflows (output, inputs, and their types)

an example of such a definition, for a real case of ISGRI (see also https://github.com/volodymyrss/dda-ddosa/):

```
ii_skyimage:
  BinEventsImage:
    ScWData
      066500110010.001  
  CatExtract:
    ScWData:
      066500110010.001  
```
In a simplified notation, skipping the common namespace. For example, full id of `ii_skyimage` is ddosa:ii_skyimage or http://odahub.io/workflows/dda/ddosa/ii_skyimage. 

the above workflow which is dynamically composed from:

```
expand:
  target:
    ii_skyimage
  modules:  
  - ddosa
  assumptions:
  - ScWData:
      066500110010.001  
```

and is eventually computed to be equiavalent to:

```
data:
  ii_skyimage-066500110010.001
```

Note that all details needed to actually compute a given workflow (e.g. types, cwl, container name, etc) are hidden, and cab be extracted using the URI. The scheme instead represents purely the relation between the analysis processes.



## Provenance?

benefits of provenance are numerous, see XX for details.


## Security implications of distributed analysis
