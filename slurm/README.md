Single node Slurm [^f9hgz] test environment configured with  [`slurm.conf`](slurm.conf)

[^f9hgz]: Slurm Project, SchedMD  
<https://slurm.schedmd.com/>  
<https://github.com/SchedMD/slurm>

Custom Slurm RPM package repository in `/etc/yum.repos.d/slurm-packages.repo`

```bash
# set the URL of the Yum RPM package repository for Slurm packages
export SLURM_REPO=https://...
```
