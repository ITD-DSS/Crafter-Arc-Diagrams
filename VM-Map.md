# CrafterCMS/ITD Architecture Docs
## Virtual Machine Layout

### Requirements for ALL VM's
Each ENV (DEV, STAGE, PROD) MUST have:

- SSH Connection to Managed Git Repos
- SSH Connection to Jenkins for Automation scripts
- SSH for STUDIO to DELIVERY Git Deployments
- SSO Authentication AD groups
- SSL/TLS Certificates

### DEV/STAGE 16 CORES
#### Networking
- SSO Endpoint - Internal-Only
- SSH Jenkins - Internal-Only
- GIT-SSH - OUT/IN - Github
#### Notes: 
- Supports BOTH DEV and STAGE environments.
- Ideally even though on the same machine, separating them into different Linux namespaces would be helpful for process isolation.
- They don't need to talk directly. Only via DevOps processes.
- SSH connections to managed GitHub Account

**Namespace Suggestions**
- *DEV-STUDIO
- *STAGE-STUDIO
- *DEV-DELIVERY
- *STAGE-DELIVERY

```mermaid
graph TB
    classDef devBg fill:LemonChiffon;
    subgraph devstage [DEV/STAGE 16 CORES]
    dev-s[(DEV-STUDIO 4 CORES)]
    dev-e[(DEV-ENGINE 4 CORES)]
    stage-s[(STAGE-STUDIO 4 CORES)]
    stage-e[(STAGE-ENGINE 4 CORES)]
    dev-s-->dev-e
    stage-s-->stage-e
    end
    class devstage devBg;
```

### PROD-STUDIO 4-CORES
#### Networking
- SSO Endpoint - IN
- SSH Jenkins - IN
- GIT-SSH - OUT/IN
#### Notes:
- Environment that will be public for regular use by department content authoring teams.
- This will be the environment that supports delivering content directly to production.

```mermaid
flowchart TB
    prod-s[(PROD-STUDIO 4-CORES)]
```
### PROD-ENGINEs 8-CORES
#### Networking
- Public-IP - OUT
- SSH Jenkins - IN
- GIT-SSH - To PROD-STUDIO
#### Notes:
- These two environments will be used to serve static files to a CDN
- Used as a GRAPHQL/REST Endpoint Server
- Serves as a Content Cache
- Serves Any kind of resource needed for production
 
```mermaid
flowchart TB
    prod-e1[(PROD-ENGINE-1 4 CORES)]
```
```mermaid
flowchart TB
    prod-e2[(PROD-ENGINE-1 4 CORES)]
    
```
