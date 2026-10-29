# Step 2: Write the scripts that exhaust each budget

## Your budget script ends before it reaches the limit

<details><summary>Hint 1</summary>

Which proposals end a run, and which leave it running? Read each entry before the limit and ask what your graph does with it.

</details>

<details><summary>Hint 2</summary>

A tool call your configuration doesn't allow is turned down by the tool, and the run goes on. Which values in your authority configuration could make a call well formed but not allowed?

</details>

## The halt fires on the wrong budget

<details><summary>Hint 1</summary>

Add up the script's counts entry by entry. Which limit does it cross first? Does it cross both on the same entry?

</details>

## The approval pause shows up in a halted run

<details><summary>Hint 1</summary>

Which step crossed the limit? Did that step pause, or did earlier steps pause on the way there?

</details>

<details><summary>Hint 2</summary>

The requirement is about the step that crossed the limit. Read your output for that step only.

</details>

## You can't tell whether a review was blocked or just never asked for

<details><summary>Hint 1</summary>

Where in your script is the entry that would open a review: before the limit, or after it?

</details>
