# Locale | Translations

User-facing strings for `ls_signs` live in `locale.lua` at the resource root. The sign creator panel text is mostly fixed in the shipped NUI (`web/`); this file covers strings used from Lua (e.g. keybind labels).

## locale.lua (full file)

Complete default locale as shipped. Edit values only — **do not rename keys**.

```lua
--- Server-editable player-facing strings (single active language).

Locale = {
    ['keybind.open_creator'] = 'Open the sign creator',
}

--- @param key string locale key
--- @vararg any string.format placeholders
function L(key, ...)
    if type(key) ~= 'string' then
        return key
    end
    local value = Locale[key]
    if value == nil then
        return key
    end
    if select('#', ...) > 0 then
        return string.format(value, ...)
    end
    return value
end
```

## Keys in use

| Key | Used for |
|-----|----------|
| `keybind.open_creator` | FiveM key mapping description when `Config.openKeybind` is set |

## Customization

* Translate the **value** on the right of each entry; keep the key string unchanged.
* `L(key, ...)` supports `string.format` placeholders (`%s`, `%d`, etc.) if you add them to future keys.
* Permission denied and command feedback messages in `client/main.lua` are currently hardcoded with GTA colour codes (`~r~`, `~g~`). To localize those, edit the client file or add keys to `Locale` and replace the literals in a future update.

## After changing locale

Restart the resource:

```cfg
refresh
ensure ls_signs
```

No NUI rebuild is required for `locale.lua` changes.
