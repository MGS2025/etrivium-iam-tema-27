# Tema 27 — Casos Prácticos

> **Título oficial**: Administración del Sistema operativo y software de base. Funciones y responsabilidades. Actualización, mantenimiento y reparación del sistema operativo.
>
> **Formato**: 3 casos prácticos sobre supuestos reales del Ayuntamiento de Madrid. Cada caso suma **10 puntos**.
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid

Los tres casos recorren el ciclo completo de vida de un sistema en el IAM: el **Caso 1** trabaja la **puesta en servicio y la administración ordinaria** (§1-§3); el **Caso 2**, el **mantenimiento, el parcheo y el marco del ENS** (§4-§6); y el **Caso 3**, el **diagnóstico de una caída y la recuperación** (§7-§8).

---

## Caso 1 — Puesta en servicio de un servidor de la Sede Electrónica

### Enunciado

El IAM va a poner en explotación un **servidor Linux** que alojará el componente de consulta de expedientes de la Sede Electrónica. El equipo dispone de dos discos: uno para el sistema y otro, nuevo, destinado a datos y registros. Del servidor se encargarán **tres técnicos** del equipo de explotación, y una **aplicación de terceros** debe ejecutarse como servicio permanente y lanzar, además, un proceso nocturno de consolidación de datos.

Durante las pruebas se detecta que, en un servidor gemelo ya en producción, un componente entró en bucle y llenó el disco del sistema escribiendo registros, dejando el servicio caído durante dos horas.

### Cuestiones

**Cuestión 1 — Diseño del almacenamiento (3 puntos).** Proponga la organización del segundo disco de modo que el incidente del servidor gemelo no pueda repetirse, indicando las capas de la pila de almacenamiento que utilizaría y los pasos necesarios para poder ampliar el espacio más adelante sin parar el servicio.

**Cuestión 2 — Cuentas y permisos (3 puntos).** Defina el esquema de cuentas para los tres técnicos y para la aplicación, aplicando los principios exigidos por el ENS. Indique qué mecanismo usaría para que los técnicos puedan reiniciar el servicio sin ser administradores plenos.

**Cuestión 3 — Servicios y tareas programadas (2 puntos).** Explique cómo dejaría configurado el servicio de la aplicación para que sobreviva a un reinicio del servidor, y cómo planificaría el proceso nocturno indicando cuatro buenas prácticas exigibles a esa tarea.

**Cuestión 4 — Documentación (2 puntos).** Enumere la documentación mínima que debe existir antes de considerar el servidor «en servicio» y justifique por qué el inventario es la pieza fundacional.

### Solución orientativa

- **C1**: (§2.2, §2.2.1) La pila correcta es **dispositivo de bloques → partición → LVM (PV → VG → LV) → sistema de archivos → punto de montaje**. Sobre el segundo disco se crea un **volumen físico**, se integra en un **grupo de volúmenes** y se crean **volúmenes lógicos separados**, al menos uno para los **datos** y otro para los **registros** (`/var/log` o la ruta de registro de la aplicación). Esa separación es la que impide que un componente en bucle llene el volumen del sistema: llenaría únicamente su propio volumen de registros. Se completa con **cuotas** cuando el volumen sea compartido, con **rotación de registros** y con **umbrales de aviso al 80 % y de alarma al 90 %**. Para ampliar más adelante sin parar el servicio: `lvextend` sobre el volumen lógico y, a continuación, `resize2fs` o `xfs_growfs` sobre el sistema de archivos —**los dos pasos**, no solo el primero—.

