# bugswarm-renesas: 

A bugswarm connector for Renesas 8- and 16-bit microcontrollers.  This code turns a compatible evaluation board into a real-time internet enabled device.  Once the connector is deployed to a device, the device will automatically connect to the bugswarm platform and share it's peripherals using a standardized API.  This enables developers to create applications for the evaluation board in a wide variety of languages, without needing to download an SDK or physical access to the device.  

### Supported Boards

*  RL78/G13 Demonstration Kit (YRDKRL78G13) 
    *  Redpine companion WiFi Card (RS-RL78G13-2200CC)

### How to use an RL78/G13 board that has already been programmed

1. Set up a wireless access point, or Mifi tether with the SSID ```renesasdemo``` and password ```renesaspsk```.  The wireless security can be WPA1 or WPA2 Personal.  See the deployment instructions below to connect to a different ESSID.
1. (Optional) Connect a laptop or cellphone to this wireless access point, verify it can connect and verify that it has internet connectivity.
1. Make sure that Switch 2 of SW5 is set to the up or 'On' position.  [See the quick start guide](http://am.renesas.com/media/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrdkrl78g13/child_folder/YRDKRL78G13_Quick_Start_Guide.pdf) for more details.
1. Using a USB Micro cable, connect the RL78 board to a USB power source.  This can be a PC, Laptop, or USB wall charger.
1. The demo board will take several seconds to connect to the wireless access point.  When it has successfully connected, LED6 (the green led to the left of the LCD screen) will blink.
1. Navigate to [buglabs.github.com/bugswarm-renesas/](http://buglabs.github.com/bugswarm-renesas/)
1. Wait a few seconds and then click on the ```Select an RL78/G13 board to view" dropdown menu```
1. Select the entry that matches the MAC address printed on the Wifi Companion card, and hit ```Go!```
1. The graphs should update with data as it is sent by the RL78 board.

See the troubleshooting section below if board does not appear in the list, or data is not produced.


### How to Deploy the connector to an RL78/G13 demo board

1. Download and install the newest version of CubeSuite+ from [the following link](http://am.renesas.com/support/downloads/download_results/C1000000-C9999999/tools/evaluation_cubesuite_plus.jsp)
1. Open CubeSuite
1. Download the newest version of the bugswarm connecter [from this repository link](https://github.com/buglabs/bugswarm-renesas/zipball/master)
1. Extract the zip file to a reasonable location, like My Documents/CubeSuite/bugswarm-renesas/
1. Within CubeSuite, select ```File -> Open``` and navigate to ```bugswarm-renesas.Buglabs.mtud``` within the directory from the previous step.
1. In the pane on the left hand side of the application, double click on the file ```rsi_global.h``` within the ```redpine``` folder.  
1. The board is configured to connect to ESSID ```renesasdemo``` with password ```renesaspsk```.  If you would like to change these settings, modify the variables ```PSK```, ```SCAN_SSID```, and ```JOIN_SSID``` accordingly
1. Log in to [demo.bugswarm.com](http://demo.bugswarm.com)
1. Click on the New Resource button
1. Fill out the "Name" field with a unique value, such as the MAC address printed on the redpine companion card
1. Fill out the "Description" field with "RL78/G13 Demonstration Board"
1. Click on "Create"
1. Click on the "My Swarms" tab.
1. Select the "Renesas Demo" swarm.
1. Click the "Edit" button.
1. Find the resource that was created previously in the right hand side of the screen, and click on the grey "producer" button (do NOT select the "consumer" button).
1. Click on the "Update" button.
1. In the next screen, find the resource we just created and copy the text next to the ```ID:``` label.
1. In the CubeSuite IDE, double click on the file ```r_main.c``` within the ```gen``` folder.
1. Replace the text immediately following ```const char resource_id[] = ``` with the ID copied from the bugswarm webpage, similarly in quotes.
1. Connect the Redpine Wifi Card to the App header slot on the RL78/G13 board ([See this Diagram](http://am.renesas.com/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrdkrl78g13/sub/layout_child.jsp)).  The components on the wifi card should be facing inwards.
1. On the RL78G13 demo board, make sure that switch 2 on SW5 is in the downward (or 'Off') position.  [See the quick start guide](http://am.renesas.com/media/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrdkrl78g13/child_folder/YRDKRL78G13_Quick_Start_Guide.pdf) for more details.
1. Connect the RL78G13 demo board to the PC using a USB cable
1. Within CubeSuite, press the <F6> button.  The project should compile and deploy to the demo board.
1. When the download has completed, the screen should change and should highlight a single line in ```r_main.c``` in yellow.  When this happens, press the <F5> key.
1. The application should start running.

### Troubleshooting

If the RL78 demonstration board does not appear or remain online, you will need to connect to a serial console on the demo board.  

1. [Obtain an RS232 to USB converter](http://www.amazon.com/s/ref=nb_sb_noss_1?url=search-alias%3Daps&field-keywords=RS232+USB)
1. Connect the RS232 adapter to the RS232 port on the RL78 demontration board, and into a computer or laptop.
1. Open a serial terminal emulator like HyperTerm or Putty and connect to the USB-Serial port.  Use Baud rate 115200, 8 bits, no parity, 1 stop bit, and no hardware flow control.  Here is [an example tutorial](http://www.laser-interceptorusa.com/DownloadFiles/rs232_to_usb_problem_solving.pdf)
1. Press the ```Reset``` button on the RL78 demo board, and observe the serial output
1. Reproduce the error, and copy/paste all of the relevant serial output into [pastebin.com](http://pastebin.com/).  press "Submit".
1. Contact [buglabs support](http://www.buglabs.net/support), and provide the URL of the pastebin website.

### Relevant Documentation

* [bugswarm API documentation](http://developer.bugswarm.net/)
* [bugswarm javascript library](https://github.com/buglabs/bugswarm-js)
* [bugswarm preliminary configuration interface](http://demo.bugswarm.com/)
* [Redpine Signals Companion Card resources](http://www.redpinesignals.com/Renesas/Wi-Fi_with%20_RL78.html)
* [Renesas RL78G13 Demo Kit resources](http://am.renesas.com/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrdkrl78g13/index.jsp)
* [YRDKRL78G13 Quick Start Guide (how to install the SDK)](http://am.renesas.com/media/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrdkrl78g13/child_folder/YRDKRL78G13_Quick_Start_Guide.pdf)
* [YRDKRL78G13 Getting Started DVD](http://am.renesas.com/media/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrdkrl78g13/child_folder/YRDKRL78G13_DVD10.zip)
* [RL78G13 CPU Hardware Manual](http://documentation.renesas.com/doc/products/mpumcu/doc/rl78/r01uh0146ej0200_rl78g13.pdf)
* Further redpine documenation only available by contacting redpine suppport.

