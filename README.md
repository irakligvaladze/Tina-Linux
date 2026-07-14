# Tina-Linux

Tina-Linux for T113/D1-H/D1s

### Ubuntu environment

```sh
sudo apt-get install build-essential subversion git-core libncurses5-dev \
zlib1g-dev gawk flex quilt libssl-dev xsltproc libxml-parser-perl \
mercurial bzr ecj cvs unzip lib32z1 lib32z1-dev lib32stdc++6 \
libstdc++6 libmpc-dev libgmp-dev -y
```

### SDK download from GitHub

```sh
git clone --recursive https://github.com/irakligvaladze/Tina-Linux.git
cd Tina-Linux

# If you didn't clone with --recursive
git submodule update --init --recursive

# Download required build dependencies
RELEASE_URL="https://github.com/irakligvaladze/Tina-Linux/releases/download/dependencies-v1"

# Prebuilt files
wget -c "$RELEASE_URL/prebuilt.tar.gz"
tar xzvf prebuilt.tar.gz

# Download split dl archive
wget -c "$RELEASE_URL/dl.tar.part-00"
wget -c "$RELEASE_URL/dl.tar.part-01"

# Reassemble and extract
cat dl.tar.part-* > dl.tar
tar xvf dl.tar

# Toolchains
mkdir -p ./lichee/brandy-2.0/tools/toolchain/

wget -c \
"$RELEASE_URL/riscv64-linux-x86_64-20200528.tar.xz" \
-P ./lichee/brandy-2.0/tools/toolchain/

wget -c \
"$RELEASE_URL/gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabi.tar.xz" \
-P ./lichee/brandy-2.0/tools/toolchain/

# Optional cleanup
rm -f prebuilt.tar.gz dl.tar dl.tar.part-*
```

### Compile

```sh
source build/envsetup.sh
lunch
```

```
You're building on Linux

Lunch menu... pick a combo:
    1. d1_mq_pro-tina
    2. d1_nezha_min-tina
    3. d1_nezha-tina
    4. f133_evb1-tina
    5. f133_mq_r-tina
    6. t113_evb1-tina
    7. t113_mq_r-tina
```

```sh
# Select your target (for example: 1, 5, or 7)

make
mboot
pack

# Output image:
Tina-Linux/out/d1-mq_pro/tina_d1-mq_pro_uart0.img
```

### Flash to TF-Card

Use PhoenixCard to flash the generated image.

More information:

* PhoenixCard: https://mangopi.cc/_media/phoenixcard4.2.8.zip
* MangoPi documentation: https://mangopi.cc/d1
