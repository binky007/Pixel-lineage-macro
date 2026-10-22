# Pixel Lineage — Starfall Macro

A Windows macro for Pixel Lineage, with per-class skill profiles, opening combos, repeated mouse-wheel scrolling, adventure setup and HP-triggered character recovery.

**Built on the work of [1vtt](https://www.youtube.com/@1-vtt), the original macro creator, and [remainversatile](https://github.com/remainversatile), whose [Starfall fork](https://github.com/remainversatile/roblox_shit) provides the foundation for this edition.**

## New additions in this fork

These features are added or restored compared with the linked Starfall base:

| Addition | What it does |
| --- | --- |
| **Per-class skill profiles** | Saves separate skill settings for Warrior, Mage, Thief, Bard, Fist and Archer. Switching class loads its saved panel. |
| **Automatic SCROLL for low EN** | Uses an available SCROLL when EN is below the skill requirement, then reads EN again. Greyed-out SCROLL text is skipped. (original macro only scrolled once and used scroll lines via windows but roblox has a set line scroll amount so it scrolls x amount of times instead of x amount of lines)|
| **Repeated mouse-wheel scrolling** | Searches the skill list with separate downward wheel actions, checking for the skill after each action. Replaces the fork's S-key scrolling. |
| **Skill-menu recovery** | Distinguishes the skill list from target selection, recovers from premature basic-attack selection and checks whether a skill went through. |
| **EnhancedEN-reading retries** | Retries failed readings and checks expanded or default capture areas before giving up. |
| **Archer Power Shot correction** | Recognizes the green Power Shot panel and meter fill instead of treating it as the Thief minigame. |
| **BACK detection correction for co-op play** | Filters out the gold dungeon divider, including the section interrupted by the co-op turn timer. |
| **Boss-path detection correction** | Excludes landscape strips that could be mistaken for selectable path cards when a boss path pops up. |
| **Next-map toggle** | Chooses an available NEXT button after a clear, with PLAY AGAIN as the fallback. |
| **HP protection and character recovery** | Opens PARTY, monitors your HP, leaves and rejoins when the threshold is crossed, selects your character and fully stops the macro at UNFINISHED BATTLE to HELP preserve lives. |

### HP protection: what happens

HP protection is enabled by default with a **50%** threshold. It requires **two valid readings below the threshold**; exactly 50% does not trigger the default setting so adjust accordingly.

1. Clicks **PARTY** at the start of each battle so the player HP panel is visible.
2. Reads your own current/max HP from the selected capture area (when playing in co-op ensure that the capture area is ON YOU and not another party member).
3. On confirmed low HP, opens Roblox's menu and confirms **Leave**.
4. Reopens Pixel Lineage through the existing Roblox launch link.
5. Clicks **Character Select**, retrying at 0.5-second intervals for up to 10 seconds.
6. Clicks **Enter** for the character slot selected in the Adventure tab.
7. **Stops the macro completely at UNFINISHED BATTLE.**

**The pending battle is left for you to handle manually.** The macro does not click Resume Battle, Abandon or Set Out on that screen. Rejoining can retain your previous HP; this feature does not heal your character or guarantee that lives will be preserved.

** There is a bug to abuse to save your lives when you rejoin, if you attack then quit before the mob attacks back you can go back to the battle with the new mob health and it'll be your turn again abuse at your own discretion as it might be patched in a later update**

Locked or empty character slots are left untouched. If Character Select remains unresponsive after the retry window, the macro stops with a status message.

After manually resolving the unfinished battle, press **F1** to start automation again. Starting while that dialog is still visible stops the macro again.

## Credits

| Creator | Contribution |
| --- | --- |
| **[1vtt](https://www.youtube.com/@1-vtt)** | Original Pixel Lineage Macro, including the core combat/minigame engine and original Discord webhook implementation. |
| **[remainversatile](https://github.com/remainversatile/roblox_shit)** | Starfall base: adventure/lobby workflow, world selection, animated interface, popup scanning and the existing rejoin foundation. |

This edition builds on both projects. This is a community modification and does not imply endorsement by either creator, Roblox or Pixel Lineage.

## Requirements

- Windows with Windows OCR available; use an English game interface and an OCR language that can read it.
- 64-bit [Python 3.10–3.13](https://www.python.org/downloads/windows/), including Tkinter.
- Roblox installed and signed in, with Pixel Lineage accessible.
- Internet access for dependency installation, Roblox and any enabled Discord notifications.

## Installation

1. Download this repository using **Code → Download ZIP**, or clone it.
2. Extract it fully to a writable folder. The macro folder must contain `Setup.bat`, `Launch.bat` and `src/`.
3. Run **Setup.bat** once to create the local Python environment and install dependencies.
4. Run **Launch.bat** to open the macro.

If setup fails, check the messages in the setup window and `setup-log.txt`.

When updating an existing installation, close the macro before replacing its files, preserve your personal `config.json`, and reopen **Launch.bat** afterward.

## First-time setup

1. Open Pixel Lineage and enter your character.
2. On **Main**, choose your class and configure its skill panel.
3. Use the **Read areas** Select/Test controls to verify EN, skill-list and HP recognition.
4. On **Adventure**, choose the correct character slot, world, difficulty and modifier.
5. Check the HP threshold and PARTY click position before relying on HP protection.
6. Press **F3** to check what the macro sees, then **F1** to start.

Keep the game controls visible to the capture system. Move the macro away from capture areas or enable **Auto minimize**. Stop the macro before changing worlds or recalibrating.

### Skill settings

- **Use a skill:** enter its name as it appears in game and set the required EN threshold.
- **Turn 1 and 2 skills:** enable the checkbox and enter the two opening skill names. An empty opener falls back to the normal skill setup. Unavailable skills are skipped.
- **Auto SCROLL below required EN:** uses SCROLL only when EN is insufficient and the SCROLL row is enabled. A recognized opener cost can also request SCROLL when it exceeds the normal threshold.
- **Scrolling, up to … wheel actions:** sets the maximum number of separate downward scroll actions per search. For example, 6 permits up to six wheel actions, with a fresh skill-list check between them. It stops early when the skill appears.

Skill settings save separately for each class. An existing flat skill configuration becomes the selected class's first profile. Capture areas and click calibration remain shared.

### HP calibration

On **Main → Read areas → Your HP numbers**, press **Test** while PARTY is visible. The reported percentage should match your own character.

If needed, use **Select** around only your own current/max HP numbers. Avoid including another party member's HP. The reader ignores EN-labelled lines and rejects ambiguous readings. It supports values such as `850/2000` and `14.7K/18.4K`.

The PARTY tab click can be adjusted on **Adventure**. HP status is shown there while the macro runs. HP OCR waits during minigame play so it does not delay minigame inputs.

### Next map or repeat

Enable **Main → Go to next map after a clear** to select an active NEXT button. If NEXT is unavailable, PLAY AGAIN is the fallback.

The existing **Repeat selected adventure act** workflow returns to the castle and sets up the selected act again. With next-map progression enabled, the Adventure controller allows that progression instead of immediately returning home because the act changed.

## Default hotkeys

| Key | Action |
| --- | --- |
| **F1** | Start or stop the macro |
| **F2** | Select the minigame capture area |
| **F3** | Check the current screen recognition |
| **F4** | Exit the macro |

Hotkeys can be changed in the interface. F1 cancels pending retries and recovery actions.

## Inherited Starfall features

The base fork's animated interface, adventure/lobby setup, world cards, difficulty/modifier controls, path preferences, reward-popup scanning, disconnect recovery and optional Discord controls are retained.

| Adventure setting | Options |
| --- | --- |
| Difficulty | Normal, Hard, Nightmare, Torment |
| Modifier | No Modifier, Elite Patrols, Volatile Enemies, Exhausting Battles, Boss Rush |
| Character slot | 1–6; the selected slot must have a visible Enter button |

World cards cover Sunmeadow, Dungeon, Cursed Forest, Moonstone Rise, Underworld, Withered Meadow, Drowned Cathedral, Glass Wastes, Hollow Sky and Heart of Blight. Display names can be edited in Adventure; the corresponding worlds must be unlocked in game.

**Disconnect recovery and HP recovery finish differently:** ordinary disconnect recovery can return to adventure setup after loading the castle. HP recovery waits for UNFINISHED BATTLE and stops the macro there. The low-HP rejoin path works independently of the crash/disconnect auto-rejoin checkbox.

## Discord and saved settings

Screen recognition runs locally through Windows OCR. Optional Discord run logs and stuck alerts are configured on the **Discord** tab. Test messages and stuck alerts include a Roblox screenshot.

Settings are saved in `config.json`, which can contain a private webhook URL. Keep personal configuration, `.venv/`, backups, logs and temporary files out of public uploads and release archives. Retain the supplied `.gitignore` when publishing the source.

## Validation and current limits

The current build has been checked with **40 automated control-flow tests**, eight combat regression scripts and Windows OCR against supplied gameplay screenshots.

These checks cover profiles, scrolling, EN/SCROLL decisions, skill selection, path detection, HP thresholds, character-slot selection, retry limits and the macro-stop event. They do not establish that every live gameplay sequence works end to end.

Different resolutions, UI scales or game updates may require recalibration. A frozen client without a recognized disconnect dialog is not detected by the existing reconnect workflow. Unfamiliar Leave or Return Home dialogs can require manual intervention. The act-10 ending and full HP leave/rejoin flow have not been verified end to end in live play.
