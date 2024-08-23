## Statesman: A Ruby State Machine Library

This README provides an overview of the Statesman library, a Ruby state machine library that allows you to define and manage state transitions for your objects.

### API

The Statesman library provides a simple and intuitive API for defining and managing state transitions.

**Defining a State Machine:**

```ruby
class Order
  include Statesman::Machine

  state :pending, initial: true
  state :processing
  state :shipped
  state :completed

  transition from: :pending, to: :processing
  transition from: :processing, to: :shipped
  transition from: :shipped, to: :completed

  # Define callbacks for state transitions
  before_transition from: :pending, to: :processing do |order|
    # Perform actions before transitioning to the 'processing' state
  end

  after_transition from: :processing, to: :shipped do |order|
    # Perform actions after transitioning to the 'shipped' state
  end

  # Define guards for state transitions
  guard_transition from: :pending, to: :processing do |order|
    # Return true if the transition is allowed, false otherwise
  end
end
```

**Using a State Machine:**

```ruby
order = Order.new
order.current_state # => "pending"

# Transition to the 'processing' state
order.transition_to!(:processing)
order.current_state # => "processing"

# Trigger an event to transition to the 'shipped' state
order.trigger!(:ship)
order.current_state # => "shipped"
```

### Data Model

Statesman uses a simple data model to store state transitions. The `statesman_transitions` table stores information about each transition, including:

* `to_state`: The state the object transitioned to.
* `sort_key`: A unique identifier for the transition.
* `metadata`: A hash containing additional information about the transition.

### Business Logic

Statesman provides the following business logic:

* **State Definition:** Define the possible states for your objects.
* **Transition Definition:** Define the allowed transitions between states.
* **State Transition:** Transition objects between states.
* **Event Triggering:** Trigger events to transition objects between states.
* **Callbacks:** Define actions to be performed before or after state transitions.
* **Guards:** Define conditions that must be met before a state transition can occur.

### Events Consumed

Statesman does not consume any external events.

### Events Published

Statesman does not publish any external events.

### Repository

The Statesman library is available on GitHub: [https://github.com/themsaid/statesman](https://github.com/themsaid/statesman)

### Timestamp

2023-10-27T15:34:12.882572+00:00
