# Kubernetes Multiple Config Merge

## Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Usage](#usage)
- [Result](#result)

## About <a name = "about"></a>

This playbook merges all the config files that you use for switch between kubernetes clusters.

## Getting Started <a name = "getting_started"></a>

Actually you can do this manually. But if you have 10 cluster you need to run the command below 10 times. What playbook does is read a folder that you save config files, and assign them in to variable. Then it merges them. Simple as that.

```
    KUBECONFIG=/home/{{ user }}/.kube/config:/home/{{ user }}/{{ item }} kubectl config view --flatten >> /tmp/config
    cp /tmp/config /home/{{ user }}/.kube/config
```

### Prerequisites

You need the following items to run this playbook

- ansible
- kubectl
- kubectx(optional)
- kubernetes config files

Also you should place your config files into yamlfiles directory. Structure should like this.
```
.
.
├── main.yml
├── README.md
└── yamlfiles
    ├── cluster1.yaml
    ├── cluster2.yaml
    └── cluster3.yaml

1 directory, 5 files
```
## Usage <a name = "usage"></a>

Place all your config files to a folder. Than simple run the playbook like below.
```
mkdir yamlfiles
cp *.yaml ./yamlfiles
export CONFIG_DIR=yamlfiles
ansible-playbook main.yml --extra-vars="user=$USER config_path=$CONFIG_DIR"
```

## Result <a name = "result"></a>

![Alt Text](./terminal.gif)