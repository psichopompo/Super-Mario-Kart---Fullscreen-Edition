<img width="1280" height="400" alt="Super-Mario-Kart-Logo" src="https://github.com/user-attachments/assets/838b9ed3-0d4c-4db8-a1d1-c81326d3d1ab" />

# Super Mario Kart – Fullscreen Edition (USA)

**A real full-screen view for single-player Super Mario Kart: the camera moved closer to the kart, and everything that depended on the old layout rebuilt around the extra room.**

By Psicopompo · Patch for the USA ROM · IPS and BPS

---

<img width="256" height="224" alt="Super Mario Kart (USA) (patched)-261002-222409" src="https://github.com/user-attachments/assets/e7da9dbb-28f2-425a-bfb0-714e8307a836" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-222732" src="https://github.com/user-attachments/assets/f5519df5-4ac0-479e-bf02-50e9db8743f5" />



## Why this exists

Super Mario Kart is a gorgeous game that has always played single-player with one hand tied behind its back. The race is drawn in a cropped part of the screen, and the lower area is reserved for a map or rear-view mirror. It is a leftover from the split-screen design of the two-player mode.

The obvious first step is to switch off the HDMA windowing that carves the picture in two, so the Mode 7 floor takes the whole 256×224 image. But that is only the first step. The picture is bigger and everything else is where it was: the camera still points at the old spot, the kart is still drawn for the old layout, and every piece of HUD, every banner and every effect still believes the screen is cropped.

**This is not just "removing the map".** This patch moves the camera and then deals with the consequences.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003333" src="https://github.com/user-attachments/assets/631fc658-0991-45ac-8723-63d9ac101e27" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003554" src="https://github.com/user-attachments/assets/46090e30-12c6-43ff-b6fa-80ef56e649be" />


## The idea, in one paragraph

The Mode 7 floor is projected by the console's DSP-1 coprocessor from a focus point under the kart. If you simply draw the kart lower, it floats: its shadow, its collisions, the rivals and the objects are still projected from the old point. So instead of moving the sprite, the patch feeds the DSP a focus point moved forward along the view direction. The real kart ends up lower on the screen, and the floor, the shadow, the objects and the collisions are all projected consistently from there. Same perspective, same rotation, nothing stretched. At the start of the race Mario sits on the floor mark of his grid spot.

## What changes

* **Camera.** Closer to the kart, with kart, shadow, collisions and rivals consistent with the larger picture.
* **HUD relocation.** With room to spare, layout problems the original kept for lack of space are gone. The clearest example: the big finishing-rank digit no longer overlaps the small rank digit beside the kart and coin counters (the small digit moved about 8 px to the left; the big one is untouched).
* **Centered tables and banners.** The LAP TIME table and the rank faces (moved 20 px down from the original), Game Over, ROUND 1, and the Ranked Out banner with RETRY / END separated from it.
* **Effects and objects that depend on the kart's position**, repositioned: bananas, squash smoke, moles, lost coins.
* **2P mode.** Kept working. The design decision was not to chase every bug that comes from moving the player's view one by one: the 2P logic is handled separately, and the menus, effects, objects and artifacts that leaked into it were patched individually.
* **Side effects found along the way and fixed:** credits flicker, retry text position in 2P, Time Trial / 2P artifacts, a ball appearing behind Mario at the Time Trial start, and Lakitu's shadow during the rescue (it stayed up in the air, far from where Mario falls).
* **Title screen.** A discreet, white `Fullscreen Edition · Psicopompo` line under Nintendo's copyright. The copyright line itself was 2 px off-center in the original and has been nudged 2 px to the right.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-235523" src="https://github.com/user-attachments/assets/bf975651-62c8-4ca9-b89d-275134a13105" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-225311" src="https://github.com/user-attachments/assets/ccef2f32-302b-4048-bc9e-7a9cb7ac8702" />

## Map and rear-view mirror: gone, on purpose

The first plan was to keep both as a small inset over the full view. They are secondary Mode 7 renders, so keeping them meant splitting the frame again in mid-picture. That defeats the point (a clean full-screen image) and kept producing artifacts elsewhere. Every workaround broke something else. A clean screen beat a cluttered one.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003628" src="https://github.com/user-attachments/assets/3c5f4f1a-1f72-4f38-85d1-d4f236b2507d" />

## How it was built: fixes that broke other things

Almost every fix opened a new problem. Raise one banner and it collides with another. Move a counter and an effect still draws where the counter used to be. Adjust a table and the 2P version falls apart. The work was therefore regression-driven: dozens of save states (start line, cups, Ranked Out, Game Over, ROUND 1, Time Trial, 2P retry, credits, and more) are replayed against every change and compared frame by frame with the previous build. Nothing was patched on a hunch: each change was checked against code traces and frame captures first.

Performance mattered too. A first approach to hiding sprites that fell outside the picture cost enough CPU time to slow heavy scenes down. It was reworked so the patch adds no measurable load.

This project was developed in collaboration with an AI assistant. The AI did the technical work (reading and understanding the game code, writing and verifying the patches); Psicopompo directed it, decided what to do and how, tested every build and reported the problems with save states.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223050" src="https://github.com/user-attachments/assets/0e15be06-1bbe-4cb1-9b44-5df626976089" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223113" src="https://github.com/user-attachments/assets/990be6ee-a48a-4e8c-a422-15ec17976c61" />

## Applying the patch

Input: a clean **Super Mario Kart (USA)** ROM, headerless.

| | Size | CRC32 | SHA-1 |
|---|---|---|---|
| Original | 524,288 | `CD80DB86` | `47E103D8398CF5B7CBB42B95DF3A3C270691163B` |
| Patched | 1,048,576 | `755E23E7` | `DD741C34FAF2FB928FEDB0A135BDC0E7A8198DBD` |

* `Super Mario Kart - Fullscreen Edition (v1.0) (by Psicopompo).bps` — recommended; it verifies the input ROM. Use Flips, beat, MultiPatch or RomPatcher.js.
* `Super Mario Kart - Fullscreen Edition (v1.0) (by Psicopompo).ips` — any IPS patcher.

The output is expanded to 1 MB (new code and data live in the added space; the header size byte is updated). Apply the patch to a copy of your ROM.

## Status and limitations

* **USA only.** The PAL ROM crops the screen and is not supported.
* Tested in bsnes-accuracy emulation. Real hardware and flash carts are untested.
* The 50cc and 100cc cups have been played through with the final patch. 150cc, Mirror mode and the remaining modes have had less testing.
* Track objects (pipes, for example) appear and disappear by zones, exactly as in the original game: the game loads them by the section of the track the kart is in. With the camera closer, this is a bit more noticeable.
* Bug reports are very welcome, ideally with a save state.

## Credits and notice

* **Psicopompo** — camera, HUD, 2P work, testing, direction.
* Super Mario Kart © Nintendo. This is an unofficial fan project, not affiliated with or endorsed by Nintendo. No game data is distributed: bring your own legally obtained ROM.
