# This is application development  ----- by Huy Nguyen

*This application offers a possibility to turn a Raspherry Pi as a sound
device. The application comes with 2 functions: a sound collector and a test tone generator.

# List of Content
   1. Congfiguration Instruction
   2. Installation Instruction
   3. Operating Instructions
   4. List of Files
   5. Copyright / CopyLeft
   6. Contact Info.
   7.Credits and Acknowlegements


#1. Configuration Instruction
  * 1.1 All the devices needed
     16GB microSD card 
     Raspherry Pi
     USB sound card
     Microphone
  * 1.2. Configure USB sound as a default audio device
     * 1.RPi onboard sound card does not have microphone interface, so we need to change the default audio device to USB sound card
     * 2.Boot up RPi, and apply the USB sound card. Use "lsusb" command to check if your USB sound card is mounted:
```
        pi@raspberrypi:~ $ lsusb
        Bus 001 Device 004: ID 0d8c:000c C-Media Electronics, Inc. Audio Adapter
        Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter
        Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp.
        Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

     * 3.Use "sudo nano /etc/asound.conf" command and put following content to the file:
```
        pcm.!default {
          type plug
          slave {
             pcm "hw:1,0"
          }
        }
        ctl.!default {
            type hw
            card 1
        }
```
     * 4.Go to your home directory. Use "nano .asoundrc" command and put the same content to the file.
     * 5.Run "alsamixer" you should be able to see that USB sound card is the default audio device. For a more sensitive sound detection, it is better to maximize the volume of "Mic".
  * 1.3. Install Libcurl library
     * 1.First use command "ls /usr/include/curl" or "ls /usr/include/arm-linux-gnueabihf/curl" to identify that libcurl library is installed.
     * 2.If the folder doesn.t exist. Run "sudo apt-get update" to update the application list
     * 3.Run "sudo apt-get install libcurl3" to install the libcurl3.
     * 4.Run "sudo apt-get install libcurl4-openssl-dev" to install the development API of libcurl4

#2. Installation Instruction
  * In your installation directory, use "make" command to create executable file, which is file "sound.out"
  * Now sound.out should be in the same directory

#3. Operating Instructions
  * Use command "/.sound.out" without argument to see a decibel barchart of captured sound throught microphone
  * Press "Ctrl"+"c" to stop program
  * Use command "/.sound.out arg" to generate a testTone.wav  and put specified options
  * Use command "make clean" to delete all the executable file.

#4. List of files
  * README.md : contains short infomation of this application and how to use it
  * comm.c and comm.h: connect to the server and send the data to server
  * main.c: contains the functions which is used for readind the input and open "test.wav" file, call fuctions to display barchart
  * makefile: to generate some simple command to run and clean the apllication
  * screen.c and screen.h: contains the fuctions which generates the bartchart and set its color
  * sound.c and sound.h:  cotains the fuctions use for processing the sound recieved ( such as calculating pieces and peak of wave ) and generate the tone.
  * sound.php: this php file recieves the data from appllication and write all the data in a text file.
  * testcurl.c: contains the fucntions which test the curl library by sending some infomation to server

#5. Copyright / Copyleft
  * Coppyright 2019: All the source code were written  by Huy Nguyen
  * Coppyleft 2019: This application is done under the instruction of Mr. Gao Chao (teacher in Vaasa University of applied sciences)

#6. Contact Infomation 
  * Name:  Huy Nguyen
  * Email: ng.huy0708@gmail.com
  * Phone number: 046 547 1125

#7. Credits and Acknowledgements
  * Huy Nguyen- application developer
  * Mr. Gao Chao- the instructor.

## NOTE:
   Because I had some problems in setting USB sound card as Default, so I had to reomved all file in my SD card and installed it again.    
