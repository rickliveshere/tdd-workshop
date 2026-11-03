# TDD Workshop: FizzBuzz

A 45-minute, hands-on introduction to Test-Driven Development. Choose **Python** or
**TypeScript**; both are set up in the same dev container.

The goal is **not** to solve FizzBuzz. You've probably done that before. The goal is to
practise the *process*: writing a failing test, making it pass in the simplest way
possible, and refactoring safely while the requirements change underneath you.

---

### Overview video (40 seconds)


https://github.com/user-attachments/assets/09151f0d-bd59-4052-b088-d0a72f7883d1

 
<video src="docs/tdd-red-green-refactor.mp4" controls loop muted width="720"></video>
 
If the video doesn't play above, [open it directly](docs/tdd-red-green-refactor.mp4).


## Getting started

### Option 1: Dev container (recommended)

You need [Docker](https://www.docker.com/products/docker-desktop/) and
[VS Code](https://code.visualstudio.com/) with the
[Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).

1. Clone this repo and open the folder in VS Code.
2. When prompted, click **Reopen in Container**
   (or run **Dev Containers: Reopen in Container** from the command palette).
3. Wait for the container to build. Python and Node dependencies install automatically.
4. Open a terminal in VS Code and check your chosen language works (see below).

The container includes Python 3.15.2 and Node 24 (LTS), so you can pick either language.
The first build can take several minutes because Python is installed from source.

### Option 2: GitHub Codespaces

Open the repo in [GitHub Codespaces](https://github.com/features/codespaces). It uses the
same dev container, so nothing else is needed.

### Option 3: Run locally without Docker

| | Python | TypeScript |
| --- | --- | --- |
| Requires | Python 3.15 (3.10+ also works) | Node 24 LTS (20+ also works) |
| Install | `cd python && pip install -r requirements-dev.txt` | `cd typescript && npm install` |

---

## Pick your language

### Python

```bash
cd python
pytest
```

You should see `test_environment_works` pass.

| Command | What it does |
| --- | --- |
| `pytest` | Run all tests once |
| `ptw .` | Watch mode: re-runs the tests every time you save |
| `pytest -k fizz` | Run only tests with "fizz" in their name |
| `pytest -x` | Stop at the first failure |

```
python/src/fizzbuzz.py          <- your production code
python/tests/test_fizzbuzz.py   <- your tests (start here)
python/tests/test_setup.py      <- environment check, leave alone
```

### TypeScript

```bash
cd typescript
npm test
```

You should see `environment works` pass.

| Command | What it does |
| --- | --- |
| `npm test` | Run all tests once |
| `npm run test:watch` | Watch mode: re-runs the tests every time you save |
| `npx vitest -t fizz` | Run only tests with "fizz" in their name |
| `npx vitest run --bail 1` | Stop at the first failure |

```
typescript/src/fizzbuzz.ts           <- your production code
typescript/tests/fizzbuzz.test.ts    <- your tests (start here)
typescript/tests/setup.test.ts       <- environment check, leave alone
```

**Tip:** keep watch mode running in a terminal beside your editor. You'll see red and
green instantly.

---

## The rules of the game

1. **Do not write code without a failing test first.**
2. Write the **smallest** test that fails, and make sure it fails for the right reason.
3. Write the **simplest** code that makes it pass. Hardcoding is allowed!
4. Once green, **refactor**: remove duplication, improve names. Tests must stay green.

### Working in pairs (ping-pong)

- **Person A** writes a failing test.
- **Person B** makes it pass, refactors, then writes the next failing test.
- Swap roles every cycle.

---

## The exercise

You are building a function `fizzbuzz(n)` that takes an integer and returns the output
for that single number as a string.

**You don't get the full spec up front.** Requirements arrive one at a time, just like
in real life. Your facilitator will tell you when to open the next rule. Don't peek
ahead, as the point is to see how your code and tests cope with change.

For each rule: write a failing test, make it pass, refactor, then wait.

<details>
<summary><strong>Rule 1: Fizz</strong></summary>

If the number is a multiple of **3**, return `"Fizz"`.
Otherwise, return the number as a string (e.g. `1` returns `"1"`).

</details>

<details>
<summary><strong>Rule 2: Buzz</strong></summary>

If the number is a multiple of **5**, return `"Buzz"`.

</details>

<details>
<summary><strong>Rule 3: FizzBuzz</strong></summary>

If the number is a multiple of **both 3 and 5**, return `"FizzBuzz"`.

</details>

<details>
<summary><strong>Rule 4: Bang</strong></summary>

If the number is a multiple of **7**, return `"Bang"`.

Words combine in the order Fizz, Buzz, Bang. For example, 21 returns `"FizzBang"`
and 105 returns `"FizzBuzzBang"`.

</details>

<details>
<summary><strong>Rule 5: Numbers containing a 3</strong></summary>

If the number **contains the digit 3** (e.g. 13, 31, 43), it also counts as a Fizz.

Be careful with numbers that are *already* Fizz. 3 and 33 should return `"Fizz"`,
not `"FizzFizz"`.

</details>

<details>
<summary><strong>Rule 6: Make the rules configurable</strong></summary>

The business wants to change the rules without touching the code. Refactor so the rules
are data rather than hardcoded `if` statements.

For example, something like this should work (the exact design is up to you):

**Python**

```python
rules = [
    (3, "Fizz"),
    (5, "Buzz"),
    (7, "Bang"),
]
fizzbuzz(21, rules)   # "FizzBang"
```

**TypeScript**

```ts
const rules: [number, string][] = [
  [3, "Fizz"],
  [5, "Buzz"],
  [7, "Bang"],
];
fizzbuzz(21, rules); // "FizzBang"
```

Calling `fizzbuzz(n)` with no rules must keep behaving exactly as before.
**Your existing tests should still pass throughout the refactor.** That's the safety
net doing its job.

</details>

---

## Retrospective questions

- Did you ever want to skip ahead and write more code than the test required? What happened?
- Which rule change was the most painful? Did the tests help or get in the way?
- How did it feel to refactor with a full green test suite behind you?
- What would have been different if you'd written the tests *after* the code?

---

## Stuck?

- Is your test failing for the **right** reason? (A "not implemented" error is not a good
  red. Read the failure message.)
- Is your test too big? Make it smaller.
- Resist the urge to write the "real" solution. What is the *dumbest* thing that would pass?

---

---
 
## Advanced exercises: stubs and mocks
 
Stretch material for fast pairs or a follow-up session. It won't fit in the 45 minutes.
The rules are the same as before: red, green, refactor, and no production code without a
failing test.
 
### Stub vs mock in one minute
 
A **test double** stands in for a real collaborator (a network call, a database, the
clock, another service) so a test stays fast and deterministic. Two kinds come up most:
 
| | Stub | Mock |
| --- | --- | --- |
| Job | Feeds the code under test **indirect inputs**: canned answers | Lets you check **indirect outputs**: the calls your code makes to a collaborator |
| Typical collaborator | Queries ("give me the rules", "what time is it?") | Commands ("send this email", "write this audit entry") |
| You assert on | The **result** returned by the code under test | That the **call happened**: how many times, with which arguments |
| Fails the test when | Never. It just answers, and nobody cares how often it was asked | The expected interaction doesn't happen, or happens when it shouldn't |
| Style | State verification | Behaviour verification |
 
**When to use which**
 
1. **Use a stub when your code reads from a collaborator.** Set up the answer, run the
   code, assert on the output.
2. **Use a mock when the side effect is the behaviour**, and the call itself is the only
   way to observe it. Fire-and-forget things like sending an email or publishing an event
   are the classic cases.
3. **Prefer state over interactions when you can.** If the outcome is visible in a return
   value or a simple in-memory **fake**, assert on that. Interaction tests are more tightly
   coupled to how the code is written, so they break more often during refactoring.
4. **Don't double what you don't need to.** Pure functions and simple values (like your
   `fizzbuzz` function) should just be called for real.
5. **Don't mock what you don't own.** Wrap a third-party library in a thin adapter of your
   own and double the adapter.
The other doubles you'll hear about: a **dummy** fills a parameter and is never used, a
**fake** is a working lightweight implementation (an in-memory repository), and a **spy**
records calls for you to check afterwards. Most libraries' "mocks" are really spies, and
the same object can play either role. If you only set what it returns, it's a stub. If you
assert on its calls, it's a mock. The role is decided by how you use it.
 
Tools: Python's built-in `unittest.mock.Mock`, and `vi.fn()` from Vitest (already
installed). Nothing extra to set up.
 
Further reading: Martin Fowler's
[Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html).
 
### Setup: a service with two collaborators
 
The pure `fizzbuzz` function needs no doubles. Now wrap it in a `FizzBuzzService` that
talks to two collaborators:
 
- **`RulesProvider`** (input): returns the current rules. In real life this would call a
  remote config service.
- **`AuditLog`** (output): `record(n, output)` stores an entry. In real life this would
  write to a database.
You will **never write the real versions**. That's the point: the tests don't need them.
 
Create new files and write your first failing test before the class exists:
 
| | Python | TypeScript |
| --- | --- | --- |
| Production code | `python/src/service.py` | `typescript/src/service.ts` |
| Tests | `python/tests/test_service.py` | `typescript/tests/service.test.ts` |
 
`FizzBuzzService` takes the two collaborators in its constructor and has a
`run(start, end)` method that returns a list of strings, one per number from `start` to
`end` inclusive. The rules provider's `get_rules()` returns rules in the same shape you used
in Rule 6, and the audit log's `record(n, output)` returns nothing. Use your own
`fizzbuzz(n, rules)` from Rule 6 inside the service.
 
<details>
<summary><strong>Hint: the shape to aim for</strong></summary>
**Python**
 
```python
class FizzBuzzService:
    def __init__(self, rules_provider, audit_log): ...
 
    def run(self, start: int, end: int) -> list[str]:
        """FizzBuzz for every number from start to end, inclusive."""
```
 
**TypeScript**
 
```ts
interface RulesProvider { getRules(): Rule[]; }  // Rule is whatever you defined in Rule 6
interface AuditLog { record(n: number, output: string): void; }
 
class FizzBuzzService {
  constructor(rulesProvider: RulesProvider, auditLog: AuditLog) {}
  run(start: number, end: number): string[] { /* ... */ }
}
```
 
</details>

### Exercise A: stubs (rules come in)
 
Write a failing test for each requirement, one at a time:
 
1. `run(1, 5)` with a provider that returns the rules `Fizz` for 3 and `Buzz` for 5 gives
   `["1", "2", "Fizz", "4", "Buzz"]`.
2. With a provider that returns only `[(2, "Even")]`, `run(4, 6)` gives
   `["Even", "5", "Even"]`. This proves the service uses the provider and doesn't have
   rules hardcoded.
3. If the provider **throws** (the config service is down), the service falls back to the
   default behaviour: calling `fizzbuzz(n)` with no rules. A stub can simulate failure as
   well as answers.
Then discuss: **does any of these tests care how many times `get_rules` was called?**
It shouldn't. That's what makes it a stub.
 
<details>
<summary><strong>Hint: how to set up the stub</strong></summary>
**Python**
 
```python
from unittest.mock import Mock
 
from service import FizzBuzzService
 
 
def stub_provider(rules=((3, "Fizz"), (5, "Buzz"))):
    provider = Mock()
    provider.get_rules.return_value = list(rules)  # stub: a canned answer
    return provider
 
 
def test_uses_the_rules_from_the_provider():
    audit_log = Mock()  # dummy: only here to satisfy the constructor
    service = FizzBuzzService(stub_provider([(2, "Even")]), audit_log)
 
    assert service.run(4, 6) == ["Even", "5", "Even"]  # assert on the result
 
 
def test_falls_back_to_the_default_rules_when_the_provider_fails():
    rules_provider = Mock()
    rules_provider.get_rules.side_effect = ConnectionError("config service down")
    service = FizzBuzzService(rules_provider, Mock())
 
    assert service.run(1, 5) == ["1", "2", "Fizz", "4", "Buzz"]
```
 
**TypeScript**
 
```ts
import { describe, it, expect, vi } from "vitest";
import { FizzBuzzService } from "../src/service";
 
const stubProvider = (
  rules: [number, string][] = [
    [3, "Fizz"],
    [5, "Buzz"],
  ],
) => ({
  getRules: vi.fn().mockReturnValue(rules), // stub: a canned answer
});
 
it("uses the rules from the provider", () => {
  const service = new FizzBuzzService(stubProvider([[2, "Even"]]), { record: vi.fn() });
 
  expect(service.run(4, 6)).toEqual(["Even", "5", "Even"]); // assert on the result
});
 
it("falls back to the default rules when the provider fails", () => {
  const failingProvider = {
    getRules: vi.fn().mockImplementation(() => {
      throw new Error("config service down");
    }),
  };
  const service = new FizzBuzzService(failingProvider, { record: vi.fn() });
 
  expect(service.run(1, 5)).toEqual(["1", "2", "Fizz", "4", "Buzz"]);
});
```
 
</details>

### Exercise B: mocks (audit entries go out)
 
Add a new behaviour. Each numbered item is another red, green, refactor cycle:
 
1. For every number whose output is **not just the number itself**, the service calls
   `audit_log.record(n, output)` once. `run(1, 5)` records `(3, "Fizz")` and
   `(5, "Buzz")`, and nothing else.
2. For an **empty range** (`start` greater than `end`) the service returns `[]` and never
   touches the audit log.
Notice that the audit log has no return value you can inspect. The call is the only way to
observe the behaviour, so a mock is the right tool here. You'll normally use a stub (for
the rules) and a mock (for the audit log) in the same test.
 
<details>
<summary><strong>Hint: how to set up the mock</strong></summary>
These reuse the `stub_provider` / `stubProvider` helper from Exercise A.
 
**Python**
 
```python
from unittest.mock import Mock, call
 
 
def test_records_only_the_numbers_that_were_transformed():
    audit_log = Mock()  # mock: we assert on the calls it received
    service = FizzBuzzService(stub_provider(), audit_log)
 
    service.run(1, 5)
 
    assert audit_log.record.call_args_list == [call(3, "Fizz"), call(5, "Buzz")]
 
 
def test_records_nothing_for_an_empty_range():
    audit_log = Mock()
    service = FizzBuzzService(stub_provider(), audit_log)
 
    assert service.run(5, 1) == []
    audit_log.record.assert_not_called()
```
 
**TypeScript**
 
```ts
it("records only the numbers that were transformed", () => {
  const auditLog = { record: vi.fn() }; // mock: we assert on the calls it received
  const service = new FizzBuzzService(stubProvider(), auditLog);
 
  service.run(1, 5);
 
  expect(auditLog.record.mock.calls).toEqual([
    [3, "Fizz"],
    [5, "Buzz"],
  ]);
});
 
it("records nothing for an empty range", () => {
  const auditLog = { record: vi.fn() };
  const service = new FizzBuzzService(stubProvider(), auditLog);
 
  expect(service.run(5, 1)).toEqual([]);
  expect(auditLog.record).not.toHaveBeenCalled();
});
```
 
</details>

### Exercise C: loosen the mock, then swap it for a fake
 
Mocks make tests sensitive to *how* the code works. Find out how sensitive.
 
1. **Break it without changing behaviour.** Refactor the service so it records entries in
   a different order (for example, collect the entries first and record them in reverse).
   Which tests fail? Has the behaviour changed in a way the requirements care about? If
   your test pins down call order but the requirement doesn't, it is over-specified. Loosen
   it so it checks *what* was recorded, not *in which order*.
2. **Swap the mock for a fake.** Write a small `InMemoryAuditLog` that stores entries in a
   list, and assert on that list instead of on calls.
3. **Compare** the two tests. Which is easier to read? Which survives a refactor better?
   When would you keep the mock anyway? (Think: no observable state, or "exactly once"
   *is* the contract.)
<details>
<summary><strong>Hint: loosened mock and a fake</strong></summary>
These also reuse the stub helper from Exercise A.
 
**Python**
 
```python
def test_records_only_the_numbers_that_were_transformed_any_order():
    audit_log = Mock()
    service = FizzBuzzService(stub_provider(), audit_log)
 
    service.run(1, 5)
 
    assert audit_log.record.call_count == 2
    audit_log.record.assert_has_calls([call(3, "Fizz"), call(5, "Buzz")], any_order=True)
 
 
class InMemoryAuditLog:
    def __init__(self):
        self.entries = []
 
    def record(self, n, output):
        self.entries.append((n, output))
 
 
def test_records_only_the_numbers_that_were_transformed_with_a_fake():
    audit_log = InMemoryAuditLog()
    service = FizzBuzzService(stub_provider(), audit_log)
 
    service.run(1, 5)
 
    assert sorted(audit_log.entries) == [(3, "Fizz"), (5, "Buzz")]
```
 
**TypeScript**
 
```ts
it("records only the numbers that were transformed, in any order", () => {
  const auditLog = { record: vi.fn() };
  const service = new FizzBuzzService(stubProvider(), auditLog);
 
  service.run(1, 5);
 
  expect(auditLog.record).toHaveBeenCalledTimes(2);
  expect(auditLog.record).toHaveBeenCalledWith(3, "Fizz");
  expect(auditLog.record).toHaveBeenCalledWith(5, "Buzz");
});
 
class InMemoryAuditLog {
  entries: [number, string][] = [];
  record(n: number, output: string) {
    this.entries.push([n, output]);
  }
}
 
it("records only the numbers that were transformed, using a fake", () => {
  const auditLog = new InMemoryAuditLog();
  const service = new FizzBuzzService(stubProvider(), auditLog);
 
  service.run(1, 5);
 
  expect(auditLog.entries).toHaveLength(2);
  expect(auditLog.entries).toContainEqual([3, "Fizz"]);
  expect(auditLog.entries).toContainEqual([5, "Buzz"]);
});
```
 
</details>

### Exercise D: spot the smell (discussion)
 
Each of these tests would pass today. What's wrong with each, and what would you do
instead?
 
1. A test replaces `fizzbuzz` with a mock inside the service and asserts it was called
   five times for `run(1, 5)`.
2. A test uses a stub provider, then also asserts that `get_rules` was called exactly once.
3. A test creates a mock audit log and runs the service, but never asserts anything about
   the audit log.
4. A test mocks the audit log's `record` method *and* the service's own private helper
   method, then asserts the helper was called.
   
<details>
<summary><strong>Answers</strong></summary>
1. **Doubling a pure function.** `fizzbuzz` is fast, deterministic and has no side effects,
   so there's nothing to isolate. The test only proves the implementation calls it five
   times, and it breaks if you ever process the range differently. Call the real function
   and assert on the returned values.
2. **A stub turned into a mock for no reason.** The call count isn't a requirement. This
   test will fail if you later cache the rules or fetch them twice, even though the
   behaviour is still correct. Delete the assertion and keep the one on the result.
3. **A mock that verifies nothing.** The test would pass even if the audit log were never
   called, so it gives false confidence. Either assert on the interaction (or use a fake and
   check its entries), or use a plain dummy and say so.
4. **Mocking the code under test.** The helper is an implementation detail, so the test is
   coupled to the code's structure and fails on any internal refactor. Test through the
   public `run` method.
</details>
