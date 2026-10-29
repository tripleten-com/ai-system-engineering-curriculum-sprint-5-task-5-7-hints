# Step 5: Prove it with tests and write the evidence note

## Breaking the tool events doesn't fail your order test

<details><summary>Hint 1</summary>

Which run's trail does your order test read? Does that run ever have a tool call that fails?

</details>

<details><summary>Hint 2</summary>

Which of your scripts turns down a tool call before it succeeds? Assert its trail as well.

</details>

## A doubled `approval_requested` passes

<details><summary>Hint 1</summary>

Does your test count the records, or only check that one exists?

</details>

## Your tests can't see the records

<details><summary>Hint 1</summary>

Which audit store does the graph write to in your tests? Could the test hand it a store that keeps the records in memory?

</details>

## The credential test passes even when you put a token in a record

<details><summary>Hint 1</summary>

Where does the test get the value it searches for? Is it the same value the code would write, read from the same fixture?

</details>

## The budget tests pass even with the check removed

<details><summary>Hint 1</summary>

Does each test assert the status, the halt reason, and that nothing was written and nothing was asked?

</details>
