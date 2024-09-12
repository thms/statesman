```
# High-Level Architecture Diagram for Statesman Codebase

## Overview
The Statesman codebase is a Ruby library for managing state machines and transitions. It supports different storage adapters like ActiveRecord and Mongoid, and provides a mechanism for defining states, transitions, callbacks, and guards.

## Diagram

```plaintext
+--------------------------------------------------+
|                    Statesman                     |
| +----------------------------------------------+ |
| |                 Machine                      | |
| | +------------------------------------------+ | |
| | | States                                  | | |
| | | Events                                  | | |
| | | Successors                              | | |
| | | Callbacks                               | | |
| | +------------------------------------------+ | |
| |                                              | |
| | +------------------------------------------+ | |
| | | Adapters                                | | |
| | | +--------------------------------------+ | | |
| | | | ActiveRecord                         | | | |
| | | | +----------------------------------+ | | | |
| | | | | ActiveRecordTransition          | | | | |
| | | | | ActiveRecordQueries             | | | | |
| | | | +----------------------------------+ | | | |
| | | +--------------------------------------+ | | |
| | | +--------------------------------------+ | | |
| | | | Mongoid                             | | | |
| | | | +----------------------------------+ | | | |
| | | | | MongoidTransition                | | | | |
| | | | +----------------------------------+ | | | |
| | | +--------------------------------------+ | | |
| | | +--------------------------------------+ | | |
| | | | Memory                              | | | |
| | | | +----------------------------------+ | | | |
| | | | | MemoryTransition                 | | | | |
| | | | +----------------------------------+ | | | |
| | | +--------------------------------------+ | | |
| | +------------------------------------------+ | |
| +----------------------------------------------+ |
+--------------------------------------------------+
```

## Components Description

- **Statesman**: The main module that encapsulates the entire functionality of the library.
  - **Machine**: The core class that defines the state machine behavior, including states, events, successors, and callbacks.
    - **States**: A collection of all states defined in the state machine.
    - **Events**: A collection of events that can trigger transitions.
    - **Successors**: A mapping of states to their possible next states.
    - **Callbacks**: A collection of before, after, and guard callbacks associated with transitions.
  - **Adapters**: Modules that provide integration with different storage mechanisms.
    - **ActiveRecord**: Adapter for ActiveRecord ORM.
      - **ActiveRecordTransition**: Defines the behavior of transitions when using ActiveRecord.
      - **ActiveRecordQueries**: Provides query methods for ActiveRecord models based on their states.
    - **Mongoid**: Adapter for Mongoid ODM.
      - **MongoidTransition**: Defines the behavior of transitions when using Mongoid.
    - **Memory**: Adapter for in-memory storage, useful for testing.
      - **MemoryTransition**: Defines the behavior of transitions when using in-memory storage.

Note: The diagram is a simplified representation of the Statesman codebase architecture, focusing on the main components and their relationships.
```
