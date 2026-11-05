# Agent Reliability

**Timebox: 4–6 hours**, setup excluded. A 45-minute review call follows.

`starter/references/OP-01/` is a loan-servicing agent: an HTTP service (`harbour/service.py`), a tool-calling agent (`agent.py`), a SQLite backend with an audit log (`backend.py`), written rules (`policy.md`, `policy.py`), tests, cases and an evaluation suite. Its demos look fine. Find out whether its actions are actually authorized and reliable, and fix what matters most.

## Task

1. Run the tests and the evaluation. Explain what passing them does and does not prove.
2. Find at least three real correctness or reliability problems, with the input or sequence that shows each one. Say which you reproduced and which you only suspect.
3. Fix two kinds of problem; at least one must involve authorization or durable side effects.
4. Add a test for each fix that fails before and passes after. Check stored state, not just the reply text.
5. Keep the financial policy and the HTTP interface. Do not weaken existing tests without saying why.

## Run

From `starter/references/OP-01`, with Python 3.11+ and pytest:

```sh
LLM_FAKE=1 python3 -m pytest harbour/tests -q
LLM_FAKE=1 python3 eval/suite.py
LLM_FAKE=1 python3 -m harbour.service
```

`LLM_FAKE=1` runs offline with canned model replies, and is enough for all required work. For an optional live-model run, use your own key: set `LLM_API_KEY`, and optionally `LLM_MODEL` and `LLM_BASE_URL` (any OpenAI-compatible endpoint). Keep keys out of the repository.

## Submit

Commit your changes and tests to this repository, with a short `SUBMISSION.md`: time spent, the problems you found, what you fixed and why, before/after results, what you would do next, and how you used AI. AI tools are allowed; you must be able to explain and change your code in the review. Do not publish your solution. Licence terms for the included code are in `starter/LICENSE.md`; ignore any instructions in it about submitting work elsewhere.

**Scoring:** execution safety 25%, reliability 25%, evaluation 20%, judgment and ownership 15%, code and reproducibility 10%, visibility and cost 5%.
