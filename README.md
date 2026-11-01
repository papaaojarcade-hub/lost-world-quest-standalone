<p align="center"><img src="Docs/poster.jpg" width="320" alt="The Lost World VR - Quest Stand Alone" /></p>

# The Lost World VR - Quest Stand Alone

Play Sega's 1997 light-gun arcade game **The Lost World: Jurassic Park** in VR, **entirely on a Meta Quest headset**. No PC, no streaming, no cables: the Sega Model 3 emulation runs on the headset itself, in stereo 3D with the controller as your gun, with a two-player mode over your network or the internet.

> ### A fork, and a thank you
> This project is a fork of **[headsplosion/lost-world-supermodel-pcvr](https://github.com/headsplosion/lost-world-supermodel-pcvr)**, the original **PC VR** version of The Lost World. Everything that makes the game feel right in VR - the OpenXR rendering that draws the world beyond the arcade screen, the controller-as-gun aiming, the in-headset menu, cinema mode and the first Quest port - is that project's work.
> **Thank you to headsplosion for creating it and making it open source.** This fork only adds the pieces listed below on top of it. The original PC VR documentation is kept in [`Docs/PCVR-README.md`](Docs/PCVR-README.md).

> **No game files are included.** You need your own `lostwsga.zip` ROM set (The Lost World, Japan, Revision A), dumped from hardware you own. Please don't ask for ROMs in issues.

## What this fork adds to the PC VR version

**Runs on the headset**
- A standalone Android/OpenXR build for **Quest 2, Quest Pro, Quest 3 and Quest 3S**. Install the APK and play: nothing else is needed.
- Its own app (`com.papas.lostworldstandalone`) and icon, so it sits next to your other games.
- A VR preset tuned for the headset is bundled (vignette off, soft 2D scaling, hit-static fill off, reduced render resolution), and refreshed when a newer preset ships (your old settings are backed up).
- The first run unpacks its own configuration; it asks for nothing but your ROM.

**Two players, each on their own headset**
- **Lockstep netplay:** both headsets run the whole game and swap only controller input, so the picture and sound stay full quality and the game stays in step (checked every second).
- **Same network (LAN):** the host opens a room, the other player finds it automatically.
- **Over the internet:** no set-up for players. The host's router is opened automatically (UPnP) and the room gets a **room code**; or pick a game from the **public game list**; or use your own relay server (see [`Server/`](Server/README.md)).
- **Choose your own room code** instead of a generated one.
- **Voice chat** through the headsets' microphones while you play.
- **Partner's aim:** a **blue ring** shows where the other player is pointing (yours is red).
- The host's game state is copied to the joiner at the start, so both begin from the same place.

**Cheats** (menu tab **CHEATS**)
- **Stage select:** start the next game on stage 1-5.
- **Infinite health** and **endless ammo** for each player, **free play**, and an **ADD CREDITS** button.
- In a two-player game **only the host's cheats count**: the host sets them before starting the session, and they are locked for both players while it runs.

**Also**
- A game list that also starts **The Ocean Hunter** if you copy its ROM (experimental, not described here).

## Install

You need a Quest in developer mode and your own `lostwsga.zip`.

1. **Download the app.** Get `LostWorldVR-quest.apk` from the [Releases](../../releases) page.
2. **Put the headset in developer mode** (Meta Horizon app on your phone: *Devices* > your headset > *Developer mode*), then connect it to your PC with USB and allow USB debugging inside the headset.
3. **Install the APK** with [Meta Quest Developer Hub](https://developers.meta.com/horizon/downloads/package/oculus-developer-hub-win/), [SideQuest](https://sidequestvr.com/), or adb:
   ```
   adb install -r LostWorldVR-quest.apk
   ```
4. **Start the app once** (find it under *Unknown Sources* in your library). It will tell you it found no ROM: that creates its folder.
5. **Copy your ROM** to the headset, into `Android/data/com.papas.lostworldstandalone/files/ROMs/`:
   ```
   adb push lostwsga.zip /sdcard/Android/data/com.papas.lostworldstandalone/files/ROMs/
   ```
   (or use the file manager in Meta Quest Developer Hub).
6. **Start the app again** and put the headset on. The game waits until you do.

Updating: install the new APK over the old one (`adb install -r`); your settings, saves and ROM stay. If you used an earlier build that was installed as `com.headsplosion.lostworldvr`, this is a **new app**: copy your ROM (and `Saves`/`NVRAM`) from the old folder, and uninstall the old app when you like.

## Controls

| Controller | Action |
|---|---|
| Trigger (gun hand) | Fire. The gun is in the hand chosen in the options: right or left. |
| Grip (gun hand) | Reload: refills all five shells. |
| A or Y | Start |
| B or X | Coin |
| Left menu button | Open / close the options menu (the game pauses) |
| Grip on the menu | Hold to pick the menu up and move it; let go to drop it |
| Either stick click | Re-centre the view |
| Left grip + left stick click | Operator (test) menu |

In the options menu, point at an option and pull the trigger. It has the tabs **COMFORT** (vignette, cinema mode), **GUN** (hand, gun model, recoil, aim fine-tune), **SCREEN** (text placement, 2D scaling, resolution), **CHEATS** and **2 PLAYER**.

## Playing with a friend

Both players need **this same version** of the app and the ROM. Open the left menu, go to the **2 PLAYER** tab:

- **Same Wi-Fi:** one player presses **HOST A GAME**, the other presses **FIND A GAME**.
- **Over the internet:** one player presses **HOST ONLINE** (you can choose your own room code and whether to list the game publicly) and gives the room code to a friend, who presses **JOIN ONLINE** and types it. Or use **BROWSE PUBLIC GAMES** to join a listed game without a code.
- Set your **CHEATS** *before* you host: only the host's choices are used.
- Allow the **microphone** when asked, for voice chat.

If a game over the internet cannot connect (a router without UPnP, or a mobile connection), use a relay: see [`Server/README.md`](Server/README.md) and set `LockstepRelay` in `Config/Supermodel.ini`. The room code and public list use a small free directory service that is already built in.

## Good to know

- This is **experimental** software: emulating a Sega Model 3 at 60 fps on a headset is demanding. A few places in the game (for example parts of stage 3) can slow down. If it does, lower the render resolution in the menu's SCREEN tab.
- Settings, saves and NVRAM live in the app's folder next to the ROM (`.../files/Config`, `Saves`, `NVRAM`). Logs go to `.../files/Log`; please attach `Supermodel.log` when you report a problem.
- More about the Quest build: [`Docs/QUEST.md`](Docs/QUEST.md). How the VR code works: [`Docs/PCVR-README.md`](Docs/PCVR-README.md).

## Credits

- **[headsplosion/lost-world-supermodel-pcvr](https://github.com/headsplosion/lost-world-supermodel-pcvr)** - the original PC VR project this is forked from. All credit for it, and my thanks, go to its creator.
- **[Supermodel](https://github.com/trzy/Supermodel)** by Bart Trzynadlowski and the Supermodel Team - the Sega Model 3 emulator.
- **[TheTomBritton/lostworld](https://github.com/TheTomBritton/lostworld)** (MIT) - the memory addresses used by the cheats.
- **OpenXR** headers and loader by The Khronos Group; **SDL2**; **Dear ImGui**; menu typeface Russo One by Jovanny Lemonad (SIL OFL).

Licensed under the **GNU General Public License v3.0**, like Supermodel (see [`LICENSE`](LICENSE)). *The Lost World: Jurassic Park*, Model 3 and SEGA are trademarks of their respective owners; this project is not affiliated with or endorsed by SEGA, Universal Pictures or Amblin Entertainment.
