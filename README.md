# 🔐 Lab 06 — GRE sobre IPSec + IKEv2

**Estudiante:** Enmanuel Feliz Soto | **Matrícula:** 2025-1402  
**Institución:** Instituto Tecnológico de Las Américas (ITLA)  
**Curso:** Seguridad en Redes | **Sección:** 2-1C  
**Docente:** Jonathan Esteban Rondón Corniel

---

## 📋 Descripción

GRE sobre IPSec con IKEv2. Evolución del Lab03 usando el protocolo de negociación más moderno.

| Campo | Valor |
|-------|-------|
| **Tipo de VPN** | Site-to-Site |
| **Protocolo** | IKEv2 + IPSec ESP-AES256-SHA256 + GRE |
| **Mecanismo** | Túnel GRE + IKEv2 Profile + tunnel protection |
| **Routing** | Rutas estáticas sobre Tunnel0 GRE |
| **Pre-shared Key** | `Cisco2025-1402-GRE-V2!` |

---

## 🗺️ Topología

> 📸 <img width="1472" height="805" alt="Captura de pantalla 2026-06-21 154657" src="https://github.com/user-attachments/assets/1779a99f-a845-4feb-b5bb-e5120228d31e" />


<!-- Coloca aquí el screenshot de PNetLab con la topología del Lab 06 -->

**Entorno:** PNetLab — Cisco IOL  
**Peers:** R1-S1 (20.25.6.2) ↔ R4-S2 (20.25.6.6)

### Tabla de Direccionamiento

| Router | Rol | IP WAN | Interfaz WAN | IP LAN | Interfaz LAN |
|--------|-----|--------|--------------|--------|--------------|
| ISP | ENLACE / INTERMEDIARIO | 20.25.1.2 | Ethernet0/0 | -- | -- |
| R3 | Peer 1 / INICIADOR | 20.25.2.6 | Ethernet0/0 | 30.30.30.1/24 | Ethernet0/1 |

### ISP

| **Interfaz ISP** | **IP** | **Descripción** | | **Rol** |
|-------------|-----|-------------|-------------|---------|
| Ethernet0/0 | 20.25.1.1/30 | Link to R1-S1 | | **RESPONDEDOR** |

### Dirección Túnel
| Endpoint | IP Tunnel |
|----------|-----------|
| R3 Tunnel0 | 14.2.10.1/30 |
| ISP Tunnel0 | 14.2.10.2/30 |

---

## ⚙️ Configuración

El script completo de configuración se encuentra en:  
📄 [`EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv2_P3.txt`](./EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv2_P3.txt)

### Parámetros IKE/IPSec

| Parámetro | Valor |
|-----------|-------|
| Encryption | AES-256 |
| Hash/Integrity | SHA-256 |
| DH Group | 14 (2048-bit) |
| SA Lifetime (IKE) | 86400 s (24h) |
| SA Lifetime (IPSec) | 3600 s (1h) |
| PFS | Group 14 |
| Auth Method | Pre-Shared Key |

---

## ▶️ Procedimiento de Ejecución

### 1. Cargar configuración en PNetLab
```
# Aplicar configuración en cada dispositivo en el orden:
# 1. ISP → 2. R1-S1 → 3. R4-S2 → 4. R2/Server
```

### 2. Verificar la VPN

```
show crypto ikev2 sa
```
```
show crypto ipsec sa
```
```
show interface Tunnel0
```

### 3. Prueba de conectividad
```
ping 10.14.25.10 source 10.14.15.2
```

---

## 📸 Capturas de Verificación

> 📸 <img width="726" height="150" alt="image" src="https://github.com/user-attachments/assets/e9dc6550-cec2-4e18-a85d-658b83e8f816" />


<!-- Captura mostrando el estado QM_IDLE / ESTABLISHED -->

> 📸 <img width="637" height="372" alt="image" src="https://github.com/user-attachments/assets/ebeb4b9c-e07e-47f3-802e-adc5974f76f2" />


<!-- Captura mostrando pkts encaps/decaps incrementando -->

> 📸 <img width="710" height="259" alt="image" src="https://github.com/user-attachments/assets/7f2ff8b9-9735-48c6-9b72-8f2db6ebb3cc" />


<!-- Captura del ping source 10.14.15.0/24 -->

---

## 🔍 Análisis y Comparativa

### Ventajas de este tipo de VPN
- Ver documentación técnica en el informe PDF

### Diferencias con otros labs
- Ver tabla comparativa en el README principal

---

## 📎 Recursos

| Recurso | Enlace |
|---------|--------|
| Repositorio Principal | [Enmafs/NetSec](https://github.com/Enmafs/NetSec) |
| Script de configuración | [`EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv2_P3.txt`](./EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv2_P3.txt) |
| Video demostración | 🎬 [Aquí](https://youtu.be/G_8rjwIpjy4) |

---

> ⚠️ *Laboratorio realizado en entorno controlado (PNetLab). Fines exclusivamente académicos.*
