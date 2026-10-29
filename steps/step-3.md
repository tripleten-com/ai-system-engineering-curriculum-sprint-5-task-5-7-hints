# Step 3: Record the agent's events in the audit trail

## An inherited test fails when you add the event names

<details><summary>Hint 1</summary>

Where did you add them? Read the banner at the top of that file and the test that failed.

</details>

<details><summary>Hint 2</summary>

Does the audit sink accept event names declared outside that file? Try one in the shell.

</details>

## `approval_requested` appears twice for one pause

<details><summary>Hint 1</summary>

What happens to every line in `act` before `interrupt()` when the decision arrives?

</details>

<details><summary>Hint 2</summary>

What would let the second run of the same step recognize that its record is already there? Think about what identifies one event of one step of one run.

</details>

## Your agent's records have no trace id

<details><summary>Hint 1</summary>

Where does the sink get the trace id from? Does your agent server's process have a current trace when a node runs?

</details>

<details><summary>Hint 2</summary>

Compare how the API and the worker set up tracing at startup with what your agent server does. Write down what you find, either way, in your evidence note.

</details>

## The trail shows `tool_called` for a call that failed

<details><summary>Hint 1</summary>

Which value decides which event you record: what the proposal asked for, or what the tool's result says?

</details>

## Your "success run" trail has no approval or tool events

<details><summary>Hint 1</summary>

Which script did you run? Does it ever propose a tool call? Which script does `poe demo` play?

</details>

## The trail command shows other runs' records

<details><summary>Hint 1</summary>

The store reads a trail by exception. What in each record tells you which run wrote it?

</details>
