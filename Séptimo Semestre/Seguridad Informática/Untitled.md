## Motivaciones: Amenazas de Ciberseguridad

Los ataques no son lo mismo que las amenazas. Se deben proteger los layers, datagramas, segmentos, etc. 

Se tiene TCP/IP y sus capas.

AL: Mensajes.
IL: Segmentos. 2 a la 16 TCP UDP
NL: Datagramas. IP
DEL: Frames:
PL: Bits. Ethernet card

(Incluir esquema)

La información pasa por estas capas bidireccionalmente.

Al mensaje se le añade un header de la capa de transporte (contiene los puertos de http, https, smtp o ptp de origen y de destino).

En la network layer se añaden las direcciones de origen y destino en el header.

El header dedata

El header de PL es con los bits y el ethernet.

La PC A pasa por internet (red (ISP) de redes 1969) y llega hasta B.

Para asegurar un dulce, se tiene un SKP, que es guardarlo en un bolsillo, pasarlo a alguien más (pidiendo), almacenarlo en una caja o contenerlo. Pero esto vuelve complicado obtener el dulce. En el caso de las redes, no nos es posible cerrar los puertos, sino que se deben proteger.

Tier 1 ISP 1969 (NAP)

Tier 2 pays Tier 1 

Tier 3 pays Tier 2 pays Tier 1

Local ISP passes several networks.

ISP requires: servers, routers (3 (routing), 2 (filtering), 1 layers), switches (2, 1 layers).

Data can be intercepted in the way between servers (man in the middle) via wireshark (sniffer) which is a passive attack cuz is just listening (if you dont touch the data, is undetectable).

DNS spoofing (phishing).

