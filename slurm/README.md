# Slurm Test Environments

sub-directories hold multiple different test-environments for the Slurm [^f9hgz]
workload management system use in HPC (High-Performance Computing).

[^f9hgz]: Slurm Project, SchedMD  
<https://slurm.schedmd.com/>  
<https://github.com/SchedMD/slurm>

Directory | Description
----------|--------------
`ansible` | Configuration of Slurm with Ansible
`cluster` | Dedicated `slurm{dbd,ctld}`, accounting database & multiple execution nodes
`packages`| Work with different custom build Slurm packages

