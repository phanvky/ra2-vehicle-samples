# RA2 Yuri's Revenge vehicle samples (Elaina mod)

Four complete vehicles taken from the **Elaina mod 1.4.10** for Red Alert 2: Yuri's Revenge, as reference for designing a new vehicle in the same format.
All models, icons and rules belong to the Elaina mod authors. They are shared here only as a format reference for a personal, non-commercial game setup. Please support the original mod.

The game runs on **VERA20k**, a re-implementation of the RA2/YR engine. It reads the standard Westwood formats below. Ares/Phobos DLL-only features are **not** available, so use only standard `rulesmd.ini` / `artmd.ini` keys.

## What each vehicle folder contains

| Path | Meaning |
|---|---|
| `1-file-hinh/*.vxl` | Voxel model (body). |
| `1-file-hinh/*.hva` | Hierarchical voxel animation for the `.vxl` with the same name. **Required** for every `.vxl`. |
| `1-file-hinh/*tur.vxl/.hva` | Turret (only for `Turret=yes` vehicles). |
| `1-file-hinh/*icon.shp` | Sidebar cameo, SHP (TS) 60x48, 1 frame. |
| `2-anh-xem-truoc/*.png` | Preview renders (8 facings) and the cameo as PNG. Not used by the game. |
| `3-luat-cua-xe.ini` | Excerpts of `rulesmd.ini` (vehicle, weapons, projectiles, warheads) and `artmd.ini` (art) for the vehicle. |

### K300P – coastal anti-ship missile launcher
- `K300P` (mobile) deploys into `K300PD` (separate VehicleType with its own model `k300pd.vxl`), linked by `UnloadingClass=K300PD`.
- No turret. Weapons `FakeWeapon` / `KH38`, `LandTargeting=1` (cannot hit land targets).

### XCB01 – amphibious tracked IFV with turret
- Body `xcb01.vxl` + turret `xcb01tur.vxl`.
- On water it uses `WaterImage=XCB01W` (`xcb01w.vxl` + `xcb01wtur.vxl`).
- Weapons `BMP1Gun` (cannon) and `M1134Launcher` (missile).

### S400 – long-range SAM launcher
- `S400` (mobile) deploys into `S400D` (`IsSimpleDeployer=yes`, `UnloadingClass=S400D`, `DeployFire=yes`). No turret. `Sight=15`.
- Weapons `S400Misl` / `S300MislE`, projectile `S300Proj`, warhead `BUKWH`.

### S300RADAR – search radar truck
- `S300RADAR` (mobile, `Sight=7`) deploys into `S300RADARD` (`Sight=25`). No weapon.

### How the radar extends the launchers' reach (VERA code, not INI)
This link is **not** in the mod's INI files. It is a custom rule in this VERA build (`src/sim/smart_tactics.rs`):
- `RADAR_GUIDED_TYPES = ["S300", "S300D", "S400", "S400D"]`, `RADAR_TYPE = "S300RADARD"`, `RADAR_DETECT_CELLS = 45`.
- Today the rule covers **air targets** (the S-300/S-400 are SAMs); for an anti-ship launcher Claude would extend it to ships. A radar-guided launcher picks targets by itself, deploys for them and keeps them (a player's order too) only when the target is inside its own `Sight=` **or** within 45 cells of an allied **deployed** `S300RADARD`. One radar serves every launcher. The weapon `Range=` still decides whether it can actually hit.
- So a new launcher (e.g. anti-ship) that should work with a radar needs: normal INI sections (vehicle, deployed form, weapon with long `Range=`, short `Sight=`), and its type names added to that list in the code (Claude does this part). A new radar truck would also be added there.

## What a new vehicle needs
1. `NAME.vxl` + `NAME.hva` (plus `NAMEtur.vxl/.hva` and `NAMEbarl.vxl/.hva` if it has a turret / separate barrel, and extra sets for deployed or water forms).
2. `NAMEicon.shp` cameo, 60x48 (or a 60x48 PNG to be converted).
3. A `rulesmd.ini` section (copy one of the samples and change `Name`, `Strength`, `Armor`, `Speed`, `Cost`, `Owner`, `Prerequisite`, `Primary`/`Secondary`, ...), any new weapon / projectile / warhead sections, and an `artmd.ini` section (`Voxel=yes`, `Remapable=yes`, `Cameo=NAMEicon`, fire FLH).
4. A short description: Vietnamese display name, which countries can build it, which building it requires.
5. Reuse existing sounds (`VoiceSelect`, `Report`, ...) where possible.

Vietnamese notes: see `DOC TRUOC - huong dan.txt`.
