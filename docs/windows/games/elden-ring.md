# Elden Ring

## Mods

The game, installed with Steam, is capped at 60 fps.

Download:

- [Anti-cheat toggler and offline launcher](https://www.nexusmods.com/eldenring/mods/90?tab=files&file_id=4063)
- [Elden Mod Loader](https://www.nexusmods.com/eldenring/mods/117?tab=description)
- [Unlock the framerate](https://www.nexusmods.com/eldenring/mods/216?tab=description)

## Anti-cheat toggle

Extract the contents of "ToggleAntiCheat-xxx.zip" inside the game folder (`C:\Program Files (x86)\Steam\steamapps\common\ELDEN RING\Game`).

Run "toggle_anti_cheat.exe" and it will disable EAC and turn on any installed DLL mods. (Run the .exe again to re-enable the anti-cheat and disable all DLL mods, letting you play online again without issues.)

While the anti-cheat is off, the game will say "inappropriate activity detected" in the main menu, this is fine.

## Mod Loader

Extract the contents of "EldenModLoader--xxx.zip" inside the game folder (`C:\Program Files (x86)\Steam\steamapps\common\ELDEN RING\Game`).

Any mods (.dll files) in the "mods" folder will then load on game launch.

To uninstall/disable all mods, rename or delete "dinput8.dll".

## Framerate unlock

> Turn off vsync or any other graphics card setting that may lock the FPS: [steps](https://github.com/uberhalit/EldenRingFpsUnlockAndMore?tab=readme-ov-file#follow-these-steps-on-nvidia-see-below-for-gsync) (the mod on the linked page is not mine).
> Download Elden Mod Loader which will automatically load the mod on startup.
> If you're having issues, try putting the game into borderless windowed in the game graphics options.

Extract the contents of "UnlockTheFps---xxx.zip" inside the game folder (`C:\Program Files (x86)\Steam\steamapps\common\ELDEN RING\Game`).

Edit the limit value inside "mods\UnlockTheFps\config.ini".
