░███    ░██ ░███     ░███    ░███    ░██    ░██ 
░████   ░██ ░████   ░████   ░██░██    ░██  ░██  
░██░██  ░██ ░██░██ ░██░██  ░██  ░██    ░██░██   
░██ ░██ ░██ ░██ ░████ ░██ ░█████████    ░███    
░██  ░██░██ ░██  ░██  ░██ ░██    ░██   ░██░██   
░██   ░████ ░██       ░██ ░██    ░██  ░██  ░██  
░██    ░███ ░██       ░██ ░██    ░██ ░██    ░██ 
                                                


# 🔎 NMAX

Este script Bash realiza escaneos TCP y UDP con Nmap de forma robusta, clara y portable. Está diseñado para entornos de CTF (Capture The Flag), pruebas de red, pentesting y situaciones donde necesitas resultados rápidos, legibles y sin errores de terminal.

El script **no utiliza descubrimiento dinámico de puertos**, es **compatible con cualquier versión de awk**, tiene **colores activados por defecto**, e incluye una opción para desactivarlos (--no-color).

---

## ✅ Características principales

- Escaneo TCP:
  - top1000 (por defecto) o escaneo completo -p-
- Escaneo UDP:
  - configurable por --top-ports N, full, o desactivado (0)
  - incluye puertos open|filtered
- Spinner visual durante el escaneo
- Resultados claros con lista de puertos abiertos y comandos nmap -sC -sV sugeridos
- Compatible con awk en mawk, gawk y busybox
- Guarda los informes -oA en una carpeta organizada por fecha y hora
- Salida coloreada por defecto, con opción --no-color para desactivar

---

## 📂 Estructura de salida

Por cada objetivo se genera una carpeta de salida como:

scans/20250901-181958/

Dentro de ella tendrás archivos como:

- 10.10.10.203_tcp_top1000.nmap
- 10.10.10.203_udp_top200.nmap
- 10.10.10.203_tcp_top1000.gnmap
- etc.

---

## 🚀 Requisitos

- Nmap instalado (sudo apt install nmap) En caso de no tenerlo instalado lo detecta y no permite continuar.
- Bash (funciona en Linux y macOS)
- awk estándar

No necesitas color en el terminal, pero si lo tienes, el script se verá mejor.

---

## 🛠️ Uso básico

chmod +x nmax 

./nmax -t 10.10.10.203

Esto realizará:

- Un escaneo TCP top-1000
- Un escaneo UDP top-200
- Mostrará los puertos abiertos encontrados
- Sugerirá comandos con -sC -sV para cada protocolo

---

## ⚙️ Opciones disponibles

-t <objetivo>  
Obligatorio. Puede ser una IP, un hostname o un fichero con una IP por línea.

--tcp {top1000|full}  
Modo de escaneo TCP. Por defecto top1000. Usa full para escaneo completo (-p-).

-U {N|full|0}  
Modo de escaneo UDP:  
- N = escaneo de los N puertos más comunes (por ejemplo, -U 200)  
- full = escaneo completo -p-  
- 0 = desactivar escaneo UDP completamente

--aggr  
Activa modo agresivo (-T5 --min-rate 4000)

--slow  
Activa modo conservador (-T3 --min-rate 300)

--no-color  
Desactiva todos los colores ANSI (útil para scripts y logs)

---

## 🧪 Ejemplos de uso

Escaneo rápido con colores:

./nmax -t 10.10.10.203

Escaneo TCP completo + UDP top-1000:

./nmax -t 10.10.10.203 --tcp full -U 1000

Solo escaneo TCP, sin UDP:

./nmax -t 10.10.10.203 -U 0

Escaneo sin colores (ideal para logs):

./nmax -t 10.10.10.203 --no-color

Escaneo de varios objetivos desde archivo:

./nmax -t objetivos.txt

---

## 🗂️ Resultado típico

Ejemplo de salida:

==> Objetivo: 10.10.10.203  
TCP abiertos: 22,80  
  Comando -sC -sV: nmap -sC -sV -p22,80 10.10.10.203  
UDP abiertos: 53,161  
  Comando -sC -sV: nmap -sU -sC -sV -p53,161 10.10.10.203

---

## 📦 Integración y mejoras

Este script puede integrarse fácilmente con herramientas de automatización, generación de informes o workflows de pentesting.

### Ideas para siguientes mejoras:

- Exportar los comandos sugeridos a archivos .sh
- Añadir detección de servicios (como http, ftp, smb, etc.)
- Autoejecutar -sC -sV si se desea
- Analítica sobre los resultados

---

## 🧠 Autoría

Script desarrollado por Roberto Peralta para uso en entornos profesionales, laboratorios CTF, prácticas de red y formación. 