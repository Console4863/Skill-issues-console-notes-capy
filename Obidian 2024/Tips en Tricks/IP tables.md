tags: #linux [[School]] [[besturingsystemen]] [[IT]]
links: [https://linuxhint.com/configure-nat-on-ubuntu/](https://linuxhint.com/configure-nat-on-ubuntu/)

--- 
The summary of the configuration of the two virtual machines is given in the below table:

> [!warning]
> De namen van de interfaces kunnen anders zijn.

|   |   |   |   |   |
|---|---|---|---|---|
|Interface Name →|**enp0s3**|   |**enp0s8**|   |
|VM Name ↓|IP address|Gateway IP|IP address|Gateway IP|
|VM1(NAT Router )|192.168.11.201/24|Via DHCP|10.10.10.1/24||
|VM2(Client)|10.10.10.3/24|10.10.10.1|||

![](https://linuxhint.com/wp-content/uploads/2021/11/image2-23.png)

## Let’s Begin…

Now that we have set up the required IP addresses on our machine, we are set to configure them. Let us first check the connectivity between these machines. Both the machines should be able to ping each other. VM1, which is our NAT router machine, should be able to reach the global internet as it is connected to WAN via enp0s3. VM2, which is our local client machine, should not be able to reach the internet until we configure the NAT router on VM1. Now, follow the steps below:

**Step 1.** First check the IP addresses on both the machines with the command:

```
$ ip add | grep enp
```

**Step 2.** Also check the connectivity of the machines before configuring the NAT router as mentioned above. You can use the ping command like:

```
$ ping 8.8.8.8
```

Or

```
$ ping www.google.com
```

Result for the VM1 (NAT Router VM) are shown below:  
![](https://linuxhint.com/wp-content/uploads/2021/11/image4-21.png)

Result for the VM2 (ClientVM) are shown below:

![](https://linuxhint.com/wp-content/uploads/2021/11/image3-21.png)

Both the VMs are working as we have expected them to be. Now we will start configuring VM2(NAT Router).

**Step 3.** On VM2 open the sysctl.conf file and set the “net.ipv4.ip_forward” parameter to one by uncommenting it:

```
$ sudo nano /etc/sysctl.conf
```

**Step 4.** Now enable the changes to above file using the command:

```
$ reboot
```

**Step 5.** Now, install the iptables-persistent package (boot-time loader for netfilter rules, iptables plugin) using:

```
$ sudo apt install iptables-persistent
```

![](https://linuxhint.com/wp-content/uploads/2021/11/image6-19.png)

**Step 6.** List the already configured iptable policies by issuing the command:

```
$ sudo iptables –L
```

**Step 7.** Now mask the requests from inside the LAN with the external IP of NAT router VM.

```
$ iptables -t nat -A POSTROUTING -o ens19 -j MASQUERADE
```


```
$ sudo iptables -t nat –L
```

**Step 8.** Save the iptable rules using:

```
$ sudo iptables-save > /etc/iptables/rules.v4
```

![](https://linuxhint.com/wp-content/uploads/2021/11/image5-18.png)

## Testing The Setup

Now, to check if everything is working fine, ping any public IP from the VM2(client):

**Note:** If you want, you can add a DNS server manually in the client network configuration for domain name resolution. This will suppress the ‘Temporary failure in name resolution’. We have used the Google DNS IP i.e. 8.8.8.8 in our VM1.

![](https://linuxhint.com/wp-content/uploads/2021/11/image1-25.png)