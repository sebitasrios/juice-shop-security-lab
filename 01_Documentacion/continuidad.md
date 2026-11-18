# Estado del laboratorio

## Topología en VirtualBox

| Interfaz de OPNsense | Red | IPv4 |
| --- | --- | --- |
| WAN (em0) | NAT de VirtualBox | 10.0.2.15/24, gateway 10.0.2.2 |
| LAN (em1) | LAB-SECUTIRY | 192.168.50.1/24 |
| juiceshop (em2) | lab-juice-shop | 192.168.60.1/24 |

## Pruebas verificadas

- OPNsense 26.7 arrancó desde el disco virtual. Parrot recibió 192.168.50.139 por DHCP, abrió el panel de OPNsense y obtuvo HTTP/2 200 al consultar example.com por HTTPS.
- Debian 13 arrancó con 192.168.60.10/24 y usa 192.168.60.1 como puerta de enlace y DNS.
- Live View registró el bloqueo DNS mientras la tabla activa del alias estaba vacía. Tras reaplicar JUICESHOP_DEBIAN, Debian resolvió deb.debian.org.
- La regla DNS permite TCP/UDP 53 desde JUICESHOP_DEBIAN hacia la IP del firewall en juiceshop. La regla HTTPS permite TCP 443 desde ese servidor hacia DEBIAN_MIRROR.
- Debian descargó 140 kB del archivo InRelease de Trixie desde deb.debian.org por HTTPS.

## Próximo paso

Configurar las fuentes de APT y verificar apt update. Después instalar Docker, desplegar Juice Shop y probar las reglas de acceso desde Parrot. Wazuh queda pendiente.
