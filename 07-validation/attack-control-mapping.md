\# Attack-to-Control Mapping



| Attack Scenario | Baseline Weakness | Control Implemented | Hardened Result |

|---|---|---|---|

| Cross-tenant service access | Tenant A accessed Tenant B service and received HTTP 200 OK | Default-deny NetworkPolicy | Connection timeout / blocked |

| Cross-tenant DNS discovery | Tenant A could resolve Tenant B service FQDN | NetworkPolicy restrictions and DNS control | Discovery restricted where policy applied |

| Privileged container | Privileged pod could be created | OPA Gatekeeper deny-privileged policy | Admission denied |

| HostPath mount | Pod could mount host filesystem | OPA Gatekeeper deny-hostpath policy | Admission denied |

| Secret exfiltration | Secret data could be retrieved and decoded | NetworkPolicy + RBAC | Timeout / HTTP 403 Forbidden |

| Unauthorized API access | Service account token could reach API server | NetworkPolicy + least-privilege RBAC | Timeout / HTTP 403 Forbidden |

| Resource abuse | CPU hog consumed nearly one CPU core | LimitRange + ResourceQuota | CPU capped at approximately 498m |

| RBAC misconfiguration | ClusterRoleBinding allowed cross-namespace visibility | Namespace-scoped RoleBinding | HTTP 403 Forbidden |

| Istio integration | Service mesh introduced additional control-plane dependency | Targeted control-plane NetworkPolicy exception | Operational limitation documented |

