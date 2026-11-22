# 🛡️ Laboratorio de Infraestructura y Seguridad

Entorno de virtualización y simulación de ataque y defensa de alto rendimiento, optimizado en recursos y con una arquitectura de diseño ligero, construido dentro de **Oracle VirtualBox**.

> 📢 **Aviso y Alcance del Proyecto**  
> Este entorno de laboratorio se ha construido y se mantiene estrictamente para uso educativo privado, práctica técnica (hands-on) y desarrollo profesional. Todas las pruebas de seguridad, simulaciones de exploits y métricas de monitoreo de red se ejecutan dentro de un ecosistema virtual completamente aislado (**SOCLAB**). Ningún sistema en producción ni red externa fue atacado o afectado, parcial ni totalmente, durante la creación de este proyecto.

---

## 🗺️ Topología de Red

```text
┌──────────────────────────────────────────────────────────────┐
│                   COMPUTADORA FÍSICA (HOST)                  │
│                                                              │
│  IP Host-Only: 192.168.56.1                                  │
│  Administración Web: https://192.168.56.10                   │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               │ HOST-ONLY
                               │ 192.168.56.0/24
                               ▼
┌──────────────────────────────────────────────────────────────┐
│                     OPNsense-Firewall                        │
│                                                              │
│  WAN  : 10.0.2.15/24                                         │
│  OPT1 : 192.168.56.10/24                                     │
│  LAN  : 192.168.50.1/24                                      │
│                                                              │
│  Rol: Gateway de Seguridad, Enrutamiento y Control NAT       │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               │ SOCLAB LAN
                               │ 192.168.50.0/24
                               │
          ┌────────────────────┼────────────────────┐
          ▼                    ▼                    ▼
   ┌──────────────┐    ┌────────────────┐    ┌────────────────┐
   │ Kali-Manual  │    │ SOC-PLATFORMS  │    │ Wazuh-Manager  │
   │ Red Team     │    │                │    │     SIEM       │
   │ Atacante     │    │                │    │                │
   │              │    │     (Zeek,     │    │                │
   │              │    │  Wazuh Agent)  │    │                │
   │              │       Docker Apps   │    │                │
   └──────────────┘    └───────┬────────┘    └────────────────┘
                               │
                  ┌────────────┼────────────┐
                  ▼            ▼            ▼
            ┌──────────┐ ┌──────────┐ ┌──────────────┐
            │ Windows  │ │ Rocky9   │ │ DFIR         │
            │ Server   │ │ Vulnerable │ │ Workstation │
            │ Vulnerable │          │ │              │
            └──────────┘ └──────────┘ └──────────────┘


## Infraestructura Principal

| Máquina Virtual | Rol en el Laboratorio | SO Base | Hardware Dedicado | Plataformas Instaladas |
| :--- | :--- | :--- | :--- | :--- |
| **`OPNsense-Firewall`** | Gateway de Seguridad y Enrutamiento | FreeBSD | 1 GB RAM / 1 CPU | Dnsmasq DHCP |
| **`Kali-Manual`** | Emulación de Ataques Adversarios | Debian | 2 GB RAM / 1 CPU | Frameworks de ataque |
| **`SOC-PLATFORMS`** | Centro de Sensores (Sensor Hub) | Ubuntu | 5 GB RAM / 2 CPUs | Zeek, Wazuh Agent |
| **`Wazuh-Manager`** | Motor de Análisis de Logs y SIEM | Ubuntu | 4 GB RAM / 2 CPUs | Wazuh Dashboard |
| **`WindowsServer-Victim`** | Objetivo Vulnerable (Blue Team) | WinServer | 4 GB RAM / 2 CPUs | Sysmon, Wazuh Agent, Apps Objetivo ej.: OWASP JuiceShop |
| **`Rocky9.8 - Red Hat`** | Objetivo Vulnerable (Blue Team) | LinuxServer | 2 GB RAM / 2 CPUs | Auditd, Wazuh Agent |
| **`Digital Forensic - Ubuntu Desktop`** | Análisis Forense Digital | LinuxDesktop | 8 GB RAM / 2 CPUs | Wazuh Agent, Autopsy, Volatility3, YARA, The Sleuth Kit |

## Plataformas de Análisis de Malware

| Máquina Virtual | Rol en el Laboratorio | SO Base | Hardware Dedicado | Plataformas Instaladas |
| :--- | :--- | :--- | :--- | :--- |
| **`REMNux`** | Ingeniería Inversa y Análisis de Software Malicioso | Ubuntu 24.04 LTS (Noble Numbat) | 2 GB RAM / 2 CPUs | Simulación de Red, Triaje y Forense |
| **`FLARE VM`** | Detonación e Ingeniería Inversa en Windows | Dentro de Windows 11 Desktop | 6 GB RAM / 2 CPUs | Detonación y Depuración en Windows |


