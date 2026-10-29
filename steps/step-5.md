# Step 5: Prove it with tests and write the evidence note

## The idea

Three claims need tests:

- **The budgets:** the check halts a run over either budget, with nothing written and nothing asked.
- **The trail:** it's complete and in order.
- **No credentials:** no record carries a credential or the model's words.

The budget check is a plain function, so its tests build a state and call it. The run tests build the graph the way your Task 6 tests do: an in-memory saver, the stand-in ports and the in-process tool. Give it one more replaceable piece, an audit store that keeps records in memory, so a test can read every record the run wrote.

Order tests are where weak tests hide. A test that only checks the trail isn't empty passes a trail with one event. A test that checks events exist, but not their order, passes a trail with the right events in the wrong order. Assert the sequence, and assert exactly one approval request per pause, so a doubled record after a resume fails too.

Pick the run that exercises the rule. The approval script's trail has no failed tool call, so it can't catch a run that records a call where a failure belongs. Your recovery run can.

For the credential test, read the token and secret values from their fixture files at test time. A value pasted into a test is a value in the repository.

> Covered in **CI Gates and Release Verification**.

## What's expected

- The budget tests cover four states and one bad file:
  - over steps
  - over tokens
  - over both, which halts with the step reason
  - within both, which comes back unchanged
  - a bad file, which is refused
- Each budget script, run in-process, ends halted with its reason, with no packet, no job and no approval request on the crossing step.
- The approval script's trail test asserts the full order and one request per pause.
- The recovery trail test asserts a failure event, not a call event, for the turned-down call.
- The credential test reads fixture values at test time and finds none of them in any record.
- You broke each group once and saw tests fail:
  - a budget check that never halts
  - a failed call recorded as a call
  - a doubled request
- `poe verify` and `poe demo` pass after your last edit.

## When you're stuck

### Breaking the tool events doesn't fail your order test

<details><summary>Hint 1</summary>

Which run's trail does your order test read?

</details>

<details><summary>Hint 2</summary>

Does that run ever have a tool call that fails?

</details>

<details><summary>Hint 3</summary>

Add an order test on your recovery run's trail, which has a turned-down call, and assert the failure event appears where the call was.

</details>

### A doubled `approval_requested` passes

<details><summary>Hint 1</summary>

Does your test count the records, or only check that one exists?

</details>

<details><summary>Hint 2</summary>

How many pauses does the run have? How many requests should the trail hold?

</details>

<details><summary>Hint 3</summary>

Assert the exact count, then remove your once-per-step protection and watch the test fail.

</details>

### Your tests can't see the records

<details><summary>Hint 1</summary>

Which audit store does the graph write to in your tests?

</details>

<details><summary>Hint 2</summary>

Could the test hand the graph a store that keeps records in a list?

</details>

<details><summary>Hint 3</summary>

Pass an in-memory store through the run configuration, the same way your tests pass the in-process tool, and read its list after the run.

</details>

### The credential test passes even with a token in a record

<details><summary>Hint 1</summary>

Where does the test get the value it searches for?

</details>

<details><summary>Hint 2</summary>

Is it the same value the code would write, read from the same fixture?

</details>

<details><summary>Hint 3</summary>

Put a fixture token into one record on purpose and run the test. If it still passes, the test is searching for the wrong thing.

</details>

### The budget tests pass even with the check removed

<details><summary>Hint 1</summary>

What does each test assert: only that the run ended?

</details>

<details><summary>Hint 2</summary>

Does it check the status, the halt reason, and the absence of the packet, the job and the approval request?

</details>

<details><summary>Hint 3</summary>

Assert all five, then make the check return the state unchanged and watch the tests fail.

</details>
