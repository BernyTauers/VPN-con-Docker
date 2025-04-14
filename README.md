# VPN-con-Docker
Este proyecto implementa una Red Virtual Privada (VPN) utilizando Docker, configurando un entorno de red simulado tipo empresarial para prácticas de seguridad de redes. Se utiliza OpenVPN como servidor VPN y herramientas de análisis como Wireshark para capturar tráfico.

## Tecnologías utilizadas
- Docker
- OpenVPN (Imagen: `kylemanna/openvpn`)
- tcpdump
- Docker Compose 

### 1. Crear una red privada en Docker
```bash
docker network create --driver bridge --subnet 172.25.0.0/16 --gateway 172.25.0.1 mi_red_privada
