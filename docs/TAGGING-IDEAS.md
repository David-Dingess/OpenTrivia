# Tagging ideas

Every built question already knows a lot about itself: its table, column, recipe, format, genre, category, topic, the rows it uses, a difficulty score and a rating. This page suggests what to add next, for anyone who picks the data up.

None of this was built. These are proposals, roughly in order of value for effort.

## 1. Prove the difficulty with players (IRT)

The ratings here are priors. No row reached enough plays to move them (see [DIFFICULTY.md](DIFFICULTY.md)). The single best upgrade is real answers.

- Fit a one-parameter IRT model with a guessing floor: `P(correct) = c + (1 − c) × σ(θ − b)`, where `c = 1 / options`, `θ` is the player's skill and `b` the question's difficulty.
- Start each question at its prior. Each built question converts cleanly: `b = (score − 0.5) × 3`, with `sd = 1.2 − confidence`.
- Pool by **row**, not by question. One row appears in many questions, so a few hundred answers calibrate thousands of questions.
- An Elo-style update (player vs question) is the cheap version and works live.

## 2. A per-question classifier (the "Jev" idea)

The project considered **Jev AI**, TypeSafe's System-1 classifier, to label questions one by one. It wasn't used. Judging each question *style* once, then building from it, made per-question labels unnecessary there. A classifier still makes sense for anyone who wants labels the templates can't give:

- Run it, or any LLM with a fixed rubric, over each question once and store the labels.
- Calibrate it against a small human-rated set first. The lesson here: judges called 1% of questions bad where a person called 27% bad. Prime the classifier with the seven "bad" rules in [DIFFICULTY.md](DIFFICULTY.md) and check its agreement before trusting it.
- `questions/rejected/` gives 1,450 labelled negatives, each with a reason, to train or test on.

## 3. Tags worth adding

| Tag | Values | Why |
|---|---|---|
| `ageBand` | `kids` · `family` · `adult` | PG-13 is the line now. A classroom needs a stricter cut (no wine, no horror). |
| `region` | `global` · `us` · `uk` · `europe` … | US state capitals are easy in Ohio and hard in Osaka. Every question is `global` today. |
| `answerKind` | `person` · `place` · `work` · `thing` · `number` · `year` | Lets a show balance a round. Row `kind` already holds the fine-grained version. |
| `skill` | `recall` · `recognition` · `estimation` · `ordering` | Typing a name is harder than picking one. Recipe and format give most of this already. |
| `era` | the decade or century the fact belongs to | Balance old and new. Stops a round from being all 1990s. |
| `fiction` | the work and franchise | Makes the fiction caps easy to apply. Today it's only implied by the table. |
| `clueFame` / `answerFame` | 0 to 1 each | Split the one fame score in two. A famous clue with an obscure answer plays very differently from the reverse. |
| `distractorCloseness` | 0 to 1 | How alike the wrong options are to the right one (embedding similarity, or same-kind share). Tight options make a hard question fair. |
| `readability` | a reading grade | Short prompts for a 4-second bolt, longer ones for a slow round. |
| `teaches` | `true` / `false` | Does the reveal (`learn`) teach something new? The best trivia leaves you knowing more. |
| `shelfLife` | `evergreen` · `years` · `months` | Volatile tables (records, current holders) go stale. `timeSensitive` is the blunt version today. |
| `argueRisk` | 0 to 1 | How likely a room is to argue the answer. Anything above a low bar should be cut, per the rules. |
| `multiHop` | `true` / `false` | Needs two facts joined ("the director of the film that won…"). These are harder than their rows suggest. |

## 4. Use what's already here

Before you add anything, notice what you can derive today:

- **Kind balance:** each row's `kind`.
- **Wide vs tight calls:** a question's rows and their values in `learn`.
- **How a style plays:** the template's `hardness`, `score` and `why`.
- **Famous core of a list:** filter `lists/` by `fame ≥ 0.45`.
- **Stale risk:** the table's `verification.volatile`.

## 5. Keep a human in the loop, a little

The biggest jump in quality came from one person rating 71 questions once. Not a standing review. A single blind sample, turned into rules the judges read. If you extend this, do the same: rate a small blind sample, write down what made the bad ones bad, and teach that to whatever does the labelling.
