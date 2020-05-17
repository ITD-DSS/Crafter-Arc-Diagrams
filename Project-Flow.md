# Crafter CMS ITD Architecture and Planning Diagrams

## Git Branching Model
**Brief** - The git branching model is important in the context of this project as it is pertinent to how all the systems interact and in what fashion and time. This unifies the project management schema across different departments and stakeholders and allows for maximum amounts of flexibility. An understanding of this model will be critical and so some recommended reading on the topic is 

## Environment Responsibilties

### DEV-STUDIO/ENGINE - Studio(4 Cores), Engine(4 Cores)
Project Repo Branch: Develop - Upstream updates(from Crafter), New Websites, In-House features, Bug Fixes
### STAGE-STUDIO/ENGINE
Project Repo Branch: Staging - Content Development, Site QA, Accessibility QA
## Project Workflow Entitys Diagram
To get and idea of how a proposed workflow would look and also to get a full end to end idea of all the pieces involved.

```mermaid
erDiagram
        GITHUB-PROJ-REPO }|..|{ DEV-STUDIO 
        GITHUB-PROJ-REPO ||--o{ PROD-STUDIO : "liable for"
        DELIVERY-ADDRESS ||--o{ ORDER : receives
        INVOICE ||--|{ ORDER : covers
        ORDER ||--|{ ORDER-ITEM : includes
        PRODUCT-CATEGORY ||--|{ PRODUCT : contains
        PRODUCT ||--o{ ORDER-ITEM : "ordered in"
```

## Development

```mermaid
erDiagram
        LOCAL-DEV )|--|( GITHUB-PROJ-REPO : Local Dev push project repos
```
        GITHUB-PROJ-REPO )|--|| STUDIO-DEV : 
        GITHUB-PROJ-REPO )|--|| STUDIO-STAGE : 
        GITHUB-PROJ-REPO )|--|| STUDIO-PROD :


<!-- ```mermaid
sequenceDiagram
    autonumber
    participant git as Github
    participant jnk as Jenkins
    participant studev as Studio-DEV
    participant engdev as Engine-DEV
    participant stustg as Studio-STAGE
    participant engstg as Engine-STAGE
    participant nodewrk as NodeJS-DEV/STAGE
    participant stuprod as Studio-PROD
    participant engprod as Engine-PROD
    participant nodeprod as NodeJS-PROD

    studev->>git: Initialize Site from Blueprint Repo or New Repo
```     -->
