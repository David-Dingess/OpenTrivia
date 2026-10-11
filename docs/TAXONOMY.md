# Taxonomy

Everything is filed **Genre › Category › Topic**. The full tree is [taxonomy.json](../taxonomy.json).

- A **genre** is a broad shelf (Science, Math, Technology). There are 6.
- A **category** is what a player picks (Biology). There are 31.
- A **topic** is one subject inside it (Dinosaurs). There are 187.
- A **table** is one set of facts on a topic (Dinosaurs and what they ate). A topic holds many tables.

Every table, list and question carries its `genre`, `category` and `topic`.

## Rules for the tree

1. **One home.** Every table sits under exactly one topic. If two fit, pick the one a player would look in first.
2. **Short, single-subject names.** "Film & TV", not "Film, Television and Streaming Media".
3. **Topics grow freely. Categories don't.** A new topic inside a category is cheap. A new category, a rename, a move or a merge was a human decision, made once and on purpose.
4. **Wants.** A topic can list `wants`: tables someone asked for that don't exist yet (217 of them). Each says what to ask ("superheroes → their secret identity"). They're a ready to-do list for anyone extending this.
5. **Barred.** A topic marked `barred` is never asked. World Records is barred: records go stale and invite arguments.

## Growing it

The set was grown in a fixed order. It's a fair order to keep:

1. Tables people asked for (the wants).
2. Coverage: the thinnest genre first.
3. Balance: keep genres within about 20% of each other.
4. Depth: more tables in topics people enjoy.
5. New topics.

## The tree

Counts are tables and lists filed under each topic. A blank means none yet: the topic exists, and its wants say what to build.

### Art & Entertainment

_movies and TV, music, books, famous paintings, Broadway_

| Category | Topic | Tables | Lists |
|---|---|---:|---:|
| Literature | Poetry | 2 | 1 |
| Literature | Classic Novels | 2 | 4 |
| Literature | Modern Fiction | 2 | 2 |
| Literature | Comics & Manga | 4 |  |
| Literature | Memoirs | 1 |  |
| Literature | Literary Devices | 1 |  |
| Literature | Fictional Worlds | 1 |  |
| Art | Renaissance Art | 1 | 1 |
| Art | Painters | 2 | 2 |
| Art | Sculpture | 2 | 1 |
| Art | Landmarks | 7 | 16 |
| Art | Photography | 1 |  |
| Art | Fashion | 2 |  |
| Art | Famous Homes | 2 |  |
| Art | Typography | 1 | 1 |
| Stage | Theater | 4 | 1 |
| Stage | Opera | 1 | 2 |
| Stage | Ballet |  |  |
| Stage | Dance | 1 | 1 |
| Stage | Magic | 1 |  |
| Film & TV | The Oscars | 4 | 1 |
| Film & TV | Box Office | 5 | 15 |
| Film & TV | Directors | 2 | 4 |
| Film & TV | Indie Film | 2 |  |
| Film & TV | Screenwriters | 2 |  |
| Film & TV | Animated Films | 3 | 3 |
| Film & TV | Cartoons & Anime | 2 | 3 |
| Film & TV | Sitcoms | 2 | 3 |
| Film & TV | TV Dramas | 2 |  |
| Film & TV | Classic TV | 2 | 1 |
| Film & TV | Reality TV | 2 |  |
| Film & TV | Streaming Shows | 2 |  |
| Music | Chart-Toppers | 2 | 13 |
| Music | Bands | 7 | 16 |
| Music | Grammys | 2 | 1 |
| Music | Composers | 3 | 2 |
| Music | Instruments | 1 | 1 |
| Music | Music Videos | 1 |  |
| Music | One-Hit Wonders | 1 |  |
| Music | Festivals & Scenes | 2 |  |
| Music | Record labels | 1 | 1 |

### Daily Life

_food and drink, shops and money, getting around, holidays_

