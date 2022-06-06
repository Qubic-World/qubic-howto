# Table of Contents

> 1. [Qubic a quorum-based computations protocol](#qubic-protocol)
> 2. [Hardware Requirements](#hardware-requirements)
> 3. [Software Requirements](#software-requirements)
> 4. [The steps we will take to achieve a successful running efi application](#steps)
> 5. [Before we start read very carefully](#before-start)
> 6. [Preparing motherboard and bios settings](#preparing-motherboard)
> 7. [Code modifications](#code)
>    1. [Seeds](#code-seeds)
>    2. [Browser](#code-browser)
> 8. [Preparing an USB stick to run Qubic](#preparing-usb)
>   1. [Set writing privileges with DISK PART](#disk-part)

---
   



<a name="qubic-protocol"></a>
# Qubic a quorum-based computations protocol.

In this tutorial we'll setup a [Qomputor](https://www.computors.org/computing/qomputor "Qomputor") Node (A mining node will maybe require an other approach), we try to make this tutorial as easy as possible but some knowledge of computer systems is definitely required. This tutorial is a community initiative. For more information or questions join [Syzygy Discord ](https://discord.gg/2vDMR8m "Syzygy Discord").

Qubic software is running on baremetal machines without any OS installed, the software is a so called UEFI application and for security reasons we compile it ourselves with the .cpp files provided by [Come-from-Beyond](https://twitter.com/c___f___b "Twitter"). The latest releases will always be on [Syzygy Discord ](https://discord.gg/2vDMR8m "Syzygy Discord").

Because we use a UEFI application, the successful use of the software is very dependent on the system that is used. Here are some examples of motherboard/cpu combinations that have been tested and which are working successfully.

| Motherboard        | CPU         | RAM  | Connection |
| ------------------ |:-----------:| ----:| -------:   |
| MSI B450-A PRO MAX | Ryzen 3950x | 64GB | 1gbps      |

For now, the exact conditions for a successful system are not yet available. 

<a name="hardware-requirements"></a>
# Hardware Requirements
* Highend CPU
* Motherboard which accept UEFI software (disable secure boot)
* 64GB Ram
* 1GBps internet connection
* 128GB USB Stick

<a name="software-requirements"></a>
# Software Requirements
* Qubic.cpp file
* [Visual Studio Code Community 2022](https://visualstudio.microsoft.com/vs)
* [Rufus](https://rufus.ie)

<a name="steps"></a>
# The steps we will take to achieve a successful running efi application

1. Prepare motherboard/bios settings
3. Compiling Qubic
4. Prepare USB
5. Run

<a name="before-start"></a>
# Before we start read very carefully.
As a community or as an individual, we are in no way responsible for losing passwords or losing money. We assume that self-research is being done and that the common sense of an individual does its job. No rights can be obtained from its contents, nor is it meant as personal or professional advice. Also check if this info is up to date or even outdated.

<a name="preparing-motherboard"></a>
# Preparing motherboard and bios settings 
Since every motherboard is different, it is advisable to consult the manual if you cannot find certain settings. There are a number of important things that need to be set up.

1. Make sure motherboard can run or boot with UEFI
2. Disable secure boot
3. Change boot order to USB (uefi)
4. Set time to UTC TIME +0
5. Make sure network stack is available (if not then maybe you need to install drivers, we'll be covering this later and its yet not described in this tutorial)

<a name="compiling"></a>
# Compiling Qubic with Visual Studio Code Community 2022

1. Install Visual Studio Code Community 2022, while installing make sure the Desktop Development with C++ components are installed. If you already had installed Visual Studio Code you install the components at Tools >> Get Tools and Features.

![alt text](sreenshots/qubic1.png)

2. When we start Visual Studio we need to create a new project make sure you use the following settings.

![alt text](sreenshots/qubic2.png)

![alt text](sreenshots/qubic3.png)

3. Give the project a name

![alt text](sreenshots/qubic4.png)

4. When the project file is succesfully made and opened we are going to add the latest .cpp file from our [Discord Server](https://discord.gg/2vDMR8m "Syzygy Discord"). ( they are in the #qubic channel in the pinnend messages.)

![alt text](sreenshots/qubic5.png)

5. When downloaded load it in the project.

![alt text](sreenshots/qubic6.png)

![alt text](sreenshots/qubic7.png)

6. When the file is imported we are going to setup our personal settings.

![alt text](sreenshots/qubic8.png)

At number 1 we're specifying how many cores or threads should be mining (in the end Computor Nodes will do other tasks, before that we'll need 676 computors), read you manual from cpu to check. For now best results are (total threads - 3 threads, but its also machine dependent so play with it, some systems its better to do cores - 2), for now we leave computing threads as 1.

At number 2 we need to specify our secret [seeds](#code-seeds), '''make a 55 lowercase password and share it with no one anytime''' you are responsible for your own password and no one else. Write it down save it somewhere where noboby can find it, dont loose it.. We cant say this enough.

At number 3 we're going to setup our router settings (log in to your router to see if settings are matching, when you wanna run a public node make sure you forwarding port 21841 en disabling firewall settings and check if port is open. Enter the values as they are in your router also dont forget to specify public IP its necessary your're having a static IP address as a computor.

At number 4 we specify our COMPUTOR ID (its generated automatically when your're log in with earlier generated seed on the web client, its also provided in our [Discord Server](https://discord.gg/2vDMR8m "Syzygy Discord") also generate another 55 lowercase password and log in on the client this ID will be your operator ID with this we can look at statics on the webclient for more info or ask on Discord.

At number 5 we're specifying public IPs ask for latest public IPs on discord in #qubic channel. 

So with everything setup, we're going to compile the .efi file. The next steps are very important to create a succesfull compiled file.

7. Make sure each following setting matches the settings in Visual Studio Code.

![alt text](sreenshots/qubic9_1.png)

![alt text](sreenshots/qubic10_1.png)

![alt text](sreenshots/qubic11.png)

![alt text](sreenshots/qubic12.png)

![alt text](sreenshots/qubic13.png)

![alt text](sreenshots/qubic14.png)

![alt text](sreenshots/qubic15.png)

![alt text](sreenshots/qubic16.png)

![alt text](sreenshots/qubic17.png)

![alt text](sreenshots/qubic18.png)

![alt text](sreenshots/qubic19.png)

![alt text](sreenshots/qubic20.png)

![Stack size](sreenshots/stacksize.png)

![Command Line](sreenshots/commandline.png)

After al these settings we have set up, hit CTRL SHIFT + B, if every thing is fine you should see something like this in your Visual Studio Code screen.

![alt text](sreenshots/qubic21.png)

<a name="code"></a>
# Code modifications

<a name="code-seeds"></a>
### Seeds

More than one seed can be entered into 
`static unsigned char ownSeeds[][55 + 1] = { "<seed>" };`
`static unsigned char ownSeeds[][55 + 1] = { "<seed1>", "<seed2>", "<seed3>" };`

In this case a single machine will be doing computor job once but signing the results with all listed seeds. Note that a failure of this machine will have negative impact on all computors whose seeds are used, so don't put too many seeds in one basket.

__Very important:__ There should be only 1 (one) machine in the universe with computor seed entered into ownSeeds, if there are more than one such machines that computor will likely face decimations (-10% to revenue multiple times) because of signing conflicting messages.

<a name="code-browser"></a>
### Browser

Requires port `80` to be open as well. Set `NUMBER_OF_CLIENT_CONNECTIONS` to `0` if you don't need to connect to your node with a browser.

<a name="preparing-usb"></a>
# Preparing an USB stick to run Qubic

Running the .efi application successfully, depends on the system (check tested motherboard/cpu section). Make sure the system has no access to other disks. Qubic needs to be running from USB FS0: and at the time of writing @N-010 at [Discord](https://discord.gg/2vDMR8m "Syzygy Discord") has written a solution to specify other disks, but this has not been tested by me. For example i needed to remove completely mij SSD disk.

For now lets start. The .efi file created earlier should be in the folder you created the project, something like /QubicTest/x64/Release/QubicTest.efi

If you haven't downloaded [Rufus](https://rufus.ie) yet, do it now. Open and make the following changes.

1. Make sure to select your right USB at least 128GB
2. Download [UEFI SHELL](https://github.com/pbatard/UEFI-Shell/releases/download/21H2/UEFI-Shell-2.2-21H2-RELEASE.iso) and load it into Rufus
3. Set MBR
4. Set UEFI
5. Set FAT32
6. Press Start

![alt text](sreenshots/rufus.png)

<a name="disk-part"></a>
### Set writing privileges with DISK PART

After that make sure to do following steps so .efi can write to USB stick. Connect your write protected USB Stick to your computer.

Right Click on Start. Click Command Prompt (Admin). Click Yes in the UAC message.

Type **diskpart** and hit Enter.

Type **list disk** and hit Enter. 

Here, you’ll be able to see a list of storage media connected to your computer like your internal hard drive, SSD, pen drive, or USB Stick.
Type select **disk number of your disk**. Example, select disk 1 in my case. Make sure you enter the number correctly and don’t end up changing the attributes of your internal hard drive or any other storage media.

Type **attributes disk clear readonly** and press Enter.

Type **exit** and press Enter to get out of the diskpart utility. 

Type **exit** and press Enter again to get out of the command line.
