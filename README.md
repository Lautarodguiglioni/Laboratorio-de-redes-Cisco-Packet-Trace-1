# Laboratorio de redes — Packet Tracer

Práctica de subneteo, configuración de routers y rutas estáticas en Cisco Packet Tracer.

## Topología

- **R1** conecta LAN A con R2.
- **R2** conecta LAN B con R1.
- **R3** conecta LAN B con LAN C.
- En LAN B, R2 y R3 comparten el switch SB.

## Direccionamiento

| Segmento | Red / máscara | IP de router | Equipo de prueba | Gateway |
|---|---|---|---|---|
| LAN A | `172.16.0.0/19` · `255.255.224.0` | R1: `172.16.0.1` | PC-A: `172.16.0.10` | `172.16.0.1` |
| LAN B | `172.16.32.0/19` · `255.255.224.0` | R2: `172.16.32.1`; R3: `172.16.32.2` | PC-B: `172.16.32.10` | `172.16.32.1` |
| LAN C | `172.16.64.0/19` · `255.255.224.0` | R3: `172.16.64.1` | PC-C: `172.16.64.10` | `172.16.64.1` |
| Enlace R1–R2 | `10.0.0.0/30` · `255.255.255.252` | R1: `10.0.0.1`; R2: `10.0.0.2` | — | — |

Las LAN usan `/19` para admitir hasta 8190 direcciones de host. El enlace punto a punto usa `/30`, con dos direcciones utilizables.

## Rutas estáticas

```text
R1
ip route 172.16.32.0 255.255.224.0 10.0.0.2
ip route 172.16.64.0 255.255.224.0 10.0.0.2

R2
ip route 172.16.0.0 255.255.224.0 10.0.0.1
ip route 172.16.64.0 255.255.224.0 172.16.32.2

R3
ip route 172.16.0.0 255.255.224.0 172.16.32.1
```

## Verificación

Se revisaron las interfaces con `show ip interface brief` y las rutas con `show ip route`. Las interfaces utilizadas quedaron `up/up`.

Desde PC-A, el ping al gateway `172.16.0.1` respondió 4/4. El ping a PC-B (`172.16.32.10`) respondió 4/4 al repetirlo. El primer intento tuvo pérdidas parciales, por lo que se repitió la prueba.

## Archivos

- `Laboratorio_3LAN_3ROUTERS.pkt`: simulación editable en Cisco Packet Tracer.
- `Informe-Actividad-TD3.pdf`: informe de la práctica.

## Abrir la práctica

1. Descargá el archivo `.pkt`.
2. Abrilo con Cisco Packet Tracer.
3. Usá los comandos `show ip interface brief` y `show ip route` para revisar la configuración.