| Category | Topic | Tables | Lists |
|---|---|---:|---:|
| Food & Drink | World Cuisine | 2 | 18 |
| Food & Drink | Fast Food | 1 | 2 |
| Food & Drink | Wine & Beer | 3 | 11 |
| Food & Drink | Ingredients | 5 | 2 |
| Food & Drink | Food History | 1 |  |
| Food & Drink | Sweets & Snacks | 2 | 8 |
| Food & Drink | Coffee & Tea | 1 | 4 |
| Food & Drink | Cooking | 5 | 1 |
| Food & Drink | Chefs | 2 | 1 |
| Business | Big Companies | 6 | 9 |
| Business | Slogans | 1 |  |
| Business | Logos | 1 |  |
| Getting Around | Cars | 7 | 6 |
| Getting Around | Airports | 6 | 2 |
| Getting Around | Trains | 1 | 7 |
| Getting Around | Ships | 1 | 6 |
| Getting Around | Roads | 1 | 2 |
| Getting Around | Canals & Routes | 1 | 1 |
| Holidays | Festivals | 5 | 4 |
| Holidays | Traditions | 6 |  |
| Holidays | Costumes | 3 | 1 |
| Holidays | Christmas | 3 |  |
| Money | Banknotes | 1 |  |
| Money | Coins | 1 | 1 |
| Money | Department Stores | 1 | 1 |
| Money | Markets | 2 | 4 |

### Games & Sports

_teams and athletes, video games, board games, toys_

| Category | Topic | Tables | Lists |
|---|---|---:|---:|
| Sports | Soccer | 4 | 3 |
| Sports | Football | 5 | 2 |
| Sports | Basketball | 3 | 3 |
| Sports | Baseball | 3 | 2 |
| Sports | Hockey | 2 | 3 |
| Sports | Tennis | 2 | 2 |
| Sports | Golf | 2 | 2 |
| Sports | Cricket | 3 | 1 |
| Sports | Rugby | 1 | 3 |
| Sports | Cycling | 1 | 1 |
| Sports | Racing | 3 | 4 |
| Sports | Combat Sports | 3 | 3 |
| Sports | Extreme Sports | 2 | 3 |
| Sports | Olympics | 3 | 22 |
| Sports | Stadiums | 2 | 1 |
| Sports | Sports Lore | 7 | 5 |
| Sports | Horse Racing |  |  |
| Sports | Wrestling | 2 | 1 |
| Sports | Darts & Snooker | 1 |  |
| Video Games | Consoles | 3 | 24 |
| Video Games | Best-Sellers | 4 | 3 |
| Video Games | Studios | 3 | 1 |
| Video Games | Indie Games | 2 |  |
| Video Games | Arcade | 1 | 1 |
| Video Games | Esports | 2 |  |
| Video Games | Soundtracks | 2 |  |
| Video Games | Game Mechanics | 2 |  |
| Video Games | Pokémon | 1 | 1 |
| Games | Chess | 2 | 1 |
| Games | Board Games | 4 | 1 |
| Games | Card Games | 1 | 1 |
| Games | Trading Cards |  |  |
| Games | Tabletop RPGs |  |  |
| Toys | Toy Lines | 4 | 1 |
| Toys | Hobbies | 2 |  |

### General

_wordplay, world records, the internet, oddities_

