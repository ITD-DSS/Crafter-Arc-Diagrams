```mermaid
sequenceDiagram
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

    git->>jnk: Initialize Site
```    
