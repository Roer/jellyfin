Jellyfin
============

Jellyfin is a personal media server. The Jellyfin project was started as a result of Emby's decision to take their code closed-source, as well as various philosophical differences with the core developers. Jellyfin seeks to be the free software alternative to Emby and Plex to provide media management and streaming from a dedicated server to end-user devices.

Jellyfin is descended from Emby 3.5.2, ported to the .NET Core framework, and aims to contain build facilities for every platform.

For further details, please see [our wiki](https://github.com/jellyfin/jellyfin/wiki). To receive the latest project updates feel free to join [our public chat on Matrix/Riot](https://matrix.to/#/#jellyfin:matrix.org) and to subscribe to [our subreddit](https://www.reddit.com/r/jellyfin/).

## Feature Requests

While our first priority is a stable build, we will eventually add features that were missing in Emby or were not well implemented (technically or philosophically).

[Feature Requests](http://feathub.com/jellyfin/jellyfin)

## Contributing to Jellyfin

If you're interested in contributing, please see [our wiki for guidelines](https://github.com/jellyfin/jellyfin/wiki/Contributing-to-Jellyfin).

## Prebuilt Jellyfin packages

Prebuild packages are available for Debian/Ubuntu and Arch, and via Docker Hub.

### Docker

The Jellyfin Docker image is available on Docker Hub at https://hub.docker.com/r/jellyfin/jellyfin/

### Arch

The Jellyfin package is in the AUR at https://aur.archlinux.org/packages/jellyfin-git/

### Unraid

An Unraid Docker template is available. See [this documentation page](https://github.com/jellyfin/jellyfin/blob/master/unRaid/docker-templates/README.md) for details on installing it.

### Debian/Ubuntu

A package repository is available at https://repo.jellyfin.org.

NOTE: Ubuntu users may find that the `ffmpeg` dependency package is not present in their release or is simply a rebranded `libav` which is not directly compatible. Please [obtain the ffmpeg package directly from the FFMPEG site](https://ffmpeg.org/download.html#build-linux) to use Jellyfin on Ubuntu.

For instructions on using the repository, please see [our wiki](https://github.com/jellyfin/jellyfin/wiki/Jellyfin-Debian-repository).

## Building Jellyfin packages from source

Jellyfin seeks to integrate build facilities for any desired packaging format. Instructions for the various formats can be found below.

NOTE: When building from source, only cloning the full Git repository is supported, rather than using a `.zip`/`.tar` archive, in order to support submodules.

### Debian/Ubuntu

Debian build facilities are integrated into the repo at `debian/`.

0. Install the `dotnet-sdk-2.2` package via [Microsoft's repositories](https://dotnet.microsoft.com/download/dotnet-core/2.2).
0. Run `dpkg-buildpackage -us -uc`.
0. Install the resulting `jellyfin_*.deb` file on your system.

A huge thanks to Carlos Hernandez who created the original Debian build configuration for Emby 3.1.1.

### Windows (64 bit)

A pre-built windows installer will be available soon. Until then it isn't too hard to install Jellyfin from Source.

0. Install the dotnet core SDK 2.2 from [Microsoft's Webpage](https://dotnet.microsoft.com/download/dotnet-core/2.2) and [install Git for Windows](https://gitforwindows.org/)
0. Clone Jellyfin into a directory of your choice.
    ```
    git clone https://github.com/jellyfin/jellyfin.git C:\Jellyfin
    ```
0. From the Jellyfin directory you can use our Jellyfin build script. Call `Build-Jellyfin.ps1 -InstallFFMPEG` from inside the directory in a powershell window. Make sure you've set your executionpolicy to unrestricted.

    Additional flags:
      * If you want to optimize for your environment you can use the `-WindowsVersion` and `-Architecture` flags to do so; the default is generic Windows x64.
      * The `-InstallLocation` flag lets you select where the compiled binaries go; the default is `$Env:AppData\JellyFin-Server\` .
      * The `-InstallFFMPEG` flag will automatically pull the stable ffmpeg binaries appropriate to your architecture (x86/x64 only for now) from [Zeranoe](https://ffmpeg.zeranoe.com/builds/) and place them in your Jellyfin directory. 
0. (Optional) Use [NSSM](https://nssm.cc/) to configure JellyFin to run as a service
0. Jellyfin is now available in the default directory (or the directory you chose). Assuming you kept the default directory, to start it from a Powershell window, run, `&"$env:APPDATA\Jellyfin-Server\EmbyServer.exe"`. To start it from CMD, run, `%APPDATA%\Jellyfin-Server\EmbyServer.exe`
