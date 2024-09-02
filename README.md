```mermaid
graph TD;
    %% Push Event
    A[Push Event] --> B{Branch is 'develop' or 'master'};

    %% Develop Branch Workflow
    B --> |develop| C[Trigger Build and Deploy Workflow];
    C --> D[Build];
    D --> E[Release Versioning];
    E --> F[Tag and Release Creation];
    F --> G[Deploy to Dev Environment];
    G --> H[Dev Environment Health Check];
    H --> I{Health Check Passed?};
    I --> |Yes| J[Skip Rollback];
    I --> |No| K[Rollback to Previous Release];

    %% Master Branch Workflow
    B --> |master| L[Trigger Build and Deploy Workflow];
    L --> M[Combined: Previous Deployment Status & Dev Environment Health Check];
    M --> N{Checks Passed?};
    N --> |Yes| O[Deploy to Prod];
    N --> |No| K;
    O --> P[Prod Environment Health Check];
    P --> Q{Prod Health Check Passed?};
    Q --> |Yes| J;
    Q --> |No| K;
