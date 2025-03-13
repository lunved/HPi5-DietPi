# HackberryPi5 - Kali on SSD 

This is the hardware I used:

<img src="https://m.media-amazon.com/images/I/61gL8zmcDIL._AC_SL1500_.jpg" width="200" />

[Waveshare PCIe to M.2 Adapter Board (E) For Raspberry Pi 5, With Cooling Fan, Compatible With 2242/2230 NVMe Protocol M.2 Solid State Drive, 8Gbps Data Rate, High-Speed Reading/Writing, Pi 5 NVMe](https://www.amazon.it/dp/B0DBZ6PWF6)

<img src="https://m.media-amazon.com/images/I/613+hkU87eL._AC_SL1500_.jpg" width="200" />

[Waveshare SK M2 NVME 2242 256GB Solid State Drive, 3D TLC Flash Memory, High-Speed Reading/Writing Compatible With Windows/Raspberry Pi OS/CentOS/Ubuntu/Linux](https://www.amazon.it/dp/B0D5CJPKN9)

<img src="https://m.media-amazon.com/images/I/71NHG5ox2cL._AC_SL1500_.jpg" width="200" />

[ELUTENG M.2 NVMe to USB Adapter, USB 3.1 Card 10Gbit/s, USB to M.2 NVMe SSD Card Reader USB SSD Adapter 10Gbps for M Key SSD Support M.2 2230 2242 2260 2280](https://www.amazon.it/dp/B0CB7MGWGQ)


## Summary
1. Check RPi5 EProm settings and change EProm to enable boot from SSD
2. Install NVMe Hat and SSD

## 1. Check RPi5 EProm Settings
1. Using the Raspberry Pi Imager install Raspberry PI OS (64Bit) onto a 32Gb SD card.  
2. If you are using this on the HackberryPi5 then remember to add ONLY the following line to the /boot/config.txt file on your SD card.
```
dtoverlay=vc4-kms-dpi-hyperpixel4sq
```
3. Next follow the steps from [here](https://community.volumio.com/t/guide-prepare-raspberry-pi-for-boot-from-usb-nvme/65700). The next steps are a summary of what I did.

 - 3.1 Boot from the SD Card into Raspberry Pi OS
  
  - 3.2 Checked EEProm version `vcgencmd bootloader_version`

  - 3.3 Edit this file /etc/default/rpi-eeprom-update
    
```
sudo nano /etc/default/rpi-eeprom-update
```
	Changed 
        FIRMWARE_RELEASE_STATUS="default" 
	- to - 
		FIRMWARE_RELEASE_STATUS="latest" 

  - 3.4 Run `sudo rpi-eeprom-update -a`
    - Reboot

4. Check Boot order by running this `sudo rpi-eeprom-config`
	
- Mine already had a boot order of 
`
BOOT_ORDER=0xf461
`
	
5. Next I had to add "PCIE_PROBE=1" to the bottom of the file on screen.
```
sudo -E rpi-eeprom-config --edit
```
It should liike this:

<img src="https://community.volumio.com/uploads/default/original/3X/6/9/69b2c14bd2a62d777153b4c2e4e5f6a81fcab272.png" width="500">

6. Save your changes (Ctrl-O) and exit (Ctrl-X)
7. Reboot

## 2. Install Hat and SSD into HPi5
This is what mine looks like

<img src="https://github.com/lunved/HPi5/blob/main/images/NVMe%20hat%20and%20SSD.jpg" width="500">



