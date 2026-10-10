# Install Docker, kubectl, and KIND on Windows

## Prerequisites

- Windows 10/11 (64-bit)
- PowerShell
- Internet connection
- Windows Package Manager (`winget`)

Check `winget`:

```powershell
winget --version
```

If missing, install App Installer: https://apps.microsoft.com/detail/9nblggh4nns1

## Docker Desktop

Check installation and status:

```powershell
docker --version
docker info
docker run --rm hello-world
```

Install if missing: https://docs.docker.com/desktop/setup/install/windows-install/

Open Docker Desktop and wait for the engine to start. KIND requires Linux containers; Docker Desktop with WSL 2 is a common Windows setup.

## kubectl

Check installation:

```powershell
kubectl version --client
```

Install if missing:

```powershell
winget install -e --id Kubernetes.kubectl
```

Verify after installation:

```powershell
kubectl version --client
```

Documentation: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

## KIND (Kubernetes IN Docker)

Check installation:

```powershell
kind version
```

Install if missing:

```powershell
winget install -e --id Kubernetes.kind
```

Reopen PowerShell and verify:

```powershell
kind version
```

Documentation: https://kind.sigs.k8s.io/docs/user/quick-start/

Windows package: https://github.com/microsoft/winget-pkgs/tree/master/manifests/k/Kubernetes/kind

## Installation status checks

| Component | Command | Success indicator |
|---|---|---|
| winget | `winget --version` | Version appears |
| Docker CLI | `docker --version` | Docker version appears |
| Docker Engine | `docker info` | Server information appears without a daemon error |
| Docker container runtime | `docker run --rm hello-world` | `Hello from Docker!` appears |
| kubectl | `kubectl version --client` | Client version appears |
| KIND | `kind version` | KIND version appears |

## Troubleshooting

- `winget` not recognized: install/update App Installer and reopen PowerShell.
- `docker` not recognized: install Docker Desktop and reopen PowerShell.
- Docker daemon error: start Docker Desktop and wait for the engine.
- `kubectl` or `kind` not recognized: reopen PowerShell and check that installation completed.
- KIND cannot run: verify Docker Desktop is using Linux containers and the engine is running.

## Official references

- Docker Desktop for Windows: https://docs.docker.com/desktop/setup/install/windows-install/
- kubectl for Windows: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
- KIND quick start: https://kind.sigs.k8s.io/docs/user/quick-start/
- KIND Windows package: https://github.com/microsoft/winget-pkgs/tree/master/manifests/k/Kubernetes/kind
