# Install Docker, kubectl, and KIND on Windows

A concise installation and installation-status guide for Windows 10/11 using PowerShell.

> Scope: This README covers installing and verifying tools only. It does **not** create a Kubernetes cluster or deploy applications.

## 1. Prerequisites

- Windows 10/11 (64-bit)
- Internet connection
- PowerShell or Windows Terminal
- Windows Package Manager (`winget`) for the commands below

Check whether `winget` is installed:

```powershell
winget --version
```

If it is missing, install/update **App Installer** from the Microsoft Store:
https://apps.microsoft.com/detail/9nblggh4nns1

## 2. Docker Desktop

### Check installation

```powershell
docker --version
docker info
docker run --rm hello-world
```

How to interpret the results:

- `docker --version` prints a version: Docker CLI is installed.
- `docker info` displays both Client and Server information without a daemon error: Docker Engine is running.
- `docker run --rm hello-world` prints `Hello from Docker!`: Docker can run a container.

### Install if missing

Official download and instructions:
https://docs.docker.com/desktop/setup/install/windows-install/

After installing, open Docker Desktop and wait for the engine to start. KIND needs Linux containers; Docker Desktop with its WSL 2 backend is a common Windows setup.

## 3. kubectl (Kubernetes command-line tool)

### Check installation

```powershell
kubectl version --client
Get-Command kubectl -ErrorAction SilentlyContinue
```

A client version and a command path indicate that `kubectl` is available.

### Install if missing

```powershell
winget install -e --id Kubernetes.kubectl
```

After installation, open a new PowerShell window and verify:

```powershell
kubectl version --client
Get-Command kubectl
```

Official documentation:
https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

## 4. KIND (Kubernetes IN Docker)

KIND runs Kubernetes nodes as Docker containers. Installing the KIND executable does not create a cluster.

### Check installation

```powershell
kind version
Get-Command kind -ErrorAction SilentlyContinue
```

If `kind version` prints a version, KIND is installed and available in PATH.

### Install if missing

```powershell
winget install -e --id Kubernetes.kind
```

Close and reopen PowerShell, then verify:

```powershell
kind version
Get-Command kind
```

Official KIND documentation:
https://kind.sigs.k8s.io/docs/user/quick-start/

Official KIND Windows package:
https://github.com/microsoft/winget-pkgs/tree/master/manifests/k/Kubernetes/kind

## 5. Check package-manager records (optional)

These commands check whether package records are listed by `winget`; they do not replace testing the actual commands.

```powershell
winget list --id Docker.DockerDesktop --exact
winget list --id Kubernetes.kubectl --exact
winget list --id Kubernetes.kind --exact
```

## 6. Installation status checklist

Use these commands to verify the tools:

| Component | Verification command | Success indicator |
|---|---|---|
| winget | `winget --version` | Version is printed |
| Docker CLI | `docker --version` | Docker version is printed |
| Docker Engine | `docker info` | Server information appears without a daemon error |
| Docker container runtime | `docker run --rm hello-world` | `Hello from Docker!` appears |
| kubectl | `kubectl version --client` | Client version is printed |
| KIND | `kind version` | KIND version is printed |

## 7. Troubleshooting

- **`winget` is not recognized:** install/update App Installer from the Microsoft Store, then reopen the terminal.
- **`docker` is not recognized:** install Docker Desktop and reopen PowerShell.
- **Docker daemon connection error:** start Docker Desktop and wait until the engine is running.
- **`kubectl` or `kind` is not recognized after installation:** reopen PowerShell; check `Get-Command kubectl` or `Get-Command kind`; confirm the installation completed and PATH is updated.
- **Docker works but KIND cannot run:** confirm Docker Desktop is using Linux containers and the Docker engine is running.

## 8. Important: no cluster creation in this guide

This README intentionally does not include commands such as:

```powershell
kind create cluster
```

No Kubernetes cluster is created by following the installation and verification steps above.

## Official references

- Docker Desktop for Windows: https://docs.docker.com/desktop/setup/install/windows-install/
- kubectl on Windows: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
- KIND quick start and installation: https://kind.sigs.k8s.io/docs/user/quick-start/
- KIND Windows package manifest: https://github.com/microsoft/winget-pkgs/tree/master/manifests/k/Kubernetes/kind
