# CrossplayFishing

Custom fishing for **cross-play servers** (Paper or Folia with Geyser/Floodgate) with a mini-game that **Bedrock
players can play too**: Java with the mouse, Bedrock with a finger or a controller. No resource pack.

Custom fishing plugins either have no mini-game, or turn it off for Bedrock players because it needs a resource pack
or a mouse. On a cross-play server, the player on a phone just gets a fish with no game, or a broken screen. In
CrossplayFishing you follow the fish by turning your head; the bar is plain text in the action bar, so every client
shows it and there is nothing to break after an update.

> **Status:** version 1.0.0 is in final testing, not released yet. Free edition: SpigotMC, CurseForge and
> [Releases](../../releases/latest); full edition: Payhip (links when published).

## Editions

The mini-game, anti-autofish and selling are never limited in the free edition.

| | Free | Full (12.99 USD) |
|---|---|---|
| Mini-game for Java and Bedrock, anti-autofish | yes | yes |
| Custom fish with rarity, size, weight and conditions | 32 water fish | 37 (with lava fish) |
| Selling (Bedrock form, Java chest menu) | yes | yes |
| Codex and completion rewards | no | yes |
| Tournaments | no | yes |
| Baits, rod upgrades, daily quests | no | yes |
| Lava fishing | no | yes |
| Import from EvenMoreFish, PlaceholderAPI | no | yes |

## The mini-game

A fish above common rarity starts the mini-game when it bites: a track in the action bar with the fish and a green
zone. Turn your head left and right to keep the fish in the zone; the bar fills while it is inside and empties while
it is outside. Each rarity has its own fish speed, sudden turns and zone width (`rarities.yml`). Common fish are
caught at once (`minigame.skip-rarities`).

- **Bedrock:** the head turns with a finger or a stick, exactly like on Java with the mouse. Touch players get a
  slightly wider zone (`minigame.zone-bonus.touch`), detected by Floodgate.
- **Anti-autofish:** a player whose head has not moved in the last minutes (an auto-clicker, a fishing farm) catches
  neither custom fish nor treasure, and a mini-game without any head movement fails.
- **Treasure** goes through the mini-game too (`loot.treasure-difficulty`).

## What else it does

- **37 fish in 5 rarities** (common, uncommon, rare, epic, legendary), with size, weight and conditions: biome or
  group of biomes, day or night, weather, world, height. Fish are vanilla items with a name, a rarity color and a
  lore; they look right on Bedrock without a pack.
- **Selling:** on Bedrock a native form (sell all with the total, or species by species, then a confirmation); on Java
  a chest menu where you drop your fish. Price by species, rarity and size. A fish is never paid twice, and if the
  economy refuses the deposit the fish come back.
- **Codex** (full): every species, "???" until caught, then where it lives, how many you caught, your record and the
  server record. Completing a rarity gives a reward.
- **Tournaments** (full): biggest fish, most fish, points by rarity, or one species. Scheduled (`SAT 20:00`,
  `daily 18:00`) or started by command, with a boss bar, `/cfish top` and rewards by rank.
- **Baits and rod upgrades** (full): baits make fish bite sooner, bring rarer fish or specific species; three rod
  upgrades with 5 levels each (Chance: rarer fish, Speed: faster bites, Stability: wider green zone). The menus show
  your balance and stay open after a purchase.
- **Daily quests** (full): 3 per player and per day (catch a species, a rarity, at night, in the rain, a big one, sell
  for an amount), with rewards.
- **Lava fishing** (full): cast into lava, the bobber floats above it (Bedrock players see it too), and the action
  bar tells you when it bites. 5 lava fish, two of them only in the Nether.
- **Rewards** (money, items, baits, console commands): a player who is offline gets them in a recovery box
  (`/cfish claim`) when they come back, and so does a reward that does not fit in a full inventory.

## Commands

| Command | What it does | Permission (default) |
|---|---|---|
| `/cfish` | main menu | `crossplayfishing.use` (everyone) |
| `/cfish sell [all]` | sell menu, or sell every fish at once | `crossplayfishing.use` |
| `/cfish claim` | recovery box: rewards that could not be given | `crossplayfishing.use` |
| `/cfish codex`, `bait`, `rod`, `quests`, `top` | open a menu directly (full edition) | `crossplayfishing.use` |
| `/cfish tournament start <type> <duration> [species]`, `stop` | tournaments (full edition) | `crossplayfishing.admin` (op) |
| `/cfish import emf [confirm]` | import from EvenMoreFish (full edition) | `crossplayfishing.admin` |
| `/cfish give <player> <fish> [size]`, `give <player> bait:<id> [amount]` | give a fish or a bait | `crossplayfishing.admin` |
| `/cfish reload`, `/cfish version` | admin | `crossplayfishing.admin` |

`/fish` is an alias of `/cfish`.

## Import from EvenMoreFish (full edition)

`/cfish import emf` reads `plugins/EvenMoreFish` (2.x with `rarities/`, or 1.x with `fish.yml` and `rarities.yml`)
and shows what will be converted and what has no equivalent (heads, void fishing, exact in-game times...), without
writing anything. `/cfish import emf confirm` backs up your files (`fish.yml.bak-<date>`...), adds the rarities and
fish, and their names to the language files. Nothing existing is overwritten: a fish with the same id as one of yours
gets the suffix `_emf`. EvenMoreFish files are only read.

## PlaceholderAPI (full edition)

`%crossplayfishing_caught%` (fish caught), `%crossplayfishing_discovered%` (species caught),
`%crossplayfishing_record_<fish>%` (personal record, cm), `%crossplayfishing_tournament_rank%`,
`%crossplayfishing_tournament_top_<n>_name%`, `%crossplayfishing_tournament_top_<n>_score%`.

## Configuration

Everything is in `plugins/CrossplayFishing/`, commented, and works without any change:

- `config.yml`: language, mini-game (cells, degrees per cell, anti-autofish, zone bonus by input), loot shares,
  lava fishing and codex rewards (full).
- `fish.yml` (species and biome groups), `rarities.yml` (draw weight, price multiplier, mini-game difficulty).
- Full edition: `baits.yml`, `upgrades.yml`, `quests.yml`, `tournaments.yml`.

## Languages

`lang/en.yml` and `lang/fr.yml` (MiniMessage). **Every text is there, fish names and descriptions included**: copy
`en.yml` to `es.yml`, translate, done. Each player gets the language of their game when a file exists (Bedrock
included), otherwise `language` from the config. Text added by an update is added to your files at startup, without
touching what you changed.

## Requirements

- Paper or Folia 1.21.4 to 26.x, Java 21+ (tested on Paper 1.21.11, Paper 26.3 and Folia 26.3)
- For selling and money rewards: [Vault](https://www.spigotmc.org/resources/vault.34315/) (on Folia: VaultUnlocked,
  the maintained fork of Vault) **and an economy plugin**. Without them fishing works and selling is turned off.
- Optional: [Floodgate](https://geysermc.org/download), for the native Bedrock forms. Without it, Bedrock players get
  the chest menus.
- Optional (full edition): [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/).
- No resource pack. No license server.

## Data

`plugins/CrossplayFishing/data.db` (SQLite): codex, records, quests, tournament results, recovery box.

## Support

Bug reports and questions: [issues](https://github.com/TheMax98000/CrossplayFishing/issues).

## Also by the author

- [CrossplayMarket](https://www.spigotmc.org/resources/crossplaymarket-free.139834/): auction house with native
  Bedrock menus.
- [CrossplayHomes](https://www.spigotmc.org/resources/crossplayhomes.139801/): homes and TPA with native Bedrock
  menus.
- [CrossplayShield](https://www.spigotmc.org/resources/crossplayshield.139762/): anti-exploit for cross-play servers
  that does not kick Bedrock players.
- [BedrockGuard](https://www.spigotmc.org/resources/bedrockguard-free.139718/): anti-cheat built for Bedrock players.
- [BedrockAssist](https://www.spigotmc.org/resources/bedrockassist.139746/) (free): native Bedrock menus for what
  Geyser cannot translate.
