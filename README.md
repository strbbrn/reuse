```mermaid
graph TD;
    %% Push Event
    A[Push Event]:::desc1 --> B{Branch is 'develop' or 'master'};

    %% Develop Branch Workflow
    B --> |develop| C[Trigger Build and Deploy Workflow]:::desc2
    C --> D[Build]:::desc3
    D --> E[Release Versioning]:::desc4
    E --> F[Tag and Release Creation]:::desc5
    F --> G[Deploy to Dev Environment]:::desc6
    G --> H[Dev Environment Health Check]:::desc7
    H --> I{Health Check Passed?}:::desc8
    I --> |Yes| J[Skip Rollback]:::desc9
    I --> |No| K[Rollback to Previous Release]:::desc10

    %% Master Branch Workflow
    B --> |master| L[Trigger Build and Deploy Workflow]:::desc2
    L --> M[Combined: Previous Deployment Status & Dev Environment Health Check]:::desc11
    M --> N{Checks Passed?}:::desc8
    N --> |Yes| O[Deploy to Prod]:::desc12
    N --> |No| K
    O --> P[Prod Environment Health Check]:::desc13
    P --> Q{Prod Health Check Passed?}:::desc14
    Q --> |Yes| J
    Q --> |No| K

    %% Descriptions
    click A callback "Push Event: This is triggered when code is pushed to the repository."
    click C callback "Trigger Build and Deploy Workflow: Initiates the build and deploy process."
    click D callback "Build: Compiles the code and prepares artifacts."
    click E callback "Release Versioning: Increments the version number for this release."
    click F callback "Tag and Release Creation: Creates a Git tag and formal release."
    click G callback "Deploy to Dev Environment: Deploys the build to the development environment."
    click H callback "Dev Environment Health Check: Verifies that the deployment was successful."
    click I callback "Health Check Passed?: Determines whether the health check passed or failed."
    click J callback "Skip Rollback: If the health check passes, no rollback is performed."
    click K callback "Rollback to Previous Release: If the health check fails, rolls back to the last known good release."
    click L callback "Trigger Build and Deploy Workflow (master): Same as for develop, but for the master branch."
    click M callback "Combined Check: Performs both the previous deployment status and dev environment health check."
    click O callback "Deploy to Prod: Deploys the build to the production environment."
    click P callback "Prod Environment Health Check: Verifies that the production deployment was successful."
    click Q callback "Prod Health Check Passed?: Determines whether the production health check passed or failed."

    classDef desc1 fill:#f96,stroke:#333,stroke-width:2px;
    classDef desc2 fill:#bbf,stroke:#333,stroke-width:2px;
    classDef desc3 fill:#dfd,stroke:#333,stroke-width:2px;
    classDef desc4 fill:#ffd,stroke:#333,stroke-width:2px;
    classDef desc5 fill:#dff,stroke:#333,stroke-width:2px;
    classDef desc6 fill:#fbb,stroke:#333,stroke-width:2px;
    classDef desc7 fill:#bfb,stroke:#333,stroke-width:2px;
    classDef desc8 fill:#ff9,stroke:#333,stroke-width:2px;
    classDef desc9 fill:#d9d,stroke:#333,stroke-width:2px;
    classDef desc10 fill:#fdd,stroke:#333,stroke-width:2px;
    classDef desc11 fill:#9fd,stroke:#333,stroke-width:2px;
    classDef desc12 fill:#cfc,stroke:#333,stroke-width:2px;
    classDef desc13 fill:#ccf,stroke:#333,stroke-width:2px;
    classDef desc14 fill:#ffc,stroke:#333,stroke-width:2px;
