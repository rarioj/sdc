![](Thumbnail.png 'application-thumbnail')

# Simple DOSBox Client

「**SDC**」

> ❝ A lightweight DOSBox client in one shell script ❞
>

📌 ┃ Script Version: **1.0.23.5h** ┃ Type: **Shell Script** ┃ Shell: **POSIX Compliant** ┃ Interface: **CLI** ┃ License: **MIT** ┃ Library Version: **23.5h** ┃ Library Name: **Example Freeware** 

📦 ┃ **[DOSBox](https://www.dosbox.com/) 🟩** ┃ **[DOSBox Staging](https://dosbox-staging.github.io/) 🟩** ┃ **[DOSBox-X](https://dosbox-x.com/) 🟩** 

📎 ┃ Cover Arts: **[MobyGames](https://www.mobygames.com/)** ┃ Program Assets: **[Archive.org](https://archive.org/)** 

## What is *Simple DOSBox Client*?
Ever want to relive your past gaming experience, but your modern computer can no longer run it?

- *The good news is* — there is *DOSBox*. DOSBox is a free and open-source emulator which runs software for DOS-compatible disk operating systems.
- *The not-so-good thing is* — setting up programs in DOSBox is not that simple — you would be tinkering with hardware configuration, downloading floppy or CD-ROM images, mounting them, installing the program, executing DOS commands, and so on.

**Simple DOSBox Client (SDC)** aims to simplify these processes and, at the same time, manage your collection of DOS programs. All the actions needed for setting up a program in DOSBox, from downloading the asset files to finally running the program, can be organised into a single configuration file. You can compile all the configuration files into a collection of programs (library). **SDC** combines several utilities into a single shell script (the `Setup` script). It switches functionality based on the script's filename.

### `🎛️ Setup + 📚 Library.txt`
The `Setup` script is the only script you will ever need to start building your retro gaming system. It will copy itself into other script files according to their intended roles. It pairs up with the `Library.txt` configuration file in the root directory of your library to deliver all the program configuration files; generate all program, category, and library documents; and build the directory structure of your library.

### `🚀 Launch + 📓 Program.txt`
The `Launch` script and the `Program.txt` configuration file are the central core of a program. They are responsible for downloading assets, integrity checking, executing custom code, restoring from or loading a snapshot, generating a montage image of screen captures (located in the `System/capture` directory), and running the program. The `Launch` script will copy itself into other script files after the first execution:

- **`🪲 Debug`** — It launches DOSBox without running the `[autoexec]` section of the `Program.txt` configuration file. The debug console is a clean-slate DOSBox terminal, so manually mount hard-disk drives and floppy or CD-ROM images as needed.
- **`📷 Snapshot`** — It saves the entire content of the directory `System/drive` as a compressed file. Some programs require a snapshot of another program (e.g. certain games only run on *Windows 3.1x*).
- **`🗑️ Uninstall`** — It uninstalls the program by removing the generated `System` directory, `Debug` script, `Snapshot` script, and itself.

## Host Requirements
### DOSBox Variant
You require at least one variant (flavour) of DOSBox as the backend. Well-known **DOSBox** forks are **DOSBox Staging** and **DOSBox-X**. The script supports these three variants (the original and the two forks).

- `dosbox` 📎 ┃ [Homepage](https://www.dosbox.com/) ┃ [Wikipedia](https://en.wikipedia.org/wiki/DOSBox) ┃ [Source](https://sourceforge.net/projects/dosbox/) ┃ [Homebrew](https://formulae.brew.sh/formula/dosbox)
  - **DOSBox** is the de facto standard for running DOS games. It was first released in 2002 when DOS technology was becoming obsolete.
- `dosbox-staging` 📎 ┃ [Homepage](https://dosbox-staging.github.io/) ┃ [Source](https://github.com/dosbox-staging/dosbox-staging) ┃ [Homebrew](https://formulae.brew.sh/formula/dosbox-staging) ┃ [Snap](https://snapcraft.io/install/dosbox-staging/ubuntu)
  - **DOSBox Staging** aims to be a modern continuation of DOSBox, with better coding practices and more advanced features.
- `dosbox-x` 📎 ┃ [Homepage](https://dosbox-x.com/) ┃ [Source](https://github.com/joncampbell123/dosbox-x) ┃ [Homebrew](https://formulae.brew.sh/formula/dosbox-x) ┃ [Snap](https://snapcraft.io/install/dosbox-x/ubuntu)
  - **DOSBox-X** aims to be compatible with all pre-2000 DOS and Windows 9x-based hardware scenarios. It offers a screen capture functionality that works well with the montage image generation feature (requires **ImageMagick**).

If you have multiple DOSBox variants in the system, you can set the `SDC_DOSBOX` environment variable to enforce which DOSBox variant to use.
```shell
# shell profile
SDC_DOSBOX="dosbox-staging"
export SDC_DOSBOX

# direct invocation
SDC_DOSBOX="dosbox-x" ./Launch
```

### Recommended Tools (Optional)
- `imagemagick` 📎 ┃ [Homepage](https://imagemagick.org/) ┃ [Wikipedia](https://en.wikipedia.org/wiki/ImageMagick) ┃ [Source](https://github.com/imagemagick/imagemagick) ┃ [Homebrew](https://formulae.brew.sh/formula/imagemagick)
  - **ImageMagick** provides `mogrify` and `montage` commands. If installed, it will automatically generate a montage for all screen captures you made during the program run.
- `mdcat` 📎 ┃ [Source](https://github.com/swsnr/mdcat) ┃ [Homebrew](https://formulae.brew.sh/formula/mdcat)
  - **`mdcat`** renders markdown format on your terminal. Hence, it works best with a terminal emulator that supports graphics rendering (such as [iTerm2](https://iterm2.com/), [Kitty](https://sw.kovidgoyal.net/kitty/), or [WezTerm](https://wezfurlong.org/wezterm/)).
- `pandoc` 📎 ┃ [Homepage](https://pandoc.org/) ┃ [Wikipedia](https://en.wikipedia.org/wiki/Pandoc) ┃ [Source](https://hackage.haskell.org/package/pandoc) ┃ [Homebrew](https://formulae.brew.sh/formula/pandoc)
  - **Pandoc** allows converting markdown documents into HTML. You can browse the library/collection from a web browser.
- `pngquant` 📎 ┃ [Homepage](https://pngquant.org/) ┃ [Source](https://github.com/kornelski/pngquant) ┃ [Homebrew](https://formulae.brew.sh/formula/pngquant)
  - The **`pngquant`** tool is a command-line utility and a library for the lossy compression of PNG images.

## Getting Started
### The Example Library
It is not necessary to clone or download the whole repository. All you need is a [`Setup`](https://raw.githubusercontent.com/rarioj/sdc/main/Setup) script and a library configuration file. An example library file is available as [`Library.txt`](https://raw.githubusercontent.com/rarioj/sdc/main/Library.txt). It includes _**fifteen freeware games**_ ready to play. Steps to follow:

1. Create an empty library directory.
2. Download the `Library.txt` configuration file and the `Setup` script.
3. Make the `Setup` script executable.
4. Run the `Setup` script.

```shell
mkdir sdc-example
cd sdc-example
curl "https://raw.githubusercontent.com/rarioj/sdc/main/Library.txt" -o Library.txt
curl "https://raw.githubusercontent.com/rarioj/sdc/main/Setup" -o Setup
chmod a+x Setup
./Setup
```

5. Once the library is ready, go to the desired game directory.
6. Run the `Launch` script and enjoy the game.

```shell
cd "Games/By Genre/Adventure/Beneath a Steel Sky"
./Launch
```

### Setting Up a Library
If you have a `Library.txt` configuration file available, all you need is the `Setup` script:

1. Go to the directory where the `Library.txt` configuration file resides.
2. Download the `Setup` script.
3. Make the `Setup` script executable.
4. Run the `Setup` script.
5. Once the library is ready, go to the desired program directory.
6. Run the `Launch` script.

```shell
cd [path/to/library]
curl "https://raw.githubusercontent.com/rarioj/sdc/main/Setup" -o Setup
chmod a+x Setup
./Setup
cd [path/to/program]
./Launch
```

### Setting Up a Program (Without Library)
If you have a single `Program.txt` configuration file and want to run it without setting up the whole library, you can download the `Setup` script as `Launch`:

1. Go to the directory where the `Program.txt` configuration file resides.
2. Download the `Setup` script as `Launch` (use the `curl -o` option to rename the output).
3. Make the `Launch` script executable.
4. Run the `Launch` script.

```shell
cd [path/to/program]
curl "https://raw.githubusercontent.com/rarioj/sdc/main/Setup" -o Launch
chmod a+x Launch
./Launch
```

![](Montage.png 'Simple DOSBox Client')

> <table><tr><td width="50%">
>
> ### 🗄️ 6 Categories
> - 🗂️ [All Programs ‣ Games (15)](./All%20Programs/Games/README.md)
> - 🗂️ [Games ‣ By Genre ‣ Action (10)](./Games/By%20Genre/Action/README.md)
> - 🗂️ [Games ‣ By Genre ‣ Adventure (4)](./Games/By%20Genre/Adventure/README.md)
> - 🗂️ [Games ‣ By Genre ‣ Puzzle (2)](./Games/By%20Genre/Puzzle/README.md)
> - 🗂️ [Games ‣ By License ‣ Freeware (15)](./Games/By%20License/Freeware/README.md)
> - 🗂️ [Games ‣ By Platform ‣ DOS (15)](./Games/By%20Platform/DOS/README.md)
>
> </td><td width="50%">
>
> ### 📓 15 Programs
> 🔎 ┃ [Alien Carnage](./All%20Programs/Games/Alien%20Carnage/README.md) ┃ [Beneath a Steel Sky](./All%20Programs/Games/Beneath%20a%20Steel%20Sky/README.md) ┃ [Bio Menace](./All%20Programs/Games/Bio%20Menace/README.md) ┃ [Blackthorne](./All%20Programs/Games/Blackthorne/README.md) ┃ [Electroman](./All%20Programs/Games/Electroman/README.md) ┃ [Flight of the Amazon Queen](./All%20Programs/Games/Flight%20of%20the%20Amazon%20Queen/README.md) ┃ [God of Thunder](./All%20Programs/Games/God%20of%20Thunder/README.md) ┃ [Jetpack](./All%20Programs/Games/Jetpack/README.md) ┃ [Lure of the Temptress](./All%20Programs/Games/Lure%20of%20the%20Temptress/README.md) ┃ [One Must Fall 2097](./All%20Programs/Games/One%20Must%20Fall%202097/README.md) ┃ [Stargunner](./All%20Programs/Games/Stargunner/README.md) ┃ [Supaplex](./All%20Programs/Games/Supaplex/README.md) ┃ [Teen Agent](./All%20Programs/Games/Teen%20Agent/README.md) ┃ [The Lost Vikings](./All%20Programs/Games/The%20Lost%20Vikings/README.md) ┃ [Xargon](./All%20Programs/Games/Xargon/README.md) 
> </td></tr></table>

&nbsp;

