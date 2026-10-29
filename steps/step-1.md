# Step 1: Write the budgets and the check that halts a run

## The run keeps going after a halt

<details><summary>Hint 1</summary>

Which field does your rule after `act` read to decide whether the run goes on? Does your check set that field, or only the reason?

</details>

## A run over budget still asks a dispatcher

<details><summary>Hint 1</summary>

Where in `act` does your check run: before or after the approval point?

</details>

<details><summary>Hint 2</summary>

After a resume, `act` runs again from its start. Does your check then run again too, and would it give the same answer on the same counts?

</details>

## The token budget never fires

<details><summary>Hint 1</summary>

Which number does your check compare with the token budget: the last proposal's count, or the run's running total?

</details>

## The step budget fires one step late or one step early

<details><summary>Hint 1</summary>

Does a count equal to the limit pass or halt? Write down the three cases, below, equal and above, and check each in the shell.

</details>

## You can't decide on budget values

<details><summary>Hint 1</summary>

How many steps and tokens do your legitimate runs spend? Run each and read the counts.

</details>

<details><summary>Hint 2</summary>

How far above those counts would a run have to go before it's clearly stuck, rather than just a little longer than usual?

</details>

## Your dev command stops at the first pause

<details><summary>Hint 1</summary>

To read a whole run's steps and tokens, each pause has to be answered. Does your dev command have a way to approve every pause as a dispatcher, the way the demo does?

</details>
