---
Title: 2025-10-12, AutoErase
---
### Welcome to my writeup on autoerasetool/Tribeca, a new security system added in iOS 15/16 for internal devices. 
Tribeca and autoerase will be used interchangeably as Tribeca is the internal codename for it 

Published on 10/12/2025 4:57AM EST 

## What is autoerase (or TriBeca, or AutoEraseTool)? 
**Autoerase** is, judging by its name, a system to automatically erase devices. Specfically, the purpose from various notes I've found, is mainly prevent devices with pre-release confidential builds and features of iOS having their operating system files exfiled.

This system from various research appears to have been added in iOS 15, and is also part of the "security" project (securityd). 

It is also referred to in some places as "Tribeca" (an internal codename), and "Auto Erase" likely referring to the functionality/system of it. 

In addition, from what i can tell, its not implemented/compiled in with later (i.e. shortly after initial betas are out) builds, in this case, the autoerasetool binary has the "autoerase is not compiled into this build" string. This is likely due to the features for said versions of iOS being revealed and thus no longer secret. 

## What does it actually do? 

### What it does before it triggers
From a stringdump of said tool, a few things are the case:

* It relies on an XPC service, judging by a string "TribecaXPCProtocol".
* It can be disabled via a command or the GUI, however, it appears to be only for one boot.

* It relies on an expiration date (likely as a way of detecting "lost" devices as devices that would run InternalUI can't be updated (why would you anyway)), judging by the strings:
```
yyyy-MM-dd HH:mm
AutoErase State:     
Scheduled Autoerase: %s
Time Left:           %s
Last Restore:        %s
Enabled - using AEToken  
Enabled - using last LastRestore (minTTL Passed)  
Enabled - using last LastRestore  
Disabled For Current Boot
```
There is also a macOS version of it, in HomeDiags (and iirc, NonUI/InternalUI versions of macOS), it seems to be used to handle "AETokens" (not sure what this is).
```
orangera1n@J314sAP Downloads % AETool
OVERVIEW: autoerase tool

USAGE: AETool <command> [options] [args]

SUBCOMMANDS:
  extend                  automatically extends (and issues) tokens for all attached (or specified) devices
  issue                   issues a token
  listen                  automatically extends (and issues) tokens for all attached (or specified) devices
  status                  lists aetoken status for all connected devices
```

### When it triggers
From what I can tell, it does a rather, unique type of obliteration (Apple's name for erasing (not to be confused with restoring) the device).

Specifically it does the type "BrickOnly", added seemingly in iOS 15, what this does is makes the device unbootable but keeps the Data parititon. This is different to the common type of obliteration, Data (which does the data partition).

But Brick oblit type means thrown to DFU, right? Well in most cases, yes, but here, no due.

I decided to grab the strings of trigger_obliteration which calls mobile_obliterator when ran and found out that there's a "--nofirmware" arguement which specifies to ''not'' wipe the firmware (iBoot, Images, etc.). 

The BrickOnly argument in this case retains the Data partition, and there's likely some sort of --nofirmware flag passed designed to only delete the '''kernelcache''', rendering the device unbootable but can boot to recovery, its unclear why but one speculated reason is that its to allow recovery of the data if autoerasetool is erroneously triggered.  

## How did I first find autoerasetool? 
Background: around September 2023, I heard various reports of proto owners having their internal UI prototypes bricked into recovery despite not connecting to the internet (it's commonly said that internalui prototypes if connected to the internet will brick if iCloud locked, this *is* 100% possible but requires the setting "Enable Remote Brick" where upon erasure via find my, the device will brick), with the obliteration reason being along the lines of ``oblit-begins=2022-05-18 16:47:28 GMT-7: Caller: security, Type: ObliterationTypeBrickOnly, Reason: AutoErased: was on 20A207a. Max lifetime of build exceeded (maxTTL)``.

I later looking through a dump of a device and for information about SSH Warnings (i may or may not do a blogpost about ssh changes in iOS 17 for internal builds) and noticed that there was this line in said warning.

```
"# PROMPT_COMMAND

PROMPT_COMMAND="test -x /usr/local/bin/autoerasetool && /usr/local/bin/autoerasetool warn"
```
## What to do if you get a proto now?
If your device hasn't been autoerased yet:

If your device has already booted atleast once to InternalUI, if you haven't already, dump the software off of the device fully (you 100% want the kernelcache, also you should dump the software anyway), as it can be used to boot back into InternalUI and put it back.

If you haven't booted your device yet to InternalUI, boot it to recovery mode, enable the boot-args of "-s" in addition to your usual boot-args to stop any obliterations, verify if autoerasetool is not compiled in, and if not, run these commands (you may need to add cs_enforcement_disable=1, which seems to not be allowed on CPFM 03 (rare for internaluis espically in cases with autoerase) for some reason or something, not sure what causes the "can't has cs_enforcement_disable" panic in some cases) (by the way i'd do these commands anyway because of other things that could be done reguarding obliteration)
```
cd /usr/libexec/
cp mobile_obliterator mobile_obliterator_old
touch mobile_obliterator
chmod +x mobile_obliterator
```

## Thanks to? 
The people who provided various resources for this writeup.

- Asahi Scarlett (朝日すかーれっと)

