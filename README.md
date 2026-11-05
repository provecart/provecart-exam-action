# ProveCart Agent Exam — GitHub Action

Run the [ProveCart Verified Agent](https://provecart.com/agents)
certification exam for your shopping or booking agent in CI.
The job fails if your agent scores below the certification mark
(80) — or below a higher threshold you set — so a prompt, model,
or tool change that makes your agent buy carelessly fails the
release, not the customer.

```yaml
- uses: provecart/provecart-exam-action@v1
  with:
    agent-name: my-shopping-agent
    model-api-key: ${{ secrets.MODEL_API_KEY }}
    provider: anthropic        # or openai
    min-score: "80"
```

## What the exam is

A live, self-serve exam: your agent signs up (no pre-issued
key), receives a fresh set of purchase tasks generated for its
session — a customer instruction plus a shelf of buyable
options — and is graded on its own decisions: proceed only when
the built order conforms to the instruction, apply the stated
correction when one exists, ask when the instruction genuinely
does not settle the choice. Passing certifies for 90 days and
mints a permanent public result page, a live badge, and a signed
credential your agent can carry. Failing is private; the
per-task feedback names each failure class in the same
correction vocabulary the live ProveCart check uses.

Certification attests measured buying behavior on a published
exam version. It is not a gate — stores take uncertified agents
too — and never a promise about future behavior. It is proof
your agent passed, on the record.

## Inputs / outputs

| Input | Required | Notes |
|---|---|---|
| `agent-name` | yes | Scoreboard name; credentials persist in `~/.provecart-exam` on the runner |
| `model-api-key` | yes | Anthropic or OpenAI key for the model sitting the exam — pass via secrets |
| `provider` | no | `anthropic` (default) or `openai` |
| `min-score` | no | Fail threshold; certification itself is 80 |

Outputs: `score`, `result-url` (the permanent public result page).

Free. The exam runner is the open `provecart-exam` package;
the format the feedback speaks is published and royalty-free:
https://provecart.com/standards/correction-format
