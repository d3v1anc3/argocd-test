# Talos Kubernetes Cluster Setup

## Setup

Creating a Talos test setup on a windows system with docker desktop.
- Download the Talos Command Line Tool.
  ```powershell
  Invoke-WebRequest -Uri "https://github.com/siderolabs/talos/releases/latest/download/talosctl-windows-amd64.exe" `
    -OutFile "$env:USERPROFILE\talosctl.exe"
  $env:PATH += ";$env:USERPROFILE"
  ```

### VMWare Environment

>⚠️ TODO

### Local Docker Desktop Environment
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

## References
- [Talos](https://www.talos.dev)