[discuss the desire to run networking equipment at home]
[discuss reasons as to why linux is important to networking jobs]
[]








My love for computers and desire to work in IT is becoming impossible to ignore, who would have thought? I think it's about time to stop uninstalling Linux every time I hit a wall. Before starting this, I had been the type of enthusiast to gain lots of excitement from hearing about the sustainability, performance and customisability of Linux systems, and timidly (read: terrified, being the PC-loving kid I was, to ruin the family computer) would crawl through the installation instructions, trying not to worry about snarky forum users I saw who turned their noses up at the suggestion that someone might use a GUI Windows binary like Rufus or something, or even worse "Umm, really? Ubuntu...?" How embarrassing! If only it weren't over a decade before I would start to understand what I really wanted in life, and that those people were so, so painfully wrong.
I will admit that as a teenager I have done the "reinstall of shame," that is, hopping into bios to boot from my Windows recovery partition, probably five times. I simply didn't know enough, not even just about computers. An immense amount of work had to be done to rectify this situation. And it turned out it had nothing to do with Linux. Once I actually returned in a decent enough headspace to stay calm through the problem-solving process and knowing what I know now, I'm more prepared than ever.
Finally fed up with frustrations of the self, and those of Windows 11, I backed up all of my precious configs, documents, photos, save games, notes, yadda, yadda... took one last look at the thing mentally holding me back, and took the plunge. 


Some of the stuff I've done so far:

- Decided to try out CachyOS+COSMIC rather than my usual Debian or Ubuntu install because it's doing some cool new (barely comprehensible) stuff and this provisional laptop I'm using (Surface Pro 7 (read: it was a gift)) could use the performance boost. CachyOS being essentially a fork of Arch meant to me that I would have some great documentation, most of which is written from a "from scratch" perspective. Which is good for those who want to learn. Plus, a minimal amount of "bloat" packages, which is good for those with a soul!

- Backed up every important/personal file to a flash drive with a couple of redundancies elsewhere.

- The one time I used Linux on my Surface before, I used a custom kernel called surface-linux. It was a godsend for features like touchscreen support (not good enough on the Surface to care about on this level), hibernation (fixable in other ways and not an issue), and awesome things like not forgetting that the trackpad exists (....). Unfortunately, the custom kernel hadn't really been maintained since I was gone. Last update was actually around the last time I had used the thing!

- Not only that, but because of these "half-assed" (quote: https://discuss.cachyos.org/t/install-surface-touchscreen/3599/5) updates, CachyOS has opted to stop including the surface-linux patches in their own kernel altogther.

- If I ever decide I have a good reason to hibernate the computer while it's plugged in, I'll consider compiling the kernel myself. Since it's my only machine for now, I think it might just be best to skip this step altogether for now.


- Installed CachyOS + COSMIC via bootable flash drive with the GUI installer.

- COSMIC seems to have helped me to settle some of the gripes I'd had with various WMs and desktop setups in Linux, e.g. ugly-ass, glitchy-ass window support, UAGA (new acronym lol) tiling support, UAGA dock, UAGA essential system settings menu (learning about all kinds of configs and daemons and stuff but I'm still new here give me a break). In the past I have used gnome, cinammon, kde, xfce and i3 in that order. In the past, despite my best attempts, while avoiding lengthy guides, I could not manage to make a system nearly as stable, quick, beautiful and functional as this setup I currently have.

- Built Packet Tracer [fill out steps]

- (For educational purposes only) used ftp/lftp, nano, mount, cp, mv, mkdir, ls, lsblk, lsof, various extraction methods, to install the latest (and most wacky) Xbox 360 modification method, XeUnshackle.
    - Nearly decided to automate the process of ftp-getting my nand flash dumps while I was backing those up into nested folders for redundancies, but decided I had rather better things to do than make this simple process less dumb! But it would go something like this: 
        cron scheduler runs script (no systemd configured right now) -> script starts ftp client, connects to xboxftp -> if changes are detected between last get and current get of /Hdd1/nandflash/flashdmp.bin, update most recent iterative directory (i.e. /home/netloc/nanddumps/1/, 2/, 3/, 4/, 5/, ...) and exit, else exit.

- 