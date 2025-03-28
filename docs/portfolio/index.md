# Portfolio

## Case Studies

### RAG Chatbot with Single Webpage
???+ example "Research"
    **Category**: _AI Experimentation_

    **Technologies Used**: _OpenAI, Pinecone, LangChain_

    #### Concept
    I wanted to be able to provide an AI Knowledge Base for a Chatbot that could be easily implemented and prototyped. This was so that I could make a baseline implementation to enhance with client needs and apply to their specific use-case.

    #### Process
    ```mermaid
    graph LR
        subgraph Data Sources
            D1[Raw Website Data] -->|Process| D2[Filtered & Chunked Data]
            D2 -->|Embed| D3[Vector Embeddings]
        end

        subgraph Storage
            D3 -->|Store| VDB[(Pinecone Vector DB)]
        end

        subgraph Query Flow
            Q1[User Question] -->|Query| VDB
            VDB -->|Context| Q2[Enhanced Question]
            Q2 -->|Process| Q3[GPT-4 Response]
        end

        style D1 fill:#f9f9f9,stroke:#489FB5,stroke-width:2px
        style D2 fill:#f9f9f9,stroke:#489FB5,stroke-width:2px
        style D3 fill:#f9f9f9,stroke:#489FB5,stroke-width:2px
        style VDB fill:#f9f9f9,stroke:#489FB5,stroke-width:2px
        style Q1 fill:#f9f9f9,stroke:#489FB5,stroke-width:2px
        style Q2 fill:#f9f9f9,stroke:#489FB5,stroke-width:2px
        style Q3 fill:#f9f9f9,stroke:#489FB5,stroke-width:2px
    ```

    I took the idea that I had and templated the workflow using FlowiseAI. The no-code UI allowed me to experiment with how I wanted to source the information and make connections with the embeddings from OpenAI to the Pinecone vector DB. Using the VectorDB, I enhanced questions that were asked of the chatbot using the `gpt-4o-mini` model to give contextual information.

    #### Outcomes
    - I made a github repository with my base implementation that I can now showcase to people what high level prototyping can lead to
    - I learned about the efficacy that sanitizing the data and chunking it appropriately can have on the cost and token utilization when leveraging LLM Models

## Product Development

### Notification System Optimizations
??? abstract "Details"
    **Category**: _Software Engineering_

    **Technologies Used**: _Spring Boot, Java, Apache Kafka, Microsoft SQL Server, Kubernetes_
    
    ---
    #### Problem Statement
    The existing notification system was complex, obfuscated, and inconsistent. We needed a framework to standardize the creation of new notification types and their default behaviors within our system.

    #### Previous Architecture
    ```mermaid
    sequenceDiagram
        participant Timer
        participant Scheduler
        participant DB
        participant UserService
        participant NotificationService
        
        Note over Timer: Every 5 minutes
        Timer->>Scheduler: Trigger notification check
        Scheduler->>DB: Query events from last 5 minutes
        DB-->>Scheduler: Return recent events
        
        Scheduler->>UserService: Get all users
        UserService-->>Scheduler: Return user list
        
        loop For each event
            Scheduler->>UserService: Filter users by profile
            UserService-->>Scheduler: Return matching users
            
            loop For each matching user
                Scheduler->>NotificationService: Send notification
                NotificationService-->>Scheduler: Notification sent
            end
        end
    ```

    #### Issues
    The main issue with this implementation was not that it was inherently complex, but that we had so many notifications and this single service was bloated with a lot of timers that couldn't work for the company standards long term. The amount of code became un-maintainable and features were easily lost on what was being used and what wasn't being used. Finally, if there was any change to one notification setup, it would affect all other notifications within the product.

    #### Implementation
    I had created a new Spring Boot application that leveraged events streamed through Apache Kafka to then get user notification profiles and send a notification to them based on their existing preferences. 

    #### New Architecture
    ```mermaid
    sequenceDiagram
        participant EventSource
        participant Kafka
        participant NotificationProcessor
        participant UserService
        participant NotificationService
        
        EventSource->>Kafka: Publish event with user data
        Kafka->>NotificationProcessor: Stream event
        NotificationProcessor->>UserService: Get user notification profile
        UserService-->>NotificationProcessor: Return profile preferences
        NotificationProcessor->>NotificationService: Send notification based on profile
        NotificationService-->>NotificationProcessor: Notification sent
        
        Note over EventSource,Kafka: Event-driven architecture
        Note over NotificationProcessor: Single responsibility per processor
    ```

    ---
    #### Value Provided
    The new architecture enabled easy expansion of notification types and eliminated duplicates through Apache Camel routing and the Idempotent Consumer pattern. This provided developers with clear documentation of upstream event sources and their relationships with our notification system.

    - I was able to reduce the existing complexities within the notification system by making a template for new notifications to be built upon.
    - I reduced the number of unused notifications in the system from a legacy application.
    - Removed the reliance on a legacy application which wasn't on the current deployment standards.

