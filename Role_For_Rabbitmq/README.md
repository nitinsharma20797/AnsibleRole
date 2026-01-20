

# Ansible Role for installing Rabbitmq

# Author Information

| Created by   | Created on  | Version | Last updated ON |  Reviewer    |
|--------------|------------|---------|----------------|----------------|
| Nitin Sharma | 20-01-2026 | V1.0    | 20-01-2026     | Shweta Tyagi  |

---

## Table of Content

* [Introduction](#introduction)
* [Pre-requisites](#pre-requisites)
* [Procedure](#procedure)
* [Conclusion](#conclusion)
* [FAQs](#faqs)
* [Contact Information](#contact-information)

---

## Introduction

This Ansible role installs and configures a **RabbitMQ cluster** with optional HA (high availability) support.  
It is OS-aware and works on both **Debian/Ubuntu** and **RHEL/CentOS 9** distributions.  

Key features:  

- Installs RabbitMQ and Erlang packages  
- Configures Erlang cookie for clustering  
- Sets up users and vhosts  
- Enables management plugin and cluster HA policy  
- Optional SSL support (future-ready)  
- Can be used for both development and production environments  

---

## Pre-requisites

| Resource                     | Description |
|-------------------------------|------------|
| Control Node OS               | A Linux machine (Ubuntu, RHEL, CentOS) with Ansible installed |
| Managed Nodes OS              | Ubuntu 22.04+, RHEL 9, or compatible Linux distribution |
| SSH Access                    | Passwordless SSH access from control node to all RabbitMQ nodes |
| Ansible                       | Version 2.9+ recommended |
| Python                        | Python 3 installed on all nodes (required by Ansible) |
| Package Management            | `apt` on Debian/Ubuntu, `dnf` on RHEL/CentOS |
| Hostname Resolution           | All nodes must resolve each other via `/etc/hosts` or DNS |
| Firewall / Ports              | Ports 5672 (AMQP), 15672 (Management), 25672 (Clustering) open between nodes |
| Sudo Privileges               | The SSH user should have passwordless sudo on managed nodes |
| RabbitMQ SSL Certificates     | Optional, only needed if `rabbitmq_ssl_enabled: true` is set |
| Internet Access               | Required to fetch RabbitMQ and Erlang packages (or local repo mirror) |

---

## Procedure


Clone the role repository

```bash
git clone <repo-url>
cd <repo-directory>
```

Update the inventory
Ensure your inventory file lists all RabbitMQ nodes with correct hostnames/IPs.

Run the common setup first
This will ensure that each node can resolve other nodes via /etc/hosts or SSH known hosts:

```bash
ansible-playbook -i inventory common.yml
```

Set variables

Defaults are in rabbitmq/defaults/main.yml

Change rabbitmq_erlang_cookie, rabbitmq_user, rabbitmq_password as needed

Optional SSL variables are already in defaults; enable later if certs are available.

Run the RabbitMQ role playbook
```bash
ansible-playbook -i inventory playbook.yml
```

To run only specific nodes:
```sh
ansible-playbook -i inventory playbook.yml --limit node3
```

Verify installation & clustering
On any node:
```sh
sudo rabbitmqctl cluster_status
sudo rabbitmqctl status
```

Ensure all nodes are running and part of the cluster

Check listeners and ports (5672, 15672, 25672)

Optional SSL setup

Currently commented out in tasks/ssl.yml

Place your certs in /etc/rabbitmq/ssl/ and set rabbitmq_ssl_enabled: true

Rerun the playbook to enable SSL

Access RabbitMQ management GUI

```sh
http://<node-ip>:15672
Username: admin
Password: Admin123
```

---

## Conclusion

This Ansible role provides a fully automated setup for a multi-node RabbitMQ cluster with:

Installation of RabbitMQ and Erlang on Debian and RHEL nodes

Configuration of Erlang cookies for clustering

Automatic creation of users, vhosts, and HA policies

Enabling the management plugin and verifying cluster status

Future-ready SSL support (optional)

By running common.yml first, all nodes can resolve each other and SSH connectivity is ensured, allowing seamless clustering. This role is idempotent—you can safely re-run the playbook without breaking the cluster.

---

## FAQs

**Q1: Can I run this playbook multiple times?**

**A1:** Yes, the role is idempotent. Re-running will ensure all configurations remain consistent without breaking the cluster.

**Q2: How do I enable SSL?**
**A2:** Place your SSL certificates in /etc/rabbitmq/ssl/ and set rabbitmq_ssl_enabled: true in defaults/main.yml. Re-run the playbook to apply SSL.

**Q3: What ports need to be open for this cluster?**
**A3:** Ensure the following ports are open between nodes:

5672 – AMQP

15672 – Management GUI

25672 – Clustering and CLI tools

**Q4: Can I add more nodes to the cluster later?**
**A4:** Yes, add the new node to the rabbitmq_nodes list in defaults/main.yml and rerun the playbook. The new node will join the cluster automatically.

**Q5: What if I face package download issues on RHEL nodes?**
**A5:** This usually occurs when the Erlang or RabbitMQ repo is unreachable. Verify connectivity and try later or configure a local repository mirror.

---

---

##  Contact Information

| Name | Email address |
| :--- | :------------ |
| Nitin Sharma  | nitin.sharma.snaatak@mygurukulam.co |

---



