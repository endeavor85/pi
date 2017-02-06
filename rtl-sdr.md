### GNU Radio

```sh
sudo apt install gnuradio
```

### `gr-osmosdr`
RTL-SDR block for GNU Radio

```sh
sudo apt install gr-osmosdr
```

### rtl-sdr
For tools like `rtl_fm`

See: http://osmocom.org/projects/sdr/wiki/Rtl-sdr

```sh

git clone git://git.osmocom.org/rtl-sdr.git
sudo apt install cmake
sudo apt install libusb

cd rtl-sdr/
mkdir build
cd build
cmake ../
make
sudo make install
sudo ldconfig
cd ../..
```

If you wish to run the `rtl-sdr` tools with a non-root account, you will need to give these accounts permission to access the RTL-SDR USB device.  This is done by adding a "rules" file to the `udev` (device manager).

Luckily, the `rtl-sdr` project comes with the rules file, we just need to copy it to the right place.

```sh
sudo cp rtl-sdr/rtl-sdr.rules /etc/udev/rules.d/20-rtl-sdr.rules
sudo service udev restart
```
