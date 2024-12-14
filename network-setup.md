In this docuent I will mark down all my network devices that I created in task 1:
----------------------------------------------------------------------------------
|  NAME   |  Type  |   Model   | IP Address |
|---------|--------|-----------|------------|
| Router2 | Router |    1941   |------------|
| Switch1 | Switch | 2960-24TT | 168.90.0.1 |
| Server2 | Server | Server-PT | 168.90.0.2 |
|   PC0   |   PC   |   PC-PT   | 168.90.0.3 |
| Laptop0 | Laptop | Laptop-PT | 168.90.0.4 |
|   PC1   |   PC   |   PC-PT   | 168.90.0.5 |
|   PC3   |   PC   |   PC-PT   | 168.90.0.6 |
| Switch0 | Switch | 2960-24TT | 210.3.14.1 |
| Server0 | Server | Server-PT | 210.3.14.2 |
|   PC2   |   PC   |   PC-PT   | 210.3.14.3 |
| Server1 | Server | Server-PT | 210.3.14.4 |
|   PC4   |   PC   |   PC-PT   | 210.3.14.5 |


for the DHCP comands I first typed enable to go to the priviledge EXEC mode and then configer terminal to make it into a global configuration in the CLC area
I made the interface of each pools which are for the switch0(as second switch) and switch1 (as first switch):

! Interface for the first switch network
interface gigabitEthernet0/0 
(as the first switch switch1, the 0/0 is the ethernet network port that is conected from the router to the switch)
ip address 168.90.0.1 255.255.0.0 
(the first one is the ip address for the interface going on also called the default gateway for the devices connected to the other network and the second one is the subnet mask that allows nearly 65,000+ ip addresses in the network ip address)
no shutdown 
(activates the interface thing)

! Interface for the second switch network
interface gigabitEthernet0/1
(as the second switch switch0, the 0/1 is the ethernet network port that is conected from the router to the switch)
ip address 210.3.14.1 255.255.255.0 
(the first one is the ip address for the interface going on also called the default gateway for the devices connected to the other network and the second one is the subnet mask that allows nearly 65,000+ ip addresses in the network ip address)
no shutdown 
(activates the interface thing)
------------------------------------------------------------------
the first was to create the interfaces now for the DHCP's to be able to automaticaly assign the ip adresses for the devices in each network
------------------------------------------------------------------
the second thing I did:
! DHCP pool for the first switch 
ip dhcp pool FirstSwitch
(create a DHCP pool called firstswitch)
network 168.90.0.0 255.255.0.0
(this is just the configuration for the pool just as stated before the first is the ip addresss and second is the subnet mask which will allow the divices to use the ip address in the range of 168.90.0.1 till .254)
default-router 168.90.0.1
(the router will take 168.90.0.1 so the other divices wil take from .2 till needed max .254, but mainly this will allow the devices to comunicate through the router interface as a gateway to other networks)

! DHCP pool for the second switch
ip dhcp pool SecondSwitch
(create a DHCP pool called  secondswitch)
network 210.3.14.0 255.255.255.0
(this is just the configuration for the pool just as stated before the first is the ip addresss and second is the subnet mask which will allow the divices to use the ip address in the range of 210.3.14.1 till .254)
default-router 210.3.14.1 
(the router will take 210.3.14.1 so the other divices wil take from .2 till needed max .254, but mainly this will allow the devices to comunicate through the router interface as a gateway to other networks)
exit
(the exit is here to just to exit the DHCP config and go back to the global config mode)
------------------------------------------------------------------------
after all of this I went to each device desktop and into the ip configuration I switched it from static to DHCP so i can get an automaticaly made IPV4 address like 168.90.0.3, the .3 states the exact device address which help in uniqely identifying the devices so you can know to which other device you will communicate (I did this switching across all the devices on the network)
------------------------------------------------------------------------
