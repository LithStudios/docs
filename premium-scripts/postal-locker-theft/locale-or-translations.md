---
description: Locale (translations) file for postal locker theft
---

# Locale | Translations

```lua
LOCALE = {
    ['carry_prompt'] = 'Press %s to loot ~n~Press %s to drop',
    ['3d_loot_prompt'] = 'Press %s to loot item',
    ['target_loot_prompt'] = 'Loot item',
    ['3d_hack_prompt'] = 'Press %s to hack locker',
    ['target_hack_prompt'] = 'Hack locker',
    ['3d_break_door_prompt'] = 'Break open door',
    ['target_break_door_prompt'] = 'Break open door',
    ['minigame_title'] = '',
    ['minigame_info'] = 'Enter keys in sequence',
    ['3d_pickup_prompt'] = 'Press E to pick up',
    ['target_pickup_prompt'] = 'Pick up',
    ['dispatch_message'] = 'Locker theft',
    ['dispatch_description'] = 'A postal locker is being broken into',
    ['dispatch_code'] = '10-31',
    ['dispatch_blip_message'] = 'Post locker theft'
}

function L(prompt)
    return LOCALE[prompt]
end
```
