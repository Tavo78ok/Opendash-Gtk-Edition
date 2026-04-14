## OpenDash v2.0
### Monitor y Optimizador del Sistema — ArgOs Platinum Edition

![GTK4](https://img.shields.io/badge/GTK-4.0-brightgreen?style=flat-square)
![Libadwaita](https://img.shields.io/badge/libadwaita-1.x-blue?style=flat-square)
![Python](https://img.shields.io/badge/Python-3.8%2B-yellow?style=flat-square)
![License](https://img.shields.io/badge/Licencia-MIT-lightgrey?style=flat-square)
![Platform](https://img.shields.io/badge/Plataforma-Debian%20%2F%20Ubuntu-orange?style=flat-square)

---

## Descripción

**OpenDash** es un dashboard de rendimiento y optimización del sistema diseñado para **ArgOs Platinum Edition**. Construido con **GTK4 + libadwaita**, ofrece monitoreo en tiempo real con una estética neon sobre fondo oscuro, gráficos históricos animados y herramientas de administración del sistema integradas.

---

## Capturas

> Dashboard principal con ring meters animados, gráficos históricos en tiempo real y especificaciones del equipo.

---

## Funciones

### Dashboard
- **Ring meters** animados con colores neon por recurso (CPU, RAM, Disco, Temperatura)
- **Gráficos históricos** en tiempo real de CPU, RAM y Red (últimos 60 segundos)
- Especificaciones del equipo: OS, HOST, KERNEL, CPU, GPU, paquetes, uptime
- Botones de acción rápida: **Optimizar RAM** y **Limpieza Profunda**

### Monitor
- Temperatura CPU/GPU en tiempo real con gráfico histórico
- Estadísticas de red detalladas (bytes recibidos/enviados, velocidad actual)
- **Top 10 procesos** ordenados por consumo de CPU

### Gamer
- Perfiles de energía con highlight neon al activar:
  - 🍃 **Modo Ahorro** — reduce frecuencia del CPU para maximizar batería
  - ⚖️ **Modo Balanceado** — equilibrio entre temperatura y velocidad
  - 🔥 **Modo Gamer** — desbloquea límites de energía para máxima performance
- El perfil seleccionado se guarda y se restaura al abrir la app

### Red
- Listado de interfaces de red activas con sus IPs
- Gráfico de tráfico en tiempo real (KB/s)
- Procesos activos con uso de CPU y RAM

### Software
- Lista completa de paquetes instalados vía `dpkg`
- Búsqueda en tiempo real
- **Desinstalador gráfico** con `apt purge` + `autoremove`

### Inicio
- Gestión de aplicaciones de **autostart** (`~/.config/autostart`)
- Toggle activar/desactivar por app sin salir de la interfaz

### Servicios
- Lista completa de **servicios systemd** con estado en tiempo real
- Indicadores de estado: 🟢 Activo / ⚫ Inactivo / 🔴 Fallido
- Búsqueda por nombre o descripción
- Iniciar/detener servicios con autenticación via `pkexec`

### Controles
- Slider de **brillo de pantalla** (via `brightnessctl` o `/sys/class/backlight`)
- Slider de **volumen del sistema** (via `pactl`)
- Toggle **tema claro/oscuro** sincronizado con el botón del header

---

## Instalación

### Opción 1 — Paquete .deb (recomendado)

```bash
sudo dpkg -i opendash_2.0_all.deb
```

El script de post-instalación instala automáticamente todas las dependencias necesarias.

### Opción 2 — Desde el código fuente

```bash
# Instalar dependencias manualmente
sudo apt install python3 python3-gi python3-gi-cairo \
    gir1.2-gtk-4.0 gir1.2-adw-1 python3-pip \
    brightnessctl pulseaudio-utils power-profiles-daemon

pip3 install psutil --break-system-packages

# Ejecutar
python3 opendash.py
```

---

## Dependencias

| Paquete | Uso | Instalación |
|---|---|---|
| `python3-gi` | Bindings GTK4/Adwaita | apt |
| `gir1.2-gtk-4.0` | GTK4 | apt |
| `gir1.2-adw-1` | libadwaita | apt |
| `python3-gi-cairo` | Gráficos Cairo | apt |
| `psutil` | Métricas del sistema | apt / pip |
| `brightnessctl` | Control de brillo | apt (opcional) |
| `pulseaudio-utils` | Control de volumen (`pactl`) | apt (opcional) |
| `power-profiles-daemon` | Perfiles de energía | apt (opcional) |
| `policykit-1` | Autenticación con `pkexec` | apt (opcional) |

---

## Arquitectura

```
opendash.py
├── Helpers (lbl, vbox, hbox, run_cmd...)
├── Hardware helpers (get_temp, get_volume, get_brightness...)
├── RingMeter        — gauge circular Cairo
├── HistoryGraph     — gráfico de línea histórico Cairo
├── MetricCard       — tarjeta con ring + valor + etiqueta
├── OpenDashWindow   — ventana principal (8 pestañas)
│   ├── _build_dashboard
│   ├── _build_monitor
│   ├── _build_gamer
│   ├── _build_network
│   ├── _build_software
│   ├── _build_inicio
│   ├── _build_servicios
│   └── _build_controles
└── OpenDashApp      — Adw.Application entry point
```

---

## Uso

```bash
# Desde terminal
opendash

# O desde el menú de aplicaciones
# Categoría: Sistema / Monitor
```

---

## Changelog

### v2.0 (Abril 2026)
- Migración completa de CustomTkinter a **GTK4 + libadwaita**
- Ring meters animados con Cairo
- Gráficos históricos en tiempo real
- Nueva pestaña: **Monitor** (temperatura, red, procesos)
- Nueva pestaña: **Servicios** (systemd)
- Nueva pestaña: **Controles** (brillo, volumen, tema)
- Toggle tema claro/oscuro
- Sistema de notificaciones con `Adw.Toast`
- Threading para operaciones pesadas sin bloquear la UI
- Paleta neon por pestaña (verde, cyan, amber, rojo, púrpura...)

### v1.5
- Dashboard con CustomTkinter
- Tabs: Dashboard, Gamer, Red, Software, Inicio
- Perfiles de energía básicos
- Limpieza del sistema

---

## Autor

**Tavo** ([@Tavo78ok](https://github.com/Tavo78ok))  
Proyecto: **ArgOs Platinum Edition**  
Licencia:
