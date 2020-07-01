# TU Libraries SolrCloud Ansible Role

[![Build Status](https://travis-ci.com/tulibraries/ansible-role-solrcloud.svg?branch=main)](https://travis-ci.com/tulibraries/ansible-role-solrcloud)

This Ansible role installs an Apache SolrCloud cluster on Centos 7 boxes. It expects Java (tested with Java 8) is installed and a Zookeeper install is running.

## Prerequisities

To execute this role:
- Ansible 2.8.1 was used to write + test this role
- Java 8 installed on hosts
- Zookeeper (standalone or cluster) running on known IPs
- Networking is setup to allow VMs in cluster to communicate with each other

## Testing

```
$ pipenv install -r test-requirements.txt --python 2.7
$ pipenv run molecule test
```

## Using in a Playbook

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

Inventory:

```
[solr]
solrcloud-stage-01 ansible_host=192.168.138.179
solrcloud-stage-02 ansible_host=192.168.156.231
solrcloud-stage-03 ansible_host=192.168.199.175
```

Then run the playbook:

```

- name: Solrcloud cluster setup
  hosts: solr
  sudo: yes
  roles:
    - role: solrcloud
```

## Variables

You need the following set in your playbook for your inventory(ies):
- zookeeper_hosts: `[zk_1_ip, zk_2_ip, zk_3_ip]` (an array of zookeeper host IPs; include ports if non-standard)
- solr_collections: `{ 'collection1': { 'shards': 1, 'replicas': 2, 'shards_per_node': 1 } }` (a dictionary of dictionaries for solrcloud collections to be created)
- solr_collections_template_path: `{{ playbook_dir }}/templates/collections/` (where the playbook can find the solr configs, in directories per collection defined above)
- solr_collections_transfer_mode: copy or synchronize - basically, copy or rsync the above collection configurations to the hosts for then loading to Zookeeper

Other Variables are defined in `defaults/main.yml`.
