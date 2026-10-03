<img width="1280" height="400" alt="Super-Mario-Kart-Logo" src="https://github.com/user-attachments/assets/838b9ed3-0d4c-4db8-a1d1-c81326d3d1ab" />

# Super Mario Kart – Fullscreen Edition (USA)

**A true full-screen view for single-player Super Mario Kart: the camera reference is changed so the projected scenery moves closer to the kart, while everything that depended on the old layout is rebuilt around the extra room.**

By **Psicopompo** · USA ROM · IPS and BPS

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

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-235523" src="https://github.com/user-attachments/assets/bf975651-62c8-4ca9-b89d-275134a13105" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-225311" src="https://github.com/user-attachments/assets/ccef2f32-302b-4048-bc9e-7a9cb7ac8702" />

## What changes

* **True fullscreen in 1P.** The race view uses the complete 256×224 display.
* **New camera reference.** The kart, road, rivals, objects, shadows and collision logic remain consistent with the new projection.
* **HUD relocation.** The extra space allows the position digits, car counter and coin counter to be rearranged without the original layout constraints. The small position digit is moved about 8 pixels left, while the large finishing-position digit is moved into the new space.
* **Centered tables and banners.** The LAP TIME table and standings faces are moved 20 pixels down. Game Over, ROUND 1, Ranked Out and the RETRY / END menus are also repositioned.
* **Position-dependent effects fixed.** Bananas, crush smoke, Monty Moles, lost coins and other effects that were tied to the old kart position are moved to match the new camera layout.
* **2P preserved.** The fullscreen logic is restricted to 1P. The 2-player branch keeps the original game logic through dedicated gates, while side effects that leaked into 2P were fixed individually.
* **Secondary graphical issues fixed.** Credits flicker, retry text in 2P, Time Trial artifacts, a stray ball behind Mario at the start of Time Trial, Lakitu's shadow during the rescue sequence, bottom-edge sprites, coin/life counter flicker, and several other problems were tracked down and corrected.
* **Title screen.** A discreet white `Fullscreen Edition · Psicopompo` line was added below Nintendo's copyright. The original copyright line was also nudged 2 pixels to the right to center it.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223050" src="https://github.com/user-attachments/assets/0e15be06-1bbe-4cb1-9b44-5df626976089" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223113" src="https://github.com/user-attachments/assets/990be6ee-a48a-4e8c-a422-15ec17976c61" />

## Map and rear-view mirror: gone, on purpose

The original idea was to keep both as small insets over the full race view.

Both are secondary Mode 7 renders, however, and keeping them meant dividing the frame again partway down the screen. That went directly against the goal of a clean fullscreen race view and introduced a new collection of timing, HDMA and rendering problems.

The map and rear-view mirror were therefore left out.

**A clean full-screen race view won over a cluttered compromise.**

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003628" src="https://github.com/user-attachments/assets/3c5f4f1a-1f72-4f38-85d1-d4f236b2507d" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-013030" src="https://github.com/user-attachments/assets/513fa905-178b-40e1-984c-91c2062df0cf" />

## How it was built: fixes that broke other things

This turned out to be much deeper than moving a sprite and changing a few coordinates.

The game combines the DSP-1, Mode 7, HDMA, OAM, sprite-depth sorting, collision routines, screen-space limits, color windows and several other systems that all assumed the original 1-player layout.

Almost every major fix opened another problem.

Rivals could pass through Mario because the collision code still used the old depth range. Pipes could become effectively invisible to collision detection. Objects could disappear too early because the new camera pushed them outside the original visibility limits. Sprites could wrap from the bottom of the screen to the top because the SNES stores their Y coordinate in 8 bits. Lakitu, shadows, smoke, coins, bananas and other effects could all remain tied to the old player position.

The OAM ordering of the karts also had to be investigated to understand why some rivals overlapped incorrectly. Some experimental fixes worked visually but cost too many CPU cycles, causing slowdown in the NTSC version. Those approaches had to be discarded and replaced with much cheaper hooks.

The work therefore became heavily regression-driven. **Dozens of reproducible save states** covering race starts, cups, collisions, effects, Time Trial, Ranked Out, Game Over, retry screens, credits, 2P and other situations were repeatedly replayed and compared frame by frame after changes.

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
| Patched  | 1,048,576 | `755E23E7` | `fa18bde9a9184ae268e0419273f11f73` | `DD741C34FAF2FB928FEDB0A135BDC0E7A8198DBD` |

* `Super Mario Kart - Fullscreen Edition (v1.0) (by Psicopompo).bps` — **recommended**; it verifies the input ROM. Use Flips, beat, MultiPatch or RomPatcher.js.
* `Super Mario Kart - Fullscreen Edition (v1.0) (by Psicopompo).ips` — use any IPS-compatible patcher.

The output is expanded to 1 MB. New code and data are stored in the added space, and the ROM size byte is updated.

Apply the patch to a copy of your clean ROM.

## Status and limitations

* **USA only.** The PAL version is not supported.
* **224 lines / 60 Hz NTSC.**
* Tested in **bsnes** and **RetroArch**.
* **Real hardware and flash cartridges are untested.**
* The **50cc and 100cc cups** have been played through with the final build. 150cc, Mirror Mode and other modes have received less testing.
* Track objects such as pipes still follow the original game's section-based loading rules. With the new camera reference, some of those appearance/disappearance boundaries are simply more noticeable.
* The 2-player mode retains its original split-screen behavior and does not use the fullscreen 1-player camera.
* Bug reports are welcome, ideally with a save state that reproduces the problem.

## Credits and notice

* **Psicopompo** — project direction, research, analysis, solution design, testing and validation.
* **AI assistant** — code analysis, reverse-engineering tools, patch implementation and test automation, under Psicopompo's direction.

Super Mario Kart © Nintendo.

This is an unofficial fan project and is not affiliated with or endorsed by Nintendo.

No game data is distributed. You must provide your own legally obtained ROM.
