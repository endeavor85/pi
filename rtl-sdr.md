```sh
sudo apt install gnuradio
sudo apt install gr-osmosdr

# rtl-sdr tools (like rtl_fm)
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
```
