# Kodi Flatpak

Kodi is an award-winning free and open source software media player and
entertainment hub for digital media. Available as a native application for
Android, Linux, BSD, macOS, iOS, tvOS and Windows operating systems, Kodi runs
on most common processor architectures. This repository packages it through
Flatpak.

## Building

You'll need almost all of an 8GB machine, so dont use memory up with the desktop before you do the build. A 16GB or more SBC is recommended.

```
flatpak-builder build-dir --user --ccache --force-clean --install ozacas.kodi.Kodi.yml
```

Then you can run it via the command line:

```
flatpak run ozacas.kodi.Kodi
```

or just search for the installed app on your system

## Exclusions

A lot of the pvr addons dont build as they depend on inputstream.ffmpegdirect, which doesnt build right now.
If anyone can take a look, that would be great! In addition:

- `audiodecoder.dumb`
- `game.libretro.2048`
dont build

## Contributing

The list of binary addons in each branch of Kodi may be found
[here](https://github.com/xbmc/repo-binary-addons/), and dependencies
[here](https://github.com/xbmc/xbmc/tree/master/tools/depends/target). Kodi
releases are found [here](https://github.com/xbmc/xbmc/releases).

You need to have the `PyGithub` Python module installed, to run the update script:

```sh
pip install PyGithub
```

`make update-addons` can help updating existing addons and also list missing ones. It will need a `GITHUB_TOKEN` environment variable set to a valid GitHub token. You can do this via an `.env` file in the root of the repository or by exporting the variable in your shell.

You can contribute by updating addons, modules and the Kodi version.
