## Statesman: A Ruby State Machine Library

**Repo:** [https://github.com/state-machine/statesman](https://github.com/state-machine/statesman)

**Author:** thms

**Current Time (UTC):** 2023-10-27 09:58:11

**API:**

* **Statesman::Machine:** The main class for defining state machines.
    * **state(name, options = { initial: false }):** Defines a state.
    * **transition(options = { from: nil, to: nil }, event = nil):** Defines a transition between states.
    * **before_transition(options = { from: nil, to: nil }, &block):** Defines a callback to be executed before a transition.
    * **guard_transition(options = { from: nil, to: nil }, &block):** Defines a guard to be executed before a transition.
    * **after_transition(options = { from: nil, to: nil, after_commit: false }, &block):** Defines a callback to be executed after a transition.
    * **event(name, &block):** Defines an event that triggers a transition.
    * **current_state:** Returns the current state of the machine.
    * **allowed_transitions:** Returns a list of allowed transitions from the current state.
    * **last_transition:** Returns the last transition that occurred.
    * **can_transition_to?(new_state, metadata = {}):** Checks if the machine can transition to the given state.
    * **transition_to!(new_state, metadata = {}):** Transitions the machine to the given state.
    * **trigger!(event_name, metadata = {}):** Triggers the given event.
    * **transition_to(new_state, metadata = {}):** Transitions the machine to the given state, returning false if the transition fails.
    * **trigger(event_name, metadata = {}):** Triggers the given event, returning false if the transition fails.
    * **available_events:** Returns a list of available events for the current state.

**Data Model:**

* **Statesman::Adapters::MemoryTransition:** A simple in-memory transition object.
* **Statesman::Adapters::ActiveRecordTransition:** An ActiveRecord-based transition object.
* **Statesman::Adapters::MongoidTransition:** A Mongoid-based transition object.

**Business Logic:**

* **Statesman::Machine:** Implements the state machine logic, including:
    * State definition and validation.
    * Transition definition and validation.
    * Callback and guard execution.
    * Event triggering.
    * State change management.
* **Statesman::Adapters:** Provides different storage adapters for transition history:
    * **Memory:** Stores transitions in memory.
    * **ActiveRecord:** Stores transitions in an ActiveRecord table.
    * **Mongoid:** Stores transitions in a Mongoid collection.

**Events Consumed:**

* None

**Events Published:**

* None

**Example Usage:**

```ruby
class Order
  include Statesman::Machine

  state :pending, initial: true
  state :paid
  state :shipped

  transition from: :pending, to: :paid
  transition from: :paid, to: :shipped

  def pay!
    transition_to!(:paid)
  end

  def ship!
    transition_to!(:shipped)
  end
end

order = Order.new
order.current_state # => "pending"
order.pay!
order.current_state # => "paid"
order.ship!
order.current_state # => "shipped"
```
