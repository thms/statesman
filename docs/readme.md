## Statesman: A Ruby State Machine Library

**Repo:** [https://github.com/state-machine/statesman](https://github.com/state-machine/statesman)

**Author:** [thms](https://github.com/thms)

**Description:** Statesman is a Ruby library that provides a simple and flexible way to implement state machines in your Ruby applications. It is designed to be easy to use and extend, and it can be used with a variety of different data storage mechanisms.

**API:**

* **Statesman::Machine:** The main class for defining state machines.
    * **state(name, options = { initial: false }):** Defines a state in the state machine.
    * **transition(options = { from: nil, to: nil }, event = nil):** Defines a transition between states.
    * **before_transition(options = { from: nil, to: nil }, &block):** Defines a callback that is executed before a transition.
    * **guard_transition(options = { from: nil, to: nil }, &block):** Defines a guard that is executed before a transition.
    * **after_transition(options = { from: nil, to: nil, after_commit: false }, &block):** Defines a callback that is executed after a transition.
    * **event(name, &block):** Defines an event that can trigger a transition.
    * **current_state:** Returns the current state of the state machine.
    * **allowed_transitions:** Returns a list of allowed transitions from the current state.
    * **last_transition:** Returns the last transition that was executed.
    * **can_transition_to?(new_state, metadata = {}):** Checks if the state machine can transition to the given state.
    * **transition_to!(new_state, metadata = {}):** Transitions the state machine to the given state.
    * **trigger!(event_name, metadata = {}):** Triggers the given event.
    * **transition_to(new_state, metadata = {}):** Transitions the state machine to the given state, returning false if the transition fails.
    * **trigger(event_name, metadata = {}):** Triggers the given event, returning false if the transition fails.
    * **available_events:** Returns a list of available events for the current state.

* **Statesman::Callback:** The base class for callbacks and guards.
    * **call(*args):** Executes the callback.
    * **applies_to?(options = { from: nil, to: nil }):** Checks if the callback applies to the given transition.

* **Statesman::Guard:** A subclass of Statesman::Callback that represents a guard.

**Data Model:**

* **Statesman::Adapters::MemoryTransition:** A simple in-memory transition class.
* **Statesman::Adapters::ActiveRecordTransition:** A transition class that uses ActiveRecord to store transitions.
* **Statesman::Adapters::MongoidTransition:** A transition class that uses Mongoid to store transitions.

**Business Logic:**

* **Statesman::Machine:** The main class for defining state machines. It provides the logic for defining states, transitions, callbacks, and guards. It also provides methods for transitioning between states, triggering events, and checking if a transition is allowed.

**Events Consumed:**

* None

**Events Published:**

* None

**Example Usage:**

```ruby
class Order
  include Statesman::Machine

  state :pending, initial: true
  state :shipped
  state :delivered

  transition from: :pending, to: :shipped
  transition from: :shipped, to: :delivered

  after_transition from: :pending, to: :shipped do |order, transition|
    # Send a shipping notification email
  end
end

order = Order.new
order.current_state # => "pending"
order.transition_to!(:shipped)
order.current_state # => "shipped"
```

**Note:** This README is based on the codebase provided in the context. It may not be complete or accurate if the codebase is incomplete or has changed.
