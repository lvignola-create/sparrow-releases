# Sparrow

Sparrow is a menu-bar app for the Mac. It shows the other Macs on your Tailscale network in Finder's sidebar and
moves files between them fast. Every file is checked end to end before Sparrow calls it delivered.

This page is where Sparrow's signed, notarized downloads live, and where installed copies look for updates.

- [Requirements](#requirements)
- [Install](#install)
- [Using Sparrow](#using-sparrow)
- [Updates](#updates)
- [Security and privacy](#security-and-privacy)
- [Uninstall](#uninstall)
- [Troubleshooting](#troubleshooting)
- [Versions](#versions)
- [About this repository](#about-this-repository)

## Requirements

- macOS 14 (Sonoma) or later, on Apple silicon or Intel.
- [Tailscale](https://tailscale.com/) installed and signed in on every Mac involved.
- Sparrow running on each Mac you want to reach. A Mac that isn't running Sparrow doesn't appear.

## Install

1. Open the [latest release](https://github.com/lvignola-create/sparrow-releases/releases/latest) and download
   `Sparrow-<version>.zip`.
2. Unzip it and move `Sparrow.app` to your Applications folder.
3. Open Sparrow. A sparrow appears in the menu bar. Sparrow opens at login by default; you can turn that off in
   its Settings.
4. Allow the Finder extension. macOS keeps a new Finder extension off until you allow it:
   - macOS 15 (Sequoia): System Settings > General > Login Items & Extensions > File Providers, then switch
     Sparrow on.
   - macOS 14 (Sonoma): System Settings > Privacy & Security > Extensions, then switch Sparrow on under the
     Finder or File Provider entries.
5. Check it worked. Open a Finder window: each other Mac running Sparrow on your Tailscale network is listed in
   the sidebar under Locations.

Sparrow is notarized by Apple, so it opens without a Gatekeeper warning.

## Using Sparrow

- **Browse.** Click a Mac in Finder's sidebar to see its files. There is no password prompt: Tailscale tells
  Sparrow who you are. Changes on the other Mac show up within a second or so.
- **Copy in and out.** Drag files into or out of a Sparrow location, or copy and paste, as with any disk.
  Dragging in moves the original, as it would into iCloud Drive; hold Option to copy instead. You can also open
  a file straight from the other Mac, edit it in place, rename, move and delete.
- **Sync tools.** Sync and backup tools that work with Finder locations can use Sparrow's locations as a
  source or a destination.
- **Delivered means verified.** A copy counts as done on the other Mac only after Sparrow has delivered it and
  checked it. That can be a moment after Finder says it is finished. Your Mac stays awake until then, and a
  copy that fails is reported in a notification that names the file.
- **The menu-bar panel.** Click the sparrow to see what is moving now, a live speed meter, a log of recent
  files, and each Mac and whether it can be reached. You can pause and resume transfers, set a speed limit, and
  open Settings from the panel's menu.
- **Quitting.** Quit Sparrow from its menu and the other Macs disappear from Finder until you open it again.
  Sparrow asks first if copies are unfinished.

## Updates

Sparrow updates itself, quietly:

- About two minutes after it opens, and every six hours after that, it checks this repository for a newer
  version.
- A newer version is downloaded in the background and verified.
- It installs only after a couple of minutes in which nothing is moving, then relaunches itself. It never
  interrupts a transfer, and you are not asked anything.

To see which version you have, open Sparrow's Settings; the version is shown there.

If a Mac stays on an old version, quit Sparrow and open it again, or install the latest release over it by
hand.

## Security and privacy

- Releases are signed with a Developer ID certificate and notarized by Apple.
- Every update is signed with an EdDSA key, and Sparrow checks that signature before installing anything. An
  update that doesn't verify is refused.
- Sparrow only listens on your Tailscale network. Nothing is exposed to the internet, and there is no Sparrow
  server or account.
- Tailscale identifies every request, so who can see what follows from it:
  - **The Mac's owner** (the same Tailscale user the Mac is signed in as) sees its mounted drives and its home
    folder.
  - **Everyone else** on the network sees only the folders that Mac shares in System Settings > General >
    Sharing > File Sharing. Read-only shares stay read-only.
- Sparrow does not keep copies of another Mac's files on your Mac beyond what you are using: copies are freed
  once they are safely on the other Mac or no longer in use.

## Uninstall

1. Quit Sparrow from its menu-bar menu.
2. Move `Sparrow.app` from Applications to the Trash. Its Finder locations and its login item go with it.
3. Optionally, remove what it leaves behind:
   - `~/Library/Application Support/Aspora`: its queue, history and settings.
   - `~/Library/Logs/Sparrow`: its log.
   - `~/Sparrow Inbox` (`~/Aspora Inbox` on Macs set up before October 2026): where files sent to your Mac arrive by default. Keep anything in there you still need.
   - In `~/Library/Group Containers`, the folder whose name ends in `.com.aspora`: Finder's records of the
     other Macs.
   - `~/Library/CloudStorage`: any `Sparrow-` folders that remain.

   Sparrow was called Aspora until October 2026, which is why some folders still carry that name.

## Troubleshooting

- **A Mac doesn't appear in Finder.** Check that Tailscale is running and signed in on both Macs, and that
  Sparrow is running on the other Mac. A Mac that is asleep or offline is hidden until it comes back.
- **No Macs appear at all.** The Finder extension is probably still off. Allow it as in step 4 of
  [Install](#install), then reopen Sparrow.
- **A Mac shows an older Sparrow.** The panel says "Update Sparrow on ..." when another Mac runs an older
  version. Open Sparrow on that Mac and it will update itself, or install the latest release there.
- **Updates don't arrive.** Updates wait for a quiet moment, so give a busy Mac some time. Make sure the Mac
  can reach github.com, then quit and reopen Sparrow to trigger a fresh check.

## Versions

Releases are numbered by date, `yyyy.MM.dd`. Two releases on the same day are told apart by the commit they
were built from. A release tag looks like `v2026.10.10-6bedb63`, and its download is
`Sparrow-2026.10.10-6bedb63.zip`.

Each release has two files: the app zip and `appcast.xml`, the update feed Sparrow reads. The newest release
is the one Sparrow offers to installed copies. An older release's zip is there for the record, not for
downgrading: Sparrow only moves forward, so installing an old zip over a newer app leaves that Mac behind and
it will update again by itself.

## About this repository

This repository holds the downloads and the update feed only: signed app zips and `appcast.xml`, as release
assets. Sparrow's source code is private.
