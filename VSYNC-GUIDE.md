# V-Sync explained: On, Off, Fast, and G-SYNC

**Reviewed November 6, 2026.** Recommendations for an RTX 5090, Alienware AW3423DWF at 3440 × 1440 / 165 Hz over DisplayPort, and ARC Raiders. These are starting settings, not benchmarks from this PC.

**V-Sync prevents screen tearing. Its possible costs are input delay and uneven motion, depending on how frames are delivered. For this setup, choose V-Sync On together with G-SYNC and a frame rate below 165 FPS.**

See also the [complete RTX 5090 settings guide](RTX-5090-GAMING-GUIDE.md).

## What tearing actually is

The monitor draws a refresh over time. If the GPU changes the displayed frame partway through that process, the screen can contain pieces of different frames. A moving object may appear horizontally split or misaligned.

That is different from:

- **Stutter:** motion pauses or advances unevenly.
- **Input latency:** a delay between your action and its visible result.
- **VRR brightness flicker:** brightness varies as refresh timing changes.

A synchronization setting can improve one symptom while worsening another. V-Sync is not a fix for every hitch, freeze or crash.

## What each NVIDIA option does

| Option | Behavior | Recommendation for this setup |
| --- | --- | --- |
| **Use the 3D application setting** | Lets the game's V-Sync setting decide. | Useful when intentionally relying on the game's implementation. |
| **Off** | Removes this synchronization requirement. Frames can appear during an ongoing refresh, permitting tearing. | An alternative for competitive play if you accept tearing to minimize latency. |
| **On** | Coordinates frame presentation to prevent tearing. Traditional fixed-refresh operation can introduce waiting. | **Use with G-SYNC and below-refresh limiting.** |
| **Fast** | Keeps rendering without a normal V-Sync FPS ceiling, displaying completed frames and discarding surplus ones. | Not our ARC Raiders baseline; see the Fast Sync section below. |
| **Adaptive** | Uses traditional V-Sync above the refresh threshold and disables it below that threshold. Tearing is then possible. | Not needed for this G-SYNC configuration. |
| **Adaptive (half refresh rate)** | Uses half the display refresh rate as its threshold. | Not appropriate for the intended 165 Hz experience. |

