# Lenovo Legion 7 Gen 10 (16IAX10H) OpenRGB Support

This repo is a small “portfolio” wrapper around my OpenRGB contribution adding lighting support for the **Lenovo Legion 7 Gen 10** laptop.

The actual OpenRGB change is submitted upstream as a GitLab Merge Request; this repo primarily contains:
- A ready-to-apply patch file
- The MR description text
- Notes on how to reproduce / validate

## Device / Hardware

- Model: `Lenovo Legion Pro 7 16IAX10H` (Legion 7 Gen 10)
- OS tested: Arch Linux (Hyprland)
- USB lighting controller: `VID 048D` / `PID C197`
- Lighting zones:
  - Per-key keyboard (matrix)
  - Front “Neon” bar
  - Rear “Logo”
  - Fan shroud / vents

## Links

- Upstream OpenRGB project: https://gitlab.com/CalcProgrammer1/OpenRGB
- My fork/branch: https://gitlab.com/idiom444/OpenRGB/-/tree/lenovo-legion-gen10
- Merge Request: https://gitlab.com/CalcProgrammer1/OpenRGB/-/merge_requests/3111

## Contents

- `openrgb-legion-gen10.patch`: Patch against OpenRGB `master`.
- `OPENRGB_MR_DESCRIPTION.md`: Text used for the MR description.
- `OPENRGB_GITLAB_MR_GUIDE.md`: “first contribution” GitLab workflow notes.

## Applying the Patch (local OpenRGB clone)

```bash
git clone https://gitlab.com/CalcProgrammer1/OpenRGB.git
cd OpenRGB
git checkout -b lenovo-legion-gen10
git apply /path/to/openrgb-legion-gen10.patch
```

Then build OpenRGB normally for your platform and verify the device is detected.

## Notes

This work is derived from OpenRGB and is licensed under the same terms (GPL-2.0-or-later). See `LICENSE`.

