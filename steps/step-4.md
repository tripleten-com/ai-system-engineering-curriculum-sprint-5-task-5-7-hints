# Step 4: Reconstruct your recovery run from its trail alone

## The idea

An audit trail passes one test: can someone who wasn't there say what happened, from the trail alone? This Step puts you in that position on purpose. You run a recovery-shaped script you haven't run before, save its output to a file without reading it, and then rebuild the run from its records.

The rule is strict for a reason. If you already know the run's shape, you reconstruct from memory, and the trail never gets tested. That's why the lesson asks for a second recovery-shaped script. By now you know your first one's steps and tokens by heart.

For each value you rebuild, name the record it came from:

- the number of steps
- the kind of each proposal in order
- each decision and who made it
- whether a review opened and how many calls failed
- the final status
- the halt reason
- the total tokens

If a value has no record behind it, or you had to guess, the trail is missing an event or carrying the wrong value. That's a defect in your events, not in your reading. Fix the event, rerun, and reconstruct again. This Step is where you find those defects, before a dispatcher does.

> Covered in **Audit Logging and Data Handling**, in **Guarding Model Output and Personal Data**.

## What's expected

- A second recovery-shaped script exists, with a different count of turned-down calls from your first, and you hadn't run it before this Step.
- Its run's output is saved to a file you opened only at the end.
- Your reconstruction has one line per value, each naming the record it came from.
- Every value matches the saved output. If one didn't at first, the fix went into your events, and you reran.
- From the trail alone, you can answer what the agent did before the review opened, and who said yes.

## When you're stuck

### You already know what the run will do

<details><summary>Hint 1</summary>

Is this the recovery script you ran in Step 1?

</details>

<details><summary>Hint 2</summary>

If you know its steps and tokens already, what are you testing: the trail, or your memory?

</details>

<details><summary>Hint 3</summary>

Write a second recovery-shaped script with a different number of turned-down calls before the one that succeeds, run it once with every pause approved, and save the output without reading it.

</details>

### You can't find who approved

<details><summary>Hint 1</summary>

Which record names a decision?

</details>

<details><summary>Hint 2</summary>

Which field in it identifies the dispatcher?

</details>

<details><summary>Hint 3</summary>

The role isn't in that record. What does the approval point guarantee about the role of every decision it accepts?

</details>

### The total tokens don't match

<details><summary>Hint 1</summary>

Which record did you take the total from?

</details>

<details><summary>Hint 2</summary>

Is that one proposal's count, or the run's total?

</details>

<details><summary>Hint 3</summary>

Take the total from the record that ends the run.

</details>

### A value disagrees with the saved output

<details><summary>Hint 1</summary>

Is the trail missing an event, or is an event carrying the wrong value?

</details>

<details><summary>Hint 2</summary>

Find the record you'd have needed, then find where in the code it's written.

</details>

<details><summary>Hint 3</summary>

Fix the event, not the reconstruction. Run the script again on a fresh exception and rebuild the run from the new trail.

</details>
