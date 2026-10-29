# TDD Workshop: FizzBuzz with a Twist

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
