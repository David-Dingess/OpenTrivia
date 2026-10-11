# Family-friendly and out of arguments

The trivia was made to be played in front of anyone. So the content had to be safe for a family room and dull for an argument. These rules did that. They're all still true of the data here.

## The line

1. **PG-13 at most.** Nothing sexual. No gore. No drugs. Nothing a parent would wince at on a TV in the living room.
2. **When in doubt, remove.** Contested, disputed, political, violent at heart, sexual, or simply unsure: it's out. Nobody argued for a row. A doubtful row was cut.
3. **No politics in fun tables.** No politicians as answers in light topics. No politicians or religious figures as wildcard options.
4. **No live controversy.** A person in the middle of a public scandal is left out, even when they're famous for something else.
5. **Facts, not opinions.** No question asks you to judge a person, a country or a belief. The opinion polls are about doodling and pizza toppings, never anything political, medical or about a real private person.
6. **Religion as fact.** Religion is a category (holy books, festivals, sacred places). It asks what and where, never who's right.
7. **History is allowed to be history.** A war or a death in a history fact is fine. Lingering on violence is not.
8. **Contested is removed.** If a pub would argue about the answer, it's not a question. Where Krav Maga comes from, or Karate, is out. Wrong beats contested, and both are removed.

## The blocklist

[reference/blocklist.json](../reference/blocklist.json) lists entities that may never appear in a table, a list or a question. Code refuses any row that names one. It's a safety line, not a judgement of the work or the person.

Each entry is a Wikidata QID, its name and one category:

| Category | Examples |
|---|---|
| nudity | famous nude paintings |
| sexual themes | novels and series built on sexual content |
| mature animation | anime rated for adults, or banned for its content |
| hate | hateful texts, and topics that invite hate talk |
| profanity in the name | a programming language with a swear in its name |
| slur in the title's common use | a classic whose title became a slur |
| public controversy | people in the middle of a public scandal |
| contested political figure | a statesman whose record divides people |

The list is short (22 entries) because the fame floor and "when in doubt, remove" did most of the work earlier, at the table.

## Rows with no clean hook

Every row gets a hook: what it's famous for, in our words. Some famous things are famous only for something past PG-13. Those 67 rows got no hook and are never asked by their famous-for line.

## Fiction caps

Fiction is fun, but a trivia set can drown in one franchise. These caps were held when choosing what to play:

- At most **25** in-universe questions from one work.
- At most **100** from one franchise.
- At least **70%** of what plays is real-world facts.
- No quoted dialogue, no lyrics, no catchphrases.

The built questions here are the whole pool, not a playlist. If you serve them, apply the caps yourself (`category` and `table` make it easy).

## Clean room

1. **Facts are free. Words are not.** Every fact here is checked against a source. Every sentence is our own.
2. **Nothing copied.** No question, clue or description was lifted from another trivia set, a quiz show, or Wikipedia. The only text taken as is is Wikidata's short descriptions, which are CC0.
3. **Nothing unconfirmed.** A row that couldn't be checked was removed, not guessed.

## The question rules (R1 to R15)

These are enforced by code (lint) or by a judge. The code refuses to build a question that breaks a lint rule.

| ID | Rule |
|---|---|
| R1 | **Sliding year gap.** Two dated items in one question are at least `max(3, 15% of the older one's age)` years apart. 2020 and 2023 is fine. 1800 needs 34 years. |
| R2 | **No-date formats.** True or False, Either / Or and Match Up never hinge on a date. A false statement swaps in a believable neighbour of the same kind (Minecraft "made by Nintendo"), never a flipped year. Either / Or compares only gut-feel sizes: area, height, length, speed, weight. |
| R3 | **Year slider.** A "closest year" question covers the last 50 years. |
| R4 | **Era Drop bins fit the subject.** Decades for modern things, centuries for old ones, never mixed. No card sits on a bin's edge. |
| R5 | **What-for.** Every award or record says what it was for, in our words. |
| R6 | **Count hints.** "Tap all 4" tells you how many are right. |
| R7 | **Same kind.** Every wrong option is the answer's own kind. NFL teams beside an NFL team. |
| R8 | **Famous answers to type.** A Type It answer is a household name (fame 0.80 or more). |
| R9 | **Honest ladders.** Every clue before the last fits at least two options. The first fits at least three. |
| R10 | **Odd by kind.** The odd one out is a different kind of thing, never a different date. |
| R11 | **Match = association.** Every pair is a thing and its partner (inventor and invention), never a date. |
| R12 | **Date cap.** At most 20% of a category's questions hinge on a date. |
| R14 | **One direction.** Every sort runs ascending: earliest to latest, smallest to biggest. |
| R15 | **Any-year shots.** Bullseye asks one famous thing's year (1000 to now). Nothing in the sentence names a year, decade or century. |

(R13 retired a format that is no longer used.)

On top of these, the code enforces:

- **No giveaways.** A row's name never shares a word or root with its answer. "What language is spoken in Turkey?" is never built.
- **No place giveaways.** "The Sydney Opera House" is never asked about countries.
- **Known floors.** Every row asked about is known by at least 40 of 100 players. See [FAME.md](FAME.md).
- **Typical measures say so.** "Which usually lives longer?", never "Which lives longer?"

## Family-friendly is not kid-only

PG-13 is the line, not "for small children". A few tables are fine for a family room but not for a classroom:

- `food-and-drink/wine-grapes-region`, `food-and-drink/spirits-made-from` and drinks in `food-and-drink/drinks` (alcohol)
- `pop-culture/horror-icons` (horror films)
- `games/card-games` (poker and other betting games, as games)
- History tables with wars and battles (facts, never gore)
- Film, TV and book descriptions and hooks, which name a plot's murder or heist the way a TV guide would

If you need content strictly for kids, drop those tables. [TAGGING-IDEAS.md](TAGGING-IDEAS.md) suggests an age-band tag that would do this properly.
