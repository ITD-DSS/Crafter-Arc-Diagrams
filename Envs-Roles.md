# CrafterCMS/ITD Architecture Docs

## Git Branching Model
**Brief** - The git branching model is important in the context of this project as it is pertinent to how all the systems interact and in what fashion and time. This unifies the project management schema across different departments and stakeholders and allows for maximum amounts of flexibility. An understanding of this model will be critical and so some recommended reading on the topic is provided in the links below.

- [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [Gitflow Intro + HubFlow](https://datasift.github.io/gitflow/IntroducingGitFlow.html)
- [A Succesful Git Branching Model](https://nvie.com/posts/a-successful-git-branching-model/)

*Note:* All assumptions in these architrctural docs assume this branching model.
## Environments & Roles
**NOTE:** Envirnoment names in ALL CAPS

---



### GIT w/ DEV-OPS FEATURES 
#### Options
- Preferred: [Github Team Account](https://github.com/pricing) ($4 per/user per month) OR
- [Azure Repos + Pipelines](https://azure.microsoft.com/en-us/services/devops/repos/)
- TODO: More In-Depth Comparison of Github & Azure Repos
#### Roles
- Stores Crafter Site Configurations (No Secrets) - Content, Site Config, View Templates, Static Assets
- Gives access to Github `Actions` or `Azure-Pipelines` for DevOps management practices and integration with Jenkins.
- Tracking of Issues, Features, and Milestones for a more robust development and project management experience.
---
### JENKINS
**Brief** - Crafter CMS has great support for being able to configure automation scripts for the different environments and being that Jenkins already exists as a resource it seems like a natural intergration.
Get an idea of some of [Crafters scripts here](https://docs.craftercms.org/en/3.1/developers/projects/craftercms/index.html).
#### Roles
- Software Builds via Gradle
- Site Setups
- Upgrades
- Backups
- Acts as Git Agent
- Content/Envirnoment Syncs with Git
- NodeJS Production Site Builds
- Manifests all Build Environment Variables
---
### LOCAL-STUDIO/ENGINE - Local Kubernetes Setup + Local NodeJS
#### Git Branches
Sandbox: `develop`, and any lower branches NOT `staging` or `prod`
Publish To: `develop` only
- Only Merges/Squashes into *DEV-STUDIO/ENGINE*
- Local Dev Envirnoment Maintained via Git Repo.
#### Roles
- Local Development primarily for building site features
- Testing of Upstream updates
- Develop features locally
---
### DEV-STUDIO/ENGINE - Studio(4 Cores), Engine(4 Cores)
#### Git Branches
Sandbox: `develop`
Publish To: `staging` & `develop`
- Only Merges/Squashes into *STAGE-STUDIO/ENGINE* Sandbox Branch  
#### Roles
- Integrate Upstream updates(from Crafter)
- Content Development 
- Implement New Websites, Templates, and Components.
- Develop Integration Features
- Hot fixes OR Bug Fixes
---
### STAGE-STUDIO/ENGINE - Studio(4 Cores), Engine(4 Cores)
#### Git Branches
Sandbox: `staging` *OR `Release/<semver>` *OR `RC/<semver>` RC = (Release Candidate) *(TBD)*
Publish To: `master` OR `live` *(TBD)* `self` and `develop`
Project Repo Branch: 
- Only Merges/Squashes into *STAGE-STUDIO/ENGINE* Sandbox Branch
#### Roles
- Testing
- Site QA 
- Accessibility QA
- Intermediate Review
---
### PROD-STUDIO/ENGINE - Studio(4 Cores), Engine(8 Cores - 2 Envs)
#### Git Branches
Sandbox: `staging` *OR `Release/<semver>` *OR `RC/<semver>` RC = (Release Candidate) *(TBD)*
Published: `master` OR `live` *(TBD)*
- Only Receives Updates from *STAGE-STUDIO/ENGINE* Publish To Branch
#### Roles
- Serves production ready content directly via Crafter Engine 
- Serves as REST/GRAPHQL API for building static sites or PWA's 
- Acts as content endpoint for legacy apps integrations.
- Loads the Publish To content into RAM (as a working set) to warm up its cache
- performs content inheritance, access rules, etc. to deliver the content as API/etc. 
---
### DEV-STAGE-PROD/NODEJS - Connected to DEV/STAGE-STUDIO/ENGINE and PROD on JENKINS
**Brief** - The NodeJS environments serve as tooling for various frontend operations that cannot be achieved by Crafters JAVA based backend.
- Node v12.13.0 LTS 
#### Roles
- Hosts Frontend UI framework NUXT
- Static assets compilation and bundling
- Server Side Rendering & Client Side Hydration
- Static Site Generation
- Javascript based components
- GraphQL availabilty
- UI testing and Accessibility
- CSS management
---
### MONGO-DB-DEV/STAGING/PROD
**Brief** - This piece is needed to work with Crafter's Profile module attribute store that is needed for the GSA employees as content piece.
- Local Machine Mongo for dev.
- Local Mongo for **DEV** environment
- Networked for **STAGING**
- Networked for **PROD** of course.
- TODO: More Specifics on Local Env using Kubernetes and Mongo.
#### Roles
- Act as required piece for storage of profile data
- Potentially act as a backup location for Crafter Content
- Session data cookies or something similar.

