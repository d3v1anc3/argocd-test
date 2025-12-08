# ADR03 Argo CD als Configuratie Manager.

| Status    | Draft                                          |
| --------- | ---------------------------------------------- |
| Authors   | [Rob van der Velden](rob@nforza.nl) |
| Reviewers |                                                |
| Date      | 2025-11-10                                     |

## Context
In [ADR‑02](adr02-gitops-als-deploymentstrategie-voor-kubernetes.md) hebben we besloten een GitOps‑aanpak te gebruiken voor het beheren van Kubernetes‑workloads, waarbij Git‑repositories dienen als de enige bron van waarheid voor configuraties en deployments.  

Om deze beslissing operationeel te maken, hebben we een GitOps‑operator nodig die continu de clusterconfiguratie synchroniseert met Git‑repositories, configuratiedrift detecteert en integreert met  bestaande CI/CD‑workflows. De gekozen operator moet aansluiten bij onze schaalbaarheidsvereisten, beveiligingshouding, doelen voor ontwikkelaarservaring en de complexiteit van onze omgeving.

## Opties
### Argo CD
Een declaratieve, GitOps‑gebaseerde continuous‑deliverytool voor Kubernetes. Het systeem monitort continu Git‑repositories op wijzigingen in applicatiemanifests en past deze toe op doelclusters, en biedt een uitgebreide UI, CLI en API voor het visualiseren en beheren van applicatiedeployments.

### Flux CD
Een licht, Kubernetes‑native GitOps‑pakket dat de clusterconfiguratie synchroniseert met in Git opgeslagen configuratie, met de nadruk op eenvoud, uitbreidbaarheid en modulair ontwerp. Het maakt gebruik van controllers voor deployments, image‑updates en het afdwingen van beleid.

### Jenkins X
Een opinion‑gedreven Kubernetes‑CI/CD‑platform, gebouwd op Tekton‑pipelines, dat GitOps‑workflows ondersteunt door omgevingen en deployments te beheren via Git‑repositories. Het legt de nadruk op het automatiseren van build‑, test‑ en promotiestappen en integreert met populaire ontwikkeltools.

### Fleet
Een GitOps‑gestuurde beheertool van Rancher, ontworpen voor het uitrollen van workloads over grote aantallen Kubernetes‑clusters. Het schaalt tot duizenden clusters, synchroniseert resources vanuit Git‑repositories en biedt clustergroepering, multi‑tenancy en het afdwingen van beleid.

## Argumenten
Argo CD biedt een uitgebreide en volwassen GitOps‑oplossing, waarin krachtige visualisatie‑ en monitoringmogelijkheden worden gecombineerd met gestroomlijnd, applicatiegericht beheer over meerdere Kubernetes‑clusters. De rijke web‑UI en intuïtieve workflows verhogen zowel de productiviteit van ontwikkelaars als operators, doordat deploymentstatus, synchronisatiestatus en history direct toegankelijk zijn zonder diepgaande CLI‑kennis.  

Met brede ecosysteemondersteuning, actieve community‑ontwikkeling en bewezen inzet in productieomgevingen in uiteenlopende organisaties vormt Argo CD een robuuste en toekomstbestendige keuze. De geautomatiseerde detectie van configuratiedrift en de eenvoudige rollbackfunctionaliteit verlagen het operationele risico en versnellen het herstel bij problemen, terwijl centraal beheer één consistente control‑plane biedt voor deployments in alle omgevingen. Samen vergroten deze eigenschappen operationele efficiëntie, verlagen ze de beheerslast en versterken ze de betrouwbaarheid van onze opleveringen.

## Beslissing
We zullen Argo CD gebruiken voor het beheren van de Kubernetes configuratie.

## Consequenties
- Ontwikkelaars en operators kunnen de status van applicaties, synchronisatiestatus en wijzigingen monitoren, waardoor de tijd voor probleemoplossing wordt verkort.  
- Continue synchronisatie zorgt voor consistentie met de gewenste configuratie  
- Geautomatiseerde rollbacks maken snel herstel mogelijk van mislukte wijzigingen  
- Ingebouwde RBAC‑ en SSO‑integratie ondersteunen fijnmazige toegangscontrole  
- Ondersteunt Helm, Kustomize en standaardmanifests
- Eén centrale control‑plane voor het beheren van meerdere Kubernetes‑clusters  

## Referenties
- [Argo CD](https://argo-cd.readthedocs.io/) - Read the Docs
- [Flux CD](https://fluxcd.io/) - Flux CD
- [Jenkins X](https://jenkins-x.io/) - Jenkins-x
- [Fleet](https://fleet.rancher.io/) - Rancher
