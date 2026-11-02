# cubepro-cura

Cura profile for the Cube Pro (Klipper), machine "Cube Pro" on Cura's Custom FFF printer definition, quality
profile "CubeProfile" (draft, 0.2 mm layers), two extruders.

| Folder | What it is |
|---|---|
| `cura-5.11/` | The live profile files, copied from the Cura 5.11 flatpak data directory `~/.var/app/com.ultimaker.cura/data/cura/5.11/` with the same folder names. Only the files that belong to the Cube Pro. |
| `exports/` | Two older `.curaprofile` exports from February 2026. They predate the September 2026 rebuild. |

**To install**, close Cura, copy the files in `cura-5.11/` into the same folders of your Cura data directory
(flatpak: `~/.var/app/com.ultimaker.cura/data/cura/5.11/`) and start Cura again. Cura writes its own copy back on
exit, so don't copy while it is open.

## What the slicer has to mirror from the printer

Checked against the printer's `printer.cfg` on 2026-09-12.

- No heated bed. `machine_heated_bed` stays `False`, or Cura emits M140/M190 for a heater that does not exist.
- A chamber heater instead. `machine_heated_build_volume = True`; Cura then emits only M141. The standing
  setting is 45 C. Keep it under about 50 C, because heat creep in the bowden path is the risk.
- Klipper limits: `max_accel` 6000, `max_velocity` 200, `max_z_velocity` 20. The profile uses acceleration
  6000 for every `acceleration_*` setting (travel does not inherit from print) and travel speed 200.
- Speeds: print, infill and inner walls 160, outer wall 95, top and bottom 80, first layer 15.
- Extruder `max_extrude_only_velocity` is 15 mm/s, so `retraction_speed = 15` and `machine_max_feedrate_e = 15`.
- Klipper ignores M205, so `jerk_enabled` stays `False`.
- No bed probe or mesh (no G29) and no firmware retraction (no G10/G11).
- Start G-code is `START_PRINT T={material_print_temperature_layer_0} C={build_volume_temperature}`. Cura
  turns off its own temperature prepend when it sees that token, so no M104/M109 comes before it.

Gcode files are not kept here.

## About this copy

A public snapshot of my private working repo. More of my projects: [nbdevlab.com](https://www.nbdevlab.com).


## About this copy

A public snapshot of my private working repo. More of my projects: [nbdevlab.com](https://www.nbdevlab.com).

## License

GNU General Public License v3.0 or later, see [`LICENSE`](LICENSE).

<sub>Preparing this public copy from my private repo was done with help from Claude.</sub>