- **C2**: (§3.1, §3.1.1) **Cuentas nominales** para cada uno de los tres técnicos, nunca una cuenta compartida, porque la cuenta compartida destruye la trazabilidad. Aplicando **mínimo privilegio** y **separación de funciones**, cada técnico dispone de su cuenta ordinaria y, si necesita administrar, de una **cuenta de administración diferenciada** con segundo factor. La aplicación se ejecuta con una **cuenta de servicio** propia, sin sesión interactiva y con los permisos estrictamente necesarios sobre sus directorios. Para reiniciar el servicio sin privilegios plenos se usa **`sudo` acotado**, que además **registra cada orden ejecutada**, autorizando únicamente las órdenes concretas necesarias (por ejemplo, reinicio de ese servicio y consulta del registro) al grupo de operadores. Se completa con política de contraseñas, bloqueo tras intentos fallidos y **revisión periódica y baja inmediata** de cuentas.

- **C3**: (§3.2) El servicio se declara como **unidad de systemd** y se **habilita** (`systemctl enable --now`), teniendo presente que `start` solo lo arranca en ese momento y `enable` es lo que garantiza que vuelva tras un reinicio; se configuran sus **dependencias** y su política de reinicio automático ante fallo. El proceso nocturno se planifica con `cron` o con un **temporizador de systemd** en horario de bajo impacto. Cuatro buenas prácticas exigibles: (a) que sea **idempotente**, de modo que dos ejecuciones no rompan nada; (b) que use un **bloqueo** para no solaparse consigo misma si un día tarda de más; (c) que **registre** su resultado y **avise también cuando falle**, no solo cuando termine bien; y (d) que se ejecute con una **cuenta de servicio**, nunca con la cuenta nominal del técnico que la creó, porque desaparecería con él.

- **C4**: (§4.1) Documentación mínima: **inventario del activo** (identificación, versión del sistema y del software de base, responsable funcional y técnico, criticidad y fecha de fin de soporte), **esquema de arquitectura y dependencias**, **configuración base y bastionado aplicado**, **procedimientos operativos normalizados** (arranque y parada ordenados, copia y restauración, alta de usuario), **registro de cambios**, **plan de continuidad con RPO y RTO** y **acuerdo de nivel de servicio**. El inventario es la pieza fundacional porque **no se puede proteger, parchear ni recuperar lo que no se sabe que existe**: de él dependen el análisis de riesgos, la gestión de parches y la recuperación. El ENS lo recoge en la medida **`op.exp.1`**, exigible en las tres categorías.

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Pila de almacenamiento correcta, con separación de volúmenes justificada y los dos pasos de ampliación en caliente | 3 |
| Esquema de cuentas con cuentas nominales, mínimo privilegio, cuenta de servicio y elevación acotada y auditada | 3 |
| Servicio habilitado (no solo arrancado) y tarea programada con cuatro buenas prácticas correctas | 2 |
| Documentación mínima enumerada y justificación del inventario como pieza fundacional | 2 |

---

## Caso 2 — Ventana de mantenimiento y parche crítico

### Enunciado

El **primer martes de mes** el fabricante publica las actualizaciones acumulativas del sistema operativo del parque municipal. Entre ellas figura la corrección de una vulnerabilidad con identificador **CVE** y puntuación **CVSS 9,4**, que afecta a un componente **expuesto a Internet** en los servidores de la Sede Electrónica y que, según el aviso, **está siendo explotada activamente**.

El parque afectado son 4.200 puestos de usuario en Áreas y Distritos y 40 servidores, de los cuales 6 sostienen la Sede Electrónica. El sistema de la Sede está categorizado conforme al ENS con la dimensión de **disponibilidad en nivel ALTO**.

Un responsable propone «aplicarlo esta misma tarde en todo el parque, que es crítico y no hay tiempo que perder».

### Cuestiones

**Cuestión 1 — Priorización (2 puntos).** Explique cómo se determina la prioridad real de aplicación de este parche y por qué la puntuación CVSS, por sí sola, no la determina.

**Cuestión 2 — Procedimiento de despliegue (3 puntos).** Describa el procedimiento que seguiría, valorando la propuesta de aplicar el parche esa misma tarde en todo el parque. Indique las etapas y qué se verifica en cada una.

