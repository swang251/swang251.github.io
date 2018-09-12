---
title: Setup tips for NI hardware + DAQ Toolbox on Matlab + Windows XP (SP3)
date: 2018-09-11 22:19:12
tags: [Research Daily, CAML]
categories: Research Daily
---

Working on old version software and hardware is not as easy and direct as it seems to be. I am recently trying to set up the Dantec Dynamics CTA hot-wire anemometer. Because the software could only run on Windows XP or other versions in the same era, I have to install Windows XP on the PC of our lab. 

This blog writes about the setup on Windows XP (SP3) 32-bit for the NI PCI-4472 data acquisition board and DaqPlot, a program for data acquisition and analysis written by Gary P. Scavone and is a simplified version of DataLogger by James Woodhouse.

- The latest release of Matlab for Windows XP (SP3) 32-bit is R2015b ([details here](https://www.mathworks.com/support/sysreq/previous_releases.html));
- The earliest release of Matlab (or Data Acquisition Toolbox) supporting NI PCI-4472 is R2014a ([details here](https://www.mathworks.com/hardware-support/nidaqmx.html));
- The latest release of NI-DAQmx supporting Windows XP (SP3) 32-bit is NI-DAQmx 15.5.1;
- The earliest release of NI-DAQmx for NI PCI-4472 required by Data Acquisition Toolbox on Matlab is NI-DAQmx 9.0 (or 9.1);
- Check [troubleshooting tips](https://www.mathworks.com/help/daq/troubleshooting-tips.html) for Data Acquisition Toolbox when needed, e.g. the comments recommended `daq.getVendors` and `daq.getDevices`.
