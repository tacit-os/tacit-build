# Tacit Daily on a computer

`tools/daily-bench` measures Tacit in the test VM. This is the part the VM cannot do: the battery, real sleep, Wi-Fi,
the touchpad, the camera, the microphone, Bluetooth sound, a game on a graphics card, and the steps that need an
account (WhatsApp, Google, Steam, Discord, a YouTube stream key). A tester runs it on a laptop with the release
installed. None of these is ever marked passed by the benchmark; only what a tester saw and wrote down counts.

## Before

- The laptop has the release installed (Settings > About), is charged to at least 80 %, and is signed in to the
  accounts the steps below need. Brightness at the level you use; no other apps open.
- Copy `tools/hardware-daily` to the laptop and run it in a terminal there: `python3 hardware-daily <version>`.
  It asks your name, reads the numbers it can and asks what only you can see. `--only <id>` runs one part again.
- At the end, copy `hardware-<version>.json` into this checkout's `out/x86_64/` and run
  `tools/daily-bench <version> --report`: the scorecard takes it in, with your name and the laptop beside each answer.

## The steps (about 1 h 45 min, most of it the battery)

| Part | What you do | What is recorded |
|---|---|---|
| battery | 30 min at rest, then 30 min of a 1080p YouTube video full screen, unplugged | watts and % an hour, each |
| sleep | close the lid 5 minutes, open it, unlock | whether the lock came and the desktop answers; the battery across it; Wi-Fi back within 10 s |
| wifi | join a network from the notch or Settings, load a page | connected, the page loaded |
| touchpad | two-finger scroll, three-finger swipe up and to the sides, tap to click | your answer (a swipe up must not send a window to a half) |
| camera | a call on meet.jit.si in Thyris (no account) | a frame from the camera; whether the other side sees you |
| microphone | speak for 3 seconds | the loudest sample (above 0.05 counts) |
| bluetooth | pair headphones or a speaker; a tone, then YouTube | where the sound went (a bluez output); whether you heard it, in sync |
| proton | a Proton game from Steam, 2 minutes, with MangoHud logging | frame rate (median, 1 % low), frame times (99th percentile) |
| creator.stream | stream to YouTube from OBS for 2 minutes | your answer |
| creator.whatsapp | a voice note received in WhatsApp Business Web, found by name in search, played | your answer |
| creator.sheets-topup | an online spreadsheet edited; the top-up website up to its payment page | your answer |
| office.pinch, office.mic-heard | a pinch zoom in Thyris; a real call where the other side hears you | your answers |
| gamer.discord-share | a Discord call with a screen share | your answer |
| everyday.messaging | WhatsApp Web and Discord in the background: a message's notification arrives | your answer |
| everyday.vpn-provider | your own VPN from a provider (OpenVPN or WireGuard with a server) connects and shows connected | your answer |

In the VM, `--lang de|ru` runs Tacit in German or Russian (a VPN there is a WireGuard stand-in with no server, which
shows the state the shell reads but not a provider's), and `--lived-in` updates a home lived in since earlier releases.
Run the protocol in the laptop's own language; say which in the note when it is not English.

The suites' VM steps (OBS, LibreOffice, VS Code, Zed, Steam and Discord got from Apps, the recording of a window not in
use, a call's microphone and screen share, and the rest) run in the VM with `tools/daily-bench <version> --suite all`.

## Rules

- Say what you saw, not what should happen: a step that half worked is a no, with a note.
- A number is taken on the same laptop each release, so releases can be compared. Name a new laptop in the note.
- Skip what you cannot do (no Bluetooth device, no game): a skipped step stays "needs a tester", never passed.
