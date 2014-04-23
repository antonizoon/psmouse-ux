psmouse-ux
==========

The Sony VAIO UX has an Alps DualPoint Stick that has serious tap sensitivity issues in Linux. This repository contains a patch for the `psmouse` kernel module to fix this issue. Tap to click sensitivity is heavily toned down, preventing the mouse from making random clicks everywhere.

This version has also been patched to work with Linux kernels > 3.5 (based on a similar procedure by [sphillips at LinuxSagas](http://linuxsagas.digitaleagle.net/2013/10/14/ubuntu-13-04-finally-fixing-my-touchpad/)), and tested on Lubuntu 13.10.

Instructions
------------

From the Terminal, as root:

1. Click **Download as zip** from the link on the right. Then, open a terminal in your `~/Downloads` folder. 

```bash
    cd ~/Downloads
```
    
2. Copy `mouse.tar.gz` to `/usr/src`:

```bash
    cp master.zip /usr/src
```

2. Go to `/usr/src`:

```bash
    cd /usr/src
```

3. Unzip the `master.zip` archive into `/usr/src`: 

```bash
    unzip master.zip
```
4. Add the new module to DKMS: 

```bash
    sudo dkms add -m psmouse -v ux
```

5. Build the new kernel module through DKMS:

```bash
    sudo dkms build -m psmouse -v ux
```

6. Install the new kernel module through DKMS:

```bash
    sudo dkms install -m psmouse -v ux
```

7. Remove the psmouse module from the running kernel: 

```bash
    sudo modprobe -r psmouse
```

8. Activate the newly created psmouse module:

```bash
    sudo modprobe psmouse
```

Sources
-------

* [xrgtn - The original Partial Tap Fix for 2.6](http://xrgtn.livejournal.com/)
* [MicroPCTalk - Partial Tap Fix for Alps Dualpoint Stick](http://www.micropctalk.com/forums/showthread.php?p=62447)
* [LinuxSagas - Finally Fixing my Touchpad in Ubuntu 13.04](http://linuxsagas.digitaleagle.net/2013/10/14/ubuntu-13-04-finally-fixing-my-touchpad/)
