# angband

The best game ever.

Home is still at [rephial.org](https://rephial.org/),
and I'm still on the [ladder](http://angband.oook.cz/ladder-show.php?id=2010).
Also, I [once](./Mpiper-with-One-Ring) found the One Ring.

## installation

I have been installing angband through [Homebrew](https://brew.sh),
but version 4.2.5 didn't work.
Instead, I built it from source,
taking cues from the [brew formula](https://github.com/Homebrew/homebrew-core/blob/79d7174a8c777bdedd60991b497bb26f4db55b55/Formula/angband.rb) for angband 4.2.4.

Downloaded the angband 4.2.4 [tarball](https://github.com/angband/angband/releases/download/4.2.4/Angband-4.2.4.tar.gz) from GitHub and unpacked it.
```bash
cd ~/scratch
wget https://github.com/angband/angband/releases/download/4.2.5/Angband-4.2.4.tar.gz
tar -xf Angband-4.2.5.tar.gz
cd Angband-4.2.4
```

The brew formula recommends building against the macOS *ncurses*,
located at `/Library/Developer/CommandLineTools/SDKs/MacOSX14.sdk/usr`,
but it failed to compile.

Instead, I built against the Homebrew *ncurses*:
```bash
export NCURSES_DIR=/usr/local/opt/ncurses
export NCURSES_CONFIG=$NCURSES_DIR/bin/ncurses6-config
export LDFLAGS="-L$NCURSES_DIR/lib"
export CPPFLAGS="-I$NCURSES_DIR/include"
```

From the `Angband-4.2.4` directory,
configure, make, and install:
```bash
./configure --prefix=$HOME/local
make
make install
```

Link the angband executable into the `~/bin` directory (which is in the path):
```bash
cd ~/bin && ln -s $HOME/local/games/angband
```

It doesn't work quite as well as the brew version;
e.g., I have to select the `NumLock` key every time I start angband,
but it works well otherwise.

## usage

The user directory is

    ~/.angband/Angband

I also have scripts,
`angband_backup` and `angband_restore`,
to cache and load my current game file.

### iTerm2 and xterm

angband doesn't render correctly in iTerm2.
Use an xterm instead:

    xterm -fa Monaco:size=18 -rv &

See available fonts:

    fc-list | cut -f2 -d: | sort -u

Or use Terminal, which works fine.
