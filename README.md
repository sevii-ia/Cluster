# Cluster

Kubernetes cluster configuration and deployment setup using **Minikube** and **VirtualBox**.
This repository contains scripts, manifests, and configuration files required to provision a local Kubernetes environment for development and testing purposes.

---

## Table of Contents

* [Overview](#overview)
* [Project Structure](#project-structure)
* [Requirements](#requirements)
* [Installation](#installation)
* [Minikube Setup](#minikube-setup)
* [Kubernetes Manifests](#kubernetes-manifests)
* [Usage](#usage)
* [Troubleshooting](#troubleshooting)
* [Contributing](#contributing)
* [License](#license)

---

## Overview

This project helps automate the setup of a local Kubernetes cluster environment using:

* **Minikube**
* **VirtualBox**
* **Kubernetes manifests**
* **Shell automation scripts**

It is intended for:

* Local Kubernetes testing
* Learning Kubernetes fundamentals
* Development sandbox environments
* CI/CD experimentation

---

## Project Structure

```bash
.
├── LICENSE
├── Manifest.yaml
├── README.md
└── install_kubernetes.sh
```

### Files Description

| File                    | Description                                                  |
| ----------------------- | ------------------------------------------------------------ |
| `install_kubernetes.sh` | Script used to install and configure Kubernetes dependencies |
| `Manifest.yaml`         | Kubernetes deployment/service manifest                       |
| `README.md`             | Project documentation                                        |
| `LICENSE`               | Repository license                                           |

---

## Requirements

Before starting, ensure the following tools are installed:

### Required Software

* [VirtualBox](https://www.virtualbox.org/)
* [Kubectl](https://kubernetes.io/docs/tasks/tools/)
* [Minikube](https://minikube.sigs.k8s.io/docs/start/)

### Windows Users

Disable Hyper-V before using VirtualBox:

```powershell
dism.exe /Online /Disable-Feature:Microsoft-Hyper-V
```

Restart your machine after executing the command.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/sevii-ia/Cluster.git
cd Cluster
```

Make the installation script executable:

```bash
chmod +x install_kubernetes.sh
```

Run the installation script:

```bash
./install_kubernetes.sh
```

---

## Minikube Setup

Start Minikube with allocated resources:

```bash
minikube start --cpus=2 --memory=2gb --disk-size=10gb -p STEP
```

If using VirtualBox as the driver:

```bash
minikube start --driver=virtualbox
```

Verify cluster status:

```bash
kubectl cluster-info
kubectl get nodes
```

---

## Kubernetes Manifests

Apply Kubernetes resources using:

```bash
kubectl apply -f Manifest.yaml
```

Check deployed resources:

```bash
kubectl get all
```

---

## Usage

Typical workflow:

1. Install dependencies
2. Start Minikube
3. Apply manifests
4. Verify deployment
5. Access services

Example:

```bash
kubectl apply -f Manifest.yaml
kubectl get pods
kubectl get svc
```

---

## Troubleshooting

### Minikube fails to start

Try deleting the existing cluster:

```bash
minikube delete
```

Then recreate it:

```bash
minikube start --driver=virtualbox
```

---

### Kubectl cannot connect to cluster

Check context configuration:

```bash
kubectl config current-context
```

Restart Minikube if necessary:

```bash
minikube stop
minikube start
```

---

### VirtualBox driver issues

Ensure:

* Hyper-V is disabled
* VirtualBox is updated
* BIOS virtualization is enabled

---

## Contributing

Contributions are welcome.

To contribute:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to your branch
5. Open a Pull Request

---

## License

This project is licensed under the MIT License.

See the [LICENSE](LICENSE) file for more information.
