## Example of running on two UNIGE clusters

Department of Astronomy at UNIGE relies on two clusters local [LESTA] and university-level [Baobab]. Both use SLURM. Baobab supports Singularity, which is what we use here.


* Acquire token

ask someone (e.g. support@odahub.io).

* Start the executor

```bash
$ oda-node runner start-executor \
    'bash -c "export -n partition; export batch_time=00:10:00; seq 1 3 > jobs; bao-submit-array ../integral-oda-worker/ jobid jobs"'  \
    'bao-squeue'  \
    --token my-oda-token
```
