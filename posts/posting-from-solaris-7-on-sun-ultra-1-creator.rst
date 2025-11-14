.. title: Posting from Solaris 7 on Sun Ultra 1 Creator
.. slug: posting-from-solaris-7-on-sun-ultra-1-creator
.. date: 2025-10-09 16:00:33 UTC-06:00
.. tags: computers
.. category: Old Computers
.. link: 
.. description: Posting Again... This time from Solaris 7 on a Sun Ultra 1 Creator workstation.
.. type: text

I'm posting again after another long while.  I decided I should get back to writing again (for the um-teenth-time).
I'm not much of a writer, so I feel I should practice this poorly developed skill to get better.  Writing gets more
important as careers move forward.  So with that, I'll write about an old computer that I dug out of storage and decided
to use to start practicing my writing.  That machine (really a pile of machines) is an old Sun Microsystems Ultra 1
Creator.

.. TEASER_END

The Sun Microsystems Ultra 1 series of workstations was first sold in November of 1995.  The Ultra 1 series was the
first of Sun's computers to run the UltraSPARC series (aka SPARCV9) 64-bit CPU.  The Ultra 1 series runs the UltraSPARC
I cpu and the system predates USB, making loading modern operating systems a bit of a challenge.  The system I have is
Ultra 1 Creator 170E, which means it is the second revision of the Ultra 1 containing two SBus slots and one UPA slot,
with a Creator framebuffer in the UPA slot, and a 167Mhz CPU.  I've loaded the system with 8 x 128 MB RAM sticks,
totalling 1024 MB of RAM.  I decided to load Solaris 7 on the system to give it a try.  Solaris 7 is newer than the
SunOS series of operating systems, but is still old enough to be pre-Oracle.  It also is the last version with
OpenWindows, which I wanted to give a try.  It does have the Common Desktop Environment (CDE) of the later Solaris
editions, so it seemed a good middle ground to start my journey through Solaris.  While reading up on Solaris, it
appears Solaris 8 was the really major turning point in the GUI arena, but I didn't want to push this Ultra 1 Creator.
Solaris 9 should also work, but Solaris 10 dropped support for the UltraSPARC I and early UltraSPARC II processors.
I'll probably give Solaris 8 and Solaris 9 a try in the near future.  I haven't decided if I want this Ultra 1 Creator,
or one of the older 32-bit SPARCstations to be my daily driver.  I'd really like it to be the Sun 3/50, but a 68k
processor and black and white graphics would make that machine a challenge to daily.

.. Talk about getting the machines out of storage, cleaning, ordering RAM on fleBay.

I have two of these Ultra 1 Creator machines.  Until about three months ago, they were sitting in storage for almost 10
years.  They've been bouncing from home to home to storage with me as a couple of the last survivors from a huge pile of
Sun machines I used to have.  Most of the machines were lost in a sad mistake of donating them to a local hackerspace,
which then decided to trash them about a year later without even asking if I wanted them back.  It's a huge problem with
donating these days, so be wary.

Now that these machines are out of storage, I wanted to get one nice enough to use as a daily driver for writing.  It's
too underpowered for surfing the internet in these modern days.  The biggest issue being the amount of CPU required to
handle constant processing of SSL/TLS connections for keeping modern webpages any kind of secure.  The Solaris OS isn't
going to have much malware or ransomeware these days, but leaking passwords to websites on the internet via unencrypted
connections wouldn't be good.

When the two Ultra 1 Creators came out of storage, they were obviously dirty.  One of the machines was clearly more used
in it's lifetime as it was much more full of dust bunnies.  I vacuumed both out and picked the "nicer" of the two
machines since they were both spec'd the same.  There was a sticker on the front of one of them with the name "victoria"
so I guess that will continue to be the machine's name.  A little magic eraser on the outside makes the cases look nice.
I'm not going to retro-brite the case as it's not yellowed much and will be in a stack of machines.