Options depend on driver, display, API and selected profile. Adaptive options may be unavailable when G-SYNC is selected. These are driver modes, not guarantees that every application supports every mode. [NVIDIA Control Panel reference](https://www.nvidia.com/content/Control-Panel-Help/vLatest/en-us/mergedProjects/3D%20Settings/Manage_3D_Settings_%28reference%29.htm)

## Why V-Sync can cause lag, but is still recommended here

With a fixed-refresh screen, refreshes occur on a fixed schedule. Synchronizing to that schedule can make a completed frame wait; buffering may increase the delay.

G-SYNC makes refresh timing follow frame availability within the display's operating range. V-Sync On complements that behavior by preventing tearing when timing varies. It does not force every frame to wait for a fixed 165 Hz schedule while G-SYNC is operating below the ceiling.

At or above **165 FPS**, a 165 Hz display has no further refresh-rate headroom. With V-Sync On, reaching that boundary can produce additional waiting. A below-refresh cap avoids repeatedly hitting it. G-SYNC with V-Sync Off can still permit tearing, including from timing variations; an FPS counter reports an average and cannot prove every frame arrived at a safe time. [Blur Busters explanation](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/15/)

For example, if the game is running around 120 FPS within the VRR range, the display can follow that cadence. If it could render 200 FPS, a below-refresh cap keeps presentation within the 165 Hz display's range instead.

This configuration is intended to balance image quality and responsiveness. It is not a promise of zero latency or the absolute lowest possible delay.

## Recommended ARC Raiders setup

Apply the driver choices under **NVIDIA Control Panel → Manage 3D settings → Program Settings → ARC Raiders**. Check for existing program overrides even if the global setting already looks correct.

| Location | Setting | Choose |
| --- | --- | --- |
| Windows / NVIDIA Change resolution | Refresh rate | **165 Hz** at native resolution |
| NVIDIA Set up G-SYNC | G-SYNC / G-SYNC Compatible | **Enabled** for the display and relevant game display mode |
| NVIDIA ARC Raiders profile | Vertical sync | **On** |
| NVIDIA ARC Raiders profile | Low Latency Mode | **Off**; use the game's Reflex |
| NVIDIA ARC Raiders profile | Max Frame Rate | **Off initially**, while checking automatic limiting |
| ARC Raiders | NVIDIA Reflex | **On** |
| ARC Raiders | V-Sync | **Off initially** |
| ARC Raiders | Frame Generation | **Off for initial testing** |

NVIDIA recommends Reflex for supported games and documents automatic below-refresh limiting with G-SYNC + V-Sync + Reflex. It also acknowledges that uncapped Reflex with V-Sync Off can achieve lower latency at the cost of tearing. [NVIDIA latency guide](https://www.nvidia.com/en-us/geforce/guides/system-latency-optimization-guide/)

### Do I need a 162 FPS cap?

**Only if you need a manual cap.** Start by observing whether Reflex already keeps FPS below 165.

- If it does, leave the extra manual limiter disabled.
- A Reflex limit lower than 162 FPS is normal. Do not try to raise it just to hit 162.
- If automatic limiting is not working, start with **162 FPS** in one manual limiter: preferably a well-paced in-game limiter, otherwise NVIDIA Max Frame Rate.
- If the limiter overshoots or still reaches the refresh ceiling, reduce the limit slightly.
- Avoid setting the same cap in the game, driver and an external limiter simultaneously.

The 162 value follows the common starting rule of at least three FPS below refresh rate; it is not a special value required by this monitor or a guaranteed Reflex cap. [Blur Busters optimal settings](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/14/)

The complete guide's global 162 FPS recommendation is a fallback for other games. **ARC Raiders' program-specific Off setting intentionally overrides it while Reflex handles limiting.** Different games can use different limiters.

### Why On in NVIDIA and Off in the game?

Both controls can affect synchronization. Using the driver setting provides a clear starting configuration; disabling the game's setting avoids relying on its particular implementation. It does not mean two enabled switches always “double the lag.”

The presentation path matters. NVIDIA's latency guide cautions that driver-forced V-Sync does not apply universally to windowed applications. Modern DX12 borderless presentation also differs from older desktop-window behavior.

Start with the configuration above. If G-SYNC is active but borderless play still tears or fails to behave as expected, test **in-game V-Sync On** instead; set the driver to **Use the 3D application setting** for a clear comparison. Recheck the FPS ceiling and pacing. Do not assume that every setting labeled “fullscreen” is exclusive fullscreen. [NVIDIA presentation caveat](https://www.nvidia.com/en-us/geforce/guides/system-latency-optimization-guide/), [Blur Busters display-mode guidance](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/14/)

## Why not Fast Sync?

“Fast” is a mode name, not a guarantee of better responsiveness.

Fast Sync has a useful role when a compatible game renders far above a fixed refresh rate. It selects from completed frames without limiting rendering to the monitor's rate. With too few excess frames, or FPS fluctuating around the refresh rate, displayed motion can become uneven.

Blur Busters' measurements found its benefits depended strongly on the ratio of rendered FPS to refresh rate, and recommended G-SYNC with ordinary V-Sync and a cap over pairing G-SYNC with Fast Sync. Its original tests used older hardware; treat the measured timings as those test results, not predictions for an RTX 5090. The practical recommendation here is **On**, not Fast. [Fast Sync testing](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/8/)

## When would Off be appropriate?

Choose **V-Sync Off in both driver and game**, with Reflex On, if you specifically want to compare the lowest-latency competitive configuration and accept tearing. Start uncapped and assess responsiveness, frame pacing and GPU load.

This is a different priority from smooth, tear-free presentation. For this user's mixed quality/performance goal, **On remains the recommended default**.

## Quick verification

1. Click **Apply**, restart the game, and confirm the ARC Raiders profile targets the actual game executable.
2. Check Windows reports 165 Hz. Enable NVIDIA's G-SYNC indicator temporarily and verify it appears during gameplay.
3. With frame generation Off, watch FPS during a scene that can exceed the refresh rate. Confirm the automatic or manual cap stays below 165.
4. Pan across vertical edges and look for horizontal breaks. Check motion consistency and input feel as well as the FPS number.
5. If tearing remains, verify program overrides, the active display and presentation mode before changing unrelated settings.
6. If enabling frame generation later, repeat these checks. Generated/displayed FPS and base rendered FPS differ, and limiter interactions can change. A higher displayed counter does not imply equally faster input response.

**Keep V-Sync On for the recommended G-SYNC profile. Use Off only for a deliberate tearing-versus-latency tradeoff; Fast is not an upgrade you need to enable.**

## Sources and scope

Documentation and first-hand testing reviewed on the date above:

- [NVIDIA: Manage 3D Settings reference](https://www.nvidia.com/content/Control-Panel-Help/vLatest/en-us/mergedProjects/3D%20Settings/Manage_3D_Settings_%28reference%29.htm) — mode definitions and conditional availability.
- [NVIDIA: system latency optimization](https://www.nvidia.com/en-us/geforce/guides/system-latency-optimization-guide/) — Reflex, G-SYNC/V-Sync and presentation caveats.
- [Blur Busters: optimal G-SYNC settings](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/14/) — below-refresh limits and Reflex.
- [Blur Busters: G-SYNC FAQ](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/15/) — tearing, timing variation and the refresh ceiling.
- [Blur Busters: Fast Sync measurements](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/8/) — tradeoffs compared with G-SYNC.

These sources include older foundational articles with subsequent updates. They are not a benchmark of this exact monitor, current ARC Raiders build or installed driver. Verify behavior after major updates.
