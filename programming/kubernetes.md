# Kubernetes

Sources:

* [Bare Metal with K3s](https://blog.alexellis.io/bare-metal-kubernetes-with-k3s/)

## Installation

```bash
$ yay -S arkade-bin # for arch linux users
$ arkade get kubectl
$ arkade get k3sup
$ arkade get terraform
$ arkade get kubectx
```

Update `PATH`:

```
export PATH=$PATH:$HOME/.arkade/bin/
```

## Nodes

Use terraform to provision three servers and two agents. You can alter these numbers, but three is the minimum number required for K3s' built-in HA mode using etcd.

Save main.tfvars with the following:

```
terraform {
  required_providers {
    packet = {
      source = "terraform-providers/packet"
      version = "~> 3.2.1"
    }
  }
  required_version = ">= 0.13"
}

variable "api_token" {
  description = "Equinix Metal API token"
}

variable "project_id" {
  description = "Equinix Metal Project ID"
}

variable "servers" {
  description = "Count of servers"
}

variable "agents" {
  description = "Count of agents"
}

provider "packet" {
  auth_token=var.api_token
}

resource "packet_ssh_key" "key1" {
  name       = "k3sup-1"
  public_key = file("/home/alex/.ssh/id_rsa.pub")
}

resource "packet_device" "k3s-server" {
  count		         = var.servers
  hostname         = "k3s-server-${count.index+1}"
  plan             = "c1.small.x86"
  facilities       = ["ams1"]
  operating_system = "ubuntu_20_10"
  billing_cycle    = "hourly"
  project_id       = var.project_id
  depends_on       = [packet_ssh_key.key1]
}

resource "packet_device" "k3s-agent" {
  count 	         = var.agents
  hostname         = "k3s-agent-${count.index+1}"
  plan             = "c1.small.x86"
  facilities       = ["ams1"]
  operating_system = "ubuntu_20_10"
  billing_cycle    = "hourly"
  project_id       = var.project_id
  depends_on       = [packet_ssh_key.key1]
}

output "server_ips" {
  value = packet_device.k3s-server.*.access_public_ipv4
}

output "agent_ips" {
  value = packet_device.k3s-agent.*.access_public_ipv4
}
```
