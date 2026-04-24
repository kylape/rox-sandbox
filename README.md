# rox-sandbox

Ephemeral StackRox environments with KubeVirt VMs running KinD clusters.

## Quick Start

```bash
# Create a sandbox with StackRox 4.9.2
eval $(./hack/rox-sandbox create my-test 4.9.2)

# Access the cluster
kubectl get pods -n stackrox

# Clean up
./hack/rox-sandbox delete my-test
```

## Commands

| Command | Description |
|---------|-------------|
| `create <name> <version>` | Create sandbox, outputs env vars for eval |
| `delete <name>` | Delete sandbox and clean up |
| `list` | List active sandbox VMs |
| `status <name>` | Show sandbox status |
| `connect <name>` | Re-establish port-forward |
| `kubectl <name> <args>` | Run kubectl against sandbox |

## Requirements

* `roxctl` in PATH
* `helm` in PATH
* Access to KubeVirt namespace (`rox-sandbox`)

## Architecture

```
Host Cluster (OpenShift/ROSA)
└── KubeVirt VM (namespace: rox-sandbox)
    └── KinD Cluster (Podman-based)
        └── StackRox Central (helm)
```
