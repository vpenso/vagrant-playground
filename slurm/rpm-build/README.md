Test custom build Slurm RPMs by coping packages from `~/rpmbuild/RPMS/x86_64/`
from the host to `/localrepo` in the Vagrant instance.
[`Vagrantfile`](Vagrantfile) performs the following configuration:

```bash
# Install Yum package repository tools
dnf install -y epel-release createrepo_c
dnf config-manager --set-enabled powertools

# Add a Yum repo configuration for packages in /localrepo
cat> /etc/yum.repos.d/local.repo <<EOF
local-repo]
name=local-repo
baseurl=/localrepo
enabled=1
metadata_expire=1d
gpgcheck=0
EOF

# Create the repository metadata and update the DNF cache
cd /localrepo && createrepo $PWD
dnf makecache -y
```

