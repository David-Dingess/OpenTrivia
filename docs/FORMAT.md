# Data format

Everything is JSON. Tables and lists are one `.json` file each. Questions are JSON Lines (`.jsonl`), one question per line. Files are filed by category: `tables/<category>/<slug>.json`.

## A table

`tables/biology/dinosaurs-diet.json`, trimmed:

```json
{
  "id": "table.biology.dinosaurs-diet",
  "kind": "table",
  "title": "Dinosaurs and what they ate",
  "genre": "science-math-tech",
  "category": "biology",
  "topic": "dinosaurs",
  "licence": "CC-BY-4.0",
  "source": { "name": "Wikidata (CC0)", "method": "sparql:SELECT …", "fetchedAt": "2026-10-02T18:08:39Z" },
  "verification": { "status": "verified", "checkedAt": "2026-10-02T18:08:39Z", "volatile": false },
  "columns": [ { "key": "diet", "label": "Diet", "unit": null, "type": "text" }, … ],
  "wording": {
    "one": "dinosaur", "many": "dinosaurs",
    "columns": {
      "diet": {
        "role": "link",
        "statement": "{label} was a {value}.",
        "odd": "Three of these dinosaurs were {value}s. Which one wasn't?",
        "all": "Tap all {n} dinosaurs that were {value}s."
      }
    }
  },
  "impostors": [],
  "rows": [
    {
      "label": "Tyrannosaurus", "qid": "Q14332", "fame": 0.651,
      "diet": "Carnivore",
      "description": "extinct genus of theropod dinosaurs",
      "hook": "is the famous \"king\" of the dinosaurs, with a huge skull and tiny two-fingered arms",
      "known": 0.95, "kind": "carnivore"
    }
  ]
}
```

### Row fields

| Field | Meaning |
|---|---|
| `label` | The thing's name. |
| `qid` | Its Wikidata ID. `null` for some hand-built rows. |
| `fame` | 0 to 1, from English Wikipedia views. See [FAME.md](FAME.md). |
| `known` | 0 to 1, roughly the share of ordinary players who know it. See [DIFFICULTY.md](DIFFICULTY.md). |
| `kind` | What sort of thing it is within the table. Options are always the answer's own kind. |
| `description` | Wikidata's short description (CC0). |
| `hook` | What it's famous for, in our words. Written to follow the name: "Tyrannosaurus *is the famous king of the dinosaurs…*" |
| anything else | The table's own columns (`diet`, `country`, `year`, `creator` …). `columns` names and types them. |

`kind: "list"` tables (14 of them) are closed memberships: the Beatles, NATO members, the Greek gods. They feed Odd One Out and All That Apply, where "not a member" has to be exact.

### Wording

`wording` says how a table asks. Each column has a **role**:

| Role | Meaning | Question styles it can carry |
|---|---|---|
| `link` | A value many rows share (a country, a diet, a team) | `pick`, `statement`, `match`, `odd`, `all`, `reverse` |
| `code` | A value one row owns (a car code, a chemical symbol) | `pick`, `reverse`, `statement`, `match`, `typeIt` |
| `date` | A year | `sort`, `era`, `shot` |
| `measure` | A number with a unit (a height, a speed) | `compare`, `sort`, `ask`, `scale` |

Placeholders: `{label}` is the row, `{value}` its value, `{n}` a count. Use [reference/value-names.json](../reference/value-names.json) to put a value into a sentence: it lowercases common nouns and adds "the" where English needs it ("the United States").

`hookAsk` and `hookStatement` are the sentences used to ask by a row's hook. `exclude` lists rows a style should skip, with a reason. `minFame` lowers or raises the fame floor for this table, with `minFameWhy`.

`impostors` are near-miss rows that are **not** members, kept so nobody adds them by mistake ("Titan: it orbits Saturn, not Jupiter").

## A built question

One line of `questions/built/getting-around/car-codes.jsonl`:

```json
{
  "id": "q.getting-around.bb8bbad2",
  "table": "table.getting-around.car-codes",
  "column": "country",
  "recipe": "trueFalse",
  "format": "fmt.f02",
  "widget": "choice",
  "prompt": "The international car code IL belongs to Greece.",
  "payload": { "widget": "choice", "options": [
    { "id": "a", "text": "True", "correct": false },
    { "id": "b", "text": "False", "correct": true } ], "selectMax": 1, "trueFalse": true },
  "learn": { "say": "The international car code IL belongs to Israel.", "rows": [],
             "more": "IL is a small Middle Eastern nation whose cities include Tel Aviv and Jerusalem." },
  "rows": ["Q801"],
  "genre": "daily-life", "category": "getting-around", "topic": "cars",
  "rating": "easy",
  "difficulty": { "tier": 2, "score": 0.25, "confidence": 0.5, "basis": "judged" },
  "template": { "verdict": "good", "score": 68, "why": "crisp lightning statement when the code is a familiar one", "judge": "model" },
  "tags": ["recipe-truefalse"],
  "timeSensitive": false,
  "licence": "CC-BY-4.0"
}
```