**Cuestión 3 — Exigencias del ENS (3 puntos).** Identifique la medida del anexo II del ENS que regula esta actividad y sus dos refuerzos aplicables, y explique qué obliga a hacer cada uno en este supuesto concreto.

**Cuestión 4 — Marcha atrás y registro (2 puntos).** Enumere al menos cuatro mecanismos de marcha atrás disponibles, indicando cuál elegiría para los servidores de la Sede y por qué una instantánea no sustituye a una copia de seguridad.

### Solución orientativa

- **C1**: (§6.1) La prioridad real combina **cuatro factores**: la **gravedad** (CVSS 9,4, banda crítica: 9,0-10,0), la **exposición** del activo (el componente está publicado en Internet, lo que eleva mucho el riesgo), la **criticidad del servicio** (la Sede Electrónica presta un servicio con efectos jurídicos sobre plazos) y la **existencia de explotación activa** (la hay, lo que convierte el riesgo en inminente). CVSS por sí sola no basta porque **puntúa la vulnerabilidad, no el riesgo del activo concreto**: una vulnerabilidad de 9,8 en un servicio deshabilitado o en una red aislada puede ser menos urgente que una de 7,0 explotada en un servidor publicado. En este supuesto, los cuatro factores apuntan en la misma dirección: **máxima prioridad**.

- **C2**: (§6.2) La propuesta de aplicarlo esa tarde en todo el parque **debe rechazarse tal cual**: la urgencia justifica **comprimir** los plazos, no **suprimir** las etapas; un parche defectuoso aplicado simultáneamente a 4.200 puestos convierte un incidente de seguridad en una caída generalizada. Procedimiento correcto, con los seis pasos del NIST comprimidos: **inventariar** los sistemas afectados (ya disponible), **identificar** el parche y lo que corrige, **priorizar** (hecho en C1), **probar** en laboratorio y en un piloto representativo aunque sea en horas en lugar de días, **desplegar por anillos** —laboratorio, piloto, producción no crítica y, por último, los 6 servidores de la Sede en ventana de mantenimiento— y **verificar** el resultado con pruebas funcionales concretas, no con un simple «arranca». Entre etapas se verifica que el parche instala, que el software departamental real sigue funcionando y que el servicio responde. En paralelo, y por tratarse de explotación activa, se aplican **mitigaciones temporales** en el perímetro sobre el componente expuesto mientras avanza el despliegue, y se tramita como **cambio de emergencia**: se ejecuta primero y se documenta y aprueba formalmente después, nunca «en lugar de».

- **C3**: (§4.2.1, §6.2.1) La medida es **`op.exp.4` — Mantenimiento y actualizaciones de seguridad**, del marco operacional del anexo II del ENS. Exige atender a las especificaciones del fabricante con **seguimiento continuo de los anuncios de defectos**, disponer de **un procedimiento para analizar, priorizar y determinar cuándo aplicar** las actualizaciones —priorizando según la variación del riesgo— y que el mantenimiento lo realice **solo personal debidamente autorizado**. Sus dos refuerzos: **R1, pruebas en preproducción**, que obliga a comprobar en un entorno **consistente en configuración con el de producción** que la nueva versión funciona y **no disminuye la eficacia de las funciones necesarias para el trabajo diario**; y **R2, prevención de fallos**, que obliga a **prever un mecanismo para revertir** los parches ante efectos adversos. Al estar el sistema de la Sede en categoría **ALTA** (basta con que una dimensión, aquí la disponibilidad, alcance el nivel ALTO), **le son exigibles ambos refuerzos**. Se añade la medida **`op.exp.5` (Gestión de cambios)**, también exigible.

