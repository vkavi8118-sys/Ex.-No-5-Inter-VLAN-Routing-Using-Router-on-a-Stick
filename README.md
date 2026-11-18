# Ex. No: 5 Inter-VLAN Routing Using Router-on-a-Stick
# Date:18.11.2026
________________________________________
# Objective
To configure Inter-VLAN routing using a single router interface with subinterfaces (Router-on-a-Stick) so that hosts in different VLANs can communicate with each other.
________________________________________
# Apparatus/Tools Required
•	Cisco Packet Tracer<br>
•	1 Router (e.g., 2911)<br>
•	1 Managed Switch (e.g., 2960)<br>
•	4 PCs<br>
•	Straight-through Ethernet cables<br>
________________________________________
# Network Topology Diagram
# Description:
•	PC0 and PC1 belong to VLAN 10 (192.168.10.0/24)<br>
•	PC2 and PC3 belong to VLAN 20 (192.168.20.0/24)<br>
•	Switch connected to Router via a trunk port (FastEthernet0/1 on switch → GigabitEthernet0/0 on router)<br>
•	Router subinterfaces handle VLAN routing<br>
(Insert screenshot of your Packet Tracer setup here)<br>
<img width="772" height="527" alt="Screenshot 2026-11-18 180200" src="https://github.com/user-attachments/assets/cdfcd9d6-aff6-4bad-993d-f27d5f369c5b" />
_______________________
# IP Addressing Table
Device	VLAN	IP Address	Subnet Mask	Port/Interface<br>
PC0	10	192.168.10.1	255.255.255.0	FastEthernet0/1<br>
PC1	10	192.168.10.2	255.255.255.0	FastEthernet0/2<br>
PC2	20	192.168.20.1	255.255.255.0	FastEthernet0/3<br>
PC3	20	192.168.20.2	255.255.255.0	FastEthernet0/4<br>
Router G0/0.10	10	192.168.10.254	255.255.255.0	Subinterface VLAN 10<br>
Router G0/0.20	20	192.168.20.254	255.255.255.0	Subinterface VLAN 20<br>
________________________________________
# Procedure
1.	Setup devices in Packet Tracer: Place 4 PCs, 1 switch, and 1 router.<br>
2.	Cabling:<br>
o	PCs to switch ports (PC0–F0/1, PC1–F0/2, PC2–F0/3, PC3–F0/4)<br>
o	Switch F0/5 to Router G0/0<br>
3.	Assign IP addresses to each PC as per the IP table.<br>
4.	Switch Configuration:<br>
o	Create VLAN 10 and VLAN 20<br>
o	Assign ports F0/1–F0/2 to VLAN 10, ports F0/3–F0/4 to VLAN 20<br>
o	Configure trunk on port F0/5 to the router<br>
5.	Router Configuration (Router-on-a-Stick):<br>
o	Enable subinterfaces G0/0.10 and G0/0.20<br>
o	Assign encapsulation dot1q for each VLAN ID<br>
o	Assign IP addresses to each subinterface (default gateway for respective VLANs)<br>
6.	Testing:<br>
o	Ping from PC0 to PC2 (should succeed after routing is configured)<br>
o	Ping between PCs in the same VLAN (should succeed)<br>
________________________________________
# Commands Used
Switch Configuration:<br>
python<br>
CopyEdit<br>
Switch> enable<br>
Switch# configure terminal<br>
Switch(config)# vlan 10<br>
Switch(config-vlan)# name STAFF<br>
Switch(config-vlan)# exit<br>
Switch(config)# vlan 20<br>
Switch(config-vlan)# name STUDENTS<br>
Switch(config-vlan)# exit<br>
Switch(config)# interface range fastethernet0/1 - 2<br>
Switch(config-if-range)# switchport mode access<br>
Switch(config-if-range)# switchport access vlan 10<br>
Switch(config-if-range)# exit<br>
Switch(config)# interface range fastethernet0/3 - 4<br>
Switch(config-if-range)# switchport mode access<br>
Switch(config-if-range)# switchport access vlan 20<br>
Switch(config-if-range)# exit<br>
Switch(config)# interface fastethernet0/5<br>
Switch(config-if)# switchport mode trunk<br>
Switch(config-if)# exit<br>
Router Configuration:<br>
arduino<br>
CopyEdit<br>
Router> enable<br>
Router# configure terminal<br>
Router(config)# interface gigabitethernet0/0.10<br>
Router(config-subif)# encapsulation dot1Q 10<br>
Router(config-subif)# ip address 192.168.10.254 255.255.255.0<br>
Router(config-subif)# no shutdown<br>
Router(config)# interface gigabitethernet0/0.20<br>
Router(config-subif)# encapsulation dot1Q 20<br>
Router(config-subif)# ip address 192.168.20.254 255.255.255.0<br>
Router(config-subif)# no shutdown<br>
Router(config)# interface gigabitethernet0/0<br>
Router(config-if)# no shutdown<br>
________________________________________
# Output (Screenshots)
•	VLAN configuration on the switch<br>
<img width="1920" height="1080" alt="Screenshot (260)" src="https://github.com/user-attachments/assets/f5f81fcf-bf12-46e1-958a-f0525aa62e0c" />

•	Router subinterface configuration<br>
<img width="1920" height="1080" alt="Screenshot (261)" src="https://github.com/user-attachments/assets/89d11e30-ff2e-4d85-9004-56217239267f" />

•	PC IP settings<br>
<img width="1920" height="1080" alt="Screenshot (262)" src="https://github.com/user-attachments/assets/845adfb6-6bcd-4679-9baf-4a458a77d995" />
<img width="1920" height="1080" alt="Screenshot (263)" src="https://github.com/user-attachments/assets/faf27284-691b-491c-80f5-504c1530877e" />
<img width="1920" height="1080" alt="Screenshot (264)" src="https://github.com/user-attachments/assets/571617c3-9004-40d5-b796-a1a476d2cf9d" />
<img width="1920" height="1080" alt="Screenshot (265)" src="https://github.com/user-attachments/assets/3a9c8973-10b9-4c27-976a-fc307afd155e" />


•	Successful ping between PCs in different VLANs after routing<br>
•	Successful ping between PCs in the same VLAN<br>
<img width="1920" height="1080" alt="Screenshot (259)" src="https://github.com/user-attachments/assets/4baa7b75-e51f-4907-8ec6-ffcf2af8e180" />

________________________________________
# Result
Inter-VLAN routing was successfully configured using the Router-on-a-Stick method. PCs in different VLANs could communicate through the router.

