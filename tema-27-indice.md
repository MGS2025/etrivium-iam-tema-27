# Tema 27 — Índice

> **Título oficial**: Administración del Sistema operativo y software de base. Funciones y responsabilidades. Actualización, mantenimiento y reparación del sistema operativo.
>
> **Bloque**: Parte II — Técnico (Temas 11-40)
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid

---

## Estructura del tema

El esqueleto oficial agrupa el tema en **cuatro bloques**. Cada bloque se desarrolla en **dos secciones numeradas**, de modo que el contenido tiene **8 secciones y 31 epígrafes**:

| Bloque del esqueleto oficial | Secciones del contenido |
|---|---|
| I — Administración del sistema operativo y software de base | §1 y §2 |
| II — Funciones y responsabilidades de la administración de sistemas | §3 y §4 |
| III — Actualización y mantenimiento del sistema operativo | §5 y §6 |
| IV — Diagnóstico, reparación y recuperación del sistema operativo | §7 y §8 |

### Bloque I — Administración del sistema operativo y software de base

1. **Fundamentos y arquitectura del software de base**
   1.1. Concepto, funciones y clasificación del software de base
   1.1.1. Modelos de arquitectura: monolítico, micronúcleo y modular
   1.2. Componentes principales del software de base
   1.2.1. Gestores de arranque, cargadores, controladores y bibliotecas del sistema

2. **Gestión y control de recursos del sistema operativo**
   2.1. Gestión de procesos, hilos y memoria principal
   2.2. Subsistemas de almacenamiento, archivos y entrada/salida
   2.2.1. Volúmenes lógicos, cuotas de disco y dispositivos de bloques

### Bloque II — Funciones y responsabilidades de la administración de sistemas

3. **Funciones operativas y administración técnica**
   3.1. Administración de usuarios, grupos y directivas de seguridad
   3.1.1. Autenticación, autorización y control de acceso local
   3.2. Gestión de servicios, demonios y tareas programadas

4. **Responsabilidades organizativas y marco normativo público**
   4.1. Documentación técnica, inventario y procedimientos operativos
   4.2. Marco legal, gobernanza y seguridad en la Administración pública
   4.2.1. Aplicación del Esquema Nacional de Seguridad (ENS)

### Bloque III — Actualización y mantenimiento del sistema operativo

5. **Mantenimiento y optimización del sistema operativo**
   5.1. Estrategias de mantenimiento preventivo, correctivo y evolutivo
   5.2. Monitorización del rendimiento y gestión de capacidad
   5.2.1. Análisis de métricas (CPU, memoria, E/S) y ajuste del sistema

6. **Gestión de actualizaciones y parches de seguridad**
   6.1. Ciclo de vida del software y gestión de versiones
   6.2. Procedimientos de despliegue de parches y actualizaciones
   6.2.1. Evaluaciones de impacto, entornos de prueba y mecanismos de marcha atrás

### Bloque IV — Diagnóstico, reparación y recuperación del sistema operativo

7. **Diagnóstico de fallos y gestión de incidencias**
   7.1. Análisis de registros (logs) y auditoría de eventos
   7.2. Identificación y aislamiento de anomalías del sistema

8. **Reparación del sistema operativo y recuperación**
   8.1. Técnicas de reparación y arranque de emergencia
   8.2. Copias de seguridad, restauración y continuidad operativa

---

## Conceptos clave para memorizar