- **C4**: (§6.2.1) Mecanismos de marcha atrás: **instantánea de la máquina virtual** o del volumen, **punto de restauración del sistema**, **desinstalación del parche**, **arranque con la versión anterior del núcleo**, **reversión del controlador** y, como último recurso, **restauración desde copia de seguridad**. Para los 6 servidores de la Sede la elección natural es la **instantánea previa de cada máquina virtual**, por ser inmediata y completa, complementada con la posibilidad de desinstalar el parche; la instantánea se **elimina** en cuanto se consolida el cambio, porque mantenerla degrada el rendimiento y consume espacio. Una instantánea **no sustituye a una copia de seguridad** porque depende del **mismo almacenamiento y del mismo sistema**: si se pierde la cabina, o el volumen se cifra en un ataque de secuestro de datos, se pierden el original **y** la instantánea. Toda la intervención se registra: qué se cambió, cuándo, quién lo autorizó, resultado de la verificación y porcentaje de cumplimiento del parque.

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Priorización basada en gravedad, exposición, criticidad y explotación activa, con crítica correcta al uso aislado de CVSS | 2 |
| Rechazo razonado del despliegue simultáneo, etapas del proceso y anillos con verificación intermedia y mitigación temporal | 3 |
| Identificación de `op.exp.4` y de sus refuerzos R1 y R2, con su exigibilidad según la categoría del sistema | 3 |
| Cuatro o más mecanismos de marcha atrás, elección justificada y distinción entre instantánea y copia de seguridad | 2 |

---

## Caso 3 — Caída de un servidor: diagnóstico, reparación y recuperación

### Enunciado

Un **lunes a las 08:40**, el servicio de consulta del **Padrón municipal** deja de responder. El servidor que lo aloja no admite conexiones remotas y, tras solicitar su reinicio al centro de proceso de datos, el equipo **no arranca**: se detiene mostrando un mensaje de que no encuentra el volumen raíz. La noche del domingo se aplicó una actualización del núcleo del sistema operativo.

Del servicio se sabe que tiene un **RPO de una hora** y un **RTO de cuatro horas en día hábil**, y que la estrategia de copias es: **total semanal** los sábados, **incrementales diarias** y **copia de los registros de transacción cada hora**.

### Cuestiones

**Cuestión 1 — Método de diagnóstico (3 puntos).** Describa el método que seguiría para diagnosticar la avería. Indique cuál es la primera hipótesis razonable a la vista del enunciado y por qué.

**Cuestión 2 — Reparación (3 puntos).** Explique cómo intentaría devolver el servidor al servicio, ordenando las técnicas de menor a mayor coste e indicando en qué eslabón de la cadena de arranque se ha detenido el sistema.

**Cuestión 3 — Registros (2 puntos).** Una vez restablecido el servicio, ¿qué evidencias buscaría y dónde, para acreditar qué ocurrió? Señale dos requisitos sin los cuales esas evidencias pierden valor.

**Cuestión 4 — Recuperación y cumplimiento (2 puntos).** Suponiendo que la reparación fracase y haya que restaurar, indique qué copias se necesitan, cuántos datos se perderían como máximo y si la estrategia descrita cumple el RPO y el RTO comprometidos.

### Solución orientativa

- **C1**: (§7.2) Método: **delimitar el síntoma** con precisión (el sistema arranca el núcleo pero no encuentra la raíz; no es un fallo de aplicación ni de red), **determinar el alcance** (un solo servidor, no una caída general), **buscar el cambio reciente** —que es la primera pregunta útil en cualquier incidencia—, **formular hipótesis y comprobarlas de una en una**, **aislar y contener**, **restablecer** el servicio y **analizar la causa raíz después**. La primera hipótesis razonable es directa: **la actualización del núcleo aplicada la noche anterior**. La inmensa mayoría de las incidencias siguen a un cambio, y el síntoma —«no encuentra el volumen raíz»— es la firma clásica de un **`initramfs` regenerado sin el controlador necesario** para montar la raíz (RAID, cifrado o cabina), o de un cambio en el identificador del volumen en la configuración de montaje. Es importante también **contener**: detener el despliegue de esa misma actualización en el resto de servidores hasta aclarar lo ocurrido.