| Category | Topic | Tables | Lists |
|---|---|---:|---:|
| Oddities | Mysteries | 5 | 4 |
| Oddities | Strange Laws | 1 |  |
| Oddities | Eccentrics | 1 |  |
| Oddities | Odd Sports | 1 |  |
| Oddities | Heists | 1 |  |
| Oddities | Odd Traditions | 2 |  |
| Oddities | Natural Wonders | 2 | 18 |
| Oddities | Odd Place Names | 2 |  |
| Oddities | Optical Illusions | 1 |  |
| Oddities | Paradoxes and Biases | 1 | 4 |
| Wordplay | Acronyms | 4 |  |
| Wordplay | Phobias | 1 | 1 |
| Wordplay | Eponyms | 2 |  |
| Wordplay | Nicknames | 3 |  |
| Records | World Records (barred) |  |  |
| Internet | Social Media | 3 | 3 |
| Internet | Websites and Apps | 3 | 9 |
| Pop Culture | Astrology | 1 |  |
| Pop Culture | Famous Duos | 2 |  |
| Pop Culture | Famous Quotes | 1 |  |
| Pop Culture | Fads & Crazes | 2 | 1 |
| Pop Culture | Robots | 1 | 1 |
| Pop Culture | TV | 3 | 1 |
| Pop Culture | Awards | 2 |  |
| Pop Culture | Fictional Things | 6 | 13 |
| Pop Culture | Fictional Characters | 5 | 15 |
| Pop Culture | Comic Strips | 1 | 3 |
| Pop Culture | Thrill Rides | 1 | 4 |
| Pop Culture | Famous Jewels | 1 | 1 |
| Pop Culture | Newspapers and magazines | 1 | 2 |
| General Knowledge | How Many | 3 |  |
| General Knowledge | What Colour | 2 | 1 |
| General Knowledge | Symbols | 1 |  |
| General Knowledge | Original Uses | 1 |  |
| General Knowledge | Catchphrases | 2 |  |
| General Knowledge | What Shape | 2 |  |
| General Knowledge | Numbered Sets | 2 |  |
| General Knowledge | Patterns | 1 |  |
| General Knowledge | Made Of | 2 |  |

### Science, Math, Technology

_the planets, the elements, who invented it, the human body_

| Category | Topic | Tables | Lists |
|---|---|---:|---:|
| Biology | Wildlife | 9 | 25 |
| Biology | Sea Life | 1 | 3 |
| Biology | Insects | 1 | 5 |
| Biology | Genetics | 1 |  |
| Biology | Plants | 2 | 10 |
| Biology | Pets | 1 | 6 |
| Biology | Cat & Dog Breeds | 2 | 2 |
| Biology | Dinosaurs | 2 | 1 |
| Biology | Human Body | 3 |  |
| Biology | Medicine | 3 |  |
| Earth & Space | Space | 7 | 9 |
| Earth & Space | Weather | 3 |  |
| Earth & Space | Geology | 5 | 3 |
| Chemistry | Elements | 5 | 1 |
| Chemistry | Everyday Chemistry | 6 |  |
| Tech | Hardware | 2 | 2 |
| Tech | Coding | 5 | 5 |
| Math | Geometry | 3 | 3 |
| Math | Mathematicians | 2 | 2 |
| Math | Units | 4 |  |
| Inventions | Inventors | 9 | 1 |
| Inventions | Nobel Prizes | 1 | 4 |
| Inventions | Scientists | 2 | 9 |

### Society

_history, capitals and countries, myths and legends, languages_

| Category | Topic | Tables | Lists |
|---|---|---:|---:|
| History | Ancient World | 6 | 4 |
| History | Middle Ages | 3 | 1 |
| History | Wars | 5 | 4 |
| History | Rulers | 6 | 23 |
| History | Archaeology | 3 | 2 |
| History | Universities | 5 | 1 |
| History | Explorers | 2 | 1 |
| History | Speeches & Documents | 1 | 1 |
| History | Empires | 1 | 2 |
| History | Pirates & Spies | 2 | 2 |
| Geography | Capitals | 6 | 1 |
| Geography | Cities | 2 |  |
| Geography | Borders & Maps | 6 | 14 |
| Geography | Rivers & Lakes | 3 | 7 |
| Geography | Mountains & Deserts | 4 | 11 |
| Geography | Flags & Symbols | 5 |  |
| Myth & Legend | Mythology | 8 | 7 |
| Myth & Legend | Urban Legends | 1 |  |
| Myth & Legend | Cryptids | 1 |  |
| Religion | World Religions | 5 | 3 |
| Religion | Sacred Places | 3 | 7 |
| Language | Languages | 5 | 1 |
| Language | Words | 3 |  |
