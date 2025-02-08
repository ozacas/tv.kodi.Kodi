# Kodi Flatpak

Kodi is an award-winning free and open source software media player and
entertainment hub for digital media. Available as a native application for
Android, Linux, BSD, macOS, iOS, tvOS and Windows operating systems, Kodi runs
on most common processor architectures. This repository packages it through
Flatpak.

## WARNING WARNING WARNING

This build is experimental - use at own risk. Works for me on NanoPC T6 with 8GB RAM
It does not have high quality flatpak development, just a gross hack to get ffmpeg 7.x working
with kodi Omega and rockchip GPU support. Seems to be OK.... just a starting point for further work 

This build is not present on flathub, as it is not official, and not supported in any way.

## Building

You'll need almost all of an 8GB machine, so dont use memory up with the desktop before you do the build. A 16GB or more SBC is recommended.

```
flathub install org.freedesktop.Platform//24.08  # if not already installed
flathub install org.freedesktop.Sdk//24.08       # ditto
flathub install org.freedesktop.Sdk.Extension.openjdk17//24.08 # ditto
flatpak build-init build-dir ozacas.kodi.Kodi org.freedesktop.Sdk//24.08 org.freedesktop.Platform//24.08  # if not already done
flatpak-builder build-dir --user --ccache --force-clean --install ozacas.kodi.Kodi.yml
```

Then you can run it via the command line:

```
flatpak run ozacas.kodi.Kodi
```

or just search for the installed app on your system. Dont forget to migrate your library files from `~/.var/app/tv.kodi.Kodi` to
`~/.var/app/ozacas.kodi.Kodi`

## Exclusions

I purged a few plugins before I realised that there is an unofficial branch for ffmpeg 7.x support, which
is kinda broken... needs fixing one day!

If anyone can take a look, that would be great! In addition:

- `audiodecoder.dumb`
- `game.libretro.2048`

do not build

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
