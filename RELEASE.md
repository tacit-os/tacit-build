# How Tacit is made and released

The rules every change follows, and the steps every release takes, in order. `tools/release-check <version>` checks the
gates it can; the rest are written here so they are not skipped.

## Every change

1. **Commit in the repo the change belongs to, by path.** `git commit -- <paths>`, never `git commit -a`: other work
   lives uncommitted beside yours. Push the same day.
2. **Test it where it runs, without touching the owner's desktop.**
   - Shell QML: the live shell picks it up at once; check its log (`/run/user/$UID/quickshell/by-id/*/log.log`) for
     errors. Apps that run as their own process (Settings, Praxis, Graphis) load off-screen from a copy of the tree
     (`env -u DISPLAY QT_QPA_OFFSCREEN_NO_GLX=1 QT_QPA_PLATFORM=offscreen QT_QUICK_BACKEND=software qs -p <copy>/<app>.qml`).
   - Thyris: `tools/check-engine <groups>` (a private headless screen).
   - agent-host: `cargo test`; a test never opens anything on the desktop.
   - Scripts: `bash -n`, `python3 -m py_compile`, `luac -p`; edit a script that may be running by writing a copy and
     moving it over the original.
   - A bug: reproduce it first, then show the fix changes the result (the old code fails the same test).
3. **Works on the owner's machine is not works.** Installs have no `~/dev`, no `~/.local/bin` helpers and no hand-made
   links. Call Tacit's helpers through `$TACIT_BIN` (`Directories.tacitBin` in QML), the shell through
   `qs -p $TACIT_SHELL`, and ship every file a feature needs in a package.
4. **Say what the person sees.** Release notes, the notch and Settings speak in plain words: no package names, no
   commands.

Owner, 2026-11-12, after 1.2.14 shipped three fixes nobody had seen work (Thyris played no sound, the volume still
stopped at 99% on every updated computer, a three-finger swipe up sent the window to a half):

5. **A changed default needs a migration, and a test on an old settings file.** A value in a person's settings file
   wins over the default, so a new default reaches new installs only. Change one and `Config.migrate()` carries the
   files already out there (a new config version); the shell's `tests/run` runs `migrate()` on the file every past
   release left behind and fails while a setting stays at an old default.
6. **A fix is claimed only when someone has seen it work**, on a running system: the VM or a computer. Each release
   note says how in the release's `verified` in `tacit/notes.json`, by the note's text: `"vm: <check>"`, a check
   `tools/vm-smoke` passed; `"vm-hand: <what was seen, by whom>"`, a check done by hand in the VM; or
   `"hardware: <who saw it, on what>"`. `tools/release-check` lists any other note as needing a try on hardware, and
   it stays out of the notes until someone has.
7. **A gesture, sound, camera or microphone fix needs a check that does the thing**: on hardware, or a VM check that
   exercises it (one of `tools/vm-smoke`'s, a new one there, or one done by hand that does it). A screenshot is not one:
   1.2.14's round saw Thyris draw a page, and nobody played a sound.

## Version numbers

Owner, 2026-10-25: the numbers follow how a release reaches people, not how many there have been.

- **A fix between weekly releases** bumps the last number: 1.2 -> 1.2.1 -> 1.2.2. After .9 comes .10, never a rollover.
- **The weekly release** bumps the middle number: 1.2, 1.3, 1.4. It carries the release notes and the Discord post.
- **2.0** comes when its content is done (nothing broken, everything findable, one design language, Tacit's own
  foundations, Thyris complete, easy to try), whatever the middle number has reached by then. Never by count.
- The ISO keeps its dated name (2026.10.24.1).

## A release

1. **Gather.** Read Discord since the last release; every report is fixed, answered, or written down for later in
   the release's bug list.
2. **Pick the day of Arch.** `tools/arch-day` is what installs have now. A newer day is a candidate: build and test
   with `ARCH_MIRROR=https://archive.archlinux.org/repos/YYYY/MM/DD/$repo/os/$arch`. A day with another Hyprland needs
   tacit-boot and tacit-portal rebuilt on it (their plugins are built for one Hyprland and pin it), and one with another
   Python (3.14 to 3.15) needs tacit-shell rebuilt (its colour helpers' environment pins it), and one with another Qt
   needs tacit-qt6-declarative and quickshell rebuilt, or updates refuse; `tools/arch-day <day>` refuses a day without
   a version the published packages pin (Hyprland, Python, Qt, a library's soname).
3. **Pin.** Each PKGBUILD names the pushed commit or tag it ships; a version that changed gets a new `pkgver` or
   `pkgrel` (never reuse one, even unpublished: a test computer's cache keeps the old file). `tacit/notes.json` leads
   with the release and what changed in it; `tacit` depends on the new versions it needs.
4. **Build.** `tools/cloud-packages <recipes>` on the build machine, against that day.
5. **Test in the VM like a person.** A test repo (the live `tacit.db` plus the new packages), the mirror on the day:
   Settings > Check for updates, Restart, then the version in About, "What's new", and each note in it checked one by
   one, plus a sign-in, a page in Thyris, an app from Apps, and no errors in the shell's log. Record it:
   `tools/release-check <version> --vm-passed "what was checked"`. Then `tools/vm-smoke <version>`, on a VM with the
   release before installed: the update over a lived-in home, the plugins, the volume key to 100%, a sound out of
   Thyris, Settings, Praxis and Files without QML errors, and nothing new in the shell's log, each recorded pass or fail.
   Then, on the VM now on this release, Tacit Daily: `tools/daily-bench <version> --suite all` (the daily tasks, the
   speed and lightness numbers and the five workflow suites, against the release before), and before a weekly release
   `tools/daily-bench <version> --soak 8h` as well; `tools/hardware-daily` on a laptop for what the VM cannot do
   (HARDWARE-DAILY.md). On a VM with the release before installed (as for `tools/vm-smoke`),
   `tools/daily-bench <version> --lived-in --lang de` updates a home lived in since earlier releases and judges it
   (every 1.2.14 miss was of that kind); `--lang ru` runs it in a language whose letters are not Latin.
   Each part starts from the same saved state of the computer, and a check that could not be measured (the VM, a mirror,
   a site) is neither a pass nor a failure. On a new VM, and after a change to the bench, run it with `--repeat 3 --record
   tools/daily-bench-fixtures/<name>` first: a check that is not the same every time is unstable and is fixed before it
   counts, and the recording becomes tools/daily-bench-test's answers (commit it).
   Owner, 2026-11-12: it only reports for now; read `out/x86_64/daily-<version>.md` and write
   down what it flags. After 2-3 releases have set the normal spread (run the first one twice), it joins the gate in
   step 6: a daily task that fails, or a clear slowdown or memory growth past the margin, holds the release back.
6. **Gate.** `tools/release-check <version>` passes: a VM smoke of this version newer than its packages, every check
   passed, every note seen working. `tools/publish` runs it first and publishes nothing until it does.
7. **Publish.** `tools/publish <packages>`; then `tools/arch-day <day>` if the day moved; then
   `tools/publish-source <version>`.
8. **The ISO, with every release** (owner, 2026-10-29: people download the release they read about): `tools/iso`, a
   fresh install in the VM, upload under a new dated name, move the download's `LATEST`; the release notes page links
   that release's own ISO with its size and SHA256. `tools/iso` refuses a repo that does not hold this release's
   `tacit` and records the image's name, size and SHA256; `tools/release-check <version> --iso` must pass before step 9
   (the 1.2.7 image stayed on the site through 1.2.13, and every install started on bugs already fixed).
9. **Say it.** The site's release notes and install page; a post in Discord's #releases once the owner has read it.
