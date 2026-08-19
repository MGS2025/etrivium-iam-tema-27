# Tema 27 — Fuentes

> **Título oficial**: Administración del Sistema operativo y software de base. Funciones y responsabilidades. Actualización, mantenimiento y reparación del sistema operativo.
>
> **Criterio**: todo dato del contenido cita un **ID** inline (p. ej. `[SILBERSCHATZ]`). Tier 1 = obras canónicas de sistemas operativos, estándares y especificaciones abiertas, guías metodológicas de organismos públicos de referencia (NIST, ISO/IEC, IETF, UEFI Forum) y normativa española de aplicación directa. Tier 2 = documentación oficial de productos concretos (Microsoft, Red Hat, systemd, LVM…), citada para ilustrar sin atar el tema a un único fabricante. Tier 3 = marco del puesto y contexto municipal, no citado como contenido técnico puro.

---

## Tier 1 — Obras canónicas, estándares y normativa

| ID | Referencia |
|---|---|
| `[SILBERSCHATZ]` | Silberschatz, A.; Galvin, P. B.; Gagne, G. *Operating System Concepts*. Wiley (10.ª ed.). Obra canónica: procesos e hilos, planificación, memoria virtual, sistemas de archivos, E/S, protección y seguridad. |
| `[TANENBAUM]` | Tanenbaum, A. S.; Bos, H. *Modern Operating Systems*. Pearson (4.ª ed.). Arquitecturas de núcleo (monolítico, micronúcleo, capas, máquina virtual, exonúcleo) y el debate monolítico frente a micronúcleo. |
| `[STALLINGS]` | Stallings, W. *Operating Systems: Internals and Design Principles*. Pearson (9.ª ed.). Modo núcleo y modo usuario, llamadas al sistema, gestión de recursos y rendimiento. |
| `[POSIX]` | IEEE Std 1003.1 / The Open Group Base Specifications (POSIX). Interfaz normalizada de llamadas al sistema, permisos de archivos, señales, usuarios y grupos en sistemas tipo Unix. |
| `[FHS]` | Linux Foundation. *Filesystem Hierarchy Standard* (FHS 3.0). Ubicación normalizada de binarios, configuración (`/etc`), registros (`/var/log`) y datos variables en sistemas Linux. |
| `[UEFI-SPEC]` | UEFI Forum. *Unified Extensible Firmware Interface (UEFI) Specification*. Arranque UEFI, partición del sistema EFI (ESP), variables de arranque y **Arranque Seguro** (*Secure Boot*). uefi.org. |
| `[TPM-ISO]` | ISO/IEC 11889 / Trusted Computing Group. *Trusted Platform Module (TPM) Library Specification*. Almacenamiento de claves y medición de la integridad del arranque; base del cifrado de volumen ligado al equipo. |
| `[RFC5424]` | IETF. *RFC 5424: The Syslog Protocol* (2009). Formato normalizado de mensajes de registro, con sus **severidades** (0 *emerg* a 7 *debug*) y **facilidades**. Sustituye al histórico RFC 3164 (BSD syslog). |
| `[RFC5905]` | IETF. *RFC 5905: Network Time Protocol Version 4*. Sincronización horaria, requisito imprescindible para correlacionar registros de varios sistemas. |
| `[NIST80040]` | NIST. *SP 800-40 Rev. 4: Guide to Enterprise Patch Management Planning* (2022). Metodología de gestión de parches: inventario, priorización por riesgo, pruebas, despliegue por fases y excepciones documentadas. |
| `[NIST80092]` | NIST. *SP 800-92: Guide to Computer Security Log Management*. Generación, transmisión, almacenamiento, protección, análisis y retención de registros de seguridad. |
| `[NIST80034]` | NIST. *SP 800-34 Rev. 1: Contingency Planning Guide for Federal Information Systems*. Planes de contingencia, estrategias de copia de seguridad, sitios alternativos, RPO/RTO y pruebas del plan. |
| `[NIST80061]` | NIST. *SP 800-61 Rev. 2: Computer Security Incident Handling Guide*. Ciclo de gestión de incidentes: preparación, detección y análisis, contención/erradicación/recuperación, lecciones aprendidas. |
| `[NIST-CVSS]` | FIRST. *Common Vulnerability Scoring System (CVSS) Specification* y NIST *National Vulnerability Database (NVD)*. Puntuación de gravedad de vulnerabilidades (0,0-10,0) usada para priorizar el parcheo. |
| `[CVE]` | MITRE. *Common Vulnerabilities and Exposures (CVE) Program*. Identificador único y público de cada vulnerabilidad conocida (`CVE-AAAA-NNNNN`). cve.org. |
| `[ISO14764]` | ISO/IEC 14764 (IEEE 14764). *Software Engineering — Software Life Cycle Processes — Maintenance*. Tipología canónica del mantenimiento: **correctivo, preventivo, perfectivo y adaptativo**. |
| `[ISO12207]` | ISO/IEC/IEEE 12207. *Systems and software engineering — Software life cycle processes*. Procesos del ciclo de vida del software, incluidos operación y mantenimiento. |
| `[ISO20000]` | ISO/IEC 20000-1. *Gestión del servicio de TI*. Requisitos de gestión de incidencias, problemas, cambios, configuración, capacidad y continuidad del servicio. |
| `[ISO27002]` | ISO/IEC 27002. *Controles de seguridad de la información*. Controles de gestión de vulnerabilidades técnicas, control de acceso, registro y supervisión, copias de seguridad y gestión de cambios. |
| `[ISO22301]` | ISO/IEC 22301. *Sistemas de gestión de la continuidad del negocio*. Análisis de impacto en el negocio (BIA), del que se derivan **RPO** y **RTO**. |
| `[ISO25010]` | ISO/IEC 25010 (SQuaRE). *Modelo de calidad del producto software*. Fiabilidad, mantenibilidad, eficiencia de desempeño y seguridad: marco de los criterios de §5. |
| `[ENS]` | Real Decreto 311/2022, de 3 de mayo, por el que se regula el **Esquema Nacional de Seguridad**. Principios básicos, requisitos mínimos, categorización de sistemas (BÁSICA/MEDIA/ALTA), dimensiones de seguridad y anexo II de medidas (marco organizativo, marco operacional y medidas de protección). |
| `[ENI]` | Real Decreto 4/2010, por el que se regula el **Esquema Nacional de Interoperabilidad**, y sus Normas Técnicas de Interoperabilidad. |
| `[L4015]` | Ley 40/2015, de 1 de octubre, de Régimen Jurídico del Sector Público. Arts. 156-157 (ENI, ENS y reutilización de sistemas y aplicaciones) y funcionamiento electrónico del sector público. |
| `[L3915]` | Ley 39/2015, de 1 de octubre, del Procedimiento Administrativo Común de las Administraciones Públicas. Obligación de disponibilidad de los servicios electrónicos y del registro electrónico. |
| `[RGPD]` | Reglamento (UE) 2016/679 (RGPD), arts. 5, 25 y 32, y LO 3/2018 (LOPDGDD). Integridad, confidencialidad y **disponibilidad** de los datos personales, y capacidad de **restaurar** el acceso a ellos tras un incidente. |

