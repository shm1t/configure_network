# configure_network

<code>Базовые настройки перед конфигурированием:</code>  
configure terminal  
no ip domain-lookup  
line console 0  
logging synchronous  
exec-timeout 0 0  


Base NAT route-map  

ip access-list standard NAT  
 permit 192.168.100.0 0.0.0.255  
 permit 172.16.100.0 0.0.0.255  
 exit  
  
ip access-list standard NAT  
 permit 192.168.200.0 0.0.0.255  
 permit 172.16.200.0 0.0.0.255  
 exit  
   
route-map NAT-Gi01 permit 10  
 match ip address NAT  
 match interface GigabitEthernet0/1  
 exit  
    
route-map NAT-Gi00 permit 10  
 match ip address NAT  
 match interface GigabitEthernet0/0  
 exit  
    
ip nat inside source route-map NAT-Gi01 interface gigabitEthernet 0/1 overload  
ip nat inside source route-map NAT-Gi00 interface gigabitEthernet 0/0 overload  
  
interface gigabitEthernet 0/1  
ip nat outside  
exit  
  
interface gigabitEthernet 0/2  
ip nat inside  
exit  
  
Base IP SLA configuration  
  
ip sla 1  
icmp-echo 50.50.50.2 source-ip 100.100.100.2  
frequency 5  
exit  
  
ip sla schedule 1 life forever start-time now  

track 100 ip sla 1  
delay down 15 up 10  
exit

ip sla 2
icmp-echo 10.10.10.2 source-ip 200.200.200.2
frequency 5
exit

ip sla schedule 2 life forever start-time now

track 200 ip sla 2
delay down 15 up 10
exit





