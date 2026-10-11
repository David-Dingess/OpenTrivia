# OpenTrivia

Trivia as data, not as a pile of questions.

(Not affiliated with the [Open Trivia Database](https://opentdb.com/), which is a different project.)

This is the knowledge base from a project built to deliver trivia. The project is done. The knowledge base is open sourced here so anyone can use it.

## The idea

Most trivia sets are a list of questions. This one stores **fact tables** instead. A question is built from a table on demand.

- A **table** is a set of famous things and facts about them. Famous paintings and who painted them. Countries and their capitals. Dinosaurs and what they ate.
- Every row has a **hook**: what the thing is famous for, in our own words.
- Every table has **wording**: one plain sentence per question style.
- **Recipes** turn a table and its wording into questions. Pick One, Match Up, Sort It, Odd One Out and ten more.

So you get two things here. The tables, which you can build your own questions from. And 9,698 questions already built from them, each rated easy, medium or hard.

## What's inside

| Folder | What it is | Size |
|---|---|---|
| [`tables/`](tables) | 480 fact tables, 17,784 famous rows, filed by category | facts, hooks, wording, difficulty cards |
| [`questions/built/`](questions/built) | 9,698 questions built from the tables, one file per table | easy 2,723 · medium 5,697 · hard 1,278 |
| [`questions/rejected/`](questions/rejected) | 1,450 questions from question styles a judge turned off | labelled `bad`, with the reason |
| [`questions/polls/`](questions/polls) | 320 "Split the Room" opinion polls | no right answer, just fun |
| [`lists/`](lists) | 546 name lists, 281,941 names | "Name a public aquarium", obscure members included |
| [`extras/`](extras) | Survey boards, dishes and their ingredients, auction prices, weights, film scores | for party-game formats |
| [`reference/`](reference) | The blocklist, wildcard names, every question style's verdict | the rules as data |
| [`taxonomy.json`](taxonomy.json) | Genre › Category › Topic | 6 genres, 31 categories, 187 topics |

## Read next

1. [docs/FORMAT.md](docs/FORMAT.md). How a table, a question and a list are shaped. Start here if you want to use the data.
2. [docs/TAXONOMY.md](docs/TAXONOMY.md). How everything is filed.
3. [docs/FAME.md](docs/FAME.md). The fame threshold: why every row is something people have heard of.
4. [docs/DIFFICULTY.md](docs/DIFFICULTY.md). How a question gets rated easy, medium, hard or bad.
5. [docs/FAMILY-FRIENDLY.md](docs/FAMILY-FRIENDLY.md). The rules that keep it clean and out of arguments.
6. [docs/TAGGING-IDEAS.md](docs/TAGGING-IDEAS.md). Ways to tag questions further.
7. [CREDITS.md](CREDITS.md). Every source this stands on.

## A taste

```json
{
  "prompt": "Which of these played an older woman who seduces a recent college graduate in a landmark satirical drama?",
  "payload": { "options": [
    { "text": "Helen Hayes", "correct": false },
    { "text": "Anne Bancroft", "correct": true },
    { "text": "Joanne Woodward", "correct": false },
    { "text": "Judy Holliday", "correct": false } ] },
  "learn": { "say": "Anne Bancroft won the Best Actress Oscar for The Miracle Worker in 1963." },
  "rating": "medium"
}
```

## Numbers by genre

| Genre | Categories | Topics | Tables | Rows | Questions (easy / medium / hard) |
|---|---:|---:|---:|---:|---|
| Art & Entertainment | 5 | 41 | 88 | 4,820 | 2,575 (576 / 1,521 / 478) |
| Daily Life | 5 | 26 | 69 | 2,509 | 1,565 (443 / 957 / 165) |
| Games & Sports | 4 | 35 | 82 | 2,976 | 1,622 (403 / 1,091 / 128) |
| General | 6 | 39 | 76 | 2,018 | 1,351 (555 / 662 / 134) |
| Science, Math, Technology | 6 | 23 | 79 | 2,322 | 1,158 (371 / 661 / 126) |
| Society | 5 | 23 | 86 | 3,139 | 1,427 (375 / 805 / 247) |

## How it was made

1. Facts came from **Wikidata** (CC0) and from hand-built tables checked row by row against English Wikipedia.
2. Every row had to clear a **fame floor**: about 10,000 English Wikipedia views a month.
3. **Claude** models (Anthropic) wrote the hooks and the wording, rated how well known each row is, and judged every question style. A person set the rules and rated samples to keep the judges honest.
4. Questions were built by code that enforces the rules. No built question was ever hand-edited.
5. Nothing was copied. Facts are free. Every word you read here is our own.

Be clear on what that means. **Most of this text was written by an AI and checked by AI judges and code.** Not every row was read by a person. Facts were checked against their sources, but mistakes will be in here.

## As is

This repo is offered freely, as is. It is not monitored, maintained or cleaned. Issues and pull requests won't be answered. Fork it and make it yours.

The facts are frozen as of October 2026. Some tables are marked `volatile` (records, current holders). Check those before you trust them.

## Licence

Our own work (hooks, wording, questions, the taxonomy, ratings) is **CC BY 4.0**. Credit "OpenTrivia by David Dingess". A few files carry their source's licence instead. See [LICENSE.md](LICENSE.md).