## Tier 2 — Documentación de producto y proyecto

| ID | Referencia |
|---|---|
| `[MS-WINSERVER]` | Microsoft Learn. *Windows Server documentation* — servicios, Administrador del servidor, roles y características, Registro de eventos. learn.microsoft.com/windows-server. |
| `[MS-AD]` | Microsoft Learn. *Active Directory Domain Services* — dominio, bosque, unidades organizativas, grupos de seguridad y SID. |
| `[MS-GPO]` | Microsoft Learn. *Group Policy* — directivas de grupo, GPO, precedencia LSDOU (local, sitio, dominio, unidad organizativa) y directivas de contraseña y bloqueo de cuenta. |
| `[MS-WSUS]` | Microsoft Learn. *Windows Server Update Services (WSUS)*, *Windows Update for Business* y *Microsoft Configuration Manager*. Distribución controlada de actualizaciones y anillos de despliegue. |
| `[MS-WINRE]` | Microsoft Learn. *Windows Recovery Environment (WinRE)*, `bootrec`, `sfc /scannow`, `DISM /RestoreHealth`, puntos de restauración y Restablecer este PC. |
| `[MS-PERF]` | Microsoft Learn. *Monitor de rendimiento, contadores, conjuntos de recopiladores de datos, Monitor de recursos y Administrador de tareas*. |
| `[MS-BITLOCKER]` | Microsoft Learn. *BitLocker* — cifrado de volumen completo apoyado en TPM. |
| `[SYSTEMD]` | freedesktop.org. *systemd — System and Service Manager*: unidades (`.service`, `.timer`, `.target`), `systemctl`, `journalctl`, objetivos de arranque y modo de rescate/emergencia. |
| `[MAN-PAGES]` | The Linux man-pages project y manuales de las utilidades GNU/Linux: `ps`, `top`, `vmstat`, `iostat`, `df`, `du`, `fsck`, `chroot`, `cron(5)`, `quota`, `dmesg`, `journalctl`, `useradd`, `chmod`. kernel.org/doc/man-pages. |
| `[RH-DOC]` | Red Hat. *Red Hat Enterprise Linux — System Administrator's Guide / Managing systems, storage devices and file systems*. access.redhat.com/documentation. |
| `[LVM-DOC]` | Red Hat / proyecto LVM2. *Logical Volume Manager Administration*: volumen físico (PV), grupo de volúmenes (VG), volumen lógico (LV), instantáneas y redimensionado en caliente. |
| `[GRUB-DOC]` | GNU. *GRUB 2 Manual* — configuración, entradas de arranque, modo de línea de órdenes y reinstalación del gestor. gnu.org/software/grub. |
| `[PAM-DOC]` | Linux-PAM. *Pluggable Authentication Modules* — pila de módulos de autenticación, cuenta, sesión y contraseña. |
| `[SUDO-DOC]` | Todd C. Miller. *sudo / sudoers* — elevación controlada y auditada de privilegios. sudo.ws. |
| `[SMART-DOC]` | smartmontools. *S.M.A.R.T. monitoring tools* — atributos de salud de discos (sectores reasignados, horas de encendido, desgaste de la NAND) para el mantenimiento preventivo. |
| `[ITIL]` | AXELOS. *ITIL 4* — prácticas de gestión de incidencias, problemas, cambios y niveles de servicio; vocabulario de referencia del servicio TIC (compatible con [ISO20000]). |
| `[SEMVER]` | Preston-Werner, T. *Semantic Versioning 2.0.0*. semver.org. Convenio `MAYOR.MENOR.PARCHE`. |
| `[CCN-STIC]` | Centro Criptológico Nacional. *Guías CCN-STIC*: serie 800 (ENS: categorización, política de seguridad, gestión de registros) y series 500/600 (guías de bastionado de Windows y Linux). ccn-cert.cni.es. |

