## Example of running of INTEGRAL workflows

Department of Astronomy at UNIGE relies on two clusters local [LESTA] and university-level [Baobab]. Both use SLURM. Baobab supports Singularity, which is what we use here.

* Acquire token

ask someone (e.g. support@odahub.io).

* Requirements, to setup environment

Node manager to fetch workflows to compute and upload results (established facts of equivalence between DAG expressions and data references):

```bash
$ pip install oda-node
```

pipeline managent used for INTEGRAL:

```bash
$ pip install data-analysis 
```

To allow fetching INTEGRAL data:

```bash
$ pip install integral-data-morrow
```

* Execute a single task

```bash
oda-node runner execute
```

* Start the runner

Runner will discover unsolved tasks and lauch jobs whenever it is necessary.

```bash
$ oda-node runner start-executor \
    command-to-execute-runner
    command-to-return-list-of-runners  \
    --token my-oda-token
```

Example of INTEGRAL analysis at UNIGE:

```bash
$ oda-node runner start-executor \
    'bash -c "export -n partition; export batch_time=00:10:00; seq 1 3 > jobs; bao-submit-array ../integral-oda-worker/ jobid jobs"'  \
    'bao-squeue'  \
    --token my-oda-token
```
