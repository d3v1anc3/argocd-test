# Environment Setup

## Overview
We group applications by environment:
- **Infrastructure** – core cluster services, shared components.
- **Acceptance** – staging/test workloads.
- **Production** – live workloads.

## Project Rules

| Project        | Destinations Pattern         | Namespaces Allowed        |
|----------------|------------------------------|---------------------------|
| Infrastructure | `app-*-inf`                  | `ns-*-inf`, `kube-system` |
| Acceptance     | `app-*-acc`                  | `ns-*-acc`                |
| Production     | `app-*-prd`                  | `ns-*-prd`                |

## Diagram
![Environment Setup](<environment-setup.svg>)