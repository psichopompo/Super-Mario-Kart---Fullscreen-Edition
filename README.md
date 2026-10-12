 <img width="1280" height="400" alt="Super-Mario-Kart-Logo" src="https://github.com/user-attachments/assets/838b9ed3-0d4c-4db8-a1d1-c81326d3d1ab" />

# Super Mario Kart – Fullscreen Edition (USA)

**A true full-screen view for single-player Super Mario Kart, with a wide-horizon camera, adapted backgrounds across all 20 tracks, and a complete reworking of the game logic around the expanded view.**

By **Psicopompo** · USA ROM · IPS and BPS · Current version: **v2.0**

[![Super Mario Kart in Fullscreen!](https://img.youtube.com/vi/2ajlZI5xrAw/hqdefault.jpg)](https://youtu.be/2ajlZI5xrAw)

---

<img width="256" height="224" alt="Super Mario Kart (USA) (patched)-261002-222409" src="https://github.com/user-attachments/assets/e7da9dbb-28f2-425a-bfb0-714e8307a836" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-222732" src="https://github.com/user-attachments/assets/f5519df5-4ac0-479e-bf02-50e9db8743f5" />

## Why this exists

Super Mario Kart is a gorgeous game that has always played single-player with one hand tied behind its back. The race is drawn in a cropped part of the screen, while the lower area is reserved for a map or rear-view mirror inherited from the split-screen design of 2-player mode.

The obvious first step is to remove the windowing that splits the picture so the Mode 7 floor can use the full 256×224 display.

But that is only the beginning.

The camera still points at the old position, the kart is still drawn for the old layout, and the shadow, rivals, collisions, objects, HUD and screen effects all continue to assume that the lower part of the picture is something else.

**This is not just "removing the map".** The camera reference itself is changed, and everything that depends on it has to follow.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003333" src="https://github.com/user-attachments/assets/631fc658-0991-45ac-8723-63d9ac101e27" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003554" src="https://github.com/user-attachments/assets/46090e30-12c6-43ff-b6fa-80ef56e649be" />

## The breakthrough

At first, the project tried to solve the consequences one by one: move the kart, fix the shadow, fix the effects, fix the collisions, fix the rivals, fix the objects...

Every fix seemed to uncover another part of the game that was still using the old coordinates.

Then came the idea that changed the direction of the project: **Player 2 already had much of the screen-space logic needed to place a kart around the position wanted for the new 1-player view. Why not reuse that logic for Player 1?**

It did not solve everything by itself, but it provided a much better foundation than fighting every side effect independently. That saved a huge amount of time and made it possible to concentrate on the deeper camera and projection problems.

## The camera

The Mode 7 floor is projected by the SNES's DSP-1 from a focus point associated with the kart.

Simply drawing Mario lower on the screen does not work. The sprite may move, but the road, shadow, rivals and collision calculations still belong to the old projection. The result is a kart that appears to float away from the ground.

The solution was to change the camera reference itself. **The kart stays in its new screen position while the projected scenery is brought closer to it**, similar to the visual effect produced when accelerating in the original game.

This became especially important at the starting grid. After expanding the Mode 7 area to fill all 224 lines, the grid ended up too far ahead of Mario: the kart was in the desired position, but the rivals and the painted grid mark were left behind in the old projection. Moving the kart again was not the answer. The scenery itself had to be brought back into the correct relationship with the kart.

The DSP-1's effective focus point is therefore moved forward along the direction of the view, and the camera transitions gradually into its new position when the race starts rather than switching instantly.

**The kart stays where it belongs; the world is brought toward it.**

Version 1.2 refined this relationship. The point of the track that the game treats as the kart's position was still sitting about 37 screen rows above the kart's feet (the original game has it about 6 rows above), so collisions with walls, edges and pits triggered too early. The ground projection is now realigned with the kart's on-screen position, so the point under the kart is drawn where the kart actually touches the ground.

Version 2.0 introduces a second camera option: the **wide-horizon camera**, enabled by default on all 20 tracks. It provides a more open, higher view with its own horizon, and is also used during the intro, the starting zoom and the finish turn. Press **SELECT during a race** to switch between the wide-horizon and classic cameras on the fly. SELECT has no effect in menus.

Both camera options retain the fullscreen projection and the corrections developed in earlier versions. The new camera is not a separate mode of the game; it is an alternative view built around the same fullscreen foundation.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-235523" src="https://github.com/user-attachments/assets/bf975651-62c8-4ca9-b89d-275134a13105" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-225311" src="https://github.com/user-attachments/assets/ccef2f32-302b-4048-bc9e-7a9cb7ac8702" />

## What changes

* **True fullscreen in 1P.** The race view uses the complete 256×224 display.
* **Two camera views.** The new wide-horizon camera is enabled by default on all 20 tracks. Press SELECT during a race to switch between it and the classic fullscreen camera. The new view also covers the intro, starting zoom and finish turn.
* **Backgrounds adapted across all 20 tracks.** Skies are extended to avoid black bands and colour jumps. Newly exposed areas are filled using the tone of the adjacent gradient band. Koopa Beach clouds appear at all three heights from the starting grid, and Ghost Valley pillars are properly clipped.
* **New camera reference.** The kart, road, rivals, objects, shadows and collision logic remain consistent with the new projection.
* **Collisions aligned with the kart.** Collisions with walls, track edges and pits happen where the kart actually touches them, not before.
* **HUD relocation.** The extra space allows the position digits, car counter and coin counter to be rearranged without the original layout constraints. The small position digit is moved about 8 pixels left, while the large finishing-position digit is moved into the new space.
* **Centered tables and banners.** The LAP TIME table and standings faces are moved 25 pixels down. Game Over, ROUND 1, Ranked Out and the RETRY / END menus are also repositioned. The ROUND banner is corrected in v2.0.
* **Position-dependent effects fixed.** Bananas, crush smoke, Monty Moles, lost coins and other effects that were tied to the old kart position are moved to match the new camera layout.
* **Lakitu's rescue works in fullscreen.** After falling off the track, Lakitu comes into view, picks up the kart with the coin and lifts it back onto the track, as in the original game. His head, cloud and the leftover "three hairs" are kept from appearing at the bottom edge of the screen during his entrance, rescue and departure.
* **Rival scaling refined.** The eleven original rival drawings are preserved, but their sizes are selected according to a new geometric distribution chosen after comparing the alternatives in motion. The normal player size is unchanged.
* **Starting-grid alignment refined.** The lateral correction to the starting grid is applied from the beginning of the camera approach. The full zoom and orbit of the introduction remain intact.
* **Lakitu shadows corrected.** His shadow is corrected in fullscreen and in both split-screen views, while the previous lower-edge body correction is retained.
* **Performance tuned.** The check that decides whether the fullscreen logic applies is computed once per frame instead of dozens of times. In the heaviest scene tested (Lakitu's rescue), lagged frames dropped from 18% to practically zero compared with the build before this optimization. v1.3 trims the load further: in the heaviest race start tested, the peak CPU load dropped from 95.7% to 90.5% (vanilla: 89%), and no lagged frames were measured in the first 1,061 frames of the Mushroom, Flower and Star Cup starts (50cc). v2.0 further reduces CPU cycles without changing the rendered output.
* **2P preserved.** The fullscreen logic is restricted to 1P. The 2-player branch keeps the original game logic through dedicated gates, while side effects that leaked into 2P were fixed individually. Lakitu's coin and lost coins in 2P are drawn at the correct height instead of 88 pixels too low after playing a 1P race in the same session.
* **Secondary graphical issues fixed.** Credits flicker, retry text in 2P, Time Trial artifacts, a stray ball behind Mario at the start of Time Trial, Lakitu's shadow during the rescue sequence, bottom-edge sprites, coin/life counter flicker, and several other problems were tracked down and corrected. v2.0 also fixes the duplicated player face on winning, mountain flicker during loading, intermittent black and blue lines in Ghost Valley, and the oil slick's collision threshold.
* **Attract mode corrected.** The attract mode is resynchronised in v2.0, with the original rendering preserved apart from the hack's signature.
* **Title screen.** A discreet white `Fullscreen Edition · Psicopompo` line was added below Nintendo's copyright. The original copyright line was also nudged 2 pixels to the right to center it.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223050" src="https://github.com/user-attachments/assets/0e15be06-1bbe-4cb1-9b44-5df626976089" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223113" src="https://github.com/user-attachments/assets/990be6ee-a48a-4e8c-a422-15ec17976c61" />

## Map and rear-view mirror: gone, on purpose

The original idea was to keep both as small insets over the full race view.

Both are secondary Mode 7 renders, however, and keeping them meant dividing the frame again partway down the screen. That went directly against the goal of a clean fullscreen race view and introduced a new collection of timing, HDMA and rendering problems.

The map and rear-view mirror were therefore left out of fullscreen racing. The **Time Trial results map remains visible**, including the BEST 5 / BEST LAP information.

**A clean full-screen race view won over a cluttered compromise.**

Two-player mode retains the original split-screen presentation.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003628" src="https://github.com/user-attachments/assets/3c5f4f1a-1f72-4f38-85d1-d4f236b2507d" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-013030" src="https://github.com/user-attachments/assets/513fa905-178b-40e1-984c-91c2062df0cf" />

## How it was built: fixes that broke other things

This turned out to be much deeper than moving a sprite and changing a few coordinates.

The game combines the DSP-1, Mode 7, HDMA, OAM, sprite-depth sorting, collision routines, screen-space limits, color windows and several other systems that all assumed the original 1-player layout.

Almost every major fix opened another problem.

Rivals could pass through Mario because the collision code still used the old depth range. Pipes could become effectively invisible to collision detection. Objects could disappear too early because the new camera pushed them outside the original visibility limits. Sprites could wrap from the bottom of the screen to the top because the SNES stores their Y coordinate in 8 bits. Lakitu, shadows, smoke, coins, bananas and other effects could all remain tied to the old player position.

Lakitu's rescue was a good example. His script waits for his Y coordinate to reach certain values, chosen for the original screen range. With the larger view his path crosses negative values, so those waits, and the coin that he carries, never completed. The checks had to be adapted without changing his speed or sequence.

Even once the rescue worked, Lakitu kept leaving traces at the bottom of the screen. The rescue starts with a negative Y coordinate, so his head and cloud showed up in the extra lines at the bottom while he came down from above and again when he left upward; those elements are now hidden during those moments. Fixing that exposed one more problem: his three leftover hair pieces stayed drawn at the bottom edge for the rest of the race, because the game does not rewrite those sprite slots once Lakitu is done. Those are now parked off-screen, which also cleans up save states made with earlier versions.

The OAM ordering of the karts also had to be investigated to understand why some rivals overlapped incorrectly. Some experimental fixes worked visually but cost too many CPU cycles, causing slowdown in the NTSC version. Those approaches had to be discarded and replaced with much cheaper hooks.

Profiling the slowdowns showed that one of the hooks was the culprit: the check that decides whether the fullscreen logic applies was being run 40 to 55 times per frame by the sprite-drawing routines. In the heaviest scene tested (Lakitu's rescue), the game logic was taking about as long as the frame itself. The result of that check is now computed once per frame and read directly by the most frequently called routines. v1.3 goes one step further: the projection and object-culling code reads that cached result too, and the three chained wrappers that decide whether an object is on screen were merged into one routine. Normal driving, race starts with all eight karts and full races on Donut Plains showed no lag.

The work therefore became heavily regression-driven. **Dozens of reproducible save states** covering race starts, cups, collisions, effects, Time Trial, Ranked Out, Game Over, retry screens, credits, 2P and other situations were repeatedly replayed and compared frame by frame after changes.

For v1.4, the new rival-size distribution was checked over **3,360 compared frames**. Camera, timer, position/velocity fields and player sprites matched the preceding reference, and a 360-frame split-screen test also matched its full images. This is not a claim of exhaustive mode coverage.

Version 2.0 added dedicated regression checks for the new camera and adapted backgrounds. In bsnes, cold attract mode was compared against the original ROM over **2,950 frames**, with identical output apart from the hack's signature. **Twenty-seven real race states**, compared over 120 frames each, showed no rendering differences. The finish-camera OAM also matched the approved build, and multi-thousand-frame regression tests were run on the tracks receiving special background treatment.

Performance was checked separately. In a cold-booted Bowser Castle 1 Time Trial with scripted hard turns at high speed, the original USA ROM, v1.5 and v2.0 produced identical clock ticks (11,640 of 12,000) and the same times along the same trajectory. In a Bowser Castle 3 race state, v1.5 and v2.0 also matched (2,993 of 3,000 ticks) and produced the same final time.

The hard-turn stutter observed in these tests is native game behaviour, identical with and without the patch. For that reason, v2.0 does not modify AI scheduling or physics.

A fix was not considered done just because it worked in one screenshot. It had to survive the rest of the test suite.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223050" src="https://github.com/user-attachments/assets/0e15be06-1bbe-4cb1-9b44-5df626976089" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223113" src="https://github.com/user-attachments/assets/990be6ee-a48a-4e8c-a422-15ec17976c61" />

## AI-assisted development

This project was developed in collaboration with an **AI assistant**.

The AI handled a large part of the technical implementation: analysing the game's code, writing reverse-engineering and diagnostic tools, implementing patches, testing hypotheses and automating repetitive checks.

**Psicopompo directed the project**, deciding what to investigate, proposing and discarding approaches, interpreting results, identifying problems, choosing which solutions to pursue, testing the builds and validating the final behavior.

The distinction matters: the AI did a great deal of the programming work, but the project itself was not produced by asking for a finished hack and accepting the first result. It was an iterative process of investigation, implementation, testing, failure, correction and regression testing.

## Applying the patch

Input: a clean **Super Mario Kart (USA)** ROM, headerless.

|          |      Size | CRC32      | MD5                                | SHA-1                                      |
| -------- | --------: | ---------- | ---------------------------------- | ------------------------------------------ |
| Original |   524,288 | `CD80DB86` | `7f25ce5a283d902694c52fb1152fa61a` | `47E103D8398CF5B7CBB42B95DF3A3C270691163B` |
| Patched  | 1,048,576 | `61307000` | `c140f59f1d272ed263084a27dcbef80e` | —                                          |

Download **`Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).zip`** from the releases. The archive contains the IPS and BPS patches, `LÉEME.md`, `README.md` and English and Spanish changelogs. No game ROM is included.

* `Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).bps` — **recommended**; it verifies the input ROM. Use Flips, beat, MultiPatch or RomPatcher.js.
* `Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).ips` — use any IPS-compatible patcher.

The output is expanded to 1 MB. New code and data are stored in the added space, and the ROM size byte is updated. The internal checksum is corrected, so no checksum warning should appear on compatible flashcarts or in patching tools.

Apply **only one patch** to a copy of your clean ROM. The patch is cumulative over the original ROM: **do not apply v2.0 on top of v1.4 or v1.5**.

The PAL version is not supported.

## Version history

* **v2.0** – Introduced the wide-horizon camera, enabled by default on all 20 tracks, with in-race SELECT switching between the new and classic cameras. The new view also covers the intro, starting zoom and finish turn. Adapted backgrounds across all 20 tracks, including extended skies, seamless gradient fills, Koopa Beach clouds at all three heights from the starting grid, and clipped Ghost Valley pillars. Fixed the duplicated player face on winning, mountain flicker during loading, intermittent black and blue lines in Ghost Valley, the oil slick's native collision threshold and the ROUND banner alignment. Resynchronised attract mode and reduced CPU cycles without changing rendered output. Retains all v1.5 improvements. Validated in bsnes and RetroArch through attract-mode comparison, 27 real race states, finish-camera OAM comparison and extended regression tests. No real-hardware testing is claimed.

* **v1.5** – Fixed the Time Trial results screen. Results now correctly show every lap, highlighted times, TOTAL, and the map with BEST 5 / BEST LAP, while racing remains fullscreen and the Grand Prix results layout is preserved. Tested with Time Trial and a normal race. Includes all v1.4 improvements.

* **v1.4** – New geometric distribution of the eleven original rival sizes, selected after comparing the alternatives in motion. The normal player size is unchanged. The lateral starting-grid correction now applies from the beginning of the camera approach while preserving the full zoom and orbit. Corrected Lakitu's shadow in fullscreen and both split-screen views while retaining the previous lower-edge body correction. The changes were checked over 3,360 compared frames, with a separate 360-frame split-screen comparison. Tested in bsnes and RetroArch and approved through visual testing.

* **v1.3** – Lakitu no longer peeks out at the bottom of the screen: his head and cloud are hidden while he comes down from above or leaves upward (Ghost Valley, the water falls), and the leftover pieces (the "three hairs") that stayed behind at the start and after a rescue are cleaned up. In 2P, Lakitu's coin and lost coins are drawn at the right height instead of 88 pixels too low. Lower CPU load in 1P (peak load in the heaviest start tested: 95.7% → 90.5%). Includes all v1.2 fixes.

* **v1.2** – The ground projection is realigned with the kart's on-screen position, so the track under the kart matches where the kart is drawn: collisions with walls, edges and pits now happen at the right place (they used to trigger too early). Fixed Lakitu's rescue after falling off the track. Reduced slowdowns by computing the fullscreen check once per frame. Includes all v1.1 fixes.

* **v1.1** – Fixed a few stray white pixels that appeared in the transition band of the picture. The LAP TIME table and standings faces were moved 5 pixels further down.

* **v1.0** – First release.

## Status and limitations

* **USA only.** The PAL version is not supported.
* **224 lines / 60 Hz NTSC.**
* Tested in **bsnes** and **RetroArch**. The SNES9x core has not been tested.
* **Real hardware and flashcarts:** v2.0 has not been tested on real hardware or flashcarts. Earlier versions may have been tested on hardware, but this does not establish compatibility for v2.0.
* Validation for v2.0 includes a 2,950-frame attract-mode comparison against the original ROM, 27 real race states compared over 120 frames each, finish-camera OAM verification and multi-thousand-frame regression tests on the tracks receiving special background treatment.
* The 50cc and 100cc cups were played through with v1.1. Later versions have received additional state-by-state regression, frame-by-frame comparison, performance measurements and play sessions, but this does not guarantee that every mode is free of bugs. Some modes have received less testing than others.
* Track objects such as pipes still follow the original game's section-based loading rules. With the new camera reference, some appearance and disappearance boundaries are more noticeable.
* The 2-player mode retains its original split-screen behavior and does not use the fullscreen 1-player camera.
* The map and rear-view mirror are hidden during fullscreen racing. The Time Trial results map remains visible.
* Bug reports are welcome. Please include the emulator and core, game mode, and a save state that reproduces the problem.

## Credits and notice

* **Psicopompo** — project direction, research, analysis, solution design, testing and validation.
* **AI assistant** — code analysis, reverse-engineering tools, patch implementation and test automation, under Psicopompo's direction.

Super Mario Kart © Nintendo.

This is an unofficial fan project and is not affiliated with or endorsed by Nintendo.

No game data is distributed. You must provide your own legally obtained ROM.
