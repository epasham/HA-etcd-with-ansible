# Deploy High Availability etcd cluster with Ansible.

## Prerequisites

Before you begin, you need to install all these tools:
- [Ansible (at least the version 2.8)](https://www.ansible.com/)
- [Vagrant](https://www.vagrantup.com/)
- [Virtualbox](https://www.virtualbox.org/wiki/Downloads)


## Configuration

* The PKI directory is defined in `group_vars/all`
* etcd version is defined in `roles/etcd/defaults/main.yaml`

## Deployment

1. Create the PKI infrastructure:
```bash
$ ansible-playbook pki.yaml
```

2. Deploy Etcd cluster:
```bash
$ ansible-playbook etcd.yaml
```

## Verification

Run the following command to get the health status of the cluster
```bash
$ vagrant ssh etcd3 -c "ETCD_VER=v3.3.13 etcdctl --cert-file /etc/etcd/etcd3-server.crt --key-file /etc/etcd/etcd3-server.key --ca-file /etc/etcd/server-ca.crt cluster-health"

member 2cba54b8e3ba988a is healthy: got healthy result from https://10.0.0.103:2379
member 7c12135a398849e3 is healthy: got healthy result from https://10.0.0.102:2379
member f2fd0c12369e0d75 is healthy: got healthy result from https://10.0.0.101:2379
cluster is healthy

```

## License
The source code in this repo is licenced under the GPL 3