## Tier 3 — Marco del puesto y contexto municipal (contexto, no contenido técnico)

| ID | Referencia |
|---|---|
| `[BOAM10032]` | BOAM 10.032 (23-dic-2025). Bases específicas TIC C1 Ayto. Madrid — temario oficial. Enunciado literal del Tema 27. |
| `[ORD-ADMON-E]` | Ordenanza de Atención a la Ciudadanía y Administración Electrónica del Ayuntamiento de Madrid. Marco de los servicios electrónicos municipales que sostienen los sistemas administrados. |
| `[IAM]` | Organismo Autónomo **Informática del Ayuntamiento de Madrid (IAM)**: entidad responsable de la explotación de los sistemas municipales, ámbito en el que se sitúan los ejemplos y casos prácticos del tema. |

---

*Las referencias Tier 1 fijan el fundamento del tema: las tres obras canónicas de sistemas operativos (Silberschatz, Tanenbaum, Stallings) para la parte de arquitectura y gestión de recursos; los estándares abiertos que normalizan lo que el administrador manipula a diario (POSIX, FHS, UEFI, syslog, NTP); las guías metodológicas del NIST para parcheo, registros, incidentes y contingencia; las normas ISO/IEC para el ciclo de vida del mantenimiento, la gestión del servicio y la continuidad; y la normativa española —muy especialmente el **Esquema Nacional de Seguridad**— que convierte buena parte de estas buenas prácticas en obligación jurídica para el Ayuntamiento de Madrid. Tier 2 documenta productos concretos (Windows Server, systemd, LVM, GRUB, WSUS) citados como ejemplo de cómo cada familia de sistemas implementa esos conceptos, sin que el tema dependa de ningún fabricante. Tier 3 enmarca el puesto y el contexto municipal de los ejemplos y casos prácticos.*
