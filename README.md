# configure_network

<code>Базовые настройки перед конфигурированием:</code>  
configure terminal  
no ip domain-lookup  
line console 0  
logging synchronous  
exec-timeout 0 0  


Base NAT route-map

route-map NAT-Gi01 permit 10
 match ip address NAT-Gi01
 match interface GigabitEthernet0/1
 exit
 


ip nat inside source route-map NAT-Gi01 interface gigabitEthernet 0/1 overload

interface gigabitEthernet 0/1
ip nat outside
exit

interface gigabitEthernet 0/2
ip nat inside
exit

