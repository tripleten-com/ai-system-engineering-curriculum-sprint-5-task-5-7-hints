# Before you submit

The basic checks confirm that your work is there. They don't judge whether it's right. Your instructor reads your pull requests and evidence notes with four questions. Ask them of your own work first.

## Did you meet the Task's requirements?

- Does the check run first in `act`, compare the running totals, and halt with the fixed reasons, step budget first?
- Does each budget script cross exactly one budget, with the review behind the limit?
- Does the trail show the agent's eight events after the worker's, one record per event, with no credential and no model text?
- Does `poe demo` show the run's steps and tokens against the budgets and its events?

## Did you explain your design choices?

- Does your note say why you chose your budget values?
- Does it say how you get one `approval_requested` per pause after a resume?
- Does it say what each event carries and what you kept out, and why?

## Can your tests fail when the code is wrong?

- Did you make the check return the state unchanged, record `tool_called` on a failed result and double an approval request once each, and see tests fail?
- Does an order test read a trail with a failed tool call in it?

## Did you state the limits of what your checks show?

- Did your reconstruction use a run you hadn't seen, and does your note say where it disagreed, if anywhere?
- Does it say what the trail can't show, such as a trace id the agent server doesn't have?