| Field | Meaning |
|---|---|
| `prompt` | What the player reads. |
| `payload` | The options and answers. `correct` marks right answers. Shape depends on `widget`. |
| `learn` | The reveal: a sentence (`say`), a table of what each option really was (`rows`), and a bonus line (`more`). |
| `rows` | The Wikidata IDs of the rows used. |
| `rating` | `easy`, `medium`, `hard`, or `bad` in `questions/rejected/`. |
| `difficulty` | The score behind the rating. See [DIFFICULTY.md](DIFFICULTY.md). |
| `template` | The judge's verdict on this question style. |
| `tags` | `recipe-…` and, where it applies, `year-context` (a year appears in the sentence as context only). |
| `timeSensitive` | From a volatile table. Recheck before you use it. |

### Widgets

| Widget | Payload |
|---|---|
| `choice` | `options[]` with `correct`. `selectMax` above 1 means tap all that apply. `countHint` says how many are right. |
| `order` | `items[]`, each with its `value`. The answer is ascending by value (smallest first, earliest first). |
| `match` | `pairs[]` of `left` and `right`. |
| `buckets` | `bins[]` (decades or centuries) and `cards[]`, each naming its right `bin`. |
| `number` | The `value`, its `unit` and `scale` (a fixed ruler, so the range never hints at the answer), and how close counts as a bullseye. |
| `text` | `answers[]` with accepted `aliases`, matched loosely. |

### Recipes and formats

| Recipe | Format | What it asks |
|---|---|---|
| `pick` | Pick One (F01) | Which of these is in Spain? |
| `reverse` | Pick One (F01) | Which of these did *X* make? |
| `hookPick` | Pick One (F01) | Which of these is famous for *the hook*? |
| `trueFalse` | True or False Lightning (F02) | *X* was made by *Y*. True or false? |
| `eitherOr` | Either / Or (F03) | Which is bigger? |
| `sort` | Sort It (F04) | Put these in order. |
| `closest` | Closest Call (F05) | Slide to the year or number. |
| `all` | All That Apply (F06) | Tap all 3 that … |
| `era` | Era Drop (F10) | Drop each into its decade. |
| `typeIt` | Type It (F11) | Type the answer. |
| `odd` | Odd One Out (F18) | Three of these are … Which one isn't? |
| `match` | Match Up (F20) | Match each to its partner. |
| `shot` | Bullseye (F27) | What year? Type it on the keypad. |

## A list

`lists/art/aquariums.json`, trimmed:

```json
{
  "id": "list.art.aquariums",
  "title": "Aquariums",
  "prompt": "Name a public aquarium",
  "category": "art", "topic": "landmarks",
  "people": false,
  "licence": "CC0-1.0",
  "rows": [ { "label": "Zhuhai Chimelong Ocean Kingdom", "qid": "Q16258099", "fame": 0.568, "also": ["Chimelong Ocean Kingdom"] } ]
}
```

`also` holds other names to accept. Lists keep obscure members too. Filter by `fame` for the famous core.

## A poll

`questions/polls/split-the-room.jsonl` holds 320 opinion questions with no right answer ("Notebook margins: doodles or clean pages?"). They work as a quick vote between rounds.

## Extras

| File | What it holds |
|---|---|
| `extras/survey-boards.json` | 636 survey boards. The answers real people gave to a cue in published studies, with how many gave each (`n`) and the study's `credit`. |
| `extras/dish-ingredients.json` | 449 dishes from every part of the world, with core and optional ingredients and accepted spellings. |
| `extras/estimate-auction-prices.json` | 386 famous auction sales and their price in US dollars. |
| `extras/estimate-weights.json` | 539 famous things and their weight in pounds. |
| `extras/estimate-film-scores.json` | 1,000 films and their critics' scores. |

Every `estimate-*` row has `ask` (the question), `value`, `unit`, and `source.url` (the page the number was checked on).

## Reference

| File | What it holds |
|---|---|
| `reference/template-verdicts.json` | Every question style's verdict, score, hardness and reason. |
| `reference/value-names.json` | How values read inside a sentence. |
| `reference/wildcards.json` | 161 household names used as a wildcard wrong answer. |
| `reference/blocklist.json` | What may never appear. See [FAMILY-FRIENDLY.md](FAMILY-FRIENDLY.md). |
| `stats.json` | Counts from the export. |