I wanted to max out the capabilities of my daily driver machine.  There's not much expasion available for the Ultra 1
series.  It's pretty much more RAM, better graphics card, and bigger hard disk.  I went onto the fleBay website looking
for RAM and the Creator3D framebuffer.  The framebuffers are now stupid expensive, but I found a bunch of RAM, some new
in box, for a pretty reasonable price.  I now have enough (bought a couple of lots) to upgrade something like six
Ultra 1 machines to their max of 1024 MB.  This one is now maxed on RAM.

.. INSERT PHOTOS OF CASE AND RAM HERE

.. Talk about battery modding the NVRAM.  Make sure to link to glitchworks (and back up) and the historical docs for
.. NVRAM (and back up).

All of these old Sun workstations (SUN4 types specifically) use a battery backed non-volatile RAM (NVRAM) chip with
integrated realtime clock (RTC).  The battery is a coin cell integrated into the "hat" on the top of the chip.  The cell
won't leak, so you don't have to worry about damage, but the cell does go dead.  There are occasionally available modern
replacements, but they usually have issues due to timing or issues with the RTC using 4 digit years (e.g. 2025) instead
of the original chips using 2 digit years (e.g. 25).  After reading website like Glitchworks (LINK HERE), it appears the
best solution is to dremel into the chip hat, cut one of the wires to the old cell, and solder a new cell holder to the
chip.  Glitchworks made a nice little replacement hat, but they're not available anymore.  I just purchased some cheap
cell holders from the spAmazon jungle and soldered them on.  I just taped the cell holder next to NVRAM chip once
installed in the machine.

The NVRAM will need to have the core settings reloaded, otherwise the ethernet MAC address and host ID will both be
wrong.  There's also a value that tells the OS (if it looks) what the host type is (e.g. SPARCstation 20 vs Ultra 1).
One important note for the Ultra 1 and later Ultra machines, the OpenPROM has a password feature that stores the
password on the NVRAM.  If that part of memory isn't zero'd out when the battery is reconnected (usually contains 0xFF
or 0xAA), then the password may be set to an untypable value.  The solution is to put the NVRAM chip in a programmer and
zero out the chip before putting in back into the machine.  I used a TL866II chinesium programmer.  It has support for
all the TIMEKEEPER type NVRAM chips.  The verification will fail because the last few bytes are the RTC values which
aren't writeable.  That's fine, just read the chip again and make sure all but the last few bytes are zero'd out.  Once
the NVRAM is back in the machine, it will take a very long time to boot.  It will have a blank screen for a couple of
minutes, then show the OpenPROM screen.  This is due to the full diagnostics being run due to the NVRAM being invalid
(blank).  Below I list the commands I ran for my Ultra 1 to program the NVRAM.  The system will try to boot from the
network by default in diagnostic mode.  Use the STOP+A keyboard combination to stop booting and get to the OpenBOOT
prompt.  I left mine in diagnostic mode, but I did set the system to boot from the disk in both normal and diagnostic
modes so it will boot the OS if nothing is wrong.  I don't mind the long boot time for the diagnostics.  I just power
on, then get water or something while it's booting.

.. PUT THE NVRAM RESET COMMANDS HERE

Below are the NVRAM reprogramming commands to make the NVRAM usable::

1 0 mkp
<type> 1 mkp
<mac_0> 2 mkp
<mac_1> 3 mkp
<mac_2> 4 mkp
<mac_3> 5 mkp
<mac_4> 6 mkp
<mac_5> 7 mkp
0 8 mkp
0 9 mkp
0 a mkp
0 b mkp
<host_0> c mkp
<host_1> d mkp
<host_2> e mkp
0 f 0 do i idprom@ xor loop f mkp

The <type> value sets the type code of the machine.  There's a list of these values available (LINK and copy here).  The
<mac_0>, <mac_1>, <mac_2> are usually set to 8, 0, 20 which are the assigned first half of the ethernet MAC addresses
assigned to Sun Microsystems back in the day.  <mac_3>, <mac_4>, <mac_5> are the unique part of the MAC address for this
machine.  It's usually the same as the last three bytes of the HOST ID of the machine, which are put in for the
<host_0>, <host_1>, <host_2> values.  Below are the commands again with the values for my Ultra1 replaced::

