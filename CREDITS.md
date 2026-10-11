# Credits

This trivia stands on other people's work. Here is all of it.

## Data in this repo

| Source | What we took | Licence |
|---|---|---|
| **[Wikidata](https://www.wikidata.org/)** and its contributors | The facts in 380 tables and all 546 lists. Row names, QIDs, short descriptions, review scores. Each table's `source.method` is the exact query that built it. | CC0 1.0 |
| **[Wikimedia Pageviews API](https://wikimedia.org/api/rest_v1/)** | 30-day English Wikipedia view counts, turned into each row's `fame` score. | CC0 1.0 |
| **[English Wikipedia](https://en.wikipedia.org/)** and its editors | The source we checked 99 hand-built tables against, row by row. Also the source for the dish ingredients and most auction and weight facts. Facts only. No sentence was copied. | Facts. Text is CC BY-SA 4.0 and was not reused. |
| **[Wikibooks Cookbook](https://en.wikibooks.org/wiki/Cookbook:Table_of_Contents)** | Ingredient facts for some dishes. | CC BY-SA 4.0 |
| **[Open Food Facts](https://world.openfoodfacts.org/)** | One table of grocery brands and their makers (15 rows). | ODbL 1.0 |
| **Buchanan, E. M., Valentine, K. D., & Maxwell, N. P. (2019).** English semantic feature production norms. [osf.io/cjyzw](https://osf.io/cjyzw/) | 542 survey boards: the words people listed for a cue. | CC BY 4.0 |
| **Banks, B., & Connell, L. (2023).** Category production norms. [osf.io/jgcu6](https://osf.io/jgcu6/) | 71 survey boards: the members people named for a category. | CC BY 4.0 |
| **Boratko, M., et al. (2020).** ProtoQA: A question answering dataset for prototypical common-sense reasoning. Crowdsourced dev set. [github.com/iesl/protoqa-data](https://github.com/iesl/protoqa-data) | 16 survey boards. | CC BY 4.0 |
| **Zheng, Brady, Eramudugolla & Anstey (2026).** Updated Australian category norms. [doi.org/10.1080/00049530.2025.2607180](https://doi.org/10.1080/00049530.2025.2607180) | 7 survey boards. | CC BY 4.0 |
| Auction houses, museums, makers, sports rule books and news sites | The price or weight in each `extras/estimate-auction-prices.json` and `extras/estimate-weights.json` row. Each row keeps the page it was checked on in `source.url`. | Facts |

## Ideas we borrowed

| Work | What it taught us |
|---|---|
| **PopQA.** Mallen, A., Asai, A., Zhong, V., Das, R., Khashabi, D., & Hajishirzi, H. (2023). *When Not to Trust Language Models: Investigating Effectiveness of Parametric and Non-Parametric Memories.* ACL 2023. [huggingface.co/datasets/akariasai/PopQA](https://huggingface.co/datasets/akariasai/PopQA) | Popularity predicts how many people get a fact right. That is where our fame score and fame floor come from. |
| **[burggraf/triviadb](https://github.com/burggraf/triviadb)** | Build trivia from CC0 structured facts, have a model write it, check it against the source. A strict CC0-first policy. |
| **[muety/linkeddata-trivia](https://github.com/muety/linkeddata-trivia)** | Questions generated straight from linked-data facts. |

## Studied, not used

We read these to learn what a trivia set looks like and where the licence traps are. **Nothing from them is in this repo.** Some are clean (Open Trivia Database, Mintaka, SimpleQA). Some carry rights we could not clear (Jeopardy! archive dumps, quizbowl packets, pub-quiz compilations, FunTrivia-derived sets). The clean ones are listed because they shaped our thinking:

- [Open Trivia Database](https://opentdb.com/) (CC BY-SA 4.0)
- [Mintaka](https://github.com/amazon-science/mintaka) (Amazon, CC BY 4.0)
- [SimpleQA](https://huggingface.co/datasets/basicv8vc/SimpleQA) (OpenAI, MIT)
- [TriviaQA](https://nlp.cs.washington.edu/triviaqa/) (Apache 2.0)

## Who made it

- **David Dingess** led the project, set every rule in [docs/FAMILY-FRIENDLY.md](docs/FAMILY-FRIENDLY.md), chose the taxonomy, asked for the tables, and rated the samples that calibrated the judges.
- **Claude** (Anthropic), working in Claude Code sessions, built and checked the tables, wrote the hooks and wording, rated how well known each row is (Claude Haiku), and judged every question style (Claude Sonnet).
