# WizkTerm application

[WizkTerm](https://github.com/Wizk-Modz/termux-app) is an Android terminal
application and Linux environment, forked from
[Termux](https://github.com/termux/termux-app).

Fork specifics:

- App id `com.wizk`, so it installs alongside the official Termux app.
- Architecture `arm64-v8a` only, Android `>= 7`.
- Bootstrap and packages are built from source with `$PREFIX`
  `/data/data/com.wizk/files/usr`.
  Bootstrap zips are published from
  [Wizk-Modz/termux-packages](https://github.com/Wizk-Modz/termux-packages)
  and packages are served from the APT repository at
  `https://wizk-modz.github.io/wizk-apt-repo/`.
- The official Termux plugins (`Termux:API`, `Termux:Boot`, `Termux:Float`,
  `Termux:Styling`, `Termux:Tasker`, `Termux:Widget`) are **not** compatible
  with this fork (different package name and signing key).

Quick how-to about package management is available at
[Package Management](https://github.com/termux/termux-packages/wiki/Package-Management).

## Contents
- [Installation](#installation)
- [Debugging](#debugging)
- [For Maintainers and Contributors](#for-maintainers-and-contributors)
- [License](#license)
##



## Installation

WizkTerm APKs can be obtained from
[`GitHub Releases`](https://github.com/Wizk-Modz/termux-app/releases)
(listed under `Assets`) or from the `Artifacts` section of
[`GitHub Build Action`](https://github.com/Wizk-Modz/termux-app/actions/workflows/debug_build.yml?query=branch%3Amaster+event%3Apush)
workflows (requires logging into a `GitHub` account).

Only `arm64-v8a` (and the equivalent `universal`) APKs are released. The APK
and bootstrap installation size is `~120MB`.

Since the app id (`com.wizk`) differs from the official app (`com.termux`),
both apps can be installed on the same device, each with its own separate
`$HOME` and `$PREFIX`.

**Security warning**: APK files on GitHub are signed with a test key that is
shared publicly. Do not install WizkTerm builds obtained from anywhere except
https://github.com/Wizk-Modz/termux-app.
##



## Debugging

You can help debug problems by setting an appropriate `logcat` `Log Level`
in app settings -> `WizkTerm` -> `Debugging` -> `Log Level` (log level
`Verbose` logs additional information). Revert the log level to `Normal`
after debugging since private data may otherwise be passed to `logcat`.

Run the `logcat` command in the terminal to view the logs in realtime
(`Ctrl+c` to stop) or use `logcat -d > logcat.txt` to take a dump of the
log. You can also view the logs from a PC over `ADB`. For more information,
check the official Android `logcat` guide
[here](https://developer.android.com/studio/command-line/logcat).

Moreover, a `stat` info and `logcat` dump report can be generated with the
terminal's long hold options menu `More` -> `Report Issue` option and
selecting `YES` in the prompt shown to add debug info.

Post the complete report (optionally without sensitive info) when reporting
issues. Issues opened with **(partial) screenshots of error reports** instead
of text will likely be automatically closed/deleted.

##### Log Levels

- `Off` - Log nothing.
- `Normal` - Start logging error, warn and info messages and stacktraces.
- `Debug` - Start logging debug messages.
- `Verbose` - Start logging verbose messages.
##



## For Maintainers and Contributors

This fork follows the upstream Termux [contribution
guidelines](https://github.com/termux/termux-app#for-maintainers-and-contributors),
including the [Conventional
Commits](https://www.conventionalcommits.org) spec (`Added`, `Changed`,
`Deprecated`, `Removed`, `Fixed`, `Security`) for commit messages.

The `versionName` in `build.gradle` files must follow the [semantic version
`2.0.0` spec](https://semver.org/spec/v2.0.0.html) in the format
`major.minor.patch(-prerelease)(+buildmetadata)`.

Fork-specific build inputs:

- `TERMUX_PACKAGE_VARIANT` env (default `"apt-android-7"`) selects the
  bootstrap variant in `app/build.gradle`.
- `TERMUX_BOOTSTRAP_REPO` env (default `"termux/termux-packages"`) selects
  the GitHub repo whose releases the bootstrap zips are downloaded from.
  For official WizkTerm builds it is set to
  `"Wizk-Modz/termux-packages"`.
##



## License

This repository is released under the [GPLv3
only](https://www.gnu.org/licenses/gpl-3.0.html) license, same as upstream.
Check [LICENSE.md](LICENSE.md) for details, including exceptions for the
terminal libraries and the `termux-shared` library.

Upstream project: [termux/termux-app](https://github.com/termux/termux-app).
All credit for the original work goes to the Termux contributors.
