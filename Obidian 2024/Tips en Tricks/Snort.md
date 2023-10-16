#linux 

URL: https://linuxopsys.com/topics/install-snort-on-ubuntu

URL docker?: https://github.com/dnif-archive/docker-snort

## Step 1: Update the system

First, update and upgrade your Ubuntu system

```
sudo apt update
sudo apt upgrade
```

## Step 2: Install Required Dependencies

Ubuntu default repository has snort package. The snort package available there is the old version. To install Snort 3, we have to build from the source. Before installing Snort 3, we need to install the prerequisite and required libraries.

Install Snort 3 dependencies packages with the following command:

```
sudo apt install build-essential libpcap-dev libpcre3-dev libnet1-dev zlib1g-dev luajit hwloc libdnet-dev libdumbnet-dev bison flex liblzma-dev openssl libssl-dev pkg-config libhwloc-dev cmake cpputest libsqlite3-dev uuid-dev libcmocka-dev libnetfilter-queue-dev libmnl-dev autotools-dev libluajit-5.1-dev libunwind-dev
```

After dependencies are installed, created a directory where you compile and kept source files for Snort with the following command:

```
mkdir snort-source-files
```

Then, download and install the latest version of the Snort Data Acquisition library (LibDAQ). For installing **LibDAQ** we'll need to build and install it from the source with the following command.

```
git clone https://github.com/snort3/libdaq.git
```

The next dependency is Tcmalloc, which will optimize memory allocation and provide better memory usage.

Install **Tcmalloc** with the following command.

```
cd ../
wget https://github.com/gperftools/gperftools/releases/download/gperftools-2.9/gperftools-2.9.tar.gz
```

## Step 3: Install Snort 3 on Ubuntu 20.04

After dependencies are set up, we are going to download and install Snort 3 on Ubuntu 20.04.

01. Clone Snort 3 official GitHub repository.

```
cd ../
git clone git://github.com/snortadmin/snort3.git
```

02. Change the directory to Snort3

```
cd snort3/
```

03. From there configure and enable tcmalloc with the following command.

```
./configure_cmake.sh --prefix=/usr/local --enable-tcmalloc
```

04. Navigate to build directory and compile and install Snort 3 using make and make install with the following command.

```
cd build
make 
make install
```

05. When the installation is done, update shared libraries.

```
sudo ldconfig
```

Snort by default is installed to /usr/local/bin/snort directory, it is good practice to create a symbolic link for /usr/sbin/snort

```
sudo ln -s /usr/local/bin/snort /usr/sbin/snort
```

06. Verify Snort 3 installation

```
snort -V
```

Output:

```
,,_     -> Snort++ <-
   o"  )~   Version 3.1.10.0
    ''''    By Martin Roesch & The Snort Team
            http://snort.org/contact#team
            Copyright (C) 2014-2021 Cisco and/or its affiliates. All rights reserved.
            Copyright (C) 1998-2013 Sourcefire, Inc., et al.
            Using DAQ version 3.0.4
            Using LuaJIT version 2.1.0-beta3
            Using OpenSSL 1.1.1f  31 Mar 2020
            Using libpcap version 1.9.1 (with TPACKET_V3)
            Using PCRE version 8.39 2016-06-14
            Using ZLIB version 1.2.11
            Using LZMA version 5.2.4
```

If you see a similar output, then Snort 3 is installed successfully.

## Configure Network Interface Cards

Find the interface on which Snort is listening for network traffic and enable **promiscuous** mode to be able to see all the network traffic sent to it.

```
ip link set dev eh0 promisc on
```

Verify with the following command.

```
ip add sh eth0
```

Output:

```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER UP> mtu 1500 qdisc mq state UP group default qlen 1000
     link/ether f2:3c:92:ed:7e:d8 brd ff:ff:ff:ff:ff:ff
     inet 74.207.230.186/24 brd 74.207.230.255 scope global dynamic eth0
        valid_lft 72073sec preferred_lft 72073sec
     inet6 2600:3c02::f03c:92ff:feed:7ed8/64 scope global dynamic mngtmpaddr noprefixroute 
        valid_lft 60sec preferred_lft 20sec
     inet6 fe80::f03c:92ff:feed:7ed8/64 scope link 
        valid_lft forever preferred_lft forever
```

Next, disable interface Offloading to prevent Snort 3 from truncating large packets, max to 1518 bytes. Check if this feature is enabled with the following command.

```
ethtool -k eth0 | grep receive-offload
```

If seeing this output that GRO is enabled while LRO is fixed or LRO is enabled.

Output.

```
generic-receive-offload: on
large-receive-offload: on
```

Disable it with the following command.

```
ethtool -K eth0 gro off lro off
```

Two ensure the changes persists across system reboot, we'll need to create and enable a systemd service unit to implement the changes.

```
sudo nano /etc/systemd/system/snort3-nic.service
```

Paste the following configuration that points to your network interface.

```
[Unit]
```

Reload systemd configuration settings:

```
sudo systemctl daemon-reload
```

Start and enable the service on boot with the following command:

```
sudo systemctl enable --now snort3-nic.service
```

Output.

```
Created symlink /etc/systemd/system/default.target.wants/snort3-nic.service → /etc/systemd/system/snort3-nic.service.
```

Verify the snort3-nic.service with:

```
sudo systemctl status snort3-nic.service
```

Output.

```
● snort3-nic.service - Set Snort 3 NIC in promiscuous mode and Disable GRO, LRO on boot
      Loaded: loaded (/etc/systemd/system/snort3-nic.service; enabled; vendor preset: enabled)
      Active: active (exited) since Sat 2021-09-18 12:35:17 UTC; 4min 59s ago
     Process: 182782 ExecStart=/usr/sbin/ip link set dev eth0 promisc on (code=exited, status=0>
     Process: 182783 ExecStart=/usr/sbin/ethtool -K eth0 gro off lro off (code=exited, status=0>
    Main PID: 182783 (code=exited, status=0/SUCCESS)
 Sep 18 12:35:17 li72-186 systemd[1]: Starting Set Snort 3 NIC in promiscuous mode and Disable >
 Sep 18 12:35:17 li72-186 systemd[1]: Finished Set Snort 3 NIC in promiscuous mode and Disable >
```

## Install Snort 3 Community Rulesets

In Snort, rulesets are the main advantage for intrusion detection engine. There are three types of Snort Rules: Community Rules, Registered Rules, Subscriber Rules. Community rules are submitted by the open-source community or snort integrators.

We're going to show how to install the Community Rules.

First, create a directory for the Rules in the /usr/local/etc/snort

```
mkdir /usr/local/etc/rules
```

Download Snort 3 community rules. You can find it on the official [Snort3 download page](https://www.snort.org/downloads/#snort-3.0).

```
wget https://www.snort.org/downloads/community/snort3-community-rules.tar.gz
```

Extract downloaded rules and put them in the directory that we previously create /usr/local/etc/rules/

```
tar xzf snort3-community-rules.tar.gz -C /usr/local/etc/rules/
```

Snort 3 includes two main configurations files, **snort_defaults.lua** and **snort.lua**.

The **snort.lua** file contains Snort's main configuration, allowing the implementation and configuration of Snort preprocessors, rules files inclusion, logging, event filters, output, etc.

The **snort_defaults.lua** files contain default values such as paths to rules, AppID, intelligence lists, and network variables.

When rules files are extracted and placed, we're going to configure one of these config files called **snort.lua.** Open the file with your favorite editor and will see something similar config.

```
... -- HOME_NET and EXTERNAL_NET must be set now -- setup the network addresses you are protecting
```

Set the network which you want to protect against attacks as the value for the **HOME_NET** variable, and point **EXTERNAL_NET** variable to **HOME_NET** variable.

Save and exit.

You can also edit Snort defaults in the /usr/local/etc/snort/snort_defaults.lua and under IPS section you can define the location to your rules.

```
ips = 
```

Save and exit.

## Running Snort as a Service

If you are going to run Snort as a service daemon in the background, it is also possible to create a systemd service unit for Snort. It is prudent to run it as a non-privileged system user

Create a non-login system user account.

sudo useradd -r -s /usr/sbin/nologin -M -c SNORT_IDS snort

Then, create a systemd service unit for Snort to be run as a snort user. Adjust and match to your network interface.

sudo `nano /etc/systemd/system/snort3.service`

Paste the following configuration.

```
[Unit]
```

Reload the systemd configuration.

```
sudo systemctl daemon-reload
```

Set the ownership and permissions on the log file.

```
sudo chmod -R 5775 /var/log/snort
sudo chown -R snort:snort /var/log/snort
```

Start and enable Snort to run on the system boot:

```
sudo systemctl enable --now snort3
```

Check the service status to confirm if it is running.

```
sudo systemctl status snort3
```

Output.

```
● snort3.service - Snort 3 NIDS Daemon
      Loaded: loaded (/etc/systemd/system/snort3.service; enabled; vendor preset: enabled)
      Active: active (running) since Sat 2021-09-18 12:44:32 UTC; 6s ago
    Main PID: 182886 (snort)
       Tasks: 2 (limit: 1071)
      Memory: 62.6M
      CGroup: /system.slice/snort3.service
              └─182886 /usr/local/bin/snort -c /usr/local/etc/snort/snort.lua -s 65535 -k none >
 Sep 18 12:44:32 li72-186 systemd[1]: Started Snort 3 NIDS Daemon.
```