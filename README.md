# K8S-Project: Zero Trust Kubernetes Policy-as-Code Artefact

## Project Title

**Implementing Zero Trust in Multi-Tenant Kubernetes: A Policy-as-Code Approach for Enforcing Isolation and Least Privilege**

## Dissertation Context

This repository contains the practical artefact developed for a Master's dissertation in MSc Cyber Security at Dublin Business School.

The artefact supports the implementation, validation, results, and discussion chapters of the dissertation by demonstrating how Zero Trust security principles can be applied to a multi-tenant Kubernetes environment using Kubernetes-native controls and Policy-as-Code mechanisms.

**Author:** Vishakha Arote  
**Programme:** MSc Cyber Security  
**Institution:** Dublin Business School  
**Academic Year:** 2025-2026  

## Project Overview

Kubernetes is widely used to host containerised applications, but multi-tenant clusters introduce security risks when workloads from different tenants share the same control plane and worker nodes. Without appropriate controls, a compromised pod may attempt lateral movement, unauthorised service access, API misuse, privileged execution, host filesystem access, or resource abuse.

This project investigates these risks in a controlled educational lab environment. A baseline insecure Kubernetes configuration was first created to demonstrate common attack scenarios. Security controls were then applied to harden the environment using a Zero Trust approach.

The final artefact demonstrates how Kubernetes NetworkPolicy, RBAC, OPA Gatekeeper, ResourceQuota, and LimitRange can be combined to enforce tenant isolation, least privilege, admission control, and resource governance.

Istio was also investigated as a potential service mesh enhancement. However, due to operational complexity and resource constraints in the test environment, Istio was treated as an operational finding rather than the primary enforcement mechanism.

## Zero Trust Principles Applied

The project applies the following Zero Trust principles:

- **Deny by default:** Network communication is blocked unless explicitly permitted.
- **Explicit verification:** Access to Kubernetes resources is validated through RBAC and policy enforcement.
- **Least privilege:** Service accounts and workloads are granted only the permissions required.
- **Assume breach:** The test environment assumes that a workload in one tenant namespace may be compromised.
- **Policy-as-Code:** Security controls are defined using declarative YAML manifests and OPA Gatekeeper policies.
- **Continuous validation:** Controls are tested before and after hardening to confirm effectiveness.

## Lab Environment

The experiments were carried out in a controlled cloud-based Kubernetes lab environment.

| Component | Description |
|---|---|
| Cloud Platform | Amazon Web Services |
| Kubernetes Platform | Amazon Elastic Kubernetes Service |
| Cluster Type | Multi-tenant Kubernetes test cluster |
| Network Plugin | AWS VPC CNI with NetworkPolicy support |
| Policy Enforcement | Kubernetes NetworkPolicy and OPA Gatekeeper |
| Access Control | Kubernetes RBAC |
| Resource Governance | ResourceQuota and LimitRange |
| Service Mesh Investigation | Istio lightweight profile |
| CLI Tools | kubectl, AWS CLI, istioctl |

Two tenant namespaces were used to represent separate tenants within the same cluster.

| Namespace | Purpose |
|---|---|
| `tenant-a` | Attacker or compromised workload namespace |
| `tenant-b` | Protected tenant namespace containing the target service |

All sensitive data used in this repository is simulated and created only for ethical educational testing.

## Attack Scenarios Evaluated

The project evaluated a series of controlled attack scenarios commonly associated with Kubernetes multi-tenant environments.

| Attack Scenario | Description | Control Used |
|---|---|---|
| Cross-tenant service access | A pod in `tenant-a` attempts to access a service in `tenant-b` | NetworkPolicy |
| Cross-tenant service discovery | A pod attempts DNS resolution of services in another namespace | DNS and network policy validation |
| Unauthorized Kubernetes API access | A pod attempts to access Kubernetes API resources using its service account token | RBAC and NetworkPolicy |
| Secret exfiltration attempt | A pod attempts to retrieve secrets from another namespace | RBAC |
| Privileged container deployment | A workload attempts to run with privileged container permissions | OPA Gatekeeper |
| HostPath mount attack | A workload attempts to mount host filesystem paths into the container | OPA Gatekeeper |
| Resource abuse | A CPU-intensive pod attempts to consume excessive cluster resources | ResourceQuota and LimitRange |
| Istio service mesh investigation | Service mesh deployment and sidecar behaviour were tested under strict policies | Operational finding |

## Hardening Controls Implemented

The artefact implements several layers of Kubernetes security controls.

### 1. Kubernetes NetworkPolicy

NetworkPolicy was used to enforce namespace-level segmentation. A default-deny approach was applied to tenant namespaces, followed by explicit allow rules for approved communication.

Controls included:

- Default deny ingress and egress policies
- DNS allow rules
- Controlled tenant-to-tenant service access
- Kubernetes API egress validation
- Istio control-plane communication exceptions during investigation

### 2. Kubernetes RBAC

RBAC was used to restrict what service accounts could access within the cluster.

The RBAC configuration supports least privilege by ensuring that attacker workloads cannot list or retrieve sensitive resources from other namespaces.

### 3. OPA Gatekeeper

OPA Gatekeeper was used as a Policy-as-Code admission controller. It prevents insecure workloads from being admitted into the cluster.

Policies included:

- Deny privileged containers
- Deny HostPath volume mounts
- Enforce admission-time security checks

### 4. ResourceQuota and LimitRange

Resource governance controls were applied to prevent a single tenant from exhausting shared cluster resources.

Controls included:

- CPU request and limit defaults
- Memory request and limit defaults
- Namespace-level resource quota
- Pod count limits

### 5. Istio Investigation

Istio was investigated for additional Zero Trust capabilities such as service-to-service security, sidecar-based traffic management, and potential mTLS enforcement.

The investigation showed that service mesh adoption introduces additional operational requirements, including:

- Increased CPU and memory requirements
- Sidecar injection complexity
- Need for control-plane communication exceptions
- Interaction with strict NetworkPolicy rules
- Additional troubleshooting overhead

As a result, Istio was documented as an operational finding and possible future enhancement rather than the main security enforcement mechanism.

## Repository Structure

```text
K8S-Project/
│
├── architecture/
│   └── Architecture diagrams and design notes
│
├── attacks/
│   └── Manifests used to reproduce baseline attack scenarios
│
│
├── environment/
│   └── Baseline tenant workloads and simulated sensitive configuration
│
│
├── istio-investigation/
│   └── Istio configuration files, lightweight profile, and operational findings
│
├── policies/
│   ├── network/
│   ├── rbac/
│   ├── opa-gatekeeper/
│   └── resource-governance/
│
│
├── .gitignore
└── README.md
