# experiment-mirage-ntp
This is an experimental build for https://github.com/matildah/mirage-ntp<BR>
<BR>
1. Environmental setting<BR>
   NAME="Ubuntu"<BR>
   VERSION="14.04.4 LTS, Trusty Tahr"<BR>
   ID=ubuntu<BR>
   ID_LIKE=debian<BR>
   PRETTY_NAME="Ubuntu 14.04.4 LTS"<BR>
   VERSION_ID="14.04"<BR>
   HOME_URL="http://www.ubuntu.com/"<BR>
   SUPPORT_URL="http://help.ubuntu.com/"<BR>
   BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"<BR>
   and Ubuntu 14.04 LTS runs on vbox on OSX yosemite<BR>
<BR>
2. Preparations<BR>
   apt-get install ntp<BR>
   cd /etc/<BR>
   vi ntp.conf<BR>
   please change server setting<BR>
   cd /etc/init.d<BR>
   sudo su -<BR>
   as you like if needed bellow.<BR>
   ./ntp status<BR>
   ./ntp start<BR>
   ./ntp stop<BR>
<BR>
3. Download(clone) and Build<BR>
   download zip<BR>
   unzip zip<BR>
   cd mirage-ntp-master<BR>
   oasis setup<BR>
   make<BR>
   cd unikernel<BR>
   vi unikernel.ml<BR>
   edit ntp server ip address.<BR>
   /bin/sh  ./like_a_mirage.sh<BR>
   sudo su -<BR>
   /bin/sh ./tap.sh<BR>
   ./mir-network<BR>
   in another term:<BR>
     ping 172.16.0.42<BR>
     netstat -na|more<BR>
   if you star ntp daemon already(or Radclock), you will see like bellow.<BR>

4. Output(Experimental Result)<BR>
<pre>
root@ubuntu:/home/cobweb/mirage-ntp-master/unikernel# ./mir-network<BR>
Netif: plugging into tap0 with mac xx:xx:xx:xx:xx:xx<BR>
Netif: connect tap0<BR>
Manager: connect<BR>
Manager: configuring<BR>
Manager: Interface to 172.16.0.42 nm 255.255.255.0 gw [172.16.0.1]<BR>
<BR>
ARP: sending gratuitous from 172.16.0.42<BR>
Manager: configuration done<BR>
send ONE b1442113001<BR>
ARP: transmitting probe -> 172.16.0.1<BR>
ARP: updating 172.16.0.1 -> yy:yy:yy:yy:yy:yy<BR>
recv ONE b1443f63523<BR>
send TWO b14443c30f3<BR>
recv TWO b14444505d5<BR>
THETA 3.275019306693139E-02<BR>
send THREE b155a4dbb1c<BR>
recv THREE b155b02449b<BR>
{ Types.regime = Types.WARMUP;<BR>
  parameters = { Types.ts_limit = 1.5e-05; skm_rate = 2e-07;<BR>
                 e_offset = 9e-05; e_offset_qual = 0.00027 };<BR>
  samples_and_rtt_hat = History.History (100, 3,<BR>
                          [({ Types.quality = Types.OK; ttl = 64;<BR>
                              stratum = Wire.Invalid; leap = Wire.Unknown;<BR>
                              refid = 0x494e4954; rootdelay = 0.;<BR>
                              rootdisp = 163.;<BR>
                              timestamps = { Types.ta = 0xb155a4dbb1c;<BR>
                                             tb = 3674364149.824326992;<BR>
                                             te = 3674364149.824419022;<BR>
                                             tf = 0xb155b02449b } },<BR>
                            (Some 0x8d4e2));<BR>
                           ({ Types.quality = Types.OK; ttl = 64;<BR>
                              stratum = Wire.Invalid; leap = Wire.Unknown;<BR>
                              refid = 0x494e4954; rootdelay = 0.;<BR>
                              rootdisp = 161.;<BR>
                              timestamps = { Types.ta = 0xb14443c30f3;<BR>
                                             tb = 3674364147.790860176;<BR>
                                             te = 3674364147.790915966;<BR>
                                             tf = 0xb14444505d5 } },<BR>
                            (Some 0x8d4e2));<BR>
                           ({ Types.quality = Types.OK; ttl = 64;<BR>
                              stratum = Wire.Invalid; leap = Wire.Unknown;<BR>
                              refid = 0x494e4954; rootdelay = 0.;<BR>
                              rootdisp = 161.;<BR>
                              timestamps = { Types.ta = 0xb1442113001;<BR>
                                             tb = 3674364147.787147999;<BR>
                                             te = 3674364147.787259102;<BR>
                                             tf = 0xb1443f63523 } },<BR>
                            (Some 0x1e50522))]);<BR>
  estimators = { Types.pstamp = (Some History.Fixed (1, 3));<BR>
                 p_hat_and_error = (Some (4.34217301819e-10, 0.00905027596167));<BR>
                 p_local = None; c = (Some 3674358858.19);<BR>
                 theta_hat_and_error = (Some (-0.103462917644,<BR>
                                              4.06120700048e-07)) } }<BR>
ARP responding to: who-has 172.16.0.42?<BR>
</pre>