1 0 mkp
80 1 mkp
8 2 mkp
0 3 mkp
20 4 mkp
8d 5 mkp
2c 6 mkp
99 7 mkp
0 8 mkp
0 9 mkp
0 a mkp
0 b mkp
8d c mkp
2c d mkp
99 e mkp
0 f 0 do i idprom@ xor loop f mkp

.. PUT THE BOOT DISK COMMAND HERE

.. PUT PICTURES OF THE NVRAM MOD HERE

.. Talk about current hard drive and the plans to switch to a ZuluSCSI Blaster board with a SCA adapter.

Currently, while typing this blog entry on the Ultra 1 Creator itself, I'm running on a 146 GB 10K RPM SCA-SCSI Atlas
harddrive.  It's definitely noisy, though not as noisy as the 5 1/4 full height drive that I have as an external drive
for the little Sun IPX.  I installed Solaris 7 on the harddrive without any issues.  I set the root slice a bit bigger
than the default, 2 GB or so instead of the default 900 MB.  I put the rest of the available space to the /export/home
slice, not that I'm going to be using much space there.  I'm using the network file system (NFS) to mount a share to
this Ultra 1.  The biggest reason I'm using an NFS share and not local storage is needing the git tool to upload this
blog.  The Ultra 1 is too anaemic for the hashing and encryption.  It'll do it, but it'll be slow.  Also, I haven't
found a package available to install git or ssh on Solaris 7.  I've found old packages for Solaris 8, so I might try
those in the future.

Due to the noise of the harddrive and wanting the ability to backup the harddrive as an image, I'm planning on switching
the Ultra 1 over to use a ZuluSCSI.  The recently released "ZuluSCSI Blaster" edition should be performant enough for
the Ultra 1.  The Ultra 1 Creator (really the second revision of the Ultra 1 motherboard, usually designated with an E)
has wide-SCSI but the ZuluSCSI Blaster is still narrow SCSI.  There is a ZuluSCSI Wide edition, but it has the 68-pin
connector, not the 80-pin SCA connector that the Ultra 1 drive bay uses.  Rabbit Hole Computing sells an adapter for the
80-pin SCA to 50-pin connector, so the current plan is to use the adapter with the ZuluSCSI Blaster for now.  Since I'm
using NFS shares and I'm keeping the diagnostics mode on startup, performance shouldn't be an issue for me.

NOTE: During the way too long writing of this post, Rabbit Hole Computing release a version of the ZuluSCSI-Wide with an
80-pin SCA connector directly on the board.  I've switched to that unit, but all of the other info is the same.

.. PUT PICTURES OF THE HDD AND OF THE ZULUSCSI AND ADAPTER, AND THEN THE ZULUSCSI-WIDE

.. Talk about installing Java newer than 1.1.7 and jEdit

As I've mentioned before, I'm running Solaris 7 on this Ultra 1.  I'm primarily planning on writing, which between the
restructured text and markdown files for this blogging system and LaTeX files for bigger projects, all that's really
needed is a good syntax-highlighting text editor.  I've been using one off and on for years that runs in Java and
doesn't take much in the way of resources: jEdit (LINK HERE).  I figured that it would be perfect for a Sun workstation
as Sun created Java in the first place.  Getting it to run, however, was a bit of a saga.  Also, while installing
Solaris 7 on the harddrive went smoothly, installing Solaris 7 on the ZuluSCSI-Wide did not.

This is getting a bit long, so I'll chronicle the installation of Solaris 7, Java 1.3, and jEdit in the next post.  I'll
then go through setting up Tribblix (LINK HERE), the NFS server, rlogin / rsh, and mounting the NFS share on Solaris 7.
It works, and I'm finishing this article on it now.

.. Link some docs here such as the service manual, NVRAM docs, Solaris 7 docs, etc.  Make sure there are "offline" saved
.. versions too, even if they're not linked here.

Below are some of the docs used for this effort (original link and a backup copy):

 * Sun Microsystems Ultra 1 Service Manual: LINK and LINK

.. Make sure to get some pictures of the system, both open and in-situ.

Here's some pictures of the computer:

.. thumbnail:: ../../galleries/OleRadioSwitch/amp-and-switch-brd.png

