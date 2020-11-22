# Manual de Comandos
## ESW 
## IP
## Trunk

<pre>
	<code>
	conf t
	int range f1/0 - 9
	switchport mode trunk
	end
	wr
	</code>
</pre>

## vlans


<pre>
	<code>
conf t
ip routing
!
vlan 27
name RED1
exit
!
vlan 37
name RED2
exit
!
vlan 47
name RED3
exit
!
vlan 57
name RED4
exit
!
end
wr

</code>
</pre>

## Distribucion 1

<pre>
	<code>
conf t
!
interface vlan 27
ip address 192.168.10.40 255.255.255.0
standby 12 ip 192.168.10.254
standby 12 priority 200
standby 12 preempt
!
interface vlan 37
ip address 192.168.20.40 255.255.255.0
standby 22 ip 192.168.20.254
standby 22 priority 200
standby 22 preempt
!
interface vlan 47
ip address 192.168.30.40 255.255.255.0
standby 32 ip 192.168.30.254
standby 32 priority 200
standby 32 preempt
!
interface vlan 57
ip address 192.168.40.40 255.255.255.0
standby 42 ip 192.168.40.254
standby 42 priority 200
standby 42 preempt
!
end
wr
</code>
</pre>

## Distribucion 2

<pre>
	<code>
conf t
!
interface vlan 27
ip address 192.168.10.41 255.255.255.0
standby 12 ip 192.168.10.254
standby 12 priority 200
standby 12 preempt
!
interface vlan 37
ip address 192.168.20.41 255.255.255.0
standby 22 ip 192.168.20.254
standby 22 priority 200
standby 22 preempt
!
interface vlan 47
ip address 192.168.30.41 255.255.255.0
standby 32 ip 192.168.30.254
standby 32 priority 200
standby 32 preempt
!
interface vlan 57
ip address 192.168.40.41 255.255.255.0
standby 42 ip 192.168.40.254
standby 42 priority 200
standby 42 preempt
!
end
wr
</code>
</pre>

## Distribucion 1


<pre>
	<code>
conf t
vtp domain T1Grupo17
vtp password T1Grupo17
vtp mode server
end
wr
</pre>
</code>

## Distribucion 2
<pre>
	<code>
conf t
vtp domain T1Grupo17
vtp password T1Grupo17
vtp mode client
end
wr

SH VLAN-SW
sh vtp status

</code>
</pre>

## Port Channel

(se hace en ambos switches)

ESW1 - ESW2
<pre>
	<code>
conf t
int range f1/1 - 4
channel-group 1 mode on
end
wr
	</code>
</pre>

## Asignando IPs
## Distribucion 1
<pre>
	<code>
conf t
int f1/0
no switchport
ip address 27.0.0.2 255.0.0.0
no shu
exit
int f1/9
no switchport
ip address 37.0.0.2 255.0.0.0
no shu
end
wr
</code>
</pre>

## Distribucion 2
<pre>
	<code>
conf t
int f1/0
no switchport
ip address 57.0.0.2 255.0.0.0
no shu
exit
int f1/9
no switchport
ip address 47.0.0.2 255.0.0.0
no shu
end
wr
</code>
</pre>


## Router 1
<pre>
	<code>
conf t
int s0/0
ip address 67.0.0.1 255.0.0.0
no shu
exit
int s0/1
ip address 77.0.0.1 255.0.0.0
no shu
exit
int f0/0
ip address 80.0.0.1 255.0.0.0
no shu
end
wr
</code>
</pre>

## Distribucion 1
<pre>
	<code>
conf t
int s0/0
ip address 67.0.0.2 255.0.0.0
no shu
exit
int f0/0
ip address 27.0.0.1 255.0.0.0
no shu
exit
int f0/1
ip address 47.0.0.1 255.0.0.0
no shu
end
wr
</code>
</pre>

## Nucleo 2
<pre>
	<code>
conf t
int s0/1
ip address 77.0.0.2 255.0.0.0
no shu
exit
int f0/0
ip address 57.0.0.1 255.0.0.0
no shu
exit
int f0/1
ip address 37.0.0.1 255.0.0.0
no shu
end
wr
</code>
</pre>

## Protocolo RIP
<pre>
	<code>
conf t
router rip
version 2
network 80.0.0.0
network 67.0.0.0
network 77.0.0.0
end
wr
</code>
</pre>

## Nucleo 1
<pre>
	<code>
conf t
router rip
version 2
network 27.0.0.0
network 67.0.0.0
network 47.0.0.0
end
wr
</code>
</pre>

## Nucleo 2
<pre>
	<code>
conf t
router rip
version 2
network 37.0.0.0
network 57.0.0.0
network 77.0.0.0
end
wr
</code>
</pre>

## Router 1
<pre>
	<code>
!
conf t
ip classless
ip route 0.0.0.0 0.0.0.0 67.0.0.2
ip route 0.0.0.0 0.0.0.0 77.0.0.2
ip route 192.168.22.0 255.255.255.0 67.0.0.1 
ip route 192.168.12.0 255.255.255.0 67.0.0.1 
ip route 192.168.32.0 255.255.255.0 67.0.0.1 
ip route 192.168.42.0 255.255.255.0 67.0.0.1 
ip route 192.168.12.0 255.255.255.0 77.0.0.1 
ip route 192.168.22.0 255.255.255.0 77.0.0.1 
ip route 192.168.32.0 255.255.255.0 77.0.0.1 
ip route 192.168.42.0 255.255.255.0 77.0.0.1 
ip route 27.0.0.0 255.0.0.0 67.0.0.1 
ip route 57.0.0.0 255.0.0.0 77.0.0.1
end
wr
</code>
</pre>

## Nucleo 1
<pre>
	<code>
ip classless
ip route 192.168.12.0 255.255.255.0 27.0.0.1 
ip route 192.168.22.0 255.255.255.0 27.0.0.1 
ip route 192.168.32.0 255.255.255.0 27.0.0.1 
ip route 192.168.42.0 255.255.255.0 27.0.0.1 
ip route 192.168.12.0 255.255.255.0 47.0.0.1 
ip route 192.168.22.0 255.255.255.0 47.0.0.1 
ip route 192.168.32.0 255.255.255.0 47.0.0.1 
ip route 192.168.42.0 255.255.255.0 47.0.0.1 
ip route 192.168.50.0 255.255.255.0 67.0.0.2
ip route 80.0.0.0 255.0.0.0 67.0.0.2
ip route 70.0.67.0 255.255.255.0 67.0.0.2
ip route 70.0.77.0 255.255.255.0 67.0.0.2
</code>
</pre>

