Container to build QMK
======================

This Dockerfile allows you to build the [QMK Firmware](https://qmk.fm/) and to flash it to a keyboard from an unprivileged container. This is useful is you cannot or do not want to install and run the build environment natively.

Build the container image
-------------------------

`$ docker build docker/ -t qmk-builder`

Create the keymap
-----------------

Instructions to create a custom keymap can be found in the [QMK documentation](https://beta.docs.qmk.fm/using-qmk/). Create a directory named after your keymap and add your custom code, such as the `keymap.c`, `rules.mk` and `config.h` files. Alternatively, modify the example for the [Moonlander keyboard](https://www.zsa.io/moonlander/) under `moonlander-helloworld`.

Build and flash the firmware with your keymap
---------------------------------------------

First of all, the `udev` rules for your keyboard must be installed on your system so that the keyboard can be flashed by an unprivileged user.

Once this is done, enter the bootloader mode on your keyboard so that it loads and flashes the new firmware over USB. On the Moonlander this is done by pressing the reset button.

Finally we call Docker to instanciate the container image build previously and pass it specific paramters. In the following example, the variables `KEYBOARD` and `KEYMAP` must match respectively the model of your keyboard as per QMK naming and the name of the keymap directory you created in the previous step. Moreover, the `--device` parameter to pass to Docker depends on the keyboard model. On the Moonlander, the SoC is a STM32 which is identified by udev so we pass `--device /dev/bus/usb/ --device /dev/stm32_dfu`.

```
$ KEYMAP=moonlander-helloworld
$ KEYBOARD=moonlander
$ docker run -it --rm \
	--device /dev/bus/usb/ \
	--device /dev/stm32_dfu \
	-v `pwd`/${KEYMAP}:/home/deb/qmk_firmware/keyboards/moonlander/keymaps/${KEYMAP} \
	qmk-builder \
	qmk flash -kb ${KEYBOARD} -km ${KEYMAP}
```
