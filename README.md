# Install Docker, Kubernetes, kubectl, and KIND on Windows

Installation and status verification for Windows 10/11 using PowerShell. This guide does not create a Kubernetes cluster or deploy applications.

## 1. Prerequisites

- Windows 10/11 (64-bit)
- PowerShell or Windows Terminal
- Internet connection
- Windows Package Manager (`winget`)

Check `winget`:

```powershell
winget --version
```

If `winget` is missing, install or update App Installer:
https://apps.microsoft.com/detail/9nblggh4nns1

## 2. Docker Desktop

Docker Desktop provides the container engine used by KIND.

### Check installation and status

```powershell
docker --version
docker info
docker run --rm hello-world
```

Success indicators:
- `docker --version` prints a version.
- `docker info` shows Server information without a daemon error.
- `docker run --rm hello-world` prints `Hello from Docker!`.

### Install if missing

https://docs.docker.com/desktop/setup/install/windows-install/

Open Docker Desktop and wait for the engine to start. KIND requires Linux containers; Docker Desktop with WSL 2 is a common Windows setup.

## 3. Kubernetes

Kubernetes is a container orchestration system. In this guide, Kubernetes will run locally inside Docker containers managed by KIND. You do not install a separate Kubernetes server application directly on Windows.

The Kubernetes components are provided through the Kubernetes node image used by KIND when a cluster is created. This guide intentionally does not create a cluster, so Kubernetes itself is not yet running locally.

Official documentation:
https://kubernetes.io/docs/home/

## 4. kubectl

`kubectl` is the command-line tool used to communicate with and manage Kubernetes clusters.

### Check installation

```powershell
kubectl version --client
```

If a client version appears, `kubectl` is installed.

### Install if missing

```powershell
winget install -e --id Kubernetes.kubectl
```

Open a new PowerShell window and verify:

```powershell
kubectl version --client
```

Official documentation:
https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

## 5. KIND (Kubernetes IN Docker)

KIND runs local Kubernetes clusters using Docker containers. Installing KIND installs the command-line tool only; it does not create a cluster.

### Check installation

```powershell
kind version
```

If a version appears, KIND is installed.

### Install if missing

```powershell
winget install -e --id Kubernetes.kind
```

Close and reopen PowerShell, then verify:

```powershell
kind version
```

Official documentation:
https://kind.sigs.k8s.io/docs/user/quick-start/

KIND Windows package:
https://github.com/microsoft/winget-pkgs/tree/master/manifests/k/Kubernetes/kind

## 6. Installation status checklist

| Component | Check command | Success indicator |
|---|---|---|
| Windows Package Manager | `winget --version` | Version is printed |
| Docker CLI | `docker --version` | Docker version is printed |
| Docker Engine | `docker info` | Server information appears without a daemon error |
| Docker container runtime | `docker run --rm hello-world` | `Hello from Docker!` appears |
| Kubernetes | See note in Section 3 | Runs locally after a KIND cluster is created |
| kubectl | `kubectl version --client` | Client version is printed |
| KIND | `kind version` | KIND version is printed |

## 7. Troubleshooting

- **`winget` is not recognized:** install or update App Installer, then reopen PowerShell.
- **`docker` is not recognized:** install Docker Desktop and reopen PowerShell.
- **Docker daemon error:** start Docker Desktop and wait for the engine.
- **`kubectl` is not recognized:** install `kubectl` and reopen PowerShell.
- **`kind` is not recognized:** install KIND and reopen PowerShell.
- **KIND cannot use Docker:** ensure Docker Desktop is running and configured for Linux containers.

## Official references

- Docker Desktop for Windows: https://docs.docker.com/desktop/setup/install/windows-install/
- Kubernetes documentation: https://kubernetes.io/docs/home/
- kubectl for Windows: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
- KIND quick start: https://kind.sigs.k8s.io/docs/user/quick-start/
- KIND Windows package: https://github.com/microsoft/winget-pkgs/tree/master/manifests/k/Kubernetes/kind
