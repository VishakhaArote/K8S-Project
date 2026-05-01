\# K8S-Project: Zero Trust Kubernetes Policy-as-Code Artefact



\## Dissertation Context



This repository contains the practical artefact for the Master's dissertation project:



\*\*Implementing Zero Trust in Multi-Tenant Kubernetes: A Policy-as-Code Approach for Enforcing Isolation and Least Privilege\*\*



\*\*Author:\*\* Vishakha Arote  

\*\*Programme:\*\* MSc Cyber Security  

\*\*Institution:\*\* Dublin Business School

\*\*Academic Year:\*\* 2025-2026  



This artefact supports the implementation, validation, results, and discussion sections of the dissertation. It demonstrates how Zero Trust principles can be applied to a multi-tenant Kubernetes environment using Kubernetes-native controls and Policy-as-Code mechanisms.



\## Project Overview



The project investigates security risks in a shared Kubernetes cluster where multiple tenant namespaces run workloads on the same infrastructure. The practical work first evaluates a baseline insecure configuration and then applies hardening controls to enforce tenant isolation, least privilege, admission control, and resource governance.



The artefact focuses on the following Zero Trust principles:



\- Deny by default

\- Explicitly verify access

\- Enforce least privilege

\- Apply policy consistently through code



\## Lab Environment



The experiments were conducted in a controlled educational lab environment using:



\- Amazon EKS

\- Kubernetes

\- AWS VPC CNI with NetworkPolicy enforcement

\- Kubernetes NetworkPolicy

\- Kubernetes RBAC

\- OPA Gatekeeper

\- ResourceQuota and LimitRange

\- Istio lightweight profile for service mesh investigation



Two namespaces were used to represent separate tenants:



| Namespace | Purpose |

|---|---|

| `tenant-a` | Attacker or compromised workload namespace |

| `tenant-b` | Protected tenant namespace containing the target service and simulated sensitive data |



All sensitive data used in this repository is simulated and created only for educational testing.



\## Repository Structure



```text

environment/             Baseline tenant workloads and simulated sensitive configuration

attacks/                 YAML manifests used to reproduce baseline attack scenarios

policies/                Hardening controls grouped by policy type

&#x20; network/               Kubernetes NetworkPolicy controls

&#x20; rbac/                  Least-privilege RBAC policies

&#x20; opa-gatekeeper/        OPA Gatekeeper admission control policies

&#x20; resource-governance/   ResourceQuota and LimitRange controls

istio-investigation/     Istio service mesh investigation files and findings

validation/              Before/after validation notes and attack-control mapping

evidence/                Command outputs and screenshots used as practical evidence

docs/                    Ethical scope, limitations, and setup notes

architecture/            Architecture notes or diagram placeholder

