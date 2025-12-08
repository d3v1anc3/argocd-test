# ADR05 CloudNativePG als Postgres Operator

| Status    | Draft                                          |
| --------- | ---------------------------------------------- |
| Authors   | [Rob van der Velden](rob@nforza.nl) |
| Reviewers |                                                |
| Date      | 2025-11-10                                     |

## Context
PostgreSQL draaien in Kubernetes vereist aanzienlijke handmatige handelingen voor taken zoals initialisatie, configuratie, schalen, back-ups, replicatie-instellingen en het afhandelen van failover. Deze werkzaamheden zijn complex, foutgevoelig en lastig betrouwbaar te automatiseren met alleen ruwe manifests en Helm-charts. Een PostgreSQL-operator bundelt deze operationele kennis in Kubernetes-native workflows, biedt declaratief clusterbeheer en automatiseert lifecycle-taken. Dit vermindert het risico op menselijke fouten, zorgt voor consistentie en maakt het mogelijk onze PostgreSQL-implementaties te schalen en te herstellen in lijn met onze bredere Kubernetes-platformpraktijken.

## Opties
### Zalando PostgreSQL Operator
Automatiseert de uitrol en het lifecyclebeheer van PostgreSQL-clusters op Kubernetes. Legt de nadruk op eenvoud en GitOps-vriendelijke configuratie, ondersteunt hoge beschikbaarheid met streamingreplicatie, en biedt ingebouwde opties voor back-up en herstel, samen met naadloze failover. Integreert goed met Kubernetes-native tools en volgt een op CRD gebaseerde aanpak voor clusterdefinities.

### CloudNativePG 
Een open-source operator die volledig gericht is op native Kubernetes-integratie. Ontworpen volgens de principes en best practices van Kubernetes, ondersteunt geautomatiseerde provisioning, failover, point-in-time recovery en rolling updates. Wordt actief ontwikkeld, beschikt over krachtige replicatie- en disasterrecoveryfunctionaliteit, en streeft naar minimale afhankelijkheid van externe tools terwijl Kubernetes-primitieven optimaal worden benut.

### Crunchy Data PostgreSQL Operator
Biedt PostgreSQL-functionaliteit van enterprise-niveau op Kubernetes, met een sterke nadruk op betrouwbaarheid, beveiliging en compliance. Ondersteunt complexe topologieën, hoge beschikbaarheid, back-up/herstel, monitoring (via geïntegreerde Prometheus/Grafana) en geavanceerde replicatiefuncties. Wordt geleverd met uitgebreide hulpmiddelen voor clusterbeheer en kan integreren met zowel open-source als commerciële PostgreSQL-aanbiedingen van Crunchy.

## Argumenten
Wij hebben een PostgreSQL-beheeroplossing nodig die naadloos aansluit op een Kubernetes-omgeving en routinematige operationele taken, zoals provisioning, schalen, failover, back-ups en point-in-time recovery, automatiseert. De oplossing moet voldoen aan Kubernetes-native patronen om de operationele belasting te verminderen en het gebruik van externe systemen te vermijden die de uitrol en het onderhoud compliceren. Hoge beschikbaarheid en mogelijkheden voor disaster recovery zijn essentieel om de continuïteit van de dienstverlening te waarborgen, terwijl sterke community-activiteit of ondersteuning door een leverancier belangrijk is voor langdurige duurzaamheid. Onze workflows profiteren van declaratieve configuratie en GitOps-gebaseerde operaties, waardoor CRD-gebaseerde clusterdefinities en native orchestratie kernvereisten zijn.

## Beslissing
We zullen CloudNativePG gebruiken als Postgres operator.

## Consequenties
- Verminderde operationele complexiteit door automatisering van provisioning, schalen, failover en back-ups.  
- Verbeterde betrouwbaarheid en beschikbaarheid.  
- Consistent, herhaalbaar PostgreSQL-clusterbeheer in lijn met Kubernetes-native patronen.  
- Eenvoudige integratie met GitOps-workflows via declaratieve, op CRD gebaseerde configuraties.  
- Mogelijke beperkingen ten opzichte van maatwerkdeployments indien bepaalde geavanceerde configuraties of extensies niet worden ondersteund.  

## Referenties
- [Zalando PostgreSQL Operator](https://opensource.zalando.com/postgres-operator/) - Zalando
- [CloudNativePG](https://cloudnative-pg.io/) - CloudNativePG
- [Crunchy Data PostgreSQL Operator](https://access.crunchydata.com/documentation/postgres-operator/4.6.1/) - Crunchy Data