# Step 2: Write the scripts that exhaust each budget

## The idea

Your check halts states you built by hand. Now it has to halt a run. A budget script plays the model you're guarding against: one that keeps proposing, and that would open a review on a later step if nothing stopped it.

Three ideas make a budget script prove something:

- **One budget per script:** the step script makes many cheap proposals and runs out of steps first. The token script makes a few expensive ones and runs out of tokens first. If one script crossed both at once, a check that ignored one budget would still pass.
- **A review waiting behind the limit:** the entry that would open a review sits right after the limit. If the check fails to halt, the review opens and the evidence shows it. That's what proves the halt had no side effect, not just that it happened.
- **Entries that keep the run going:** before the limit, every entry has to leave the run running without a side effect. A finish or a refusal would end the run early. Two kinds don't end it: an approval request the dispatcher approves, and a tool call the tool turns down because your authority configuration doesn't allow its input.

Every entry must still fit the contract. A malformed entry becomes a refusal and ends the run, which tests the emulator, not the budgets.

## What's expected

- Two scripts sit beside your others, one for each budget, each with a comment saying what it plays.
- Each script crosses exactly one budget. Add up its counts entry by entry to confirm.
- In each script, the entry that would open a review comes right after the limit.
- Run with your dev command on a fresh exception and approving every pause, each script halts on the first step over its limit, with `step_budget` or `token_budget`.
- After each run there's no review packet for that exception, no new review job, and no approval pause on the step that crossed the limit.

## When you're stuck

### Your budget script ends before it reaches the limit

<details><summary>Move 1</summary>

Read each entry before the limit. What does your graph do with that kind of proposal?

</details>

<details><summary>Move 2</summary>

Which proposals end a run, and which leave it running?

</details>

<details><summary>Move 3</summary>

A tool call your configuration doesn't allow is turned down by the tool, and the run goes on. Which values in your authority configuration could make a call well formed but not allowed?

</details>

<details><summary>Move 4</summary>

The approach: fill the entries before the limit with approval requests, approved by your dev command, and tool calls with a well-formed but disallowed input. Put the valid tool call right after the limit.

</details>

### The halt fires on the wrong budget

<details><summary>Move 1</summary>

Add up the script's counts entry by entry. Which limit does it cross first?

</details>

<details><summary>Move 2</summary>

Does it cross both on the same entry? The step budget wins a tie.

</details>

<details><summary>Move 3</summary>

Lower the token counts in the step script, or use fewer, larger entries in the token script, until each crosses only its own limit.

</details>

### You can't tell whether a review was blocked or just never asked for

<details><summary>Move 1</summary>

Where in your script is the entry that would open a review: before the limit, or after it?

</details>

<details><summary>Move 2</summary>

Would that entry succeed if the check didn't exist? Remove the check for one run and see.

</details>

<details><summary>Move 3</summary>

Put the valid tool call right after the limit, restore the check, and run again. The halt is now the only thing between the run and a review.

</details>

### The approval pause shows up in a halted run

<details><summary>Move 1</summary>

Which step crossed the limit?

</details>

<details><summary>Move 2</summary>

Did that step pause, or did earlier steps pause on the way there?

</details>

<details><summary>Move 3</summary>

Earlier pauses are expected. Only the crossing step must not pause. Read your output for that step alone.

</details>
