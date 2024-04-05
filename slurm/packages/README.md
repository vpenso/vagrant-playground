# Test Custom Slurm Packages

## Local Repository

Test custom build Slurm RPMs…

- …by coping packages from `~/rpmbuild/RPMS/x86_64/` from the host
- …to `/localrepo` in the Vagrant instance

[`localrepo/Vagrantfile`](localrepo/Vagrantfile) performs the following configuration:

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

## Custom Repository

Configure a custom Yum repository storing Slurm packages by setting the
environment variable `SLURM_REPO`:

```bash
# Set the URL of the Yum RPM package with environment variable
export SLURM_REPO=$URL

# …before starting the VM instance
vagrant up
```

[`custom/Vagrantfile`](custom/Vagrantfile) performs the following configuration:

- …Yum repository configured in `/etc/yum.repos.d/slurm-packages.repo`
- …very basic Slurm installation …running `slrumcltd` & `slurmd` alongside
- …`localhost` Slurm configured with [`slurm.conf`](slurm.conf)

```bash
# Prerequisites
systemctl disable --now firewalld
setenforce Permissive
dnf install -y epel-release
dnf config-manager --set-enabled powertools

# Configure the custom Slurm package repository
cat > /etc/yum.repos.d/slurm-packages.repo <EOF
[slurm-packages]
name = slurm-packages
baseurl = $SLURM_REPO
enabled = 1
gpgcheck = 0
EOF

# Configure MUINGE authentication service
dnf install -y munge
echo 123456789123456781234567812345678 > /etc/munge/munge.key
chown munge:munge /etc/munge/munge.key
chmod 600 /etc/munge/munge.key
systemctl enable --now munge

# Create a slurm user with environment
groupadd slurm --gid 900
useradd slurm --system --gid 900 --shell /bin/bash \
        --no-create-home --home-dir /var/lib/slurm \
        --comment "SLURM workload manager"
mkdir -p /etc/slurm /var/{lib,log,run}/slurm /var/spool/slurm/{d,ctld}
chown slurm --recursive /var/lib/slurm /var/spool/slurm 
chgrp slurm --recursive /var/lib/slurm /var/spool/slurm 

dnf install -y slurm-slurmctld slurm-slurmd
# use the `slurm.conf` example
ln -sf /vagrant/slurm.conf /etc/slurm/slurm.conf
systemctl restart slurmctld slurmd
```

