# Developer Guide and Examples for Embedding IoT GUI with Ubuntu Frame

Forked from [https://github.com/MirServer/iot-example-graphical-snap.git](https://github.com/MirServer/iot-example-graphical-snap.git)

## `weston-calibrator`

This example contains a recipe for the `weston-calibrator` tool that ships with the [Weston](https://gitlab.freedesktop.org/wayland/weston) Wayland compositor.

### Creating the Snap Package

In a terminal, clone the repository:

```
git clone https://github.com/hbatagelo/iot-example-graphical-snap.git
cd iot-example-graphical-snap
```

Change to branch `22/native-weston-calibrator` and build the package:

```
git checkout 22/native-weston-calibrator
snapcraft
```

### Installing and Running on Ubuntu Core with Ubuntu Frame

Follow the guide [Ubuntu Core: Preparing a virtual machine with graphics support](https://ubuntu.com/tutorials/ubuntu-core-preparing-a-virtual-machine-with-graphics-support#1-overview) to set up an Ubuntu Core VM.

With the Ubuntu Core VM running, use `scp` to copy the snap package built previously to the VM:

```
scp -P 10022 *.snap <launchpad account>@localhost:~
```

Connect to the VM using `ssh`:

```
ssh -p 10022 <launchpad account>@localhost
```

Install Ubuntu Frame if not installed yet, and then install the snap:

```
snap install ubuntu-frame
snap install --dangerous *.snap
```
Start the service `iot-example-graphical-snap.daemon`:

```
snap start iot-example-graphical-snap
```

### Reading the Calibration Values

The calibration values are available in the service log:

```
snap logs -n=all iot-example-graphical-snap | grep "Calibration values:"
```

...and in the system log:

```
sudo journalctl -u snap.iot-example-graphical-snap.daemon | grep "Calibration values:"
```
