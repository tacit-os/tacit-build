# Tacit Daily: 1.2.15

Short run in the test VM, 2026-11-14, 91 minutes, tacit 1.2.15-1, 3 times over on this build.
Report only: this does not hold a release back yet. The margins are provisional until 2-3 releases set the normal spread.
Language: en_GB.UTF-8, keyboard us (the computer's own).
Each part started from the same saved state of the computer (a snapshot), and the computer was left as found.

## In short

- Checks: 68 worked, 13 failed, 0 could not be measured (the VM, a mirror or a site, not Tacit; neither a pass nor a failure).
- Daily tasks: 6 of 9 worked every time they were measured.
- Unstable on this build (both worked and failed): 2, shown below and left out of the comparison.

## Daily tasks

| Task | Worked | Failed | Could not measure | What went wrong |
|---|---|---|---|---|
| Sound plays from Thyris | 9 | 0 | 0 |  |
| A wallpaper change shows | 9 | 0 | 0 |  |
| Files previews a picture and a PDF | 0 | 9 | 0 | the PDF was not previewed as itself on the settled screen (its worst cell 0% its colour, the box 1.4% of the screen; needs 80 % and 2%); the PDF was not preview |
| Search finds an app and starts it | 7 | 2 | 0 | unstable (2 of 3 repeats the same): Enter on "graphis" in search: did not happen in 30 s: graphis's window mapped and graphis answering |
| The notch opens and closes, with Esc and with a click outside | 7 | 2 | 0 | unstable (2 of 3 repeats the same): notch-open: no openlayer>>quickshell:islandAway within 10 s of the press |
| Praxis opens a session | 9 | 0 | 0 |  |
| Updates: a check for updates | 9 | 0 | 0 |  |
| Lock and unlock | 9 | 0 | 0 |  |
| Sleep and wake | 9 | 0 | 0 |  |

## Speed

Median, and the lowest to the highest of the times it was taken.

| | Median | Spread | Times |
|---|---|---|---|
| Settings, cold start | 4.55 s | 4.08 s to 5.21 s | 9 |
| Settings, warm start | 3.78 s | 3.63 s to 4.72 s | 9 |
| Files, cold start | 1.35 s | 1.13 s to 1.95 s | 9 |
| Files, warm start | 1.22 s | 1.09 s to 1.41 s | 9 |
| Thyris, cold start | 5.47 s | 5.18 s to 5.88 s | 9 |
| Thyris, warm start | 5.56 s | 5.18 s to 5.94 s | 9 |
| Praxis, cold start | 4.10 s | 4.05 s to 4.52 s | 9 |
| Praxis, warm start | 3.79 s | 3.54 s to 4.25 s | 9 |
| Graphis, cold start | 3.29 s | 2.98 s to 3.84 s | 9 |
| Graphis, warm start | 2.77 s | 2.60 s to 3.03 s | 9 |
| Viewer, cold start | 4.00 s | 3.61 s to 4.51 s | 9 |
| Viewer, warm start | 3.18 s | 3.05 s to 3.49 s | 9 |
| a page load in Thyris, to its load event | 659 ms | 411 ms to 1.02 s | 15 |
| a page load in Thyris, to its first paint | 332 ms | 132 ms to 784 ms | 15 |
| A wallpaper change, until the desktop shows it | 4.58 s | 2.98 s to 6.36 s | 9 |
| Search, from the key to shown | 500 ms | 290 ms to 901 ms | 9 |
| Praxis, from its start to its session list | 3.34 s | 3.21 s to 4.05 s | 9 |
| A check for updates | 5.1 s | 4.1 s to 8.2 s | 9 |
| Unlock, from Enter to the desktop answering | 866 ms | 779 ms to 1.60 s | 9 |
| Wake, until the system answers | 1.1 s | 1.1 s to 1.2 s | 9 |
| Wake, until the desktop answers (through the lock) | 6.5 s | 6.2 s to 6.8 s | 9 |
| The notch, from the key to shown | 335 ms | 302 ms to 792 ms | 14 |
| Power on to the sign-in screen | 15.0 s | 14.8 s to 22.2 s | 9 |
| Sign-in to a desktop that answers | 1.17 s | 1.06 s to 1.26 s | 9 |

## Lightness

Median, and the lowest to the highest of the times it was taken.

| | Median | Spread | Times |
|---|---|---|---|
| The shell: memory growth over the tasks | 298 MB | 276 MB to 338 MB | 3 |
| Hyprland: memory growth over the tasks | 340 MB | 320 MB to 343 MB | 3 |
| The shell: memory after 10 minutes at rest | 892 MB | 891 MB to 900 MB | 9 |
| Settings: memory after 10 minutes at rest | 358 MB | 345 MB to 363 MB | 9 |
| Praxis: memory after 10 minutes at rest | 208 MB | 204 MB to 220 MB | 9 |
| Graphis: memory after 10 minutes at rest | 173 MB | 169 MB to 174 MB | 9 |
| Viewer: memory after 10 minutes at rest | 321 MB | 308 MB to 349 MB | 9 |
| Thyris: memory after 10 minutes at rest | 587 MB | 526 MB to 588 MB | 9 |
| Hyprland: memory after 10 minutes at rest | 1791 MB | 1728 MB to 1801 MB | 9 |
| The shell: processor at rest | 4.3 % | 4.2 % to 4.5 % | 15 |
| Settings: processor at rest | 9.2 % | 8.9 % to 9.5 % | 15 |
| Praxis: processor at rest | 1.9 % | 1.8 % to 2.1 % | 15 |
| Graphis: processor at rest | 2.0 % | 1.9 % to 2.2 % | 15 |
| Viewer: processor at rest | 12.8 % | 12.4 % to 12.9 % | 15 |
| Thyris: processor at rest | 4.3 % | 4.1 % to 4.7 % | 15 |
| Hyprland: processor at rest | 516.2 % | 514.0 % to 517.8 % | 15 |
| The shell: wakeups at rest | 185/s | 182/s to 188/s | 15 |
| Settings: wakeups at rest | 480/s | 427/s to 526/s | 15 |
| Praxis: wakeups at rest | 227/s | 223/s to 239/s | 15 |
| Graphis: wakeups at rest | 166/s | 158/s to 177/s | 15 |
| Viewer: wakeups at rest | 170/s | 164/s to 176/s | 15 |
| Thyris: wakeups at rest | 135/s | 127/s to 137/s | 15 |
| Hyprland: wakeups at rest | 2000/s | 1979/s to 2054/s | 15 |
| Everything: processor at rest | 93.0 % | 92.6 % to 93.3 % | 15 |
| Disk: caches (home) | 11 MB | 11 MB to 11 MB | 3 |
| Disk: Thyris's data | 194 MB | 194 MB to 194 MB | 3 |
| Disk: journal | 24 MB | 24 MB to 24 MB | 3 |
| Disk: package cache | 128 MB | 128 MB to 128 MB | 3 |
| Disk: crash dumps | 56 MB | 56 MB to 56 MB | 3 |
| Disk: shell logs | 1.1 MB | 1.1 MB to 1.1 MB | 3 |

## Reliability

- Crashes: 30: /usr/lib/tacit/thyris/browser; /usr/lib/tacit/thyris/browser; /usr/lib/tacit/thyris/browser; /usr/bin/hyprsunset
- New QML errors: 0
- Not answering: 48: An application Blank page - browser-cef is not responding.
What do you want to do with it? --buttons Terminate;Wait; An application Blank page - browser-cef is not responding.
What do you want to do w
- Stuck surfaces: 11: after wallpaper: browser-cef: tone; after search: quickshell:islandAway; after wallpaper: browser-cef: tone; after wallpaper: browser-cef: tone
- Starts that failed: 0
- Errors in the journal: 50 (27 kinds): (coredump-worker): PIDFD validation failed: No such process; (coredump-worker): (binary); kernel: ataN.N: Check power mode failed (err_mask=NxN)

## Tried twice

A check that failed and was done once more (typing into the VM can drop a key); both results are kept.

- unlock (tasks): first not unlocked within 30 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- unlock (tasks): first not unlocked within 30 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- unlock (tasks): first not unlocked within 30 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked
- sign-in (starts from power on): first not usable within 120 s of the press; then worked

## Unstable on this build

These both worked and failed on the same build. Each is left out of the comparison until it is the same every time.

- Search finds an app and starts it
- The notch opens and closes, with Esc and with a click outside

## Not measured here

- Only on a computer: Wi-Fi, the touchpad (gestures, a pinch), the camera, the microphone heard, real sleep (a lid), the battery. The protocol is HARDWARE-DAILY.md.
