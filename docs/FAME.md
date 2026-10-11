# The fame threshold

Every row in a table is something ordinary people have heard of. That rule is the fame threshold, or fame floor.

## Why it exists

A trivia question can be hard in two ways.

- **A fair stretch.** You've heard of the Sahara and the Gobi. Which one is bigger? You have to think.
- **A stranger.** Which of these did Ward Cunningham invent? Most people have never heard the name. Nobody learns anything. Nobody has fun.

This set only wants the first kind. So difficulty comes from the fact you're asked about, never from an obscure name. The fame floor is how that rule is enforced in data.

## What "fame" measures

Fame is a number from 0 to 1. It comes from how many times the thing's **English Wikipedia** article was read.

1. Take the article's views over the **last 30 complete days**. Human readers only (user-agent views, all access methods), from the Wikimedia Pageviews API.
2. Turn the views into fame on a log scale:

   `fame = clamp((log10(views + 1) − 2) / 4.5, 0, 1)`

3. If an article has no view data, fall back to how many Wikipedias have an article on it (Wikidata sitelinks):

   `fame = clamp(log10(sitelinks + 1) / 2.3, 0, 1)`

Going the other way, `views ≈ 10^(2 + 4.5 × fame)`.

| Fame | Views a month | Feels like |
|---:|---:|---|
| 0.25 | about 1,300 | niche |
| 0.33 | about 3,000 | known to fans |
| **0.45** | **about 10,600** | **the floor: a pub-quiz crowd has heard of it** |
| 0.55 | about 30,000 | well known |
| 0.68 | about 115,000 | famous |
| 0.80 | about 400,000 | a household name |

The idea comes from PopQA (Mallen et al., 2023), which showed that page popularity predicts how many people get a fact right. See [CREDITS.md](../CREDITS.md).

## The floors

| Where | Fame | About | Why |
|---|---:|---:|---|
| **Any row in a table** | **0.45** | **10k views** | The main rule. |
| "Type It" answers (you type the answer, no options) | 0.80 | 400k | You can only type what you can spell from memory. |
| Dishes (`extras/dish-ingredients.json`) | 0.33 | 3k | Food articles get fewer views than their fame deserves. Brunswick stew is known but quiet. |
| Weights (`extras/estimate-weights.json`) | 0.22 | 1k | Everyday things (a sheep, a bowling ball) read low on views. Checkers cut obscure rows by hand, so this floor only screens out true oddities. |
| Lists (`lists/`) | none | | Lists keep every member, obscure ones too, by name only. See below. |

## When the floor misfires

View counts are a proxy, and a proxy can be wrong.

- **Everyday things.** Merlot scores 0.39. Everyone at a pub quiz knows it, but few people look it up. Hand tables of everyday concepts (foods, grapes, shapes) may keep a row under 0.45 when most adults would know it. People, places, works and brands keep the 0.45 floor. A second gate, `known`, does the real work for concepts (see below).
- **Redirects.** Butterbeer, Duff Beer and Hogwarts are household names, but their articles redirect into the franchise page and show almost no views. Tables of fictional foods and places drop the floor and use a hand-picked famous list instead.
- **Quiet pages, loud answers.** Contest-year pages (one article per year of a song contest) get few views, but the question asks for the winning country, which is mainstream. Hobby words (philately, vexillology) get a 0.40 floor because the question asks what the word means.
- **News spikes.** A 30-day window catches a death, a scandal or a release. A spike can lift a name over the floor for a month. The `known` card, rated separately, catches most of these.
- **English bias.** It's English Wikipedia only. Fame here means famous to English speakers.

## The second gate: known

Fame says how many people *read about* a thing. It doesn't say how many *know the fact*. So every row also has a `known` score, from 0 to 1: roughly the share of ordinary players who would know it. A model (Claude Haiku) rated it, table by table, with the whole table in view.

| Rule | Known at least |
|---|---:|
| Any row asked about or offered as an option | 0.40 |
| A row whose name is the clue ("Which of these did *X* invent?") | 0.60 |
| A True or False lightning statement | 0.60 |

A row can pass the fame floor and still sit out on `known`. That's on purpose.

## Lists are the exception

`lists/` holds 546 "name a ..." lists with 281,941 names. They keep **every** member, obscure ones included, because they're for checking a player's typed answer ("Name a public aquarium"). A list is never asked from. Each name still has its `fame`, so you can cut a list to the famous core yourself.

## Reproducing it

The view window rolls. Run the same row a month later and you'll get a slightly different number. The `fame` stored in each row is the value at build time (September to October 2026). Treat it as a snapshot.