- **C2**: (§8.1) El sistema se ha detenido en el **cuarto eslabón** de la cadena de arranque: firmware → gestor de arranque → cargador → **núcleo e `initramfs`** → proceso inicial → servicios. Técnicas ordenadas de menor a mayor coste: (1) **arrancar la entrada anterior del núcleo** desde el menú de GRUB, que en este supuesto es la actuación con mejor relación entre probabilidad de éxito y coste, y que devuelve el servicio en minutos; (2) desde ese sistema ya arrancado, **regenerar el `initramfs`** con los controladores correctos y revisar la configuración de montaje, o **desinstalar la actualización** del núcleo; (3) si no arranca ninguna entrada, arrancar desde un **medio vivo**, montar los volúmenes, hacer **`chroot`** sobre la instalación y reparar desde dentro (regenerar el `initramfs`, reinstalar el gestor de arranque); (4) comprobar el sistema de archivos con **`fsck`**, siempre **desmontado**, si hay indicios de daño; (5) como último recurso, **restaurar desde copia de seguridad**. En paralelo se comunica la indisponibilidad a las unidades usuarias y se registra la incidencia.

- **C3**: (§7.1) Evidencias: los **registros del arranque anterior** (`journalctl -b -1`, mensajes del núcleo con `dmesg`), los registros del **gestor de paquetes** que acreditan qué se instaló y cuándo la noche del domingo, el registro de la **tarea o ventana de mantenimiento** que ejecutó la actualización, los **registros de autenticación** para descartar una intervención manual no prevista y los registros de la **aplicación de Padrón** para acotar el momento exacto en que dejó de responder. Dos requisitos sin los cuales pierden valor: (a) la **sincronización horaria por NTP** de todos los sistemas implicados, porque sin hora común los eventos de varias máquinas no se pueden correlacionar; y (b) la **centralización en un servidor distinto y la protección de su integridad y su acceso**, para que los registros existan aunque la máquina no arranque y para que nadie con acceso privilegiado pueda alterarlos. A ello se añade una **retención** definida y conforme a protección de datos.

- **C4**: (§8.2) Con copia **total semanal** e **incrementales diarias**, la restauración exige la **última total (sábado)** y **todas las incrementales posteriores en orden** —si falta o se corrompe una, la cadena se rompe—, más la restauración de los **registros de transacción horarios** hasta el último punto disponible. Con copia horaria de registros de transacción, la pérdida máxima de datos es de **una hora**, de modo que **el RPO de una hora se cumple**. El **RTO de cuatro horas** no se cumple ni se incumple sobre el papel: **depende del tiempo real de restauración**, que solo se conoce si se ha hecho una **prueba de restauración** documentada. Ese es precisamente el refuerzo **R1 de `mp.info.6`** del ENS, que obliga a probar regularmente los procedimientos de copia **y de restauración**. Si la prueba arroja seis horas, no se cumple el compromiso y hay que **cambiar la tecnología de recuperación**, no el documento. Se completa con la regla **3-2-1** —tres copias, dos soportes, una fuera de las instalaciones, hoy además inmutable— y con la revisión posterior del cambio que originó la caída, incorporando al anillo piloto un servidor con la misma configuración de almacenamiento.

### Criterios de evaluación

| Criterio | Puntos |
|---|---|
| Método de diagnóstico ordenado, con la actualización del núcleo como primera hipótesis y contención del despliegue | 3 |
| Eslabón de arranque correctamente identificado y técnicas de reparación ordenadas por coste, empezando por el núcleo anterior | 3 |
| Evidencias pertinentes y bien localizadas, con sincronización horaria y centralización protegida como requisitos | 2 |
| Cadena de restauración correcta, pérdida máxima de una hora, y RTO condicionado a la prueba de restauración | 2 |
