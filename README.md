# VPN-con-Docker
Este proyecto implementa una Red Virtual Privada (VPN) utilizando Docker, configurando un entorno de red simulado tipo empresarial para prácticas de seguridad de redes. Se utiliza OpenVPN como servidor VPN y herramientas de análisis como Wireshark para capturar tráfico.

## Tecnologías utilizadas
- Docker
- OpenVPN (Imagen: `kylemanna/openvpn`)
- tcpdump
- Docker Compose
- Duck DNS

### 1. Crear una red privada en Docker
Se opta por utilizar la direccion 192.168.10.0/24 dado que esta diseñado para un uso moderado de hosts/contenedores
```bash
docker network create --driver bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 red_privada
```

### 2. Crear un directorio de Open Vpn
Al ser una configuracion manual de open vpn, se deberan de guardar los certificados y archivos de configuracion de vpn en una carpeta, en mi caso lo hice dentro del directorio /Documents.
```bash
mkdir openvpn_data
```
### 3. Generar archivos de configuracion dentro de la carpeta creada
```bash
docker run -v $(pwd)/openvpn-data:/etc/openvpn kylemanna/openvpn ovpn_genconfig -u udp http://turipdownfall.duckdns.org
```
docker run : iniciar un contenedor a partir de una imagen
-v : crear un volumen tipo bind mount, un volumen es un archivo que va a persistir aun que el contenedor se haya eliminado o deje de correr \n /n
$(pwd)/openvpn-data:/etc/openvpn : Se tiene considerado estar dentro de la carpeta de /Documents ya que pwd da la direccion actual y openvpn-data esta dentro de /Documents pero esta parte del comando enlaza el directorio señalado de la maquina local hacia (:) un directorio en el contenedor, se elije /etc ya que seran en su mayoria configuraciones y certificados
kylemanna/openvpn ovpn_genconfig: la imagen y una configuracion (documentacion)
-u : Se indica que se proveera un link
udp http://turipdownfall.duckdns.org : Se utilizo DuckDNS para obtenerun dominio gratuito por medio del protocolo udp.

### 4. 
```bash
docker run -v $(pwd)/openvpn-data:/etc/openvpn --rm -it kylemanna/openvpn ovpn_initpki
```
## Referencias
https://hub.docker.com/r/kylemanna/openvpn
