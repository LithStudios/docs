# Locale | Translations

All player-facing copy for `ls_mining` lives in a single file at the resource root:

```
locale.lua
```

There is no per-language folder — edit `Locale = { ... }` directly for your server's language. Keys use dot-separated hierarchy; config and shop entries store **locale keys**, not literal English, and resolve at runtime via `L()`.

## File shape

```lua
Locale = {
    ['interaction.mine'] = 'Mine',
    ['interaction.enter_mine'] = 'Enter mine',
    ['blip.mine'] = 'Mine',
    ['pickaxe.broken'] = 'Your pickaxe is broken. Equip another pickaxe.',
    ['nui.shop.title'] = 'Mining Shop',
    ['rank.gravel_rat'] = 'Gravel Rat',
    ['rank.perk.gravel_rat.blasting'] = 'Unlock: Blasting (clear cave blockers with dynamite)',
}
```

{% hint style="warning" %}
**Keys must remain unchanged.** Only translate the string values. Renaming or removing keys breaks config references, NUI hydration, and rank perk display.
{% endhint %}

## Key groups

| Prefix | Used for |
|--------|----------|
| `interaction.*` | Entity prompts (mine, enter/exit, smelt, sell, dynamite) |
| `blip.*` | Map blip labels from `config.lua` |
| `pickaxe.*` | Equip, broken, and mining-block notifications |
| `blocker.*` | Blasting lockout, dynamite, blocker cleared |
| `smelting.*` | Smelting selection UI and minigame overlay |
| `ore.*` | Ore and bar display names in smelting |
| `shop.item.*` | Shop row titles |
| `shop.error.*` | Shop purchase failure reasons (NUI) |
| `nui.*` | Stats phone tabs, stats labels, leaderboards, shop |
| `rank.*` | Localized rank display names |
| `rank.perk.*` | Perk lines on the **Experience card** |

## Rank names

Internal rank ids stay as English keys in `Config.experience` (e.g. `'Gravel Rat'`). Players see localized names through `RankL()`, which maps to `rank.<slug>` entries:

```lua
['rank.gravel_rat'] = 'Gravel Rat',   -- Config key: 'Gravel Rat'
['rank.king_of_the_hill'] = 'King of The Hill',
```

Do not rename `Config.experience` keys for translation — add or edit `rank.*` locale entries instead.

## Placeholders

Some strings accept `string.format` placeholders:

| Key pattern | Placeholders |
|-------------|--------------|
| `interaction.place_dynamite` | `%s/%s` — current stick / required sticks |
| `blocker.blasting_locked` | `%s` — required rank display name |
| `nui.xp.to_next` | `%d XP • %d XP to %s` — progress values and next rank |
| `nui.smelting.sold` | `%dx for %s` — quantity and formatted money |
| `smelting.exit_hold` | `%d%%` — hold-to-exit progress |

GTA input hints use native tokens where noted (e.g. `~INPUT_CELLPHONE_CANCEL~` in `smelting.exit_hold`).

## Config and shop labels

Fields that reference locale keys (not literal text):

* `Config.cave_blips.blip.label`, `Config.shop_crate.blip.label`, etc.
* `Config.smelting.*.label` — ore names in smelting UI
* `shop/items.lua` → `label = 'shop.item.rusty_pickaxe'`
* `Config.rank_perks.*.perks` — list of `rank.perk.*` keys

After editing locale values, restart the resource. If you changed strings bundled into the Vue NUI (`html/src/locales/` or hardcoded fallbacks), rebuild:

```bash
cd html && npm run build
```

Most gameplay notifications use Lua `L()` and do not require an NUI rebuild.

## NUI locale store

The stats phone loads a locale payload from the server when opened. Keys under `nui.*` drive tab labels, stat row titles, shop copy, and leaderboard headers. Keep Lua `locale.lua` and any NUI locale exports in sync when adding new UI strings.

## Related pages

* [Configuration (config.lua)](./config.md) — which config fields store locale keys
* [Overview](./README.md) — stats phone commands and features
