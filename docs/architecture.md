```mermaid
graph LR
    subgraph Statesman
        A[Config] --> B[Machine]
        B --> C[Adapters]
        C --> D[Memory]
        C --> E[ActiveRecord]
        C --> F[Mongoid]
        B --> G[Callback]
        B --> H[Guard]
        B --> I[EventTransitions]
    end
    subgraph Generators
        J[MigrationGenerator] --> K[GeneratorHelpers]
        L[ActiveRecordTransitionGenerator] --> K
        M[MongoidTransitionGenerator] --> K
    end
    subgraph Models
        N[MyMongoidModel] --> O[MyMongoidModelTransition]
        P[MyActiveRecordModel] --> Q[MyActiveRecordModelTransition]
    end
    subgraph Specs
        R[SpecHelper] --> S[SharedExamples]
        S --> T[AnAdapter]
        S --> U[AGenerator]
        V[ActiveRecordQueriesSpec] --> W[ActiveRecordQueries]
        X[MachineSpec] --> B
        Y[CallbackSpec] --> G
        Z[GuardSpec] --> H
        AA[ConfigSpec] --> A
    end
    subgraph Support
        AB[ActiveRecord]
        AC[Mongoid]
        AD[GeneratorsSharedExamples]
    end
    subgraph Templates
        AE[ActiveRecordTransitionModel.rb.erb]
        AF[MongoidTransitionModel.rb.erb]
        AG[UpdateMigration.rb.erb]
        AH[CreateMigration.rb.erb]
    end
    K --> AE
    K --> AF
    K --> AG
    K --> AH
    E --> W
    F --> W
    B --> X
    G --> Y
    H --> Z
    A --> AA
    AB --> P
    AC --> N
    AD --> U
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#f9f,stroke:#333,stroke-width:2px
    style C fill:#f9f,stroke:#333,stroke-width:2px
    style D fill:#f9f,stroke:#333,stroke-width:2px
    style E fill:#f9f,stroke:#333,stroke-width:2px
    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#f9f,stroke:#333,stroke-width:2px
    style H fill:#f9f,stroke:#333,stroke-width:2px
    style I fill:#f9f,stroke:#333,stroke-width:2px
    style J fill:#f9f,stroke:#333,stroke-width:2px
    style K fill:#f9f,stroke:#333,stroke-width:2px
    style L fill:#f9f,stroke:#333,stroke-width:2px
    style M fill:#f9f,stroke:#333,stroke-width:2px
    style N fill:#f9f,stroke:#333,stroke-width:2px
    style O fill:#f9f,stroke:#333,stroke-width:2px
    style P fill:#f9f,stroke:#333,stroke-width:2px
    style Q fill:#f9f,stroke:#333,stroke-width:2px
    style R fill:#f9f,stroke:#333,stroke-width:2px
    style S fill:#f9f,stroke:#333,stroke-width:2px
    style T fill:#f9f,stroke:#333,stroke-width:2px
    style U fill:#f9f,stroke:#333,stroke-width:2px
    style V fill:#f9f,stroke:#333,stroke-width:2px
    style W fill:#f9f,stroke:#333,stroke-width:2px
    style X fill:#f9f,stroke:#333,stroke-width:2px
    style Y fill:#f9f,stroke:#333,stroke-width:2px
    style Z fill:#f9f,stroke:#333,stroke-width:2px
    style AA fill:#f9f,stroke:#333,stroke-width:2px
    style AB fill:#f9f,stroke:#333,stroke-width:2px
    style AC fill:#f9f,stroke:#333,stroke-width:2px
    style AD fill:#f9f,stroke:#333,stroke-width:2px
    style AE fill:#f9f,stroke:#333,stroke-width:2px
    style AF fill:#f9f,stroke:#333,stroke-width:2px
    style AG fill:#f9f,stroke:#333,stroke-width:2px
    style AH fill:#f9f,stroke:#333,stroke-width:2px
```

**Explanation:**

* **Statesman:** The core library for managing state machines.
    * **Config:** Defines the storage adapter to use for transitions.
    * **Machine:** The main class for defining state machines.
    * **Adapters:** Provides different storage mechanisms for transitions (Memory, ActiveRecord, Mongoid).
    * **Callback:** Represents a callback function that can be triggered during state transitions.
    * **Guard:** Represents a guard condition that must be met before a transition can occur.
    * **EventTransitions:** Allows defining transitions triggered by specific events.
* **Generators:** Provides tools for generating code related to state machines.
    * **MigrationGenerator:** Generates migrations for adding Statesman attributes to existing transition models.
    * **ActiveRecordTransitionGenerator:** Generates an ActiveRecord-based transition model.
    * **MongoidTransitionGenerator:** Generates a Mongoid-based transition model.
    * **GeneratorHelpers:** Provides helper methods for generators.
* **Models:** Represents the data models used in the application.
    * **MyMongoidModel:** A Mongoid model with a state machine.
    * **MyMongoidModelTransition:** A Mongoid model representing transitions for `MyMongoidModel`.
    * **MyActiveRecordModel:** An ActiveRecord model with a state machine.
    * **MyActiveRecordModelTransition:** An ActiveRecord model representing transitions for `MyActiveRecordModel`.
* **Specs:** Contains unit tests for the codebase.
    * **SpecHelper:** Sets up the testing environment.
    * **SharedExamples:** Defines shared examples for testing adapters and generators.
    * **ActiveRecordQueriesSpec:** Tests the `ActiveRecordQueries` module for querying models based on their state.
    * **MachineSpec:** Tests the `Machine` class.
    * **CallbackSpec:** Tests the `Callback` class.
    * **GuardSpec:** Tests the `Guard` class.
    * **ConfigSpec:** Tests the `Config` class.
* **Support:** Provides helper files for testing.
    * **ActiveRecord:** Sets up the ActiveRecord environment for testing.
    * **Mongoid:** Sets up the Mongoid environment for testing.
    * **GeneratorsSharedExamples:** Defines shared examples for testing generators.
* **Templates:** Contains ERB templates used by generators.
    * **ActiveRecordTransitionModel.rb.erb:** Template for generating an ActiveRecord transition model.
    * **MongoidTransitionModel.rb.erb:** Template for generating a Mongoid transition model.
    * **UpdateMigration.rb.erb:** Template for generating a migration to update an existing transition model.
    * **CreateMigration.rb.erb:** Template for generating a migration to create a new transition model.

**Key Relationships:**

* **Machine** depends on **Adapters**, **Callback**, **Guard**, and **EventTransitions**.
* **Generators** depend on **GeneratorHelpers**.
* **Models** depend on **Statesman** for state machine functionality.
* **Specs** depend on **Statesman**, **Models**, and **Support** for testing.
* **Templates** are used by **Generators** to generate code.

This diagram provides a high-level overview of the codebase's architecture, highlighting the key components and their relationships. It can be used to understand the overall structure of the codebase and how different parts interact with each other.
