# ADR02 GitOps als deploymentstrategie voor Kubernetes

| Status    | Draft                                          |
| --------- | ---------------------------------------------- |
| Authors   | [Rob van der Velden](rob@nforza.nl) |
| Reviewers |                                                |
| Date      | 2025-11-10                                     |

## Context

## Opties
### CI/CD
Een CI/CD‑aanpak integreert geautomatiseerde build‑, test‑ en deploy‑pipelines die wijzigingen direct naar het Kubernetes‑cluster doorvoeren zodra alle kwaliteitscontroles zijn doorlopen. Dit maakt snelle en consistente oplevering en korte feedbackloops mogelijk, maar vereist robuuste pipeline‑tools en beveiligingsmaatregelen.

### GitOps
GitOps gebruikt een Git‑repository als `single source of truth` voor zowel applicatiecode als omgevingsconfiguratie. Wijzigingen worden via pull requests uitgevoerd en automatisch gesynchroniseerd met het Kubernetes‑cluster door een operator. Dit zorgt voor declaratieve, versiebeheer‑gestuurde deployments en vergroot de traceerbaarheid voor audits.

### Handmatig
Kubernetes‑manifests en directe commando's worden rechtstreeks toegepast op de cluster (bijv. via kubectl apply). Dit kan snel zijn voor kleine wijzigingen of experimenten, maar is gevoelig voor menselijke fouten, mist herhaalbaarheid en maakt auditing of terugdraaien moeilijker.

## Argumenten
Door alle cluster‑manifests in Git op te slaan als `single source of truth`, kunnen we workloads en configuraties snel beheren en herstellen door eenvoudigweg de inhoud van de repository toe te passen — een cruciaal voordeel voor disaster recovery. Om dit te realiseren, zullen we een GitOps‑gebaseerde deploymentstrategie aannemen als onze primaire methode voor het beheren en toepassen van workloads in Kubernetes.  

CI/CD‑pipelines blijven verantwoordelijk voor het bouwen, testen en publiceren van software‑artefacten. Een Kubernetes‑operator zal continu de gewenste toestand, gedefinieerd in een Git‑repository, synchroniseren met de actuele toestand van het cluster.

## Beslissing
We zullen GitOps gebruiken als deploymentstrategie voor Kubernetes.

## Consequenties
- Alle wijzigingen staan onder versiebeheer, worden via pull requests beoordeeld en zijn herleidbaar tot een commit, wat compliance en operationele transparantie verbetert.  
- Het declaratieve model zorgt ervoor dat de configuratie van het cluster consistent is in alle omgevingen en voorkomt configuratiedrift.  
- Deployment‑credentials blijven beperkt tot de GitOps‑operator in plaats van verspreid over CI/CD‑runners of de machines van ontwikkelaars.
- Efficiënte Disaster recovery door het snel kunnen herstellen van de clusterstaat via Git.
- Alle deployment‑wijzigingen moeten via Git‑commits en PR‑reviews verlopen, wat patches in noodgevallen kan vertragen.  
- Het deployment proces is afhankelijk van de beschikbaarheid en correcte werking van de GitOps‑operator.

## Referenties
- [DevOps - GitOps](https://en.wikipedia.org/wiki/DevOps#GitOps) - Wikipedia
- [CI/CD](https://en.wikipedia.org/wiki/CI/CD) - Wikipedia