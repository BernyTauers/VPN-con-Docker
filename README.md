# VPN-con-Docker
Este proyecto implementa una Red Virtual Privada (VPN) utilizando Docker, configurando un entorno de red simulado tipo empresarial para prácticas de seguridad de redes. Se utiliza OpenVPN como servidor VPN y herramientas de análisis como Wireshark para capturar tráfico.

## Tecnologías utilizadas
- Docker
- OpenVPN (Imagen: `kylemanna/openvpn`)
- tcpdump
- Docker Compose 

### 1. Crear una red privada en Docker
Se opta por utilizar la direccion 192.168.10.0/24 dado que no se tiene pensado una cantidad grande de hosts
```bash
docker network create --driver bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 red_privada