| Concepto | Dato clave |
|---|---|
| Software de base | Capa de software que hace utilizable el hardware y sostiene a las aplicaciones: **firmware, sistema operativo, controladores, bibliotecas del sistema y utilidades**. No resuelve el problema del usuario final; habilita a quien lo resuelve |
| Núcleo (*kernel*) | Único componente que se ejecuta en **modo privilegiado** (anillo 0); las aplicaciones viven en **modo usuario** y solo entran al núcleo mediante **llamadas al sistema** |
| Monolítico / micronúcleo / híbrido | **Monolítico**: todos los servicios en el espacio del núcleo (rápido, menos robusto; Linux, con módulos cargables). **Micronúcleo**: núcleo mínimo y servicios en modo usuario (robusto, más cambios de contexto; MINIX, QNX). **Híbrido**: Windows NT y XNU (macOS) |
| UEFI y arranque seguro | El firmware **UEFI** sustituye a la BIOS heredada; usa tabla de particiones **GPT** y una partición **ESP** con formato FAT32. El **Arranque Seguro** (*Secure Boot*) verifica la firma digital de cada componente de la cadena de arranque |
| Gestor de arranque / cargador | **GRUB 2** (Linux) y el **Administrador de arranque de Windows** (`bootmgfw.efi` + BCD) eligen el sistema y **cargan el núcleo** en memoria; el **initramfs/initrd** aporta los controladores necesarios para montar la raíz |
| Proceso frente a hilo | El **proceso** posee el espacio de direcciones y los recursos; el **hilo** es la unidad de planificación y **comparte** ese espacio. Cambiar de hilo dentro de un proceso es más barato que cambiar de proceso |
| Memoria virtual | La **MMU** traduce direcciones virtuales a físicas por páginas; un **fallo de página** trae la página de disco. La **hiperpaginación** (*thrashing*) es el síntoma de exceso de intercambio: mucha E/S y CPU baja |
| Dispositivo de bloques | Abstracción del almacenamiento en bloques de tamaño fijo direccionables (`/dev/sda`, `\\.\PhysicalDrive0`); sobre él se construyen particiones, volúmenes lógicos y sistemas de archivos |
| LVM (PV / VG / LV) | **Volumen físico** → **grupo de volúmenes** → **volumen lógico**. Permite **redimensionar en caliente** y hacer **instantáneas**; el equivalente en Windows son los **discos dinámicos** y los **Espacios de almacenamiento** |
| Cuota de disco | Límite de espacio o de *inodos* por usuario o grupo, con **límite blando** (*soft*, avisa y da periodo de gracia) y **límite duro** (*hard*, impide escribir) |
| Usuarios y permisos | Linux: **UID/GID**, permisos `rwx` para propietario/grupo/otros, `sudo` y **PAM**. Windows: **SID**, **ACL** con ACE de permiso o denegación, grupos de **Active Directory** y **directivas de grupo (GPO)** |
| AAA | **Autenticación** (¿quién eres?) → **Autorización** (¿qué puedes hacer?) → **Auditoría/trazabilidad** (¿qué hiciste?). Son tres funciones distintas y las tres son exigibles en el ENS |
| Mínimo privilegio | Cada cuenta debe tener **solo** los permisos que necesita: cuentas nominales de administración separadas de la cuenta de uso diario, y **nunca** trabajo ordinario con `root` o `Administrador` |
| Servicio / demonio | Proceso de larga duración sin terminal asociada, arrancado por el sistema: **unidades de systemd** (`systemctl`) en Linux moderno; **servicios de Windows** (`services.msc`, `sc`) con su cuenta de ejecución |
| Tarea programada | Ejecución diferida y periódica: **cron** y **temporizadores de systemd** en Linux; **Programador de tareas** en Windows. La sintaxis de `cron` tiene **cinco campos**: minuto, hora, día del mes, mes y día de la semana |
| Tipos de mantenimiento (ISO/IEC 14764) | **Correctivo** (arregla defectos), **preventivo** (evita fallos latentes), **perfectivo** (mejora rendimiento o mantenibilidad) y **adaptativo** (acomoda cambios del entorno). El enunciado del tema los agrupa como preventivo, correctivo y **evolutivo** (= perfectivo + adaptativo) |
| Gestión de capacidad | Analizar la tendencia de uso de CPU, memoria, disco y red para **anticipar** el agotamiento del recurso: se dimensiona sobre el **percentil alto** de la carga, no sobre la media |
| Línea base (*baseline*) | Medición del comportamiento normal del sistema con la que se comparan las mediciones posteriores. Sin línea base no se puede afirmar que un sistema «va lento» |
| Ciclo de vida del soporte | Un sistema operativo tiene fases de **soporte general**, **soporte extendido** y **fin de vida (EOL)**. Un sistema fuera de soporte **no recibe parches de seguridad**: en el sector público, mantenerlo es un incumplimiento del ENS |
| Versionado semántico | `MAYOR.MENOR.PARCHE`: **mayor** rompe compatibilidad, **menor** añade funcionalidad compatible, **parche** corrige errores sin cambiar la interfaz |
| CVE y CVSS | **CVE** es el identificador único de una vulnerabilidad publicada; **CVSS** es la puntuación de gravedad de 0 a 10 (crítica 9,0-10,0) que ordena la prioridad de parcheo |
| Despliegue por anillos | Los parches se aplican en oleadas: **laboratorio → piloto → producción no crítica → producción crítica**, con verificación entre etapas y ventana de mantenimiento comunicada |
| Marcha atrás (*rollback*) | Todo cambio debe poder deshacerse: **instantánea** previa de la máquina virtual o del volumen, **punto de restauración**, desinstalación del parche o arranque desde la entrada anterior del gestor de arranque |
| Registro de eventos | Linux: **syslog** (RFC 5424) y **journald** (`journalctl`). Windows: **Visor de eventos** con los registros Sistema, Aplicación y **Seguridad**. Los registros deben **centralizarse** en un servidor distinto del auditado |
| Correlación y SIEM | Los registros solo son útiles si se **agregan, sincronizan en el tiempo (NTP) y correlacionan**; en el ENS la trazabilidad exige conservar y proteger los registros de actividad |
| Arranque de emergencia | Medios y modos de reparación: **modo seguro**, **Entorno de recuperación de Windows (WinRE)** con `bootrec`, `sfc` y `DISM`; en Linux, **modo de rescate** de systemd, `fsck` y `chroot` desde un medio vivo |
| RPO y RTO | **RPO**: cuántos datos se admite perder (edad de la última copia útil). **RTO**: cuánto tiempo se admite estar caído. Los dos los fija **el negocio**, no el técnico |
| Regla 3-2-1 | **3** copias de los datos, en **2** soportes distintos, con **1** de ellas fuera de las instalaciones (y, hoy, preferiblemente **inmutable** frente a *ransomware*) |
| Copia total, diferencial e incremental | **Total**: todo. **Diferencial**: lo cambiado desde la última **total** (restauración = total + última diferencial). **Incremental**: lo cambiado desde la **última copia de cualquier tipo** (restauración = total + toda la cadena) |
| Restauración probada | Una copia de seguridad **no verificada mediante una restauración de prueba** no es una copia de seguridad: es una suposición |

---

*Tiempo estimado de estudio: 14-16 horas*
*Extensión del contenido: ~16.700 palabras · 14 diagramas SVG embebidos*
