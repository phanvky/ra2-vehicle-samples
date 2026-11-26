# RA2 Yuri's Revenge vehicle samples (Elaina mod)

Two complete vehicles taken from the **Elaina mod 1.4.10** for Red Alert 2: Yuri's Revenge, as reference for designing a new vehicle in the same format.
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

## What a new vehicle needs
1. `NAME.vxl` + `NAME.hva` (plus `NAMEtur.vxl/.hva` and `NAMEbarl.vxl/.hva` if it has a turret / separate barrel, and extra sets for deployed or water forms).
2. `NAMEicon.shp` cameo, 60x48 (or a 60x48 PNG to be converted).
3. A `rulesmd.ini` section (copy one of the samples and change `Name`, `Strength`, `Armor`, `Speed`, `Cost`, `Owner`, `Prerequisite`, `Primary`/`Secondary`, ...), any new weapon / projectile / warhead sections, and an `artmd.ini` section (`Voxel=yes`, `Remapable=yes`, `Cameo=NAMEicon`, fire FLH).
4. A short description: Vietnamese display name, which countries can build it, which building it requires.
5. Reuse existing sounds (`VoiceSelect`, `Report`, ...) where possible.

Vietnamese notes: see `DOC TRUOC - huong dan.txt`.
