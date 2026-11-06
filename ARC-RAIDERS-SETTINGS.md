# ARC Raiders settings — RTX 5090 + AW3423DWF 165 Hz

**Updated November 6, 2026.** Based on the user's NVIDIA Control Panel and ARC Raiders screenshots, plus the sources linked below.

## Priorities

1. **Prevent tearing, minimize input delay, and keep motion consistent.**
2. **Preserve good image quality on the RTX 5090.**

No configuration can guarantee zero input lag or eliminate every game hitch. This is a recommended baseline, not a benchmark of this PC. Actual gameplay FPS, CPU, installed driver and game build have not been measured.

**Your latest driver screenshots already look right. No broad driver overhaul is needed.** The remaining work is to verify that the ARC Raiders program profile inherits those settings, confirm G-SYNC is active, and check the frame-rate ceiling in gameplay.

Related: [all NVIDIA 3D settings](RTX-5090-GAMING-GUIDE.md) · [V-Sync explained](VSYNC-GUIDE.md).

## What moves the needle, ranked

| Priority | Setting or action | Why it matters |
| --- | --- | --- |
| **1 — Tear prevention** | G-SYNC enabled + NVIDIA V-Sync **On** + stay below 165 FPS | Synchronizes presentation without repeatedly reaching the display ceiling. |
| **2 — Responsiveness** | In-game NVIDIA Reflex **On** | Manages the render queue in the game; driver Low Latency Mode is not a substitute when Reflex is available. |
| **3 — Consistent motion** | Verify the automatic cap; use one manual cap only if needed | Prevents overshooting the refresh ceiling. If performance varies badly, a lower sustainable cap can feel steadier. |
| **4 — Real rendering performance** | Frame Generation **Off** initially; tune expensive graphics settings and DLSS | Measure actual rendered performance before adding interpolated frames. |
| **5 — Image quality** | Native output resolution, DLSS **Quality / Transformer**, High graphics starting point | Preserve detail while leaving room for stable frame times. Increase visual settings only after the first four priorities are satisfied. |

NVIDIA recommends Reflex and documents the G-SYNC/V-Sync automatic below-refresh cap. Uncapped V-Sync Off can achieve lower latency but permits tearing, so it is not the default for your stated priorities. [NVIDIA latency guidance](https://www.nvidia.com/en-us/geforce/guides/system-latency-optimization-guide/)

## NVIDIA Control Panel: keep these settings

Your three latest screenshots show **Global Settings**, not ARC Raiders' Program Settings. An existing program override can differ from the global value.

Open **Manage 3D settings → Program Settings → ARC Raiders**. Select the actual game executable, not just its launcher. For matching global values, use **Use global setting** where available; explicitly correct any conflicting game override.

| Setting | Latest screenshot | ARC Raiders recommendation | Importance / action |
| --- | --- | --- | --- |
| Monitor Technology | G-SYNC Compatible | **G-SYNC Compatible** | **Critical: keep.** Also enable the display under Set up G-SYNC; this row alone does not prove it is active in gameplay. |
| Vertical sync | On | **On** | **Critical: keep.** Do not change to Fast for this profile. |
| Max Frame Rate | Off | **Off initially** | Keep while checking Reflex automatic limiting. Use 162 FPS here only if a manual limiter is needed and the game limiter is not being used. |
| Low Latency Mode | Off | **Off** | Keep; enable Reflex inside the game. |
| Preferred refresh rate | Highest available | **Highest available**, if editable | Keep. Independently confirm Windows is running the display at 165 Hz. |
| Power management mode | Normal | **Normal** | Keep. Test Prefer maximum performance only if clock changes correlate with hitches; revert if it does not help. |
| Shader Cache Size | Driver Default | **Driver Default** | Keep. Increasing the limit is not a first-line fix; do not routinely clear the cache. |
| Texture filtering - Quality | Quality | **Quality** | Keep. High performance sacrifices quality without a demonstrated need here. |
| Texture filtering - Anisotropic sample optimization | Off | **Off** | Keep. |
| Texture filtering - Negative LOD bias | Allow | **Allow** | Keep; do not globally clamp the game's texture choices. |
| Texture filtering - Trilinear optimization | On | **On** | Keep with the Quality baseline. |
| Anisotropic filtering | Application-controlled | **Application-controlled** | Keep. Use in-game filtering options if exposed. |
| Antialiasing - Mode / Setting | Application-controlled | **Application-controlled** | Keep; use the game's DLSS/AA. |
| Antialiasing - Gamma correction | On | **On** | Keep; not an important ARC Raiders performance lever. |
| Image Scaling; Ambient Occlusion; FXAA; Transparency AA; MFAA; DSR Factors | Off | **Off** | Keep; avoid stacking legacy driver effects over the game's rendering. |
| DSR Smoothness | Inactive with DSR Off | Leave inactive | No work needed. |
| Threaded optimization | Auto | **Auto** | Keep; forcing On is not a general CPU-performance fix. |
| Triple buffering | Off | **Off** | Keep; this driver option concerns OpenGL, not ARC Raiders' DX12 buffering. |
| OpenGL GDI compatibility / rendering GPU | Auto / Auto-select | **Auto / Auto-select** | Keep; not relevant ARC Raiders tuning controls. |
| Vulkan/OpenGL present method | Auto | **Auto** | Keep; not a DX12 stutter fix. |
| CUDA - GPUs / Sysmem Fallback Policy | All / Driver Default | **All / Driver Default** | Keep; not controls for ARC Raiders' rendering latency. |
| Virtual Reality pre-rendered frames / VRSS | 1 / Off | **1 / Off** | Keep; irrelevant to this monitor game. |
| Background Application Max Frame Rate | Off | Optional **30 FPS** | Only reduces background load while tabbed out. No foreground FPS benefit promised. |

Feature applicability: [NVIDIA Control Panel reference](https://www.nvidia.com/content/Control-Panel-Help/vLatest/en-us/mergedProjects/3D%20Settings/Manage_3D_Settings_%28reference%29.htm).

**Relative to your screenshots: there is no essential visible global 3D-setting change left.** A manual FPS cap is conditional; background limiting is optional. The general repository guide's 10 GB shader-cache and global 162 FPS suggestions are optional baselines, not requirements to replace this working ARC Raiders profile.

## ARC Raiders: settings shown in your screenshots

| In-game setting | Screenshot value | Recommendation |
| --- | --- | --- |
| Window Mode | Borderless Fullscreen | **Keep** initially; verify G-SYNC in this mode. |
| Display Resolution | 3440 × 1440 | **Keep** native output. |
| NVIDIA DLSS Frame Generation | Off | **Keep Off** for your latency-first baseline. |
| VSync | Off | **Keep Off**; use NVIDIA profile V-Sync On. |
| NVIDIA Reflex Low Latency | On | **Keep On**. |
| Frame Rate Limit | Unlimited | Keep initially while testing automatic below-refresh limiting. |
| Upscaled Resolution | 100% — 3440 × 1440 | **Keep** native output. |
| Resolution Scaling Method | NVIDIA DLSS | **Keep**. |
| NVIDIA DLSS Quality | Quality | **Keep** as the starting point. |
| NVIDIA DLSS Model | Transformer | **Keep**. |
| Render Resolution readout | 50% — 1720 × 720 (DLSS) | **Verify after applying settings.** This readout appears inconsistent with the usual Quality-mode scale; do not assume the screenshot proves the active internal resolution. |

For that last row, apply settings, reselect Quality if necessary, and reopen the menu. A stale display, override or game-specific behavior could explain it; the cause is not established. If it persists, check whether NVIDIA app DLSS overrides are active and compare using the game-controlled default. Do not force the output resolution down to 1720 × 720.

## V-Sync versus Frame Generation: they are not competing choices

The screenshot tooltip says enabling frame generation automatically enables Reflex and disables **the game's V-Sync switch**. It does not mean driver V-Sync must be disabled.

For optional frame-generation testing, use **G-SYNC On + NVIDIA V-Sync On + in-game V-Sync Off**. NVIDIA documents driver V-Sync support with frame generation. Its modern implementation depends on a compatible Windows presentation path; borderless fullscreen is not automatically incompatible. [NVIDIA Streamline documentation](https://github.com/NVIDIA-RTX/Streamline/blob/main/docs/ProgrammingGuideDLSS_G.md)

For your priorities:

- **Off is the recommendation**, especially if real rendered FPS is already close to the display ceiling.
- Try **2×** only if the base game runs steadily but you want smoother displayed motion.
- Keep it only if aiming still feels good and motion artifacts/pacing are acceptable.
- Higher multipliers and Dynamic mode are not necessary for establishing this 165 Hz baseline.
- Do not enable NVIDIA Smooth Motion on top of native DLSS Frame Generation.

Generated frames improve displayed fluidity; they do not make the game sample input at the displayed generated FPS. Do not choose frame generation solely because the counter gets bigger.

## Choose and verify one frame-rate strategy

### First choice: Reflex automatic limiting

Keep the game's limit Unlimited and NVIDIA Max Frame Rate Off. With G-SYNC, driver V-Sync and Reflex enabled, check gameplay in a scene capable of reaching the refresh ceiling. The expected result is a cap below 165 FPS. A value lower than 162 is normal.

### Fallback: one manual limiter

If automatic limiting does not work, start at **162 FPS** using the in-game limiter if it offers a suitable value and paces well. Otherwise use the NVIDIA ARC Raiders profile's Max Frame Rate. Keep the other manual limiter disabled.

162 is a starting margin, not an exact required number. Lower it if it overshoots the ceiling. If performance repeatedly swings below the target, test a lower cap that representative gameplay can sustain. For example, compare 120 FPS if a 162 target produces distracting fluctuations. A lower cap trades some responsiveness for steadier pacing; choose from measurements, not GPU model alone.

This follows [Blur Busters' below-refresh guidance](https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/14/). When frame generation is enabled later, recheck displayed FPS and pacing; limiter behavior can differ from the generation-Off baseline.

## Good visuals after synchronization is working

The graphics-quality section was not visible in the supplied screenshots. These are proposed starting points, not a claim about your current settings:

| Area | Starting point | Adjustment rule |
| --- | --- | --- |
| Overall preset | **High** | Establish stable frame times before trying Epic/maximum everywhere. |
| Textures | High; test the highest available tier | Keep higher detail if memory use and streaming remain healthy. |
| RTXGI / ray-traced lighting | Moderate available level | Lower first when GPU frame time is excessive; increase for visual richness only with headroom. |
| Shadows / effects | High | Lower one step if busy fights cause GPU-bound drops. |
| DLSS | Quality / Transformer | Try Balanced if GPU-bound; compare DLAA/native AA only with spare performance. |
| Motion blur | Off by preference | Improves visual clarity during aiming; not a guaranteed FPS boost. |

NVIDIA confirms ARC Raiders supports DLSS, Reflex and ray-traced global illumination. The quality choices above are authored recommendations, not an official preset or guaranteed 165 FPS result. [NVIDIA ARC Raiders feature overview](https://www.nvidia.com/en-us/geforce/news/arc-raiders-dlss-4-multi-frame-generation-out-now/)

## Five-minute check before further tweaking

1. Confirm **3440 × 1440 at 165 Hz** over DisplayPort, and G-SYNC enabled for the selected display.
2. Confirm the ARC Raiders program profile has no conflicting overrides. Apply and restart.
3. Enable the G-SYNC indicator temporarily. With frame generation Off, test a repeatable gameplay route rather than the menu.
4. Look for tearing while panning, inspect frame-time spikes and 1% lows where available, and assess aiming response. Average FPS alone is insufficient.
5. Repeat after warm-up. Driver/game updates may require shader rebuilding. Change only one graphics option at a time.
6. If borderless still tears, check that G-SYNC is active for that presentation mode. With frame generation Off, test in-game V-Sync On and driver application-controlled as a comparison; verify the below-refresh cap again.
7. If there are large freezes or crashes, investigate those separately. Test overlays/recording Off, check temperature/utilization, and consult current game/driver known issues. CUDA, OpenGL and VR tweaks are not likely remedies.

**Recommended baseline: keep your current NVIDIA settings; keep in-game V-Sync Off, Reflex On, Frame Generation Off, and DLSS Quality/Transformer. Verify G-SYNC and below-165 FPS behavior before sacrificing image quality or adding more tweaks.**
