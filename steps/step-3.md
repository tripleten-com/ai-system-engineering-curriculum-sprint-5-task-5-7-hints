# Step 3: Record the agent's events in the audit trail

## The idea

When a dispatcher asks "what did the agent do, and who said yes?", the answer has to come from the exception's audit trail, beside the worker's events. It can't come from the server's thread. The thread exists to resume a run. The trail is the record Coldline keeps with the exception, and people who weren't there read it later.

So the agent records eight events through the same audit store the worker uses. Three rules make the trail trustworthy:

- **Record what happened, not what was intended:** a decision is recorded when the approval point accepts it, not when the request goes out. A tool event follows the tool's result, so a turned-down call is a failure in the trail, not a call.
- **Record enough, and nothing more:** every record names its exception, its run and its step. The sink adds the time, and the trace when there is one. A record never carries a credential, and never the model's words: the trail records what Coldline did, not what the model said.
- **Record once:** `act` runs again from its start after a resume, so a request recorded before the pause would be recorded twice. Something has to recognize "this event, for this run and step, is already there".

The event names are the agent's own, kept in a module of yours. The platform's audit module is settled, and an inherited test pins the worker's six names.

> Covered in **Audit Logging and Data Handling**, in **Guarding Model Output and Personal Data**.

## What's expected

- The eight event names live in a module of yours, and `poe unit` still passes.
- Your event document lists the eight events, where each is recorded, and the fields each may carry.
- `poe audit-trail` with your exception id shows the worker's events, then the agent's.
- The approval script `poe demo` plays has this trail: each `agent_step` before its `action_proposed`, one `approval_requested` per pause, `approval_decided` before `tool_called`, and `run_finished` last.
- The token script's trail ends with `budget_exhausted`, then `run_finished`.
- A refused run's trail also ends with `run_finished`.
- Your trail command prints one run's records in order, given the exception id and the run id.
- `poe demo`'s summary shows the run's steps and tokens against the two budgets, and its events.

## When you're stuck

### An inherited test fails when you add the event names

<details><summary>Hint 1</summary>

Where did you add them? Read the banner at the top of that file.

</details>

<details><summary>Hint 2</summary>

Read the test that failed. What does it say the platform's event list must hold?

</details>

<details><summary>Hint 3</summary>

Declare your eight names in a module of your own, as the same kind of value. Then check in the shell that the audit sink accepts one of them.

</details>

### `approval_requested` appears twice for one pause

<details><summary>Hint 1</summary>

What happens to every line in `act` before `interrupt()` when the decision arrives?

</details>

<details><summary>Hint 2</summary>

If you move the record after the pause, what does a run that's still waiting show in its trail?

</details>

<details><summary>Hint 3</summary>

What identifies one event of one step of one run? Could the code that writes records recognize one that's already there?

</details>

<details><summary>Hint 4</summary>

The lesson offers two ways: a check in your code before you write the record, or a small store of your own around the supplied one. Ask what each one costs when a resume runs the node again, and what each needs to know. Then pick one, keep the request record before the pause, and write the choice into your event document.

</details>

### The trail shows `tool_called` for a call that failed

<details><summary>Hint 1</summary>

Which value decides which event you record: what the proposal asked for, or what the tool's result says?

</details>

<details><summary>Hint 2</summary>

Run your recovery script and read its trail. Is its turned-down call there as a failure, with its code?

</details>

<details><summary>Hint 3</summary>

Record the call event only for an opened result, carrying the review id. Record the failure event, carrying the code, for every other result.

</details>

### A record carries more than it should

<details><summary>Hint 1</summary>

Which fields does your document allow for that event?

</details>

<details><summary>Hint 2</summary>

Are you passing a whole object, such as the approval record or the proposal, to the audit call?

</details>

<details><summary>Hint 3</summary>

Pass only the listed fields, and have your recording code refuse any field the document doesn't list for that event.

</details>

### A refused or halted run's trail has no ending

<details><summary>Hint 1</summary>

Where do you record `run_finished`: only on the finish path?

</details>

<details><summary>Hint 2</summary>

Where does every run end, whichever way it ends?

</details>

<details><summary>Hint 3</summary>

Record it wherever the status stops being `running`: after the budget check, and after any handler.

</details>

### Your agent's records have no trace id

<details><summary>Hint 1</summary>

Where does the sink get the trace id from?

</details>

<details><summary>Hint 2</summary>

Does your agent server's process have a current trace when a node runs? Compare how the API and the worker set up tracing at startup.

</details>

<details><summary>Hint 3</summary>

Either set tracing up in the agent server, or leave it out. Whichever you do, write down what you found in your note's limits.

</details>

### The trail command shows other runs' records

<details><summary>Hint 1</summary>

The store reads a trail by exception. What in each record tells you which run wrote it?

</details>

<details><summary>Hint 2</summary>

Keep only the records whose details carry your run id, in the order they were stored.

</details>

<details><summary>Hint 3</summary>

Read the trail where the database is reachable, the way `poe audit-trail` does.

</details>
