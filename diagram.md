```mermaid
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
