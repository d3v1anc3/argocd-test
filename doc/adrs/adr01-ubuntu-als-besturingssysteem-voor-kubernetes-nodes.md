# ADR01 Ubuntu als besturingssysteem voor Kubernetes‑nodes.

| Status    | Draft                                          |
| --------- | ---------------------------------------------- |
| Authors   | [Rob van der Velden](rob@nforza.nl) |
| Reviewers |                                                |
| Date      | 2025-11-10                                     |

## Context
Voor het hosten van Kubernetes hebben we een Linux‑distributie nodig die stabiel is, goed wordt ondersteund en geoptimaliseerd is voor serverworkloads. 

## Opties
### Ubuntu Server (LTS version)
Veelgebruikt in Kubernetes‑omgevingen, met een sterke community en ondersteuning van Canonical, veel documentatie voor cloud‑ en containerworkloads.

### Ubuntu Server (Non‑LTS version)
Het bestaande cluster draait op Ubuntu 23.10. Dit is een Non-LTS Version. Met kortere ondersteuning (9 maanden levenscyclus). Snellere toegang tot nieuwe features en kernels, maar hogere upgradefrequentie en mogelijk minder stabiliteit. Deze versie van niet meer onder support sinds 11 July 2024.

### Debian
Een stabiel en betrouwbaar Linux‑besturingssysteem, bekend om zijn sterke community en langdurige ondersteuning.

### Talos
Een minimaal, niet‑wijzigbaar en veilig besturingssysteem, speciaal ontworpen om Kubernetes te draaien, volledig beheerd via een API zonder directe shell‑toegang.

### Alpine
Een compact, veilig en efficiënt besturingssysteem, populair voor servers en containers waar minimaal gebruik van middelen belangrijk is.

## Argumenten
Het tijdelijk blijven draaien op het huidige Ubuntu Server 23.10 cluster voorkomt directe migratiekosten, maar vereist een geplande upgrade.

Talos is een niet‑wijzigbaar, minimaal besturingssysteem dat speciaal is ontworpen voor Kubernetes, waardoor traditioneel pakketbeheer en OS‑configuratiebeheer niet meer nodig zijn. Dit ontwerp vermindert operationele belasting, verkleint het aanvalsoppervlak en zorgt ervoor dat nodes op een consistente en geautomatiseerde manier worden geconfigureerd en bijgewerkt. Door afwijkingen en overbodige componenten te elimineren, stelt Talos ons in staat onze operationele inspanningen te richten op de Kubernetes‑laag en applicatieworkloads in plaats van op het doorlopend onderhouden van het besturingssysteem.

## Beslissing
We zullen Ubuntu gebruiken als besturingssysteem voor Kubernetes-nodes.

## Consequenties
- Geen migratie kosten
- Mogelijke afwijkingen in instellingen waardoor systemen niet meer hetzelfde werken
- Kans op instabiliteit bij kernel- of package‑updates.
- Geen beveiligingspatches voor kernel, libraries of pakketten.
- Verhoogde kwetsbaarheid voor exploits en malware.
- Nieuwe applicaties ondersteunen mogelijk verouderde libraries niet, wat installatie of updates via officiële repositories bemoeilijkt.

### Na een eventuele upgrade naar Talos
- Reproduceerbare en consistente configuratie van alle nodes in het cluster. 
- Geen handmatig patchen, pakketupdates of configuratiedrift.  
- Verminderde kans op beveiligingslekken door een beperkte set services en componenten.
- Eenvoudigere compliance audits door een vergrendeld OS.
- API‑gebaseerde beheermodel in plaats van traditionele SSH‑ en CLI‑administratie.
- Minder community‑documentatie (vergeleken met Ubuntu/Debian)

## Referenties
- [Debian](https://www.debian.org) - Debian
- [Alpine](https://wwww.alpinelinux.org) - AlpineLinux
- [Talos](https://www.talos.dev) - Talos
- [Ubuntu Server](https://ubuntu.com/server) - Ubuntu
- [Ubuntu release cycle](https://ubuntu.com/about/release-cycle) - Ubuntu