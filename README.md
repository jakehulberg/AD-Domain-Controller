# AD-Domain-Controller

<h1>Working with Active Directory in Windows Server 2022</h1>



<h2>Description</h2>
<b> In this lab I download and configure a Windows server 2022 instance in Oracle VirtualBox. I deploy the server as a domain controller and configure services such as Ras, Nat, and DHCP. I create a user, set it as an admin account and connect to the domain controller. 
</b>
<br />
<br />
<h3>Step 1: Download Windows Server 2022 ISO File from Microsoft.</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/mbdTFss.png" height="85%" width="85%" alt="Windows Server File"/>
</p>


<br />
<br />
<h3>Step 2: Setting up two network adapters on this Windows Server instance. The first will be for NAT and internet access. The second will be set to internal network so that our client machine can connect to it. Client machine adapter is set only to internal network.</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/wY41yeU.png" height="85%" width="85%" alt="First Interface Server"/>
  <img src="https://i.imgur.com/rZ5lu7i.png" height="85%" width="85%" alt="Second Interface Server"/>
</p>


<br />
<br />
<h3>These are the two network adapters in the server. The first one is connected to the internet and recieved a DHCP lease from my gateway. We gave the second one a private IPv4 address of 172.16.0.1 with a subnet mask of 255.255.255.0. Later we will set up DHCP scope so it can serve as gateway and lease out IP addresses within a certain range.</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/79y9Jb0.png" height="85%" width="85%" alt="Internet Interface"/>
  <img src="https://i.imgur.com/PhiwuG1.png" height="85%" width="85%" alt="APIPA Interface"/>
</p>



<br />
<br />
<h3>Step 3: Adding features for DHCP, Remote Access, AD Domain Services, and Routing Services.</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/QwcyfnO.png" height="85%" width="85%" alt="DHCP, Remote Access, AD Domain Services"/>
  <img src="https://i.imgur.com/DL6t8Pj.png" height="85%" width="85%" alt="Routing Services and RAS"/>
</p>




<br />
<br />
<h3>Step 4: Deploying this server as a domain controller "jakesdomain.com"</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/Lzdvcdf.png" height="85%" width="85%" alt="First Interface Server"/>
</p>


<br />
<br />
<h3>Step 5: Setting up RAS / NAT tools. Routing/remote access —> right click DC local —> configure RAS. Setting up NAT to allow internal clients to connect to the internet using one public IP address. The NIC Selected for NAT is the "Internet" one so we can access the internet.
</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/xKExKZt.png" height="85%" width="85%" alt="NAT"/>
  <img src="https://i.imgur.com/XWpjE9r.png" height="85%" width="85%" alt="NAT2"/>
  <img src="https://i.imgur.com/MIGNUJA.png" height="85%" width="85%" alt="Internet Selected"/>
</p>



<br />
<br />
<h3>Step 6: Setting up DHCP. Tools --> DHCP </h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/BS2id9A.png" height="85%" width="85%" alt="First Interface Server"/>
</p>



<br />
<br />
<h3>Step 7: Setting up DHCP. Select your domain --> IPv4 --> New Scope</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/ObtfGnN.png" height="85%" width="85%" alt="First Interface Server"/>
</p>



<br />
<br />
<h3>Step 8: Setting up DHCP. Naming our scope the range that it will be.</h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/eN5fs6u.png" height="85%" width="85%" alt="First Interface Server"/>
</p>



<br />
<br />
<h3>Step 9: Setting up DHCP scope and making it a /24 subnet with a mask of 255.255.255.0. This allows for 253 usable IP addresses but we will only have a range of 101 in our scope. We are not going to exclude any addresses so we skip this part. </h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/A9FBUkW.png" height="85%" width="85%" alt="First Interface Server"/>
  <img src="https://i.imgur.com/VdjJCX7.png" height="85%" width="85%" alt="First Interface Server"/>
</p>




<br />
<br />
<h3>Step 10: Setting up the default gateway, the router that will be used by our clients. We set this to our "Internal" IP address of 172.16.0.1 that we created earlier. After this step we did not set up a WINS server. </h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/fOTfc0O.png" height="85%" width="85%" alt="First Interface Server"/>
</p>


<br />
<br />
<h3>Step 11: Right click our domain and click "authorize", right click IPv4 and click "refresh". Now it should be working. One can see the scope and leased out IP addressses. </h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/2oZi4w9.png" height="85%" width="85%" alt="First Interface Server"/>
</p>




<br />
<br />
<h3>Step 12: Now we'll create a user account that I can log into this domain with. Click tools --> Active Directory Users and computers --> Right click jakesdomain --> New --> User. </h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/RHfPY55.png" height="85%" width="85%" alt="First Interface Server"/>
  <img src="https://i.imgur.com/oJp6R2l.png" height="85%" width="85%" alt="First Interface Server"/>
</p>


<br />
<br />
<h3>Step 13: Changing this account to an admin account! Right click on name --> Properties --> Member of. </h3>
<br />

<p align="center">
  <img src="https://i.imgur.com/wYYmrLK.png" height="85%" width="85%" alt="First Interface Server"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
