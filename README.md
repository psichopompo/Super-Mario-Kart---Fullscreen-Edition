<img width="1280" height="400" alt="Super-Mario-Kart-Logo" src="https://github.com/user-attachments/assets/838b9ed3-0d4c-4db8-a1d1-c81326d3d1ab" />

# Super Mario Kart – Fullscreen Edition (USA)

**A true fullscreen view for Super Mario Kart's 1-player mode, featuring a wide-horizon camera, adapted scenery across all 20 tracks, and a complete reworking of the game's logic around the expanded view.**

By **Psicopompo** · USA ROM · IPS and BPS · Current version: **v2.0**

[![Super Mario Kart in Fullscreen!](https://img.youtube.com/vi/2ajlZI5xrAw/hqdefault.jpg)](https://youtu.be/2ajlZI5xrAw)

---

## Why it exists

Super Mario Kart is a beautiful game whose 1-player mode has always played with one hand tied behind its back. The race is drawn in a cropped portion of the screen, while the lower area is reserved for a map or rear-view mirror inherited from the 2-player split-screen design.

The obvious first step is to remove the split-screen crop so Mode 7's ground plane can use the full 256×224 pixels.

But that's only the beginning.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-031613" src="https://github.com/user-attachments/assets/29a52de2-30c4-401c-be1a-4015c5d3c60a" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-030909" src="https://github.com/user-attachments/assets/2534d407-c5a0-4448-8118-df31ec4ef981" />

The camera still points at the old position, the kart is still drawn for the old layout, and the shadow, opponents, collisions, objects, HUD, and screen effects all still assume that the bottom part of the image is something else.

**This isn't just a matter of “removing the map.”** The camera reference itself changes, and everything that depends on it has to follow.

## The idea that moved the project forward

At first, the project tried to address the consequences one by one: move the kart, fix the shadow, fix the effects, fix the collisions, fix the opponents, fix the objects…

Each fix seemed to uncover another part of the game that was still using the old coordinates.

Then came the idea that changed the project's direction: **Player 2 already had much of the screen-space logic needed to place a kart around the position we wanted for the new 1-player view. Why not reuse that logic for Player 1?**

That didn't solve everything on its own, but it provided a much better foundation than fighting each side effect separately. It saved a great deal of time and made it possible to focus on the deeper camera and projection problems.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-040214" src="https://github.com/user-attachments/assets/fb3a2e64-65fb-4b7d-831a-8ecceedea7ad" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-041627" src="https://github.com/user-attachments/assets/1b3b37c2-3698-4f0c-b0d7-8d9ef875a610" />

## The camera

The SNES DSP-1 projects the Mode 7 ground plane from a focus point associated with the kart.

Simply drawing Mario lower on the screen doesn't work. The sprite moves, but the road, shadow, opponents, and collision calculations still belong to the old projection. The result is a kart that appears to float above the ground.

The solution was to change the camera reference itself. **The kart stays in its new screen position while the projected scenery moves closer to it**, in a way similar to the visual effect seen when accelerating in the original game.

This proved especially important on the starting grid. After expanding the Mode 7 area to fill all 224 lines, the grid ended up too far ahead of Mario: the kart was in the desired position, but the opponents and the painted grid marker had been left behind in the old projection. Moving the kart again wasn't the answer. The scenery itself had to be brought back into the correct relationship with the kart.

That's why the DSP-1's effective focus point is shifted forward along the viewing direction, and why the camera gradually transitions to its new position as the race begins instead of switching abruptly.

**The kart stays where it belongs; the world moves closer to it.**

Version 1.2 refined this relationship. The track point the game treated as the kart's position was still about 37 screen rows above the kart's feet (in the original game, it is about 6 rows above them), so collisions with walls, track edges, and pits triggered too early. The ground projection is now realigned with the kart's screen position, so the point beneath the kart is drawn where the kart actually touches the ground.

Version 2.0 introduces a second camera option: the **wide-horizon camera**, enabled by default on all 20 tracks. It provides a more open, higher view with its own horizon, and is also used during the intro, starting zoom, and finish-line turn. Press **SELECT during a race** to switch on the fly between the wide-horizon camera and the classic fullscreen camera. SELECT has no effect in menus.

Both camera options retain fullscreen projection and the fixes developed in earlier versions. The new camera is not a separate game mode: it is an alternative view built on the same fullscreen foundation.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-032540" src="https://github.com/user-attachments/assets/70bff508-ffa6-4a1e-886f-15d4369451b0" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-032728" src="https://github.com/user-attachments/assets/cd414d84-033b-4867-8f5c-935351be6fb6" />

## What's changed

* **True fullscreen in 1P.** The race view uses the full 256×224 pixels.
* **Two camera views.** The new wide-horizon camera is enabled by default on all 20 tracks. Press SELECT during a race to switch between it and the classic fullscreen camera. The new view is also used for the intro, starting zoom, and finish-line turn.
* **Adapted scenery across all 20 tracks.** Skies are extended to prevent black bands and color jumps. Newly visible areas are filled using the tone of the adjacent gradient band. Koopa Beach clouds appear at all three heights from the starting grid, and Ghost Valley pillars are clipped correctly.
* **New camera reference.** The kart, road, opponents, objects, shadows, and collision logic remain consistent with the new projection.
* **Kart-aligned collisions.** Collisions with walls, track edges, and pits occur where the kart actually touches them, rather than too early.
* **HUD repositioning.** The extra space makes it possible to rearrange the position digits, car counter, and coin counter without the original layout's constraints. The small position digit moves about 8 pixels to the left, and the large finishing-position digit moves into the newly available space.
* **Centered tables and banners.** The LAP TIME table and ranking faces are moved down by 25 pixels. Game Over, ROUND 1, Ranked Out, and the RETRY / END menus are also repositioned. The ROUND banner is fixed in v2.0.
* **Position-dependent effects fixed.** Bananas, squash smoke, Monty Moles, dropped coins, and other effects tied to the kart's old position are moved to fit the new camera layout.
* **Lakitu's rescue works in fullscreen.** After falling off the track, Lakitu enters the scene, picks up the kart with his fishing line and coin, and returns it to the track, as in the original game. His head, cloud, and leftover “three hairs” are prevented from appearing along the bottom edge of the screen during his entrance, rescue, and departure.
* **Refined opponent scaling.** The original eleven opponent drawings are retained, but their sizes are selected using a new geometric distribution chosen after comparing the alternatives in motion. The player's normal size is unchanged.
* **Refined starting-grid alignment.** The grid's lateral correction is applied from the beginning of the camera's approach. The full intro zoom and orbit are preserved.
* **Lakitu shadows fixed.** His shadow is corrected in fullscreen and in both split-screen views, while retaining the earlier fix for his body appearing at the bottom edge.
* **Performance tuned.** The check that determines whether fullscreen logic should be applied is calculated once per frame instead of dozens of times. In the heaviest measured scene (Lakitu's rescue), delayed frames dropped from 18% to virtually zero compared with the build before that optimization. v1.3 reduced the load further: in the heaviest measured race start, peak CPU load fell from 95.7% to 90.5% (original: 89%), and no delayed frames were measured during the first 1,061 frames of the 50cc Mushroom, Flower, and Star Cup starts. v2.0 reduces CPU cycles further without changing the rendered result.
* **2P preserved.** Fullscreen logic is restricted to 1P. The 2-player branch retains the game's original logic through dedicated gates, and side effects that leaked into 2P were fixed one by one. In 2P, Lakitu's coin and dropped coins are drawn at the correct height instead of 88 pixels too low after a 1P race has been played in the same session.
* **Other graphical issues fixed.** Credit-screen flicker, 2P retry text, Time Trial artifacts, a stray ball behind Mario at the start of Time Trial, Lakitu's shadow during the rescue sequence, sprites at the bottom edge, coin and life counter flicker, and several other issues were tracked down and fixed. v2.0 also fixes the duplicated player face after winning, mountain flicker during loading, intermittent black and blue lines in Ghost Valley, and the oil slick's collision threshold.
* **Attract mode fixed.** In v2.0, attract mode is resynchronized, preserving the original rendering apart from the hack signature.
* **Title screen.** A subtle white line, `Fullscreen Edition · Psicopompo`, was added below Nintendo's copyright notice. The original copyright line was also shifted 2 pixels to the right to center it.

<p align="center">
  <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo)-261012-030213" src="https://github.com/user-attachments/assets/ed38c50b-da13-445b-9caf-d51ff9f34569" />
  <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo)-261012-030211" src="https://github.com/user-attachments/assets/ce5ef69c-f19b-4fdf-bc26-9e0ffd75e452" />
</p>
<p align="center"><sub><span style="color: white;">Both selectable camera views.</span></sub></p>

## Map and rear-view mirror: deliberately removed

The original idea was to keep both as small overlays on top of the full race view.

However, both are secondary Mode 7 renders, and keeping them would have meant splitting the frame again halfway down the screen. That went directly against the goal of a clean fullscreen race view and introduced a new set of timing, HDMA, and rendering problems.

So the map and rear-view mirror were left out of fullscreen races. **The Time Trial results map remains visible**, including the BEST 5 / BEST LAP information.

**A clean fullscreen race view won out over a cluttered compromise.**

The 2-player mode retains its original split-screen presentation.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003628" src="https://github.com/user-attachments/assets/3c5f4f1a-1f72-4f38-85d1-d4f236b2507d" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-013030" src="https://github.com/user-attachments/assets/513fa905-178b-40e1-984c-91c2062df0cf" />

## How it was built: fixes that broke other things

This turned out to be much deeper than moving a sprite and changing a few coordinates.

The game combines the DSP-1, Mode 7, HDMA, OAM, sprite depth sorting, collision routines, screen-space limits, color windows, and several other systems that assumed the original 1-player layout.

Almost every major fix opened up another problem.

Opponents could pass through Mario because the collision code still used the old depth range. Pipes could become almost invisible to collision detection. Objects could disappear too early because the new camera pushed them beyond the original visibility limits. Sprites could jump from the bottom edge of the screen to the top because the SNES stores their Y coordinate in 8 bits. Lakitu, shadows, smoke, coins, bananas, and other effects could all remain tied to the player's old position.

Lakitu's rescue is a good example. Its script waits for its Y coordinate to reach certain values chosen for the original screen range. With the wider view, its path crosses negative values, so those waits—and the coin it carries—would never complete. The checks had to be adapted without changing its speed or sequence.

Even after the rescue worked, Lakitu still left traces at the bottom of the screen. The rescue begins with a negative Y coordinate, so his head and cloud appeared in the extra bottom lines as he descended from above, and again as he departed upward. Those elements are now hidden at those moments. Fixing that revealed another problem: his three leftover hair pieces remained drawn at the bottom edge for the rest of the race because the game does not rewrite those sprite slots when Lakitu finishes. They are now parked off-screen, which also cleans up save states created with earlier versions.

The karts' OAM order also had to be investigated to understand why some opponents overlapped incorrectly. Some experimental fixes worked visually but cost too many CPU cycles and caused slowdown in the NTSC version. Those approaches had to be discarded and replaced with much cheaper hooks.

Profiling the slowdowns revealed that one of those hooks was the culprit: the check that determines whether fullscreen logic should be applied was being run by sprite-drawing routines 40 to 55 times per frame. In the heaviest measured scene (Lakitu's rescue), the game's logic took almost as long as the frame itself. Now the result of that check is calculated once per frame and read directly by the most frequently called routines. v1.3 goes a step further: the projection and object-culling code also reads the cached result, and the three chained wrappers that determine whether an object is on-screen were merged into a single routine. Normal driving, race starts with all eight karts, and full races at Donut Plains showed no slowdown.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-040354" src="https://github.com/user-attachments/assets/c0163555-2ec3-4b5d-88d6-7f344ac86a8d" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-041922" src="https://github.com/user-attachments/assets/653d7a3b-8982-4892-b8ef-f2c47345538c" />

The work therefore became heavily regression-driven. **Dozens of reproducible save states** covering race starts, cups, collisions, effects, Time Trial, Ranked Out, Game Over, retry screens, credits, 2P, and other situations were replayed and compared frame by frame after every change.

For v1.4, the new opponent-size distribution was checked across **3,360 compared frames**. The camera, timer, position and speed fields, and player sprites matched the previous reference, and a separate 360-frame split-screen test also matched in its complete images. This is not a claim of exhaustive coverage of every mode.

Version 2.0 added dedicated regression checks for the new camera and adapted scenery. In bsnes, the cold-start attract mode was compared with the original ROM over **2,950 frames**, with identical output apart from the hack signature. **Twenty-seven real race states**, each compared for 120 frames, showed no rendering differences. The finish-camera OAM also matched the approved build, and regression tests spanning several thousand frames were run on tracks with special scenery treatment.

Performance was tested separately. In a cold-start Bowser Castle 1 Time Trial, with scripted hard turns at high speed, the original USA ROM, v1.5, and v2.0 produced identical clock ticks (11,640 out of 12,000) and the same times along the same trajectory. In a Bowser Castle 3 race state, v1.5 and v2.0 also matched (2,993 out of 3,000 ticks) and produced the same final time.

The stutter during hard turns seen in these tests is native game behavior, identical with and without the patch. For that reason, v2.0 does not modify AI scheduling or physics.

A fix wasn't considered finished just because it worked in a screenshot. It had to survive the rest of the test suite.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223050" src="https://github.com/user-attachments/assets/0e15be06-1bbe-4cb1-9b44-5df626976089" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223113" src="https://github.com/user-attachments/assets/990be6ee-a48a-4e8c-a422-15ec17976c61" />

## Development

This project was developed through an iterative collaboration between human and AI, built on continuous interaction, shared exploration, and mutual feedback.

The development process involved investigating possibilities, exploring approaches, evaluating results, solving problems, and refining solutions through repeated cycles of experimentation and testing. Ideas evolved, approaches were adjusted, and solutions improved throughout this process.

The final result reflects this ongoing collaboration, where the value lies not in any single contribution, but in how the interaction between human and AI shaped the development as a whole.

## Applying the patch

Input: a clean, headerless **Super Mario Kart (USA)** ROM.

| ROM | Size | CRC32 | MD5 | SHA-1 | SHA-256 |
| --- | ---: | --- | --- | --- | --- |
| Original (USA, clean and headerless) | 524,288 bytes | `CD80DB86` | `7f25ce5a283d902694c52fb1152fa61a` | `47E103D8398CF5B7CBB42B95DF3A3C270691163B` | Not provided |
| Patched (v2.0) | 1,048,576 bytes | `E9B8C210` | `0f4d2c70b6057c8af55f584244d78911` | `3C0A0D7B4E87CD6A54151F0B953A003E9353E65B` | `008a5cedb569d07487b93dbfdb0c09c98f2b30cfecfe41916fee663c5fc9992b` |

Download **`Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).zip`** from the releases. The archive contains the IPS and BPS patches, `LÉEME.md`, `README.md`, and the release notes in English and Spanish. No game ROM is included.

* `Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).bps` — **recommended**; verifies the input ROM. Use Flips, beat, MultiPatch, or RomPatcher.js.
* `Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).ips` — use any IPS-compatible patcher.

The output expands to 1 MB. New code and data are stored in the added space, and the ROM size byte is updated. The internal checksum is corrected, so compatible flash carts and patching tools should not report a checksum warning.

Apply **only one patch** to a copy of your clean ROM. The patch is cumulative from the original ROM: **do not apply v2.0 on top of v1.4 or v1.5**.

The PAL version is not supported.

## Version history

* **v2.0** – Introduces the wide-horizon camera, enabled by default on all 20 tracks, with switching via SELECT during a race between the new and classic cameras. The new view is also used for the intro, starting zoom, and finish-line turn. Scenery is adapted across all 20 tracks, including extended skies, seamless gradient fills, Koopa Beach clouds at all three heights from the starting grid, and clipped Ghost Valley pillars. Fixes the duplicated player face after winning, mountain flicker during loading, intermittent black and blue lines in Ghost Valley, the oil slick's native collision threshold, and the ROUND banner alignment. Resynchronizes attract mode and reduces CPU cycles without changing the rendered result. Includes all v1.5 improvements. Validated in bsnes and RetroArch through attract-mode comparison, 27 real race states, finish-camera OAM comparison, and extended regression testing. No claim is made that it has been tested on real hardware.

* **v1.5** – Fixes the Time Trial results screen. Results now correctly display all laps, highlighted times, TOTAL, and the map with BEST 5 / BEST LAP, while the race remains fullscreen and the Grand Prix results layout is preserved. Tested with Time Trial and a normal race. Includes all v1.4 improvements.

* **v1.4** – Introduces a new geometric distribution for the original eleven opponent sizes, selected after comparing the alternatives in motion. The player's normal size is unchanged. The starting-grid lateral correction is now applied from the beginning of the camera's approach while preserving the full zoom and orbit. Fixes Lakitu's shadow in fullscreen and both split-screen views, retaining the earlier fix for his body appearing at the bottom edge. Changes were checked across 3,360 compared frames, with a separate 360-frame split-screen comparison. Tested in bsnes and RetroArch and approved through visual testing.

* **v1.3** – Lakitu no longer appears at the bottom of the screen: his head and cloud are hidden while he descends from above or leaves upward (Ghost Valley, waterfalls), and the leftover pieces (“three hairs”) that remained at the start and after a rescue are cleared. In 2P, Lakitu's coin and dropped coins are drawn at the correct height instead of 88 pixels too low. Lower CPU load in 1P (peak load at the heaviest measured start: 95.7% → 90.5%). Includes all v1.2 fixes.

* **v1.2** – The ground projection is realigned with the kart's screen position, so the track beneath the kart lines up with where the kart is drawn: collisions with walls, track edges, and pits now occur in the right place (previously they triggered too early). Fixes Lakitu's rescue after falling off the track. Reduces slowdown by calculating the fullscreen check once per frame. Includes all v1.1 fixes.

* **v1.1** – Fixes stray white pixels in the image's transition band. The LAP TIME table and ranking faces were moved down another 5 pixels.

* **v1.0** – Initial release.

## Status and limitations

* **USA only.** The PAL version is not supported.
* **224 lines / 60 Hz NTSC.**
* Tested in **bsnes** and **RetroArch**. The SNES9x core has not been tested.
* **Real hardware and flash carts:** v2.0 has not been tested on real hardware or flash carts. Earlier versions may have been tested on hardware, but that does not establish v2.0 compatibility.
* v2.0 validation includes a 2,950-frame attract-mode comparison against the original ROM, 27 real race states compared for 120 frames each, verification of the finish-camera OAM, and regression tests spanning several thousand frames on tracks with special scenery treatment.
* The 50cc and 100cc cups were completed with v1.1. Later versions have received additional state-by-state regression tests, frame-by-frame comparisons, performance measurements, and play sessions, but this does not guarantee that every mode is bug-free. Some modes have received less testing than others.
* Track objects such as pipes still follow the game's original section-based loading rules. With the new camera reference, some appearance and disappearance boundaries are more noticeable.
* 2-player mode retains its original split-screen behavior and does not use the 1-player fullscreen camera.
* The map and rear-view mirror are hidden during fullscreen races. The Time Trial results map remains visible.
* Bug reports are welcome. Please include the emulator and core, game mode, and a save state that reproduces the issue.

## Credits and disclaimer

* **Psicopompo** — project direction, research, analysis, solution design, testing, and validation.
* **AI assistant** — code analysis, reverse-engineering tools, patch implementation, and test automation, under Psicopompo's direction.

Super Mario Kart © Nintendo.

This is an unofficial fan project and is not affiliated with or endorsed by Nintendo.

No game data is distributed. You must provide your own legally obtained ROM.
