<img width="1280" height="400" alt="Super-Mario-Kart-Logo" src="https://github.com/user-attachments/assets/838b9ed3-0d4c-4db8-a1d1-c81326d3d1ab" />

# Super Mario Kart – Fullscreen Edition (USA)

**A true fullscreen version of Super Mario Kart's 1-player mode, featuring a wide-horizon camera, a floating minimap, adapted scenery across all 20 tracks, and a complete reworking of the game's logic around the expanded view.**

[![Super Mario Kart – Fullscreen Edition v3.0](https://img.youtube.com/vi/BO4YEe-mxVU/hqdefault.jpg)](https://youtu.be/BO4YEe-mxVU)

By **Psicopompo** · USA ROM · IPS and BPS · Current version: **v3.0**

---

## Why it exists

Super Mario Kart is a beautiful game whose 1-player mode has always played with one hand tied behind its back. The race is drawn in a cropped portion of the screen, while the lower area is reserved for a map or rear-view mirror inherited from the 2-player split-screen design.

The obvious first step is to remove the split-screen crop so the race can use the full 256×224 pixels.

<img width="256" height="224" alt="Super Mario Kart (USA) (patched)_000" src="https://github.com/user-attachments/assets/720198e8-d8f6-41bf-bf2d-a980b2fca2e2" /> <img width="256" height="224" alt="Super Mario Kart (USA) (patched)_001" src="https://github.com/user-attachments/assets/d136ed1b-e4a8-4a49-a6e6-9b72715bc234" />

But that's only the beginning.

The camera still points at the old position, the kart is still drawn for the old layout, and the shadow, opponents, collisions, objects, HUD, and screen effects all still assume that the bottom part of the image is something else.

**This isn't just a matter of removing the map.** The camera reference itself changes, and everything that depends on it has to follow.

## The idea that moved the project forward

At first, the project tried to address the consequences one by one: move the kart, fix the shadow, fix the effects, fix the collisions, fix the opponents, fix the objects…

Each fix seemed to uncover another part of the game that was still using the old coordinates.

Then came the idea that changed the project's direction: **Player 2 already had much of the screen-space logic needed to place a kart around the position we wanted for the new 1-player view. Why not reuse that logic for Player 1?**

That didn't solve everything on its own, but it provided a much better foundation than fighting each side effect separately. It saved a great deal of time and made it possible to focus on the deeper camera and projection problems.

## The camera

The original camera and projection system was designed around the DSP-1 and the game's original screen layout.

Simply drawing Mario lower on the screen doesn't work. The sprite moves, but the road, shadow, opponents, and collision calculations still belong to the old projection. The result is a kart that appears to float above the ground.

<img width="256" height="224" alt="Super Mario Kart (USA) (patched)_002" src="https://github.com/user-attachments/assets/88b90047-53c8-4df4-9b2a-4bf06d72206f" /> <img width="256" height="224" alt="SMK_prueba_E_reparto_000" src="https://github.com/user-attachments/assets/8207c45b-d0fb-4497-a037-a163d21f01aa" />

The solution was to change the camera reference itself. **The kart stays in its new screen position while the projected scenery moves closer to it**, in a way similar to the visual effect seen when accelerating in the original game.

This proved especially important on the starting grid. After expanding the race view to fill all 224 lines, the grid ended up too far ahead of Mario: the kart was in the desired position, but the opponents and the painted grid marker had been left behind in the old projection. Moving the kart again wasn't the answer. The scenery itself had to be brought back into the correct relationship with the kart.

**The kart stays where it belongs; the world moves closer to it.**

Version 1.2 refined this relationship. The ground projection was realigned with the kart's screen position, so the track point beneath the kart matches where its wheels actually touch the ground. This also corrected collisions with walls, track edges, and pits, which previously triggered too early.

Version 2.0 introduced a second camera option: the **wide-horizon camera**, enabled by default on all 20 tracks. It provides a more open view with its own horizon, and is also used during the intro, starting zoom, and finish-line turn.

Version 3.0 retains both camera options and introduces a new underlying architecture: **the DSP-1 has been replaced by the SA-1 enhancement chip**. The alternative camera can still be selected during a race.

Both camera options retain fullscreen projection and the fixes developed in earlier versions. The second camera is not a separate game mode: it is an alternative view built on the same fullscreen foundation.

## What's changed

* **SA-1 migration.** The hack has been migrated from the original DSP-1 to the SA-1 enhancement chip. This is a major architectural change and the foundation of the new version.
* **True fullscreen in 1P.** The race view uses the full 256×224 pixels.
* **Floating minimap.** A new minimap displays the track layout during races, without giving up the fullscreen race view. It is displayed as an overlay rather than occupying a separate portion of the screen.
* **Two camera views.** The wide-horizon camera and the alternative fullscreen camera can be switched during gameplay.
* **Adapted scenery across all 20 tracks.** Skies are extended to prevent black bands and colour jumps. Newly visible areas are filled using the tone of the adjacent gradient band. Koopa Beach clouds appear at all three heights from the starting grid, and Ghost Valley pillars are clipped correctly.
* **Improved backgrounds.** Sky gradients have been refined, alongside additional graphical corrections.
* **New camera reference.** The kart, road, opponents, objects, shadows, and collision logic remain consistent with the new projection.
* **Kart-aligned collisions.** Collisions with walls, track edges, and pits occur where the kart actually touches them, rather than too early.
* **HUD repositioning.** The extra space makes it possible to rearrange the position digits, car counter, and coin counter without the original layout's constraints.
* **Centered tables and banners.** The LAP TIME table and ranking faces are moved down. Game Over, ROUND 1, Ranked Out, and the RETRY / END menus are also repositioned.
* **Position-dependent effects fixed.** Bananas, squash smoke, Monty Moles, dropped coins, and other effects tied to the kart's old position are adapted to the fullscreen layout.
* **Lakitu's rescue works in fullscreen.** After falling off the track, Lakitu enters the scene, picks up the kart with his fishing line and coin, and returns it to the track, as in the original game.
* **Refined opponent scaling.** The original eleven opponent drawings are retained, with their sizes selected using a new geometric distribution chosen after comparing the alternatives in motion. The player's normal size is unchanged.
* **Performance improvements.** Further optimizations have been introduced, alongside the SA-1 migration.
* **2P preserved.** Fullscreen logic is restricted to 1P. The 2-player mode retains the game's original split-screen layout and behaviour.
* **Other graphical and gameplay fixes.** Various issues have been corrected throughout the game, including visual artifacts, sprite positioning, background rendering, and other inconsistencies.

## Map and rear-view mirror

The original idea was to keep both as small overlays on top of the full race view.

However, the original map and rear-view mirror are secondary Mode 7 renders, and keeping them in their original form would have meant splitting the frame again halfway down the screen.

That went directly against the goal of a clean fullscreen race view.

Version 3.0 introduces a different solution: **a floating minimap displayed during races**, allowing players to see the track layout without sacrificing the expanded race view.

The original rear-view mirror remains removed from fullscreen races.

The Time Trial results map also remains visible, including the BEST 5 / BEST LAP information.

The 2-player mode retains its original split-screen presentation.

## How it was built: fixes that broke other things

This turned out to be much deeper than moving a sprite and changing a few coordinates.

The game combines the DSP-1, Mode 7, HDMA, OAM, sprite depth sorting, collision routines, screen-space limits, colour windows, and several other systems that assumed the original 1-player layout.

Almost every major fix opened up another problem.

Opponents could pass through Mario because the collision code still used the old depth range. Pipes could become almost invisible to collision detection. Objects could disappear too early because the new camera pushed them beyond the original visibility limits. Sprites could jump from the bottom edge of the screen to the top because the SNES stores their Y coordinate in 8 bits. Lakitu, shadows, smoke, coins, bananas, and other effects could all remain tied to the player's old position.

Lakitu's rescue is a good example. Its script waits for its Y coordinate to reach certain values chosen for the original screen range. With the wider view, its path crosses negative values, so those waits—and the coin it carries—would never complete. The checks had to be adapted without changing its speed or sequence.

The karts' OAM order also had to be investigated to understand why some opponents overlapped incorrectly. Some experimental fixes worked visually but cost too many CPU cycles and caused slowdown in the NTSC version. Those approaches had to be discarded and replaced with much cheaper hooks.

The work therefore became heavily regression-driven. **Dozens of reproducible save states** covering race starts, cups, collisions, effects, Time Trial, Ranked Out, Game Over, retry screens, credits, 2P, and other situations were replayed and compared frame by frame after changes.

For v1.4, the new opponent-size distribution was checked across **3,360 compared frames**. The camera, timer, position and speed fields, and player sprites matched the previous reference, and a separate 360-frame split-screen test also matched in its complete images.

Version 2.0 added dedicated regression checks for the new camera and adapted scenery. In bsnes, the cold-start attract mode was compared with the original ROM over **2,950 frames**, with identical output apart from the hack signature. **Twenty-seven real race states**, each compared for 120 frames, showed no rendering differences.

Performance was tested separately. In a cold-start Bowser Castle 1 Time Trial, with scripted hard turns at high speed, the original USA ROM, v1.5, and v2.0 produced identical clock ticks (11,640 out of 12,000) and the same times along the same trajectory.

Version 3.0 takes the project further with the SA-1 migration, a new floating minimap, additional optimizations, and expanded compatibility testing on flashcarts.

A fix wasn't considered finished just because it worked in a screenshot. It had to survive the rest of the test suite.

## Development

This project was developed through an iterative collaboration between human and AI, built on continuous interaction, shared exploration, and mutual feedback.

The development process involved investigating possibilities, exploring approaches, evaluating results, solving problems, and refining solutions through repeated cycles of experimentation and testing. Ideas evolved, approaches were adjusted, and solutions improved throughout this process.

The final result reflects this ongoing collaboration, where the value lies not in any single contribution, but in how the interaction between human and AI shaped the development as a whole.

## Applying the patch

Input: a clean, headerless **Super Mario Kart (USA)** ROM.

| ROM | Size | CRC32 |
| --- | ---: | --- |
| Original (USA, clean and headerless) | 524,288 bytes | `CD80DB86` |
| Patched (v3.0) | 4,194,304 bytes | Not provided |

The resulting ROM is **4 MB (4,194,304 bytes)**.

Its corrected SNES header checksum is:

* Checksum: `AE16`
* Checksum complement: `51E9`

Two patches are included:

* `SMK_Fullscreen_USA.bps` — **recommended**; verifies the input ROM before applying the patch.
* `SMK_Fullscreen_USA.ips` — does not verify the input ROM.

The IPS patch has been verified against the final patched ROM using a custom decoder, but has not been tested with third-party patching tools such as Flips or Lunar IPS.

Apply **only one patch** to a copy of your clean ROM. Do not apply either patch to a previously patched version.

The PAL version is not supported.

No game ROM is included.

## Requirements

The game requires an emulator or flashcart with **SA-1 support**.

Recommended emulators:

* **Mesen**
* **bsnes**

## Flashcart compatibility

Compatibility has been tested by players using:

* **FXPAK Pro**
* **SD2SNES with official firmware**

**Saving on flashcarts:** After saving, return to a menu and wait a moment before switching off the console. This gives the flashcart time to write the save data to the SD card.

The flashcart's red LED may remain on during gameplay. This behaviour has been observed during testing and has not caused any problems.

## Known issues

* **FXPAK Pro:** Two small white pixels may occasionally appear in the dark area on the left side of the screen in Ghost Valley.
* **Background flicker:** Occasional flickering may occur during particularly demanding moments.
* **Unofficial SD2SNES firmware:** One clone running `sd2SNES+` firmware was reported to experience random freezes. This issue has not been reported with official firmware.

These issues are still being investigated. The release improves compatibility and corrects several long-standing graphical problems, but some imperfections remain.

## Version history

* **v3.0** – Major update. Migrates the hack from DSP-1 to SA-1, introduces a floating minimap during races, and adds an alternative camera perspective that can be switched during gameplay. Improves sky gradients and background graphics, introduces further performance optimizations, fixes various graphical and gameplay issues, and adds tested compatibility with FXPAK Pro and SD2SNES using official firmware.

* **v2.0** – Introduces the wide-horizon camera, enabled by default on all 20 tracks, with switching via SELECT during a race between the new and classic cameras. The new view is also used for the intro, starting zoom, and finish-line turn. Scenery is adapted across all 20 tracks, including extended skies, seamless gradient fills, Koopa Beach clouds at all three heights from the starting grid, and clipped Ghost Valley pillars. Fixes the duplicated player face after winning, mountain flicker during loading, intermittent black and blue lines in Ghost Valley, the oil slick's collision threshold, and the ROUND banner alignment. Resynchronizes attract mode and reduces CPU cycles without changing the rendered result. Includes all v1.5 improvements.

* **v1.5** – Fixes the Time Trial results screen. Results now correctly display all laps, highlighted times, TOTAL, and the map with BEST 5 / BEST LAP, while the race remains fullscreen and the Grand Prix results layout is preserved.

* **v1.4** – Introduces a new geometric distribution for the original eleven opponent sizes, selected after comparing the alternatives in motion. The player's normal size is unchanged. The starting-grid lateral correction is now applied from the beginning of the camera's approach while preserving the full zoom and orbit. Fixes Lakitu's shadow in fullscreen and both split-screen views.

* **v1.3** – Lakitu no longer appears at the bottom of the screen: his head and cloud are hidden while he descends from above or leaves upward, and the leftover pieces that remained at the start and after a rescue are cleared. In 2P, Lakitu's coin and dropped coins are drawn at the correct height. Reduces CPU load in 1P.

* **v1.2** – The ground projection is realigned with the kart's screen position, so the track beneath the kart lines up with where the kart is drawn. Fixes Lakitu's rescue after falling off the track and reduces slowdown by calculating the fullscreen check once per frame.

* **v1.1** – Fixes stray white pixels in the image's transition band. The LAP TIME table and ranking faces were moved down another 5 pixels.

* **v1.0** – Initial release.

## Status and limitations

* **USA only.** The PAL version is not supported.
* **224 lines / 60 Hz NTSC.**
* Requires an emulator or flashcart with **SA-1 support**.
* Recommended emulators: **Mesen and bsnes**.
* Flashcart compatibility tested on **FXPAK Pro and SD2SNES with official firmware**.
* The 50cc and 100cc cups were completed with earlier versions. Later versions have received additional state-by-state regression tests, frame-by-frame comparisons, performance measurements, and play sessions, but this does not guarantee that every mode is bug-free.
* Track objects such as pipes still follow the game's original section-based loading rules. With the new camera reference, some appearance and disappearance boundaries are more noticeable.
* 2-player mode retains its original split-screen behaviour and does not use the 1-player fullscreen camera.
* The floating minimap is available during fullscreen races. The original rear-view mirror remains removed.
* Some graphical imperfections remain. See **Known issues** above.
* Bug reports are welcome. Please include the emulator or flashcart model, firmware version, game mode, and a save state that reproduces the issue.

## Credits and disclaimer

* **Psicopompo** — Project author.

Super Mario Kart © Nintendo.

This is an unofficial fan project and is not affiliated with or endorsed by Nintendo.

No game data is distributed. You must provide your own legally obtained ROM.
