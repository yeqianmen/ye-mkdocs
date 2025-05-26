

```bash
Show Pod Volumes and VolumeMounts in the cluster

Usage:
  kubectl-mounts [flags]
  kubectl-mounts [command]

Available Commands:
  completion  Generate completion script
  help        Help about any command

Flags:
  -h, --help                help for kubectl-mounts
  -k, --kubeconfig string   Path to kubeconfig file (default $HOME/.kube/config)
  -n, --namespace string    Namespace (default is current namespace)
  -o, --output string       Output format: table|yaml|json(default table)
  -p, --pod string          Filter by specific Pod name
  -v, --version             Show version

Use "kubectl-mounts [command] --help" for more information about a command.

```
Example output:

```pgsql
+-----------------------------------------+-----------------------------------+-----------------------------------+-----------------------------------------------+--------------------------------------------------+
|                   Pod                   |             Container             |            Volume Name            |                   MountPath                   |                   Volume Type                    |
+-----------------------------------------+-----------------------------------+-----------------------------------+-----------------------------------------------+--------------------------------------------------+
| default-flyflow-console-8d97c74f-mxmgp  | default-flyflow-console-container | default-flyflow-console-nginxconf | /conf                                         | ConfigMap(cm-default-flyflow-console-nagix.conf) |
+-----------------------------------------+-----------------------------------+-----------------------------------+-----------------------------------------------+--------------------------------------------------+
| hostpath-demo                           | busybox                           | host-volume                       | /data/host                                    | HostPath(/data)                                  |
+-----------------------------------------+-----------------------------------+-----------------------------------+-----------------------------------------------+--------------------------------------------------+
| mysql-operator-0                        | orchestrator                      | data                              | /var/lib/orchestrator                         | PVC(data-mysql-operator-0)                       |
+-----------------------------------------+-----------------------------------+-----------------------------------+-----------------------------------------------+--------------------------------------------------+
| nfs-client-provisioner-844c6c9489-pl8bn | nfs-client-provisioner            | nfs-client-root                   | /persistentvolumes                            | NFS(192.168.150.183:/data/nfs)                   |
+-----------------------------------------+-----------------------------------+-----------------------------------+-----------------------------------------------+--------------------------------------------------+
| nginx-0                                 | nginx                             | kube-api-access-vflg6             | /var/run/secrets/kubernetes.io/serviceaccount | ServiceAccountToken                              |
+-----------------------------------------+-----------------------------------+-----------------------------------+-----------------------------------------------+--------------------------------------------------+

                             
```
## Installation
### Homebrew

If you use Homebrew you can install like this:
```bash
brew tap yeqianmen/kubectl-mounts
brew install kubectl-mounts
```

### Using Krew (kubectl Plugin Manager)

If you use kubectl and have Krew installed, you can install Kelper as a kubectl plugin:
```bash
kubectl krew install --manifest-url https://github.com/yeqianmen/kubectl-mounts/releases/download/v0.1.1/mounts.yaml
```


### Build manually

```bash
git clone https://github.com/yeqianmen/kubectl-mounts.git
cd kubectl-mounts
go build -o kubectl-mounts
sudo mv kubectl-mounts /usr/local/bin/
```

## Completion

Supported Completions
- -n: Auto-completes available namespaces in the cluster

- -p: Auto-completes pod names in the selected namespace

- -o: Supports table, yaml, and json formats
 
### Bash

Load completion for current session:
```bash
source <(kubectl-mounts completion bash)
```
### Zsh

Load completion for current session:
```bash
source <(kubectl-mounts completion zsh)
```

