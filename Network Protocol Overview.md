# Network Protocol Overview
<style>
.cli-map{font-family:Consolas,"Courier New",monospace;background:#181818;color:#d6d6d6;border:1px solid #4b4b4b;border-radius:4px;padding:18px;overflow-x:auto;line-height:1.35;min-width:1120px}
.layer{border:1px solid #9a9a9a;margin:14px 0;background:#202020}
.layer-head{border-bottom:1px solid #9a9a9a;padding:8px 12px;font-size:18px;font-weight:700;color:#eeeeee}
.layer-body{padding:10px;display:grid;gap:10px;align-items:start}
.cols-3{grid-template-columns:1fr 260px 1fr}
.cols-4{grid-template-columns:1fr 1fr 1fr 1fr}
.cols-5{grid-template-columns:1fr 190px 190px 1fr}
.box{border:1px solid #8a8a8a;padding:8px;background:#1b1b1b;min-height:34px}
.box-title{font-weight:700;margin-bottom:6px;color:#f3f3f3}
.node{border:1px solid #9a9a9a;display:inline-block;padding:5px 12px;margin:2px 0;background:#171717;font-weight:700}
.center{text-align:center}
.line{white-space:nowrap;margin:2px 0}
.wire{text-align:center;color:#cfcfcf;white-space:pre;font-weight:700}
.wire-row{height:28px;position:relative;margin:-8px 0}
.wire-row:before{content:"";position:absolute;left:50%;top:0;bottom:0;border-left:2px solid #cfcfcf}
.muted{color:#bdbdbd}
.num{display:inline-block;min-width:72px;text-align:right;color:#e0e0e0;padding-left:12px}
.small{font-size:12px}
.cli-map a{color:#f7f7f7;text-decoration:none;border-bottom:1px dotted #bbbbbb}
.cli-map a:hover{border-bottom:1px solid #ffffff}
</style>
<div class="cli-map">
<section class="layer">
<div class="layer-head">| [7] Application Layer</div>
<div class="layer-body cols-3">
<div class="box">
<div class="box-title">+-- TCP application protocols</div>
<div class="line">|-- <a href="./application%20layer/TCP/POP3.md">POP3</a>    Post Office Protocol version 3 <span class="num">110</span></div>
<div class="line">|-- <a href="./application%20layer/TCP/SMTP.md">SMTP</a>    Simple Mail Transfer Protocol <span class="num">25</span></div>
<div class="line">|-- <a href="./application%20layer/TCP/Telnet.md">Telnet</a>  Remote control protocol <span class="num">23</span></div>
<div class="line">|-- <a href="./application%20layer/TCP/FTP.md">FTP</a>     File Transfer Protocol <span class="num">21</span></div>
<div class="line">|-- <a href="./application%20layer/TCP/HTTP.md">HTTP</a>    Hypertext Transfer Protocol <span class="num">80</span></div>
<div class="line">|-- <a href="./application%20layer/TCP/IMAP.md">IMAP</a>    Internet Message Access Protocol <span class="num">143</span></div>
<div class="line">`-- <a href="./application%20layer/TCP/HTTPS.md">HTTP-s</a>  HTTP Secure Protocol <span class="num">443</span></div>
</div>
<div class="box center">
<div class="node"><a href="./application%20layer/common/DNS.md">DNS</a> 53</div>
</div>
<div class="box">
<div class="box-title">+-- UDP application protocols</div>
<div class="line">|-- <a href="./application%20layer/UDP/DHCP.md">DHCP</a>    Dynamic Host Configuration Protocol <span class="num">67</span></div>
<div class="line">|-- <a href="./application%20layer/UDP/TFTP.md">TFTP</a>    Trivial File Transfer Protocol <span class="num">69</span></div>
<div class="line">|-- <a href="./application%20layer/UDP/SNMP.md">SNMP</a>    Simple Network Management Protocol <span class="num">161</span></div>
<div class="line">|-- <a href="./application%20layer/UDP/SLP.md">SLP</a>     Service Location Protocol</div>
<div class="line">|-- <a href="./application%20layer/UDP/NTP.md">NTP</a>     Network Time Protocol</div>
<div class="line">|-- <a href="./application%20layer/UDP/RADIUS.md">RADIUS</a>  Remote Authentication Dial-In User Service</div>
<div class="line">`-- <a href="./application%20layer/UDP/BOOTP.md">BOOTP</a>   Bootstrap Protocol</div>
</div>
</div>
</section>
<div class="wire-row"></div>
<section class="layer">
<div class="layer-head">| [5] Session Layer</div>
<div class="layer-body cols-3">
<div class="box">
<div class="line">|-- <a href="./session%20layer/common/LDAP.md">LDAP</a>  Lightweight Directory Access Protocol</div>
</div>
<div class="box center">
<div class="node"><a href="./session%20layer/common/SS7.md">SS7</a></div>
<div class="line small">Signaling System No. 7</div>
</div>
<div></div>
</div>
</section>
<div class="wire-row"></div>
<section class="layer">
<div class="layer-head">| [4] Transport Layer</div>
<div class="layer-body cols-3">
<div class="box center">
<div class="node"><a href="./transport%20layer/common/TCP.md">TCP</a></div>
<div class="line small">IP protocol number 6</div>
</div>
<div class="box center">
<div class="node"><a href="./transport%20layer/common/UDP.md">UDP</a></div>
<div class="line small">IP protocol number 17</div>
</div>
<div class="box">
<div class="box-title">+-- Transport-adjacent protocols</div>
<div class="line">|-- <a href="./transport%20layer/common/SSL_TLS.md">SSL/TLS</a>   Transport Layer Security</div>
<div class="line">`-- <a href="./transport%20layer/common/TALI.md">TALI</a>      Transport Adapter Layer Interface</div>
</div>
</div>
</section>
<div class="wire-row"></div>
<section class="layer">
<div class="layer-head">| [3] Network Layer</div>
<div class="layer-body cols-3">
<div class="box">
<div class="box-title">+-- Network control and security</div>
<div class="line">|-- <a href="./network%20layer/common/IGMP.md">IGMP</a>  Internet Group Management Protocol <span class="num">2</span></div>
<div class="line">|-- <a href="./network%20layer/common/ICMP.md">ICMP</a>  Internet Control Message Protocol <span class="num">1</span></div>
<div class="line">|-- <a href="./network%20layer/common/RSVP.md">RSVP</a>  Resource Reservation Protocol <span class="num">46</span></div>
<div class="line">|-- <a href="./network%20layer/common/ESP.md">ESP</a>   IP Encapsulating Security Payload <span class="num">50</span></div>
<div class="line">|-- <a href="./network%20layer/common/AH.md">AH</a>    IP Authentication Header <span class="num">51</span></div>
<div class="line">`-- <a href="./network%20layer/common/X.25.md">X.25</a>  Packet Switched Network Protocol <span class="num">93</span></div>
</div>
<div class="box center">
<div class="line small">carries TCP: protocol 6</div>
<div class="node"><a href="./network%20layer/common/IP.md">IP</a></div>
<div class="line small">carries UDP: protocol 17</div>
<div class="line small">network-layer packet delivery</div>
</div>
<div class="box">
<div class="box-title">+-- Routing and router-control protocols</div>
<div class="line">|-- <a href="./network%20layer/TCP/BGP.md">BGP</a>       Border Gateway Protocol <span class="num">179</span></div>
<div class="line">|-- <a href="./network%20layer/UDP/HSRP.md">HSRP</a>      Hot Standby Router Protocol <span class="num">1985</span></div>
<div class="line">|-- <a href="./network%20layer/UDP/RIP_RIPng.md">RIP/RIPng</a> Distance Vector Routing Protocol <span class="num">520/521</span></div>
<div class="line">|-- <a href="./network%20layer/common/DVMRP.md">DVMRP</a>     Distance Vector Multicast Routing Protocol</div>
<div class="line">|-- <a href="./network%20layer/common/OSPF.md">OSPF</a>   Open Shortest Path First <span class="num">89</span></div>
<div class="line">|-- <a href="./network%20layer/common/IS-IS.md">IS-IS</a>  Intermediate System to Intermediate System <span class="num">124</span></div>
<div class="line">|-- <a href="./network%20layer/common/EGP.md">EGP</a>    Exterior Gateway Protocol <span class="num">8</span></div>
<div class="line">|-- <a href="./network%20layer/common/VRRP.md">VRRP</a>   Virtual Router Redundancy Protocol <span class="num">112</span></div>
<div class="line">|-- <a href="./network%20layer/common/IGRP.md">IGRP</a>   Interior Gateway Routing Protocol <span class="num">9</span></div>
<div class="line">|-- <a href="./network%20layer/common/EIGRP.md">EIGRP</a>  Enhanced Interior Gateway Routing Protocol <span class="num">88</span></div>
<div class="line">`-- <a href="./network%20layer/common/Mobile%20IP.md">Mobile IP</a> IP mobility support</div>
</div>
</div>
</section>
<div class="wire-row"></div>
<section class="layer">
<div class="layer-head">| [2] Data Link Layer</div>
<div class="layer-body cols-3">
<div class="box">
<div class="line">|-- <a href="./data%20link%20layer/MPLS/MPLS.md">MPLS</a>  Multiprotocol Label Switching</div>
<div class="line">|</div>
<div class="line">|-- <a href="./data%20link%20layer/HDLC/HDLC.md">HDLC</a>  High-Level Data Link Control</div>
<div class="line">|-- <a href="./data%20link%20layer/HDLC/SDLC.md">SDLC</a>  Synchronous Data Link Control</div>
<div class="line">|</div>
<div class="line">|-- <a href="./data%20link%20layer/PPP/PPP.md">PPP</a>   Point-to-Point Protocol</div>
<div class="line">|-- <a href="./data%20link%20layer/PPP/PPPoE.md">PPPoE</a> PPP over Ethernet</div>
<div class="line">|</div>
<div class="line">`-- <a href="./data%20link%20layer/IEEE%20802.1/IEEE%20802.1.md">IEEE 802.1</a></div>
<div class="line">    |-- <a href="./data%20link%20layer/IEEE%20802.1/802.1d%20STP.md">802.1d</a>  Redundant-link STP</div>
<div class="line">    |-- <a href="./data%20link%20layer/IEEE%20802.1/802.1w%20Rapid%20STP.md">802.1w</a>  Rapid STP</div>
<div class="line">    |-- <a href="./data%20link%20layer/IEEE%20802.1/802.1q%20VLAN.md">802.1q</a>  VLAN</div>
<div class="line">    |-- <a href="./data%20link%20layer/IEEE%20802.1/802.1x%20Authentication.md">802.1x</a>  Authentication system</div>
<div class="line">    |-- <a href="./data%20link%20layer/IEEE%20802.1/802.1p%20QoS%20Priority.md">802.1p</a>  QoS traffic priority</div>
<div class="line">    `-- <a href="./data%20link%20layer/IEEE%20802.1/802.1g%20Remote%20Bridge.md">802.1g</a>  Remote bridge</div>
</div>
<div class="box center">
<div class="line small">CSMA/CA</div>
<div class="node"><a href="./data%20link%20layer/IEEE%20802.11/IEEE%20802.11.md">IEEE 802.11</a></div>
<div class="node"><a href="./data%20link%20layer/IEEE%20802/IEEE%20802.md">IEEE 802</a></div>
<div class="node"><a href="./data%20link%20layer/IEEE%20802.3/IEEE%20802.3.md">IEEE 802.3</a></div>
<div class="line small">CSMA/CD</div>
</div>
<div class="box">
<div class="line">|-- <a href="./data%20link%20layer/ATM/ATM.md">ATM</a>  Asynchronous Transfer Mode</div>
<div class="line">|</div>
<div class="box-title">+-- VPN Protocols</div>
<div class="line">|-- <a href="./data%20link%20layer/VPN/L2F.md">L2F</a>   Layer 2 Forwarding Protocol</div>
<div class="line">|-- <a href="./data%20link%20layer/VPN/L2TP.md">L2TP</a>  Layer 2 Tunneling Protocol</div>
<div class="line">|-- <a href="./data%20link%20layer/VPN/PPTP.md">PPTP</a>  Point-to-Point Tunneling Protocol</div>
<div class="line">|</div>
<div class="line">|-- <a href="./data%20link%20layer/switching/LACP.md">LACP</a>  Link Aggregation Control Protocol <span class="num">802.3ad</span></div>
<div class="line">|-- <a href="./data%20link%20layer/switching/ISL.md">ISL</a>   Cisco Inter-Switch Link, discontinued</div>
<div class="line">|</div>
<div class="line">|-- <a href="./data%20link%20layer/common/ARP.md">ARP</a>   Address Resolution Protocol</div>
<div class="line">`-- <a href="./data%20link%20layer/common/RARP.md">RARP</a>  Reverse Address Resolution Protocol</div>
</div>
</div>
</section>
<div class="wire-row"></div>
<section class="layer">
<div class="layer-head">| [1] Physical Layer</div>
<div class="layer-body cols-4">
<div class="box">
<div class="box-title">+-- Access Network</div>
<div class="line">|-- Private line</div>
<div class="line">|   |-- <a href="./physical%20layer/access%20network/E1_E3.md">E1/E3</a></div>
<div class="line">|   `-- <a href="./physical%20layer/access%20network/T1_T3.md">T1/T3</a></div>
<div class="line">|-- Voice</div>
<div class="line">|   |-- <a href="./physical%20layer/access%20network/PSTN.md">PSTN</a></div>
<div class="line">|   |-- <a href="./physical%20layer/access%20network/ISDN.md">ISDN</a></div>
<div class="line">|   `-- <a href="./physical%20layer/access%20network/X.25.md">X.25</a></div>
<div class="line">|-- Wired</div>
<div class="line">|   |-- <a href="./physical%20layer/access%20network/Ether.md">Ether</a></div>
<div class="line">|   |-- <a href="./physical%20layer/access%20network/ADSL.md">ADSL</a></div>
<div class="line">|   `-- <a href="./physical%20layer/access%20network/EPON.md">EPON</a></div>
<div class="line">|-- Transmission</div>
<div class="line">|   |-- <a href="./physical%20layer/access%20network/SDH.md">SDH</a></div>
<div class="line">|   |-- <a href="./physical%20layer/access%20network/RPR.md">RPR</a></div>
<div class="line">|   `-- <a href="./physical%20layer/access%20network/MSTP.md">MSTP</a></div>
<div class="line">`-- Wireless</div>
<div class="line">    |-- <a href="./physical%20layer/access%20network/GPRS.md">GPRS</a></div>
<div class="line">    |-- <a href="./physical%20layer/access%20network/3G.md">3G</a></div>
<div class="line">    `-- <a href="./physical%20layer/access%20network/4G.md">4G</a></div>
</div>
<div class="box">
<div class="box-title">+-- WLAN Standard</div>
<div class="line">|-- <a href="./physical%20layer/WLAN%20standard/IEEE%20802.11b.md">802.11b</a>  2.4GHz  11Mbps</div>
<div class="line">|-- <a href="./physical%20layer/WLAN%20standard/IEEE%20802.11a.md">802.11a</a>  5.0GHz  54Mbps</div>
<div class="line">|-- <a href="./physical%20layer/WLAN%20standard/IEEE%20802.11g.md">802.11g</a>  2.4GHz  54Mbps</div>
<div class="line">|-- <a href="./physical%20layer/WLAN%20standard/IEEE%20802.11n.md">802.11n</a>  2.4/5GHz 300-600Mbps</div>
<div class="line">|-- <a href="./physical%20layer/WLAN%20standard/IEEE%20802.11ac.md">802.11ac</a> 5.0GHz  500Mbps-1Gbps</div>
<div class="line">|</div>
<div class="line">|-- <a href="./physical%20layer/WLAN%20standard/IEEE%20802.15.md">IEEE 802.15</a> Bluetooth technology</div>
<div class="line">`-- <a href="./physical%20layer/WLAN%20standard/IEEE%20802.16.md">IEEE 802.16</a> Wireless MAN</div>
</div>
<div class="box">
<div class="box-title">+-- MAN Standard</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/IEEE%20802.3ab.md">IEEE 802.3ab</a> 1000M 1000Base-T UTP</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/IEEE%20802.3ae.md">IEEE 802.3ae</a> 10G</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/10GBase-S.md">10GBase-S</a>   multimode fiber 300m</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/10GBase-L.md">10GBase-L</a>   single-mode fiber 10km</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/10GBase-E.md">10GBase-E</a>   single-mode fiber 40km</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/10GBase-LX4.md">10GBase-LX4</a> single-mode fiber 10km</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/IEEE%20802.3an.md">IEEE 802.3an</a> 10G</div>
<div class="line">|-- <a href="./physical%20layer/MAN%20standard/10GBase-T.md">10GBase-T</a>   twisted pair 100m</div>
<div class="line">`-- <a href="./physical%20layer/MAN%20standard/IEEE%20802.3ba.md">IEEE 802.3ba</a> 100G fiber</div>
</div>
<div class="box">
<div class="box-title">+-- LAN Standard</div>
<div class="line">|-- <a href="./physical%20layer/LAN%20standard/IEEE%20802.3z.md">IEEE 802.3z</a> 1000M</div>
<div class="line">|-- <a href="./physical%20layer/LAN%20standard/1000Base-SX.md">1000Base-SX</a> 550m</div>
<div class="line">|-- <a href="./physical%20layer/LAN%20standard/1000Base-LX.md">1000Base-LX</a> 5000m</div>
<div class="line">|-- <a href="./physical%20layer/LAN%20standard/1000Base-CX.md">1000Base-CX</a> 25m</div>
<div class="line">|</div>
<div class="line">|-- <a href="./physical%20layer/LAN%20standard/IEEE%20802.3u.md">IEEE 802.3u</a> 100M</div>
<div class="line">|-- <a href="./physical%20layer/LAN%20standard/100Base-TX.md">100Base-TX</a> 100m</div>
<div class="line">|-- <a href="./physical%20layer/LAN%20standard/100Base-FX.md">100Base-FX</a> 40km</div>
<div class="line">`-- <a href="./physical%20layer/LAN%20standard/100Base-T4.md">100Base-T4</a> 100m</div>
</div>
</div>
</section>
</div>
