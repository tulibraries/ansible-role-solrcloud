# SolrCloud & Zookeeper Ansible role

This Ansible role installs an Apache ZooKeeper & SolrCloud services in a Centos 7 environment.

### Prerequisities

To execute this role:
- Ansible 2.5.5 version installed.

### Testing


```sh
$ pipenv install -r test-requirements.txt --python 2.7
$ pipenv run molecule test
```

### Using in a Playbook

Create or add to your roles dependency file (e.g requirements.yml):

```
- src: tulibraries.ansible-role-solrcloud
  name: solrcloud
```

Install the role with ansible-galaxy command:

```
ansible-galaxy install -r requirements.yml
```

## Usage

To set multiple versions

```
zookeeper_hosts:
  - host: zookeeper1
    id: 1
  - host: zookeeper2
    id: 2
  - host: zookeeper3
    id: 3
```
