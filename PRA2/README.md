
# Redes de Computadoras 1

 ## Manual Práctica 2

 Autores:  
  :pencil: Rosa Emilia Boche Naz - 200915633  
:pencil:    Alberto Gabriel Reyes Ning - 201612174  

 ## INTRODUCCIÓN 
 La configuración de enrutamiento entre redes es una habilidad esencial en el mundo de las tecnologías de la información y las comunicaciones. Los administradores de redes y profesionales de TI deben comprender los conceptos y técnicas relacionados con la agregación de enlaces, la creación de rutas estáticas, la gestión de la puerta de enlace predeterminada y la implementación de protocolos de redundancia. Estas habilidades son cruciales para garantizar un funcionamiento eficiente y confiable de las redes, especialmente en entornos empresariales donde la conectividad ininterrumpida es fundamental.

    
## OBJETIVOS

Demostrar Conocimiento en Agregación de Enlaces: El estudiante deberá mostrar su comprensión de cómo agregar enlaces para aumentar el ancho de banda y la redundancia en una red. Esto implica configurar correctamente la agregación de enlaces en dispositivos de red.

 

#  CONTENIDO DE PRÁCTICA

  ## TABLAS DE DIRECCIÓN 

 | DISPOSITIVO |INTERFAZ  |IP|MÁSCARA DE SUBRED
|---|---|---|--
| CENTRAL  |S1/0|10.0.0.1|/30  
|  |  e0/0|138.168.1.2|/29
|  |  e0/1 |138.168.2.2|/29   
| R2 |  e0/0  |138.168.1.1|/29   
| | e0/1| 138.138.0.3|/24
| R2-R3 |virtual  |138.168.0.1|/24
 | VPC11 |eth0  |138.168.0.4|/24
 | VILLA NUEVA |S1/0|10.0.02|/30
 |  |e0/0|138.178.1.1|/29
 |  |e0/1|138.178.2.1|/29
 |R5  |e0/0|138.178.1.2|/29
 |  |e0/1|138.178.0.2|/24
 | R6 |e0/0|138.178.2.2|/29
 |  |e0/1|138.178.0.3|/24
 |R5-R6  |Virtual|138.178.0.1|/24
 | VPC12 |eth0/0|138.178.0.4|/24


 ## TABLAS DE RANGOS 
 
| ID RED |Interfaz|Dirección Ip|Máscara de Subred|Total de Direcciones  | Primera IP Disponible| Última IP Disponible| Dirección de Broadcast
|--|--|--|--|--|--|--|-
| CENTRAL | s1/0 |10.0.0.1| /30 | 10.0.0.0 |10.0.0.1|10.0.0.2|10.0.0.3
CENTRAL	|e0/0|	138.168.1.2	|/29|	138.168.1.0|	138.168.1.1	|138.168.1.6	|138.168.1.7
CENTRAL|	e0/1|	138.168.2.2	|/29|138.168.2.0 |138.168.2.1|	138.168.2.6|	138.168.2.7
R2	|e0/0	|138.168.1.1	|/29|	138.168.1.0	|138.168.1.1|	138.168.1.6	|138.168.1.7
R2	|e0/1|	138.168.0.3|	/24	|138.168.0.0|	138.168.0.1	|138.168.0.254|	138.168.0.255
R2-R3 (Virtual)|	-	|138.168.0.1|	/24|	138.168.0.0	|138.168.0.1|	138.168.0.254	|138.168.0.255
VPC11|	eth0|	138.168.0.4	|/24	|138.168.0.0	|138.168.0.1	|138.168.0.254|	138.168.0.255
VILLA NUEVA|	S1/0|	10.0.0.2|	/30|	10.0.0.0|	10.0.0.1|	10.0.0.2|	10.0.0.3
VILLA NUEVA	|e0/0|	138.178.1.1	|/29|	138.178.1.0	|138.178.1.1|	138.178.1.6|	138.178.1.7
VILLA NUEVA|	e0/1|	138.178.2.1|	/29|	138.178.2.0	|138.178.2.1|	138.178.2.6	|138.178.2.7
R5	|e0/0|	138.178.1.2	|/29|	138.178.1.0|	138.178.1.1	|138.178.1.6	|138.178.1.7
R5	|e0/1|	138.178.0.2	|/24|	138.178.0.0	|138.178.0.1|	138.178.0.254|	138.178.0.255
R6	|e0/0|	138.178.2.2|	/29	|138.178.2.0|	138.178.2.1	|138.178.2.6|	138.178.2.7
R6	|e0/1|	138.178.0.3	|/24|	138.178.0.0	|138.178.0.1|	138.178.0.254	|138.178.0.255
R5-R6 (Virtual)|	-|	138.178.0.1	|/24	|138.178.0.0|	138.178.0.1	|138.178.0.254|	138.178.0.255
VPC12	|eth0/0|	138.178.0.4	|/24|	138.178.0.0	|138.178.0.1|	138.178.0.254|	138.178.0.255


