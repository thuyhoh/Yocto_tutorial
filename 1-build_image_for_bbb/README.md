#  Build a Beaglebone Black image with the Yocto Project

``` bash
sudo apt-get -y install gawk wget git-core diffstat unzip texinfo gcc-multilib \
     build-essential chrpath socat cpio python3 python3-pip python3-pexpect \
     libsdl1.2-dev xterm make xsltproc docbook-utils fop dblatex xmlto lz4
```

``` bash
git clone -b scarthgap git://git.yoctoproject.org/poky/
cd poky
git clone -b scarthgap git://git.openembedded.org/meta-openembedded
git clone -b scarthgap git://git.yoctoproject.org/meta-ti
git clone -b scarthgap https://git.yoctoproject.org/meta-arm
```
``` bash
# ~/poky
source oe-init-build-env build-bbb
```

``` bash
nano ./build-bbb/conf/local.conf
# Change MACHINE ?= "beaglebone"
```

``` bash
nano ./build-bbb/conf/bblayers.conf
```

``` bash
# bblayers.conf
POKY_BBLAYERS_CONF_VERSION = "2"

BBPATH = "${TOPDIR}"
BBFILES ?= ""

BBLAYERS ?= " \
/home/zk47/Learning/poky/meta \
/home/zk47/Learning/poky/meta-poky \
/home/zk47/Learning/poky/meta-yocto-bsp \
/home/zk47/Learning/poky/meta-openembedded/meta-oe \
/home/zk47/Learning/poky/meta-arm/meta-arm-toolchain \
/home/zk47/Learning/poky/meta-arm/meta-arm \
/home/zk47/Learning/poky/meta-ti/meta-ti-bsp \
/home/zk47/Learning/poky/meta-ti/meta-ti-extras \
/home/zk47/Learning/poky/meta-ti/meta-beagle \
"
```

``` bash
bitbake core-image-minimal
```
- kiểm tra image 
``` bash
bitbake -e core-image-minimal | grep ^WORKDIR=
# /home/thuy/embedded/embedded_linux/yocto_project/poky/build-bbb/tmp/work/beaglebone-poky-linux-gnueabi/core-image-minimal/1.0
```
## Copy image sang sd-card
```
cd /home/thuy/embedded/embedded_linux/yocto_project/poky/build-bbb/tmp/work/beaglebone-poky-linux-gnueabi/core-image-minimal/1.0
cd deploy-core-image-minimal-image-complete
```
![image](imgs/)
- Kiểm tra sd-card
```
lsblk
```
- Tải dữ liệu vào sd-card
```
sudo bmaptool copy core-image-minimal-beaglebone.wic.xz /dev/sda
```
