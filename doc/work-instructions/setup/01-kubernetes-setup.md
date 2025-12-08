# Kubernetes Setup

## Current production configuration
Ubuntu Linux VM's have been provisioned on VMWare. The setup io this configurations is not part of this documentation.

## Alternatives
Alternative setups are provided to support different needs beyond the current production configuration. These options allow for improved security, operational efficiency, or easier local development and testing, depending on the use case.

### Talos
We recommended Talos for Kubernetes clusters. It’s a minimal, immutable, and secure operating system purpose‑built for running Kubernetes. It eliminates unnecessary components, reducing attack surface and operational overhead. Its declarative, API‑driven management simplifies lifecycle tasks like upgrades and scaling, ensuring consistency across nodes. By removing traditional SSH access and mutable state, Talos enhances security and reliability, making it ideal for production‑grade, automated Kubernetes environments.

#### VMWare 

>⚠️ TODO

#### Local Docker Desktop Environment
Creating a Talos test setup on a windows system with docker desktop.
- Download the Talos Command Line Tool.
  ```powershell
  Invoke-WebRequest -Uri "https://github.com/siderolabs/talos/releases/latest/download/talosctl-windows-amd64.exe" `
    -OutFile "$env:USERPROFILE\talosctl.exe"
  $env:PATH += ";$env:USERPROFILE"
  ```
- Create the cluster
  ```powershell
  talosctl cluster create --provisioner docker --name taloslab --workers 2 
  ```

- Add the Talos cluster to your local kubectl config.
  ```powershell
  talosctl kubeconfig --nodes 10.5.0.2 --talosconfig "$HOME\.talos\config" --force
  ```
  When running Talos on docker, the kubectl config point to an internal docker ip that is not reachable by kubectl. To fix this:
    - List the running docker containers
        ```powershell
        docker ps
        ```
        ```text
        CONTAINER ID   IMAGE                                 COMMAND                  CREATED             STATUS                  PORTS                                                                                                         NAMES
        4f41e092983b   ghcr.io/siderolabs/talos:v1.11.3      "/sbin/init"             About an hour ago   Up About an hour                                                                                                                      taloslab-worker-2
        65af3d7c892c   ghcr.io/siderolabs/talos:v1.11.3      "/sbin/init"             About an hour ago   Up About an hour                                                                                                                      taloslab-worker-1
        b772a7af854b   ghcr.io/siderolabs/talos:v1.11.3      "/sbin/init"             About an hour ago   Up About an hour        0.0.0.0:52166->6443/tcp, 0.0.0.0:52167->50000/tcp                                                             taloslab-controlplane-1
        ```
    - Manually edit `~/.kube/config`. Replace the internal ip `10.5.0.2` with the external address, in this example `127.0.0.1:52166`

### Docker Desktop Kubernetes
For local development and testing, the Kubernetes option in Docker Desktop offers a quick, self‑contained environment. It enables running the ArgoCD setup without provisioning separate infrastructure, streamlining iteration and reducing setup time.

>⚠️ TODO

## References
- [What is Talos](https://docs.siderolabs.com/talos/v1.11/overview/what-is-talos) - SideroLabs