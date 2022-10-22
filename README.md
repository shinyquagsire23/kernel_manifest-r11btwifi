# Pixel Watch kernel manifest

### Dependency notes (Ubuntu, M1 Mac/ARM64 host):
```
# Specify existing sources as arm64
sed 's/^deb http/deb [arch=arm64] http/' -i '/etc/apt/sources.list'
```

Add to `/etc/apt/sources.list`:
```
# amd64 binfmt
deb [arch=amd64] http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse
deb [arch=amd64] http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse
deb [arch=amd64] http://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse
deb [arch=amd64] http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
```

```
sudo dpkg --add-architecture amd64
sudo apt-get update

# binfmt
sudo apt-get install -y --no-install-recommends \
    qemu qemu-system-misc qemu-user-static qemu-user binfmt-support

# build deps
sudo apt-get install gcc-x86-64-linux-gnu binutils-x86-64-linux-gnu libssl-dev:amd64 zlib1g-dev:amd64 libc6:amd64
```

### Building notes:
```
mkdir pixel_watch && cd pixel_watch

repo init -u git@github.com:shinyquagsire23/kernel_manifest-r11btwifi.git -b main
repo sync

build/build.sh
```

TODO: the rest of boot.img