# Configuración de Routers 
## ROUTER CENTRAL

  >- conf t
   >- interface s1/0
   >- ip address 10.0.0.1 255.255.255.252
   >- no shutdown 
   >- do write
   >- interface e0/0
   >- ip address 138.168.1.2 255.255.255.248
   > - no shutdown
   > - do write
   > - interface e0/1
   > - ip address 138.168.2.2 255.255.255.248
   > - no shutdown
   > - do write

## ROUTER R2
>- conf t
>- interface e0/0
>- ip address 138.168.1.1 255.255.255.248
>- no shutdown
>- do write
>- interface e0/1
>- ip address 138.168.0.2 255.255.255.0
>- no shutdown
>- do write



## ROUTER R5

>-conf t
>- interface e0/0
>- ip address 138.178.1.2 255.255.255.248
>- no shutdown
>- do write
>- interface e0/1
>- ip address 138.178.0.2 255.255.255.0
>- no shutdown
>- do write
>- standby version 2
>- standby 21 ip 138.178.0.1
>- standby 21 preempt
>- do write
>- show standby


## SWITCH SW7
>- conf t
>- interface range e0/0-1
>- channel-group 2 mode passive
>- no shutdown
>- do write
>
## VPC11
>- ip 138.168.0.4/24 138.168.0.1
>- save


# CONFIGURACIÓN DE RUTAS ESTÁTICAS

## CENTRAL
>- conf t
>- ip route 138.168.0.0 255.255.255.0 138.168.1.1
>- ip route 138.168.0.0 255.255.255.0 138.168.2.1
>- ip route 138.178.0.0 255.255.255.0 10.0.0.2
>- ip route 138.178.1.0 255.255.255.248 10.0.0.2
>- ip route 138.178.2.0 255.255.255.248 10.0.0.2
>- do write

## R2
>- conf t
>- ip route 10.0.0.0 255.255.255.252 138.168.1.2
>- ip route 138.168.1.0 255.255.255.248 138.168.1.2
>- ip route 138.178.0.0 255.255.255.0 138.168.1.2
>- ip route 138.178.1.0 255.255.255.248 138.168.1.2
>- ip route 138.178.2.0 255.255.255.248 138.168.1.2
>- do write

## R3
>- conf t
>- ip route 10.0.0.0 255.255.255.252 138.168.2.2
>- ip route 138.168.2.0 255.255.255.248 138.168.2.2
>- ip route 138.178.0.0 255.255.255.0 138.168.2.2
>- ip route 138.178.1.0 255.255.255.248 138.168.2.2
>- ip route 138.178.2.0 255.255.255.0 138.168.2.2
>

## VILLA NUEVA
>- conf t
>- ip route 138.168.0.0 255.255.255.0 10.0.0.1
>- ip route 138.168.1.0 255.255.255.0 10.0.0.1
>- ip route 138.168.2.0 255.255.255.0 10.0.0.1
>- ip route 138.178.0.0 255.255.255.0 138.178.1.2
>- ip route 138.178.0.0 255.255.255.0 138.178.2.2
> - ip route 138.178.1.0 255.255.255.248 138.178.1.2
> -ip route 138.178.2.0 255.255.255.248 138.178.2.2
>- do write

## R5
>- conf t
>- ip route 10.0.0.0 255.255.255.252 138.178.1.1
>- ip route 138.168.0.0 255.255.255.0 138.178.1.1
>- ip route 138.168.1.0 255.255.255.248 138.178.1.1
>- ip route 138.168.2.0 255.255.255.248 138.178.1.1
>- do write

## R6
>- conf t
> - ip route 10.0.0.0 255.255.255.252 138.178.2.1
>- ip route 138.168.0.0 255.255.255.0 138.178.2.1
>- ip route 138.168.1.0 255.255.255.248 138.178.2.1
>- ip route 138.168.2.0 255.255.255.248 138.178.2.1
>- do write

##  Creación de PortChannel con PAGP
 ### SW8
 >- conf t
>- interface range e0/2-3
>- channel-group 2 mode active
>- no shutdown
>- do write
>- do show etherchannel summary

 ## Creación de PortChannel con LACP
 ### SW9
 >- conf t
>- interface range e0/2-3
>- channel-group 1 mode desirable
>- no shutdown
>- do write
>- do show etherchannel summary

### SW10
>- conf t
>- interface range e0/0-1
>- channel-group 1 mode auto
> - no shutdown
>- do write

## Configuración de IP virtual con HSRP

## R2
>- glbp 7 ip 138.168.0.1
>- glbp 7 preempt
>- glbp 7 priority 150
>- do write
>- show glbp brief

## R3
>- glbp 7 ip 138.168.0.1
>- glbp 7 load-balancing round-robin
>- do write
>- show glbp brief

## CONFIGURACIÓN VPC 12

>- ip 138.178.0.4/24 138.178.0.1
>- save
# COMANDOS PARA VALIDAR FUNCIONAMIENTO

>- PING
>- show running-config | section ip route
> - do show glbp
> - do show lacp

