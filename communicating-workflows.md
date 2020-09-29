# Communicating Distributed Workflows

* *How do we organize communication in the federation, e.g. between the platform and the workers?*


It would be preferable to use a popular languages, interfaces to describe tasks (workflows) and data.  Unfortunately, there is not a universal format. 
Instead, a large variety of methods of modelling (describing) workflows. Most notably, for our purposes: CWL, Yadage, Luigi, Snakemake, Airflow (the latter chosen by ESA).
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
In a simplified notation, skipping the common namespace. For example, full id of `ii_skyimage` is ddosa:ii_skyimage or http://odahub.io/workflows/dda/ddosa/ii_skyimage and https://github.com/volodymyrss/integral-workflow-scheme/.

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


> **What? Another workflow definition langauge??**
> We really do not want to invent another language. But we prefer to follow the phylosophy which allows a diversity of languages and communcation formats, as long as as their conversion to known standards is defined. In fact, we see the value of this description expressed through possibility of translating it to well-estalibshed languages.
> Hence we prefer to consider our workflow description a kind of a **pseudo-code**.

See also: 
