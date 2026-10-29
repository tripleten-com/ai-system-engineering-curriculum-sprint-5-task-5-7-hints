# Step 1: Write the budgets and the check that halts a run

## The idea

The review cap from Task 4 limits what a run may do: open one review. It says nothing about a run that never opens one. A model that keeps proposing, run after run of approval requests or tool calls the tool turns down, adds a step and more tokens every time, sits on the dispatcher's exception, and spends money for nothing. Budgets bound that activity whether or not a review ever opens.

A budget is a limit plus a check:

- **The limits:** two whole numbers in configuration. One caps the steps a run may take, the other the tokens it may spend in total. The loader refuses a bad file when it loads, as your earlier loaders do.
- **The check:** compares what the run has already counted with the limits. Your `propose` node keeps both counts on the state, so the check only compares them. A count equal to its limit passes. One over it halts the run, with the step budget checked first.

Where the check runs matters most. It must run before anything acts: before the approval point asks a dispatcher, and before the tool. The first thing `act` does is the only place that's true for every proposal. A halt sets both the status and the reason, because the rule after `act` only reads the status.

Choose limits that legitimate runs never come near. A budget that halts real work teaches people to raise it until it stops halting anything.

## What's expected

- Your budget configuration holds two whole numbers above zero. A missing file, a missing value, a zero or a non-number is refused when it loads.
- In the shell, the check on a hand-built state does these:
  - over the step limit: halts with `step_budget`
  - over the token total: halts with `token_budget`
  - over both: halts with `step_budget`
  - within both: comes back unchanged
- A halted state has both `status` `halted` and the halt reason set.
- The check is the first thing `act` does. The graph still has two nodes and one conditional edge.
- Your success, refusal and recovery runs, and `poe demo`, end as they did before. You know the steps and tokens each spent.

## When you're stuck

### The run keeps going after a halt

<details><summary>Move 1</summary>

Which field does your rule after `act` read to decide whether the run goes on?

</details>

<details><summary>Move 2</summary>

Does your check set that field, or only the halt reason?

</details>

<details><summary>Move 3</summary>

Set both fields whenever a budget is crossed, and check them together in the shell.

</details>

### A run over budget still asks a dispatcher

<details><summary>Move 1</summary>

Where in `act` does your check run: before or after the approval point?

</details>

<details><summary>Move 2</summary>

Would putting the check at the end of `propose` help? Where does the run go next over the plain edge?

</details>

<details><summary>Move 3</summary>

After a resume, `act` runs again from its start. Does the check run again too, and does it give the same answer on the same counts?

</details>

<details><summary>Move 4</summary>

The approach: call the check as the very first thing in `act`. If it halts, return the halt and skip the handler, so no approval is asked and no tool is called.

</details>

### The token budget never fires

<details><summary>Move 1</summary>

Which number does your check compare with the token limit?

</details>

<details><summary>Move 2</summary>

Is that one proposal's count, or the run's running total?

</details>

<details><summary>Move 3</summary>

Compare the total your `propose` node keeps on the state.

</details>

### The step budget fires one step late or one step early

<details><summary>Move 1</summary>

Does a count equal to the limit pass or halt in your check?

</details>

<details><summary>Move 2</summary>

Build three states in the shell, one below the limit, one equal and one above, and run the check on each.

</details>

<details><summary>Move 3</summary>

Does your step count include the proposal that's about to act? Read how `propose` updates it.

</details>

### You can't decide on budget values

<details><summary>Move 1</summary>

How many steps and tokens do your legitimate runs spend? Run each one and read the counts.

</details>

<details><summary>Move 2</summary>

How far above those counts would a run have to go before it's clearly stuck rather than just a little longer than usual?

</details>

<details><summary>Move 3</summary>

Pick values with room to spare, and write the observed counts and your reasoning beside them, both in the file and in your note.

</details>

### Your dev command stops at the first pause

<details><summary>Move 1</summary>

To read a whole run's steps and tokens, every pause has to be answered. Does your dev command answer them?

</details>

<details><summary>Move 2</summary>

Your demo already answers pauses as a dispatcher. Can the dev command reuse that code?

</details>

<details><summary>Move 3</summary>

Add an option to your dev command that approves every pause as a fixture you name, using your resume code, so a run completes on its own.

</details>

### The budget file loads anything

<details><summary>Move 1</summary>

Try a missing file, a missing key, a zero, a negative number and a word. What does your loader do with each?

</details>

<details><summary>Move 2</summary>

How do your authority and approval loaders refuse a bad file? Follow the same pattern.

</details>

<details><summary>Move 3</summary>

Make each refusal name the field and the problem, and check that it happens when the file loads, before any run starts. A run should never begin with a budget it can't trust.

</details>
