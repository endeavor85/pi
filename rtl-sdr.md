### GNU Radio

```sh
$ sudo apt install gnuradio
```

### `gr-osmosdr`
RTL-SDR block for GNU Radio

```sh
$ sudo apt install gr-osmosdr
```

### rtl-sdr
For tools like `rtl_fm`

See: http://osmocom.org/projects/sdr/wiki/Rtl-sdr

```sh
$ git clone git://git.osmocom.org/rtl-sdr.git
$ sudo apt install cmake
$ sudo apt install libusb

$ cd rtl-sdr/
$ mkdir build
$ cd build
$ cmake ../
$ make
$ sudo make install
$ sudo ldconfig
$ cd ../..
```

If you wish to run the `rtl-sdr` tools with a non-root account, you will need to give these accounts permission to access the RTL-SDR USB device.  This is done by adding a "rules" file to the `udev` (device manager).

Luckily, the `rtl-sdr` project comes with the rules file, we just need to copy it to the right place.

```sh
$ sudo cp rtl-sdr/rtl-sdr.rules /etc/udev/rules.d/20-rtl-sdr.rules
$ sudo service udev restart
```

By default, the `dvb_usb_rtl28xxu` kernel driver which comes will Raspbian claims the RTL-SDR USB device when you plug it in.  In order to use the dongle for ourselves, we need to prevent the `dvb_usb_rtl28xxu` kernel driver from claiming it.  This is done by "blacklisting" the driver.  Blacklisted modules are listed in files in the `/etc/modprobe.d/` directory.  If you are having problems with the `dvb_usb_rtl28xxu` module claiming the dongle, create a `*.conf` file in the `modprobe.d` directory with the contents `blacklist dvb_usb_rtl28xxu`, then reboot.

Reboot the system to apply blacklist changes (this may be necessary even if you didn't edit the blacklist modules).

```sh
$ sudo reboot
```

Test using `rtl_test`

```sh
$ rtl_test
Found 1 device(s):
  0:  Realtek, RTL2838UHIDIR, SN: 00000001

Using device 0: Generic RTL2832U OEM
Found Rafael Micro R820T tuner
Supported gain values (29): 0.0 0.9 1.4 2.7 3.7 7.7 8.7 12.5 14.4 15.7 16.6 19.7 20.7 22.9 25.4 28.0 29.7 32.8 33.8 36.4 37.2 38.6 40.2 42.1 43.4 43.9 44.5 48.0 49.6
Sampling at 2048000 S/s.

Info: This tool will continuously read from the device, and report if
samples get lost. If you observe no further output, everything is fine.

Reading samples in async mode...
```

Then `Ctrl-c` to stop the test.

```sh
^CSignal caught, exiting!

User cancel, exiting...
Samples per million lost (minimum): 0
```

Try some FM radio!

The Pi should automatically choose the audio output device, but sometimes it doesn't.  I was using HDMI output to a TV and had to force the Pi to use the HDMI audio output. See the [official instructions](https://www.raspberrypi.org/documentation/configuration/audio-config.md).

```sh
# 0 = auto
# 1 = 3.5mm headphone jack
# 2 = HDMI
$ amixer cset numid=3 2
```
