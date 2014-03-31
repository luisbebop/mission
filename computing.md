# Hypernet Computing
Processes are inherently ephemeral so computing in a p2p enviornment isn't so much the challenge as much as handling [persistence](https://github.com/hypernet/mission/blob/master/persistence.md).  Still, programs have traditionally been run on managed hardware, where the specs, the OS and other installed and running apps are (mostly) known at compile time.  Hypernet runs on arbitrary end user machines meaning that neither the hardware, nor the operating system, nor the installed packages, nor the average load of the machine are knowable in advance.  Additionally, because Hypernet apps run on end-user machines and not dedicated hardware, there is a potential for malicious apps.  Hypernet addresses these challenges.  So what is Hypernet Computing?  It's a:

- sandbox
- system monitor
- remote launcher

# Sandbox
The sandbox protects the user in a few ways. It:
1. Denies untrusted applications access to the filesystem outside their own directory.
2. Caps the amount of disk an application can use.
3. Caps the amount of bandwidth a disk can use.
4. Denies applications access to local IP addresses (this is important to prevent security breaches behind firewalls or on VPNs where there network is assumed to be "safe")

# System Monitor
The system monitor checks things like, user idle time, power status (if the device has a battery), network connectivity, load average and other system "vitals".  The idea is to make sure the visor never affects the user's compute experience (i.e. only when a device is idle).  It is also used to advertise a machine's capabilities.

# Remote Launcher
The remote launcher is responsible for

1. Finding a machine that meets the application's requirements in terms of available memory, disk and CPU power
2. Ensuring that the application image is uploaded to a machine
3. Launching the application with user specified arguments
4. Monitoring running instances of applications
5. Ensuring that the user defined minimum of instances is always running
6. Handling log aggregation
