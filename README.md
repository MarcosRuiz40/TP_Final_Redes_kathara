# TP Final – Redes y Comunicación

## Imagen kathara/dhcp-quagga

### Por qué se creó

El router **RA** necesita correr dos servicios al mismo tiempo:

- **Quagga (OSPF)**, como todos los routers de la red.
- **Servidor DHCP**, porque la LAN LA toma sus IPs del DHCP que corre en su gateway (RA).

Ninguna imagen de Kathara trae las dos cosas juntas: kathara/quagga no tiene DHCP y kathara/dhcp no tiene Quagga. Por eso se creó una imagen propia que parte de kathara/quagga y le agrega isc-dhcp-server

### Cómo crearla

Antes de levantar el laboratorio, ejecutar:

```
docker build -t kathara/dhcp-quagga - <<'EOF'
FROM kathara/quagga
RUN apt-get update && apt-get install -y isc-dhcp-server && rm -rf /var/lib/apt/lists/*
EOF
```
