---
title: 2026-05-10, The AeroHeaven Story
---
Here is my blog post about the history of AeroHeaven, how it began, how it evolved, and where it is today.

## The beginnings
I started work on, what would eventually become, AeroHeaven in January of 2024.

I first started when I was playing around with remote installations, server shares, etc, and decided to download Windows 7/Server 2008 R2 build 6730 to a VPS for *no particular reason at all.*

I then extended it to downloading all Windows 8/Server 2012 builds, then a bunch of other versions. It took around 3 months, having to use my VPS as an "Upload box", make new OneDrive accounts when I'd run out of space, deal with "phantom storage", etc. 

But I got it into a near complete state, a state I was comfortable with, and at first, it went well. While it wasn't super popular (which ''did'' hurt me a bit), popularity isn't really the main point of projects like this. 

## Problems began
My initial approach had many flaws:

* The project being at the whim of an external provider, which could shut down or ban my account for random reasons.
* The download system was prone to errors and slowdowns due to the nature of the cloud provider I used.
* Users could not upload files to the site.
* I had to split it across multiple accounts due to capacity limits.
* No deduplication on my end, making storage take up a lot more.

But these were issues I accepted for a while, and while they did eat me up in the end, they were manageable. 

### Where it began to fall apart. 
But that changed around late October 2024, where serious file corruption was being detected by users.

It was not just bit flips, but entire sections of ISOs that were different.

I was able to narrow down the problem to how I was uploading builds, but then I did some checks on builds, and *wayyy too many builds* were corrupted.

To make a long story short, that was the thing that basically killed the archive.

### But why did I use a cloud service? 
Well, it was free for me and was fast as I did not have a fast enough server at the time that I could use to host stuff.

## The new beginnings. 
So, with the old site now unviable due to various... reasons, I was at a bit of a loss in terms of what to do, as:

* It didn't feel right to just... replace everything in the existing storage.
* A cloud storage solution would still have the same issues previously mentioned.
* I didn't have a fast enough ISP to support hosting terabytes of builds at reasonable speeds. 
** I did have a server that had enough storage (a PowerEdge R730) and processing power to handle this, but not the upload speeds.
** My VPSes could not store that much data either.

In the meantime, the OneDrive archive stayed up.

### But then, a breakthrough occurred.
I did some more research into ISPs in my area, and BrightSpeed, which would not just support faster uploads, but 2 Gigabit ''symmetric and unmetered'' uploads.

And the best part was? We would pay about the same as our existing ISP (Comcast, certified trash) for it.

I then began the process of getting BrightSpeed installed and configured, and upgrading my machines to support 2.5 Gigabit (yes, they were only 1 Gigabit at the time).

### Sooo... what now?
I then started going on the hunt to download builds, not all builds out there, but enough to start out with. 

I also started working on a few things, notably:

* Server configuration (IIS mainly).
* Deduplication.
* Setting up an upload server for users to upload builds to.

## The Launch and initial evolutions. 
I launched the website on 4/21/2025 to some fanfare. 4 Days later, I added an upload system.

### Naming 
Initially, we were called "windowsarchive.orangera.in", but truth is, that felt kind of boring and placeholderish.

At the same time, me and a friend had created a Discord server, called "AeroHeaven", with a goal of being a hub for things like legacy Windows backports and things like that.

We even set up forums for it!

#### But here's the thing: 
Few actual projects ever were with us, the Discord server mainly became for the Windows Archive.

#### So, what now.
I decided (since the other founder of the AeroHeaven community had left) to rebrand [https://windowsarchive.orangera.in windowsarchive.orangera.in] to... AeroHeaven.

Truth is, it felt like it made sense, as a way of using the name and Discord server for **something**, even if it wasn't it's original purpose. 

## Where are we at now?
Now, we're at a good point, we're not running too low on space for now (have 4TB free on the archive volume and 18TB of space I can expand into if needbe), site was redesigned last month, etc. 

So far, it's mainly been smooth sailing with this project, there have obviously been bumps along the way, but none of them were as fundamental as chronic file corruption. 

One issue I'd like to address here is that, sometimes, it does take a long time for me to process uploads. This is for two reasons:

* I am busy in life, and while I am dedicated to this project, I also do things like:
** Spend time with friends online and family.
** Work on other projects.
** Having a life beyond this project (or even the online world in general), I have to do things like school.
** Sometimes, I am really tired, and just prefer to take it easy.
* Some builds (especially stuff like 9X, XP, etc) I am not familiar with (to correct filenames and information on) and/or need to develop ways to correct said filenames.

### Overall ===
Even though my Windows build archiving adventures have been a long history of things, I am happy to say how it's gone, and the state it is in today. Thank you for reading.

- Scarlett Asahi (朝日スカーレット), 5/10/2026
