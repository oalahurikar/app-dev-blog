
Reference:
- https://www.youtube.com/watch?v=5OzLrbk82zY
- https://python-3-patterns-idioms-test.readthedocs.io/en/latest/StateMachine.html

Stateflow in python

I want to build my own stateflow python library from strach and along with learn the concept

What are applications of state machine and why and when use it

## Basic concepts
**State Representation**

```python
class State:
    def __init__(self, name):
        self.name = name
        self.transitions = {}
        self.on_entry = None
        self.on_exit = None
```

```python
class State:
    """
    Represents a state in the state machine.
    """
    def __init__(self, name):
        """
        Initializes a new State object.

        Args:
            name (str): The name of the state.
        """
        self.name = name  # The name of the state
        self.transitions = []  # List of transitions originating from this state

    def add_transition(self, transition):
        """
        Adds a transition to the state.

        Args:
            transition (Transition): The transition to add.
        """
        self.transitions.append(transition)

    def __str__(self):
        """
        Returns:
            str: The name of the state.
        """
        return self.name

class Transition:
    """
    Represents a transition between two states in the state machine.
    """
    def __init__(self, source, target, event):
        """
        Initializes a new Transition object.

        Args:
            source (State): The source state of the transition.
            target (State): The target state of the transition.
            event (str): The event that triggers the transition.
        """
        self.source = source  # The source state
        self.target = target  # The target state
        self.event = event  # The event triggering the transition

    def __str__(self):
        """
        Returns a string representation of the transition.

        Returns:
            str: A string describing the transition (e.g., "Idle --(Start)--> Running").
        """
        return f"{self.source} --({self.event})--> {self.target}"

class StateMachine:
    """
    Represents a state machine.
    """
    def __init__(self, initial_state):
        """
        Args:
            initial_state (State): The initial state of the state machine.
        """
        self.current_state = initial_state  # The current state of the machine

    def process_event(self, event):
        """
        Processes an event and transitions to the next state if a matching transition is found.

        Args:
            event (str): The event to process.
        """
        for transition in self.current_state.transitions:
            if transition.event == event:
                self.current_state = transition.target  # Update the current state
                print(f"Transitioning from {transition.source} to {transition.target} on event {event}")
                return  # Exit the loop after finding a match
        print(f"No transition found for event {event} in state {self.current_state}") # If no matching transition is found
```

Implementation of the state machine

```python
# Create states
state_idle = State("Idle")
state_running = State("Running")
state_paused = State("Paused")

# Create transitions
transition_idle_to_running = Transition(state_idle, state_running, "Start")
transition_running_to_paused = Transition(state_running, state_paused, "Pause")
transition_paused_to_running = Transition(state_paused, state_running, "Resume")
transition_running_to_idle = Transition(state_running, state_idle, "Stop")

# Add transitions to states
state_idle.add_transition(transition_idle_to_running)
state_running.add_transition(transition_running_to_paused)
state_running.add_transition(transition_running_to_idle)
state_paused.add_transition(transition_paused_to_running)

# Create state machine with initial state
state_machine = StateMachine(state_idle)

# Process events
state_machine.process_event("Start")
state_machine.process_event("Pause")
state_machine.process_event("Resume")
state_machine.process_event("Stop")
```

---

## Table-Driven State Machine


---

## Advance

Data Structure Options for States and Transitions

