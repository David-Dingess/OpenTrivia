# Difficulty: easy, medium, hard and bad

Every built question carries a `rating` and a `difficulty` block.

```json
"rating": "medium",
"difficulty": { "tier": 3, "score": 0.35, "confidence": 0.5, "basis": "judged" }
```

This page says how those numbers are made.

## The short version

1. Each **row** has a card: how many people know it (`known`).
2. Each **question style** has a verdict: is it good, and how hard is its fact to know (`hardness`).
3. A question's score blends the two, plus how tight the call is.
4. Live play pulls the score toward what players actually got right.
5. The score maps to a tier, and the tier to easy, medium or hard.
6. A question style a judge turned off is **bad**. Its questions are in `questions/rejected/`.

Difficulty comes from **rows**, not questions. A row is shared by many questions, so what players know about one row informs every question it appears in.

## 1. The row card

Each row has `known` (0 to 1) and a `kind` (a palace, a dog breed, a sports car).

- `known` is roughly the share of ordinary players who know the thing. Claude Haiku rated it table by table.
- `kind` keeps options honest. The options beside an answer are always its own kind. Three dog breeds and a dog breed, never three dogs and a cat.

If a row has no card, its `fame` stands in (see [FAME.md](FAME.md)).

## 2. The template verdict

A **template** is one table, one column, one recipe. "Famous houses, country, Tap All That Apply" is a template. Claude Sonnet judged every one, and its verdicts are in [reference/template-verdicts.json](../reference/template-verdicts.json).

| Field | Meaning |
|---|---|
| `verdict` | `good` or `off`. Off builds nothing. |
| `score` | 0 to 100. Below 65 ships as off. |
| `hardness` | 0 to 1. How hard this kind of fact is to know, even on a famous row. |
| `minKnown` | Optional. Only rows at least this well known build this template. |
| `why` | One line from the judge. |
| `judge` | `model`, or `human`. A human verdict is final. |

Of 2,491 templates, 2,134 are good and 357 are off.

## 3. The score

For the rows a question uses:

```
rowHard    = 1 − known            (or 1 − fame with no card)
tightness  = 0 for a wide call … 1 for a tight one
             (how close two sizes are, how near two years sit)

with a verdict:     base = 0.45 × rowHard + 0.35 × hardness + 0.20 × tightness
without a verdict:  base = 0.75 × rowHard + 0.25 × tightness
```

`rowHard` is averaged over the question's rows.

## 4. Live play

Players answered questions live. Each row kept a running count of answers (`n`) and correct answers. The score then moves toward the real miss rate, with the prior worth 10 answers:

```
score = average over rows of  (base × 10 + misses) / (10 + n)
```

It's a Beta-style blend. With no plays the score is the prior. With 10 plays it's half and half. With 100 it's mostly what players did.

`confidence = E / (E + 2)`, where `E` adds 1 for a verdict, 1 if every row has a card, and `n / 10`.

`basis` says what the score rests on: `play` (10+ answers a row), `judged` (a verdict or cards) or `fame` (fame alone).

**An honest note.** The project ran live for about two weeks. No row reached 10 answers, so every published question has `basis: judged` and `confidence: 0.5`. The ratings here are priors. They have not been proven by players.

## 5. Tiers and ratings

| Score | Tier | Rating |
|---|---:|---|
| under 0.14 | 1 | easy |
| 0.14 to 0.28 | 2 | easy |
| 0.28 to 0.41 | 3 | medium |
| 0.41 to 0.71 | 4 | hard |
| 0.71 and up | 5 | hard |

The cut points were fitted on 231 blind labels (easy, medium, hard) by best balanced accuracy, not picked by hand.

True or False plays only at tier 3 or below, and only in the lightning round (see below).

## 6. Bad

"Bad" is a verdict on a **question style**, not a single question. A style is bad when a judge turns it off. Every question it would build is then bad.

The judges learned "bad" from a person. David rated 30 live questions blind and reviewed 41 cut ones. He called 27% of the live ones bad. The judges had called under 1% bad. His ratings became a rulebook every judge reads first. A question is bad when:

1. **The answer is in the question.** "What is the official language of Turkey?" A shared stem gives it away.
2. **An option of the wrong kind gives it away.** A Lamborghini beside Canon, Nike and General Motors.
3. **True or False as a normal question.** It's boring outside a fast round. So True or False lives only in a lightning round: ten 4-second questions, easy or medium, on famous things.
4. **A borrowed claim.** A false statement made from another thing's fact reads as nonsense ("The Ellora Caves inspired a theory of evolution").
5. **An obscure name as the answer or the clue.**
6. **An impostor of another kind.** London among countries.
7. **Two right answers.** Near-synonyms, or a contested fact. Contested is removed, not argued.

And what he kept that the judges had cut:

- Which is bigger, between famous things, when the gap is real (at least 1.5 times).
- Who sculpted it. Whose slogan is it.
- Picks on famous works by what they're famous for.

**After the rulebook**, a blind sample of 150 questions came back 5.3% bad and 0% wrong (from 27%). A judge using the rulebook re-rated David's own 30 and caught 7 of his 8 bad ones.

`questions/rejected/` holds 1,450 questions from the 357 off templates. Each carries the judge's reason in `template.why`. Use them as negative examples. Don't play them.

## Rules the code enforces

These are never left to a judge. The recipes refuse to build a question that breaks one.

- No giveaways: a row's name never shares a word or root with its answer.
- Options are the answer's own kind.
- Known floors: 0.40 for any row, 0.60 for a named clue or a True or False statement.
- Place giveaways: a name with a famous city in it is never asked about countries.
- Dated items sit far enough apart to tell: at least `max(3, 15% of their age)` years.
- "Typical" measures (lifespans, top speeds) are worded as typical ("Which usually lives longer?").

The full list is R1 to R15 in [FAMILY-FRIENDLY.md](FAMILY-FRIENDLY.md).

## The older prior

Before row cards existed, difficulty came straight from page views. It's kept here because it's simple and still useful with no model at all:

```
b = clamp(1.6 − 1.1 × log10(views / 1000) + obscurity, −2.5, 3)
```

`obscurity` is 0 for a plain property (capital, population, year), 0.5 for a rarer one, 1 for a close call. Roughly 400k+ views a month lands at tier 1, 100k+ at tier 2 and the 10k floor at tier 3.
