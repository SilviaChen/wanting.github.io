---
layout: post
title:  "How I fixed Fedora 27 console mode blinking"
categories: Software Technical Note
---

**BG: Stuck on booting. CANNOT switch to console with 'ctrl+alt+f2'
Reason: Upgrade Fedora version
Solution step:**


1. @grub menu, enter 'e' to edit boot command

   ![Fedora 23 grub menu](/assets/images/fedora23_grub_menu.png)

2. Find the line at beginning 'linux16/vmlinuz-4.13….', then type [space] and '3' at the line end, such as '…….UTF-8 3' so that Fedora will know you want to enter console mode

3. Press 'ctrl+x' to login

4. ``` $sudo vim /etc/gdm/custom.conf ```

5. In `custom.conf`, find line ```'#WaylandEnable = false', delete '#'```

&nbsp;&nbsp;&nbsp;

### DONE