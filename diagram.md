sequenceDiagram
    participant Client
    participant APIGateway as "API Gateway"
    participant AuthorizerLambda as "Authorizer Lambda"
    participant MainLambda as "Main Lambda"
    participant Axway
    participant Salesforce

    Client->>APIGateway: 1. Send request (with token)
    APIGateway->>AuthorizerLambda: 2. Authorize request
    AuthorizerLambda-->>APIGateway: 3. Return IAM policy
    APIGateway->>MainLambda: 4. Invoke Main Lambda (if authorized)
    MainLambda->>Axway: 5. Send or enqueue payload (Salesforce data)
    Axway->>Salesforce: 6. Query/Update Salesforce
    Salesforce-->>Axway: 7. Return results
    Axway-->>MainLambda: 8. Return results/status
    MainLambda-->>APIGateway: 9. Send response
    APIGateway-->>Client: 10. Return final response

%% Style each participant
style Client fill:#E6F7FF,stroke:#006699,stroke-width:1px
style APIGateway fill:#FFFBE6,stroke:#999900,stroke-width:1px
style AuthorizerLambda fill:#E6FFE6,stroke:#339933,stroke-width:1px
style MainLambda fill:#ECE6FF,stroke:#663399,stroke-width:1px
style Axway fill:#FFECEC,stroke:#CC0033,stroke-width:1px
style Salesforce fill:#FFF0E6,stroke:#CC6600,stroke-width:1px
