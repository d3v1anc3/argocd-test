# ADR04 Azure Key Vault als Secrets Management Solution voor Kubernetes

| Status    | Draft                                          |
| --------- | ---------------------------------------------- |
| Authors   | [Rob van der Velden](rob@nforza.nl) |
| Reviewers |                                                |
| Date      | 2025-11-10                                     |

## Context
We werken met gevoelige credentials, API‑sleutels en configuratiewaarden die cruciaal zijn voor de beveiliging van de systemen en data. Zonder een dedicated proces voor het beheer van geheimen bestaat het risico dat deze waarden hard‑gecodeerd in applicaties terechtkomen, worden opgeslagen in versiebeheer of zichtbaar worden in deployment‑pipelines — allemaal situaties die de kans op onbedoelde lekken of ongeautoriseerde toegang vergroten. 

## Opties
### HashiCorp Vault
Een zeer flexibel, open-source secret management tool dat secrets veilig opslaat, opent en distribueert. Vault ondersteunt dynamische secret, encryptie-als-een-service en fijnmazige toegangscontrole. Het kan integreren met Kubernetes via injectors of sidecars en zorgt ervoor dat secret niet opgeslagen hoeven te worden in broncode of CI/CD-pijplijnen.

### Azure Key Vault
Een cloud-native sleutelbeheersysteem van Microsoft Azure dat secrets, encryptiesleutels en certificaten opslaat. Het integreert met Azure-services en Kubernetes via CSI-drivers en biedt veilige, geauditeerde toegang tot secrets zonder deze in applicatiecode of git-repositories op te nemen.

### AWS Secrets Manager 
Een beheerde secrets-opslagdienst van AWS die veilige rotatie, beheer en ophalen van inloggegevens, tokens en API-sleutels mogelijk maakt. Integreert met AWS-services en Kubernetes-clusters die in AWS draaien, gebruikt IAM voor toegangscontrole en houdt secrets buiten deploy­m­ent­artefacten.

### Sealed Secrets 
Een Kubernetes-native oplossing die secrets versleutelt tot “SealedSecrets”-objecten, veilig om in git op te slaan. De versleuteling is asymmetrisch — alleen de controller van het cluster kan ze terug ontsleutelen naar Kubernetes Secret-objecten. Deze aanpak ondersteunt GitOps-workflows en houdt gewone tekstsecrets buiten repositories.

## Argumenten
Azure Key Vault sluit naadloos aan op de bestaande Azure-omgeving, waarin reeds gebruik gemaakt wordt van Azure Container Registry en Azure DevOps. Het biedt een volledig beheerde, cloud-native oplossing, waardoor we geen beheer- en back-upverantwoordelijkheden hebben voor een on-prem installatie. In tegenstelling tot Sealed Secrets worden secrets niet in git opgeslagen, wat onze beveiligingsrisico’s en compliance-zorgen vermindert. Integratie via CSI-drivers met Kubernetes maakt het beheer en de toegang tot secrets eenvoudig en veilig, met volledige auditmogelijkheden en zonder dat secrets in broncode of CI/CD-pijplijnen terechtkomen.

## Beslissing
We zullen Azure Key Vault gebruiken als Secrets Management Solution.

## Consequenties
- Alle secrets worden opgeslagen en beheerd in één veilig systeem  
- Voorkomt risico op ongewenste blootstelling via versiebeheer en deployment-pijplijnen  
- Ingebouwde auditlogs maken het mogelijk alle secret-toegang en -wijzigingen te volgen  
- Secrets kunnen tijdens runtime worden geïnjecteerd met Vault Agent of CSI-driver, zonder ze in manifests op te nemen  
- Apart hulpmiddel nodig voor opslag van gebruikerswachtwoorden — De oplossing richt zich op applicatie- en service-secrets, niet op gebruiksvriendelijke wachtwoordbeheer

## Referenties
- [Vault](https://www.hashicorp.com/en/products/vault) - HashiCorp
- [Azure Key Vault](https://azure.microsoft.com/en-us/products/key-vault/) - Microsoft
- [AWS Secrets Management](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) - Amazon Docs
- [Sealed Secrets](https://github.com/bitnami-labs/sealed-secrets) - GitHub