# RTX 5090 NVIDIA Control Panel guide
## High quality, smooth performance and low latency — AW3423DWF / ARC Raiders

**Documentation checked: November 6, 2026.** Target: desktop RTX 5090, Alienware AW3423DWF, 3440 × 1440 at 165 Hz over DisplayPort.

These are recommended starting settings, not measured benchmarks from this PC. The installed driver version, game build and screenshots were not available for inspection. NVIDIA's public Control Panel help mixes current, legacy, laptop and workstation features; it is not a precise inventory for every driver. The tables cover the desktop GeForce feature set plus conditional/legacy entries. Skip absent or greyed-out controls. Do not expose hidden Profile Inspector flags to reproduce this guide.

**“Global” below means our recommended baseline, not NVIDIA's factory defaults.** Program Settings can override it, and built-in game profiles may already contain overrides. “Inherit” means **Use global setting** where offered; a global-only control has no separate game override.

## Start here

1. Connect the monitor directly to the RTX 5090 by **DisplayPort**. In Windows Advanced display and NVIDIA **Change resolution**, choose **3440 × 1440, 165 Hz**. Dell specifies only 100 Hz at native resolution over HDMI. The DWF is a FreeSync Premium Pro display; do not confuse it with the DW's hardware G-SYNC model. [Dell specifications](https://www.dell.com/en-us/shop/alienware-34-curved-qd-oled-gaming-monitor-aw3423dwf/apd/210-bfrp/monitors-monitor-accessories)
2. Under **Set up G-SYNC**, enable G-SYNC / G-SYNC Compatible for the selected display. If the driver shows an unvalidated-display notice, enable settings for the selected display and verify operation rather than assuming certification. Start with fullscreen; enable windowed and fullscreen if needed for borderless play. Confirm with NVIDIA's G-SYNC indicator during actual gameplay.
3. Apply the global table, then add/select **ARC Raiders** under **Program Settings**. Browse to the actual running game executable if detection fails; do not target only Steam or the launcher. Click Apply and restart the game.
4. Start ARC Raiders at native output resolution, **DLSS Quality, Reflex On, frame generation Off**, high graphics quality. Compare DLAA/native AA when there is spare performance.
5. Use the tear-free synchronization recipe below. Do not copy the old GTX 1080 Ti profile wholesale.

### Choose one synchronization recipe

| Goal | NVIDIA V-Sync | In-game V-Sync | Frame limiting | Reflex |
| --- | --- | --- | --- | --- |
| **Recommended: smooth, tear-free 165 Hz** | On in the ARC Raiders profile | Off initially in fullscreen | Start with driver Max Frame Rate Off; check Reflex's automatic below-refresh cap | On |
| Same goal, automatic cap not working | On | Off initially | Set one manual limiter to **162 FPS**; prefer a well-paced in-game limiter, otherwise driver Max Frame Rate | On |
| Lowest competitive latency, tearing acceptable | Off in the game profile | Off | Uncapped initially; compare a sustainable cap if pacing suffers | On |

NVIDIA documents automatic below-refresh limiting with G-SYNC + V-Sync + Reflex. The exact cap need not be 162 FPS; a lower automatic value is normal. **162 is our manual starting point**, not a promised Reflex value. If it still touches 165, lower it slightly. For games without Reflex, our global 162 FPS driver cap is the fallback; disable it per game when using a good in-game limiter.

Presentation mode matters: NVIDIA's latency guide cautions that driver-forced V-Sync may not apply in windowed mode. If borderless play tears or fails to engage the expected cap, test in-game V-Sync instead, with G-SYNC enabled for that mode. Verify actual behavior rather than assuming a fullscreen menu label proves the presentation path. Keep only one deliberate manual frame limiter; Reflex may still impose its own lower limit. [NVIDIA latency guidance](https://www.nvidia.com/en-us/geforce/guides/system-latency-optimization-guide/)

## Manage 3D Settings: desktop GeForce checklist

Options are UI labels or concise enumerations, not hidden driver values. Some ranges and labels vary with GPU, driver, monitor and selected application. Recommendations and tradeoffs are editorial judgments for this setup. The underlying feature reference is [NVIDIA Control Panel Help](https://www.nvidia.com/content/Control-Panel-Help/vLatest/en-us/mergedProjects/3D%20Settings/Manage_3D_Settings_%28reference%29.htm); additional primary sources are linked beside newer features.

### Image quality and antialiasing

| Feature | Available/common options and variants | Recommended global | ARC Raiders / reason |
| --- | --- | --- | --- |
| Image Scaling | Off; On (GPU Scaling & Sharpening); Sharpen 0–100%; Overlay Indicator checkbox | **Off** | Inherit. Prefer the game's DLSS; avoid stacking spatial upscaling or sharpening. |
| Ambient Occlusion | Off; Performance; Quality; unsupported profiles may grey it out | **Off** | Inherit. Use the game's lighting/AO, not a legacy driver override. |
| Anisotropic filtering | Application-controlled; Off; 2x, 4x, 8x, 16x | **Application-controlled** | Inherit; select 16x in-game if exposed. Try driver 16x only for older games with inadequate filtering. |
| Antialiasing - FXAA | Off; On | **Off** | Inherit. Avoid an extra softening pass over temporal AA/DLSS. |
| Antialiasing - Gamma correction | Off; On | **On** | Inherit. Retain for applicable AA paths; not a DLSS quality switch. |
| Antialiasing - Mode | Off; Application-controlled; Enhance the application setting; Override any application setting | **Application-controlled** | Inherit. Let the game choose compatible AA. |
| Antialiasing - Setting | Application-controlled/read-only; None; commonly 2x, 4x, 8x; older GPUs/drivers expose additional MSAA/CSAA levels such as 8xQ, 16x, 16xQ, 32x | **Application-controlled** | Inherit. Values depend on Mode and hardware; do not force legacy MSAA into ARC Raiders. |
| Antialiasing - Transparency | Off; Multisampling; 2x, 4x, 8x Supersampling (some older menus include generic or 1x Supersampling) | **Off** | Inherit. Consider only for compatible older MSAA games. |
| DSR - Factors | Off/no selections; Legacy Scaling commonly 1.20x, 1.50x, 1.78x, 2.00x, 2.25x, 3.00x, 4.00x; RTX DL Scaling commonly 1.78x DL, 2.25x DL | **Off** | Global resolution feature. Optional for less demanding games; not the baseline for 165 Hz ARC Raiders. |
| DSR - Smoothness | 0–100% when DSR/DLDSR is available | **Leave default while DSR is Off** | No effect without DSR. If experimenting with DLDSR, try 50% and compare fine detail in motion. |
| Multi-Frame Sampled AA (MFAA) | Off; On, where supported | **Off** | Inherit. This is an MSAA technique, not DLSS Multi Frame Generation. |
| Texture filtering - Anisotropic sample optimization | Off; On | **Off** | Inherit. Favor texture stability. |
| Texture filtering - Negative LOD bias | Allow; Clamp | **Allow** | Inherit. Avoid broadly overriding the game's temporal-upscaling texture choices; Clamp is a per-game experiment for older shimmering content, not a universal fix. |
| Texture filtering - Quality | High performance; Performance; Quality; High quality | **Quality** | Inherit for balance. Optional High quality comparison if shimmering is visible and performance is adequate. |
| Texture filtering - Trilinear optimization | Off; On | **On** | Inherit with Quality. For an optional texture-purity profile, use High quality and Off where editable. |

DSR/DLDSR renders at a higher resolution and downsamples; it is not the same as DLSS upscaling. Enabling a factor only exposes resolutions—you must select a higher one in the game. Display configuration can hide DSR. [NVIDIA DLDSR explanation](https://www.nvidia.com/en-us/geforce/news/god-of-war-game-ready-driver/)

### Latency, synchronization, power and caching

| Feature | Available/common options and variants | Recommended global | ARC Raiders / reason |
| --- | --- | --- | --- |
| Background Application Max Frame Rate | Off; On, 20–200 FPS | **30 FPS** | Inherit. Reduce background load while tabbed out; disable per app if it interferes with background work. |
| Low Latency Mode | Off; On; Ultra | **Off** | **Off**, use in-game Reflex On. For games without Reflex, test Ultra per game and compare pacing. |
| Max Frame Rate | Off; On, current help lists 20–1000 FPS; older versions have lower ceilings | **162 FPS** for this 165 Hz monitor | **Off initially** with Reflex automatic limiting; use 162 only if needed, following the recipe above. |
| Monitor Technology | G-SYNC / G-SYNC Compatible; Fixed Refresh; ULMB only on eligible displays | **G-SYNC Compatible**, if available | Inherit after enabling G-SYNC. The AW3423DWF does not gain ULMB from this setting. |
| Power management mode | Normal; Prefer maximum performance; older/other products may show Optimal power, Adaptive, NVIDIA driver controlled, Prefer consistent performance | **Normal** | Inherit initially. Test Prefer maximum performance only if clock changes correlate with stutter; it costs power/heat and is not a guaranteed FPS gain. |
| Preferred refresh rate (monitor name) | Application-controlled; Highest available; may be hidden/disabled with VRR | **Highest available**, if editable | Inherit. Set 165 Hz in Windows separately. |
| Shader Cache Size | Driver Default; Disabled; 128 MB, 256 MB, 512 MB, 1 GB, 5 GB, 10 GB, 100 GB; Unlimited | **10 GB** to start | Global disk cache, not VRAM allocation. Consider 100 GB for many large games only with sufficient free SSD space. |
| Vertical sync | Use the 3D application setting; Off; On; Fast; conditional Adaptive and Adaptive (half refresh rate) | **On** for this G-SYNC baseline | Inherit for tear-free play; override Off for uncapped competition. Fast is not our G-SYNC choice. Adaptive variants may disappear with VRR. |
| Triple buffering | Off; On | **Off** | Inherit. This driver control is for OpenGL, not an ARC Raiders DX12 buffering fix. |

Reflex takes precedence over driver Low Latency Mode. The claim that the driver feature is *always* DX9/DX11-only is outdated: NVIDIA added DX12 Ultra Low Latency support in **551.23**. This does not make it preferable to native Reflex, nor guarantee identical behavior in every API/game. [NVIDIA 551.23 release information](https://www.nvidia.de/Download/driverResults.aspx/%20218113/en-us/)

The 10 GB cache choice is a practical disk-space compromise, not a universal optimum. A larger cache cannot fix every compilation or streaming hitch. Avoid routine cache deletion; repeat the same route after warm-up before judging stutter.

### GPU selection, OpenGL, CUDA and VR

| Feature | Available/common options and variants | Recommended global | ARC Raiders / reason |
| --- | --- | --- | --- |
| CUDA - GPUs | All; selectable installed CUDA GPUs | **All** | Inherit. Not a general DX12 performance control. |
| CUDA - Sysmem Fallback Policy | Driver Default; Prefer Sysmem Fallback; Prefer No Sysmem Fallback | **Driver Default** | Inherit. CUDA memory behavior, not a way to increase gaming VRAM. |
| OpenGL GDI compatibility | Auto; Prefer performance; Prefer compatible | **Auto** | Inherit; no ARC Raiders tuning benefit expected. |
| OpenGL rendering GPU | Auto-select; eligible installed GPU names | **Auto-select** | Inherit. If an OpenGL app chooses the wrong adapter, select **NVIDIA GeForce RTX 5090** for that app. Never select the old 1080 Ti. |
| Threaded optimization | Auto; On; Off | **Auto** | Inherit. Do not force On as a universal CPU optimization. |
| Virtual Reality pre-rendered frames | Commonly 1, 2, 3, 4; application-controlled wording may appear on other driver versions | **1**, if present | Inherit. No benefit for ordinary monitor gaming. |
| Virtual Reality - Variable Rate Super Sampling | Off; Adaptive; Always On, subject to supported VR profiles | **Off** | Inherit. For a supported VR title, try Adaptive separately. |
| Vulkan/OpenGL present method | Auto; Prefer native; Prefer layered on DXGI Swapchain | **Auto** | Inherit. ARC Raiders is not a reason to force a Vulkan/OpenGL presentation path. |

Sources: [NVIDIA CUDA fallback support](https://nvidia.custhelp.com/app/answers/detail/a_id/5490), [NVIDIA VRSS support](https://nvidia.custhelp.com/app/answers/detail/a_id/4957), and [NVIDIA's public driver-setting definitions](https://github.com/NVIDIA/nvapi/blob/main/NvApiDriverSettings.h). The API definitions contain more values than the consumer UI; do not treat every API value as an available menu entry. The present-method UI is also illustrated in [Smode's own technical bulletin](https://shop.smode.io/download/utilities/2024_09_10_New_SMODE_synchronization_setup.pdf).

## Conditional and legacy entries

These complete the cross-generation reference; **they are not instructions to find or enable unavailable features on an RTX 5090**. Keep defaults unless an application specifically needs them. Hardware-specific lists cannot be a universal dropdown inventory.

| Feature | Options / variants | Recommendation for this setup |
| --- | --- | --- |
| Image Sharpening (older GeForce / workstation variant) | Sharpening Off/On; Sharpen 0–1; Ignore Film Grain 0–1; GPU Upscaling checkbox | Off; use game sharpening conservatively. Modern GeForce commonly uses Image Scaling instead. |
| Maximum pre-rendered frames | Application-controlled; commonly 1–4 on older menus | Leave default if encountered; use modern Low Latency Mode/Reflex guidance instead. |
| Shader Cache (old toggle) | Off; On | On; newer drivers expose Shader Cache Size. |
| Texture filtering - Anisotropic filter optimization | Off; On | Off, if exposed. Separate from sample optimization. |
| Antialiasing line gamma | Off; On on applicable professional OpenGL configurations | Default; no ARC Raiders relevance. |
| Preferred graphics processor | Auto-select; High-performance NVIDIA processor; Integrated graphics | Normally absent on a desktop 5090. On hybrid systems select the desired GPU through Windows Graphics settings when Windows owns the preference. |
| CUDA - Double precision | Select eligible GPUs / no GPUs selected | None for gaming; legacy hardware-specific compute feature. |
| Dynamic Boost | On; Off on supported notebooks | Not applicable to desktop 5090; leave notebook default On. |
| WhisperMode | Off/On via supporting software; per-game FPS slider when enabled; legacy defaults commonly 40/60 FPS | Not applicable to this desktop. |
| Multi-display/mixed-GPU acceleration | Single display performance; Multiple display performance; Compatibility performance | Legacy OpenGL feature. Leave default for actual display topology; no reason to force single-display mode for ARC Raiders. |
| Multi-GPU performance mode / SLI rendering mode | NVIDIA recommended/Auto; Single-GPU; Force alternate frame rendering 1/2; hardware-dependent split-frame or SLI AA modes | Not applicable to a single RTX 5090. |
| SILK Smoothness | Off; Low; Medium; High; Ultra, if exposed | Off for latency-sensitive gaming; not the NVIDIA app's Smooth Motion. |
| Buffer-flipping mode | Auto-select; Use block transfer; Use page flip on relevant workstation drivers | Default/Auto; legacy OpenGL. |
| Deep color for 3D applications | Enable/Disable | Default; not the monitor's output bit-depth control. |
| Enable overlay | On/Off | Default; professional OpenGL overlay planes, not the game-performance overlay. |
| Exported pixel types | Color-indexed (8-bpp); RGB555; both | Default; professional overlay formats. |
| Unified back/depth buffer | On/Off | Default; professional OpenGL memory behavior. |
| Stereo - Enable / Enabled | On/Off | Off; not needed for this monitor. |
| Stereo - Display mode | Hardware-dependent choices: shutter glasses, passive/interlaced/checkerboard, display-specific or other stereo modes | Default; no single valid list across hardware. Not relevant to ordinary OLED gaming. |
| Stereo - Force shuttering | On/Off | Off. |
| Stereo - Swap eyes | On/Off | Off. |
| Stereo - Swap mode | Application-controlled; Per Eye; Per Eye-pair | Application-controlled. |

See [NVIDIA's cross-product reference](https://www.nvidia.com/content/Control-Panel-Help/vLatest/en-us/mergedProjects/3D%20Settings/Manage_3D_Settings_%28reference%29.htm) for applicability. These are compatibility entries, not additional performance tweaks.

## ARC Raiders: recommended game profile

In NVIDIA Program Settings, inherit the global table except **Max Frame Rate: Off initially**. Keep **Low Latency Mode: Off**, **V-Sync: On**, and **Power management: Normal**. Then configure the game:

| Game setting | Starting recommendation | When to change |
| --- | --- | --- |
| Output resolution / refresh | **3440 × 1440 / 165 Hz** | Keep native output even when DLSS lowers internal rendering resolution. |
| NVIDIA Reflex | **On** | Compare On + Boost, if offered, only when it measurably improves latency/pacing; expect more power use. |
| DLSS Super Resolution / AA | **Quality** | Compare DLAA/native AA for maximum clarity with spare headroom. Try Balanced if GPU-bound and below the desired rate. |
| DLSS Frame Generation / Multi Frame Generation | **Off** for the initial competitive profile | Optional for visual fluidity when base FPS is already healthy. Generated FPS is not equivalent to input responsiveness at that FPS. |
| Graphics quality | **High starting preset**, then increase textures if desired | Reduce costly shadows/effects/lighting selectively if GPU-limited; CPU-limited scenes may not improve with lower resolution. |
| Ray-traced global illumination / RTXGI | **Start at a moderate available level** | Increase for richer lighting if frame times allow; lower it before sacrificing output resolution. Labels vary by build. |
| Motion blur | **Off** by preference | Enable only if you prefer its appearance. |
| V-Sync / FPS limit | Follow the synchronization recipe above | Check actual frame rate, tearing and pacing in the chosen display mode. |

NVIDIA confirms ARC Raiders supports Reflex, DLSS and ray-traced global illumination. These recommendations are an authored balance for this hardware, not an official Embark preset or a promise of locked 162 FPS. [NVIDIA ARC Raiders feature announcement](https://www.nvidia.com/en-us/geforce/news/arc-raiders-dlss-4-multi-frame-generation-out-now/)

### NVIDIA app features are separate from Manage 3D Settings

Do not search for these as mandatory classic Control Panel rows:

- **DLSS overrides:** model, Super Resolution/DLAA and frame-generation choices vary with app, driver and game support. Start with the game's settings; test a supported newer model per game rather than imposing a universal global override.
- **Current ARC Raiders support:** NVIDIA's 2026 material describes DLSS 4.5 Super Resolution upgrades and RTX 50-series Dynamic Multi Frame Generation up to 6X through the app. That expands available options; it does not change our frame-generation-Off competitive baseline. [NVIDIA 2026 update](https://www.nvidia.com/en-us/geforce/news/dlss-4-5-crossout-remastered-modern-warfare-4-frame-gen-beta/)
- **Smooth Motion:** keep Off for ARC Raiders. Prefer a game's native frame-generation integration if you elect to use generation; do not stack generators. [NVIDIA Smooth Motion introduction](https://www.nvidia.com/en-us/geforce/news/gfecnt/20251/nvidia-app-update-dlss-overrides-and-more/)
- **RTX HDR / RTX Dynamic Vibrance / filters:** optional image-processing features, not required performance settings. Establish the baseline without filters, then compare individually. Prefer a game's working native HDR implementation when available.

## Validate quality, latency and stutter

1. Record driver version, game build, resolution, presentation mode, DLSS mode, frame-generation state and limiter. Save screenshots of previous settings before changing them.
2. Confirm 165 Hz and G-SYNC activity in gameplay. Check for tearing and OLED brightness flicker; VRR cannot conceal large frame-time spikes.
3. With generation Off, run the same representative route several times. Compare frame-time spikes, 1% lows and available latency measurements, not only average FPS. Warm-up runs matter after driver/game updates.
4. Change one item at a time. Test High quality filtering, DLAA, higher RTXGI, or Reflex Boost independently. Keep only changes that help your priorities.
5. If stutter persists, compare overlays/recording Off, check CPU/GPU utilization and temperatures, and check the installed driver's release notes and game support updates. Do not assume a CUDA, OpenGL or VR setting can fix a DX12 streaming/CPU issue.
6. Restore the ARC Raiders program profile to roll back experiments. Global Restore and program Restore are separate; recheck your G-SYNC baseline afterward.

**Largest changes from the old Overwatch/1080 Ti profile:** use G-SYNC Compatible instead of Fixed Refresh, application-controlled AA/filtering instead of forcing them Off, Quality instead of High performance filtering, Auto threaded optimization instead of forced On, normal global power behavior, and native Reflex with a deliberate synchronization strategy.

## Maintenance

Recheck after major driver or game updates. Keep the date above tied to documentation review, not an assumed installed driver version. If a new row appears, record its exact label and dropdown from the installed Control Panel before adding it. This guide intentionally does not claim that an older public help page exhaustively describes a future driver UI.
