.. title: SparcServer5 and Wyse30
.. slug: sparcserver5-and-wyse30
.. date: 2015-07-20 10:57:44 UTC-06:00
.. tags: Sparc, Sun, Wyse, OpenBSD, ha-sts
.. category: Anachronistic Computing
.. link: 
.. description: Setting up a SparcServer5 system and a Wyse30 Terminal with OpenBSD.
.. type: text

I found an old Sun Microsystems SparcServer5 the other day when helping my parent clean out their shed.  Connect to
this a Wyse30 terminal that I had picked up, install OpenBSD and Python, connect it to the network, and enjoy a shiny
old home automation interface.

.. TEASER_END

.. -- Describe cleaning and show picture.

Here's a couple of photos of the little guy before starting cleaning.  You can see he's quite dirty.

.. thumbnail:: ../../galleries/SparcServer5/dsc_0134.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0135.jpg

|

While taking the machine apart, I realized just how dirty it was inside.  The power supply was pretty much full of 
dust.

.. thumbnail:: ../../galleries/SparcServer5/dsc_0136.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0137.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0138.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0139.jpg

|

After cleaning, the initial powerup was successful, but one of the RAM modules was bad.  Also, the NVRAM battery is 
dead. The display is the Wyse 30 terminal that I'll be using with this system.

.. thumbnail:: ../../galleries/SparcServer5/dsc_0140.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0141.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0142.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0143.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0144.jpg

|

.. -- Describe installing OpenBSD and show pictures.

I've decided to run OpenBSD as the platform for this machine.  I'm planning on writing a curses interface for my home
automation system, which will be written in python.  As an old copy of Solaris likely won't have a modern version of
python (or update packages), I figured OpenBSD would be a minimal OS that supports a modern version of python and
supports the SPARC (not UltraSPARC) architecture.

Here's some photos of the install process.  I used the autolayout for the harddisk as it's only a 9 GB disk.  I went
ahead and installed all of the default packages along with python and a couple of python libraries.  The SSH key
generation on an 85 MHz machine seemed to take forever, but it only needed to be run once.

.. thumbnail:: ../../galleries/SparcServer5/dsc_0145.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0146.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0147.jpg

|

.. -- Describe making a cable for the terminal and show pictures.

Here's a picture of the short RS232 null modem cable that I made to connect the terminal to the machine.

.. thumbnail:: ../../galleries/SparcServer5/dsc_0148.jpg

|

.. -- Describe testing the 1000base-SX network and show pictures.

Here's couple of pictures showing that I'm actually using 1000 Base-SX ethernet.  This machine happened to have a gem0
SBus card which is supported by OpenBSD.  The CPU is 85M MHz, but the line rate for the ethernet is 1000 MHz (it's a
single optical channel), which means that the ethernet can transfer data over 10 times faster than the CPU.  Truth be
told, I won't be pushing much data through it, though.

.. thumbnail:: ../../galleries/SparcServer5/dsc_0149.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0150.jpg
.. thumbnail:: ../../galleries/SparcServer5/dsc_0152.jpg

|

.. -- Describe future plans for upgrades or fixes:
.. --  * Dead battery on NVRAM ( modify to use external battery)
.. --  * Once NVRAM fixed, fix default boot device (so the machine will boot without the 'boot disk' command)

There are a couple of improvements to this system that I'll likely make in the future:
* Seeing as the NVRAM battery is dead, the system doesn't like to boot without assistance.  The dead NVRAM battery
causes the system to forget its boot settings on every reboot, which requires a 'boot disk' to be entered into the
PROM prompt to boot OpenBSD.  I'd like to try modifying one of the NVRAM chips to accept an external battery.
* Once the NVRAM situation is remedied, I'd like to fix the settings in the NVRAM to allow the system to boot by
itself.  I should also try to determine the system's original MAC address of its AUI port and set that back into the
NVRAM.

.. -- List the system specs.
