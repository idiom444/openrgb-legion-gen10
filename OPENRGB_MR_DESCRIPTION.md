## Summary

Add support for Lenovo Legion 7 Gen 10 laptop lighting (VID `0x048D`, PID `0xC197`) to the existing Lenovo Gen7/8 USB controller implementation.

This model exposes zones for:
- Per-key keyboard (matrix)
- Front "Neon" bar
- Rear "Logo"
- Fan shroud / vents

## Hardware

- Laptop: `Lenovo Legion Pro 7 16IAX10H` (Legion 7 Gen 10)
- OS tested: Arch Linux
- USB VID/PID: `048d:c197`

## What Changed

- Add Gen10 PID constant and HID detector entry.
- Add Gen10 vents zone definition (18 vent groups).
- Implement Gen10-specific protocol differences:
  - Feature report payload length is 16-bit for some reports (bytes `2..3`).
  - Direct/per-LED updates use `0x07/A1` with `(led_id_lo, led_id_hi, r, g, b)` entries.
  - Direct mode enable uses `0x07/D0` and is reasserted to keep streaming updates reliable on Gen10.
- Allow large per-key/group updates to span multiple reports when required.

## Testing Performed

- OpenRGB GUI:
  - Verified all listed hardware modes work on this device.
  - Verified brightness control works.
  - Verified profile persistence works.
  - Verified keyboard mapping appears correct during per-key edits.
- OpenRGB SDK / streaming:
  - Verified continuous per-LED updates in "Direct" mode (per-key + all zones).

## Notes / Rationale

Gen10 direct updates appear to be ignored unless direct mode (`0x07/D0`) has been enabled; reasserting `D0` prior to streaming updates keeps effects reliable on this model.

