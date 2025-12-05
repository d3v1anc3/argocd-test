# Architecture

## Context
![Xenox Kubernetes Context Diagram](<Xenox Kubernetes Context Diagram.svg>)

## Container
![Xenox Kubernetes Container Diagram](<Xenox Kubernetes Container Diagram.svg>)

### How Argo-CD manages the cluster configuration
1. Argo-CD loads its own configuration from the git repository.
2. Argo-CD loads the application manifests, as specified in its own configuration, from the git repository.
3. Argo-CD applies the application manifests to the Kubernetes API.
4. The application gets installed, removed, or modified by Kubernetes.
