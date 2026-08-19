# Tema 27 — Test de Autoevaluación

> **Título**: Administración del Sistema operativo y software de base. Funciones y responsabilidades. Actualización, mantenimiento y reparación del sistema operativo.
> **Formato**: 60 preguntas tipo test A/B/C (formato oficial oposición)
> **Nivel**: C1 — Técnico Auxiliar TIC, Ayuntamiento de Madrid
> **Versión**: v1.0 — Pendiente validación
> **Fecha**: 2026-08-20
> **Fuentes**: ver tema-27-fuentes.md

---

## Instrucciones

- Cada pregunta tiene **3 opciones** (A, B, C). Solo una es correcta.
- Penalización en examen real: respuesta incorrecta descuenta **1/3** del valor de una correcta.
- Tiempo orientativo: 1 minuto por pregunta.
- Distribución: Fundamentos y arquitectura (P1-P8), Gestión de recursos (P9-P16), Funciones operativas (P17-P24), Responsabilidades y marco normativo (P25-P32), Mantenimiento y monitorización (P33-P40), Actualizaciones y parches (P41-P48), Diagnóstico (P49-P54), Reparación y recuperación (P55-P60).

---

### Pregunta 1

**¿Qué se entiende por «software de base»?**

A) El conjunto de programas que hacen utilizable el hardware y proporcionan a las aplicaciones un entorno de ejecución homogéneo
B) El software que resuelve directamente el problema funcional del usuario final
C) Exclusivamente el núcleo del sistema operativo, sin controladores ni bibliotecas

<details><summary>Respuesta</summary>

**Correcta: A) El conjunto de programas que hacen utilizable el hardware y proporcionan a las aplicaciones un entorno de ejecución homogéneo** Incluye firmware, sistema operativo, controladores, bibliotecas del sistema, utilidades y, en sentido amplio, el middleware. No resuelve el problema del usuario: habilita a quien lo resuelve.

*Referencia: §1.1 [SILBERSCHATZ]*
</details>

---

### Pregunta 2

**¿Cuál es la única vía legítima para que una aplicación en modo usuario solicite un servicio del núcleo?**

A) El acceso directo a los registros del dispositivo
B) La escritura en el sector de arranque del disco
C) La llamada al sistema (*system call*), que provoca un cambio controlado a modo núcleo

<details><summary>Respuesta</summary>

**Correcta: C) La llamada al sistema (*system call*), que provoca un cambio controlado a modo núcleo** El hardware distingue modo privilegiado y modo usuario; una aplicación nunca toca el hardware directamente. Las llamadas tienen un coste, por lo que agrupar el trabajo rinde mejor que hacer millones de llamadas pequeñas.

*Referencia: §1.1 [STALLINGS] [POSIX]*
</details>

---

### Pregunta 3

**En un núcleo monolítico:**

A) Solo permanecen en modo núcleo la planificación, la memoria básica y la comunicación entre procesos
B) Todos los servicios del sistema (archivos, red, controladores) se ejecutan dentro del espacio del núcleo
C) Cada servicio se ejecuta en una máquina virtual independiente

<details><summary>Respuesta</summary>

**Correcta: B) Todos los servicios del sistema (archivos, red, controladores) se ejecutan dentro del espacio del núcleo** De ahí su ventaja (rendimiento: las llamadas entre subsistemas son llamadas a función) y su inconveniente (un fallo en un controlador puede tumbar el sistema entero).

*Referencia: §1.1.1 [TANENBAUM]*
</details>

---

### Pregunta 4

**¿Cómo se clasifica el núcleo de Linux?**

A) Monolítico modular, con módulos cargables y descargables en caliente
B) Micronúcleo puro, con los controladores en modo usuario
C) Núcleo por capas estrictas, sin posibilidad de extensión en ejecución

<details><summary>Respuesta</summary>

**Correcta: A) Monolítico modular, con módulos cargables y descargables en caliente** Es un error frecuente confundir la modularidad con el micronúcleo: los módulos de Linux se cargan **dentro** del espacio del núcleo (`lsmod`, `modprobe`, `rmmod`). Micronúcleos puros son MINIX 3, QNX o L4.

*Referencia: §1.1.1 [TANENBAUM]*
</details>

---

### Pregunta 5

**¿Qué permanece en el espacio del núcleo en una arquitectura de micronúcleo?**

A) Los sistemas de archivos y la pila de red completa
B) Únicamente la planificación, la gestión básica de memoria y la comunicación entre procesos
C) Todos los controladores de dispositivo, por razones de rendimiento

<details><summary>Respuesta</summary>

**Correcta: B) Únicamente la planificación, la gestión básica de memoria y la comunicación entre procesos** El resto —sistemas de archivos, pila de red, controladores— corre como procesos servidores en modo usuario que se comunican por paso de mensajes. Gana robustez y pierde rendimiento.

*Referencia: §1.1.1 [TANENBAUM] [SILBERSCHATZ]*
</details>

---

### Pregunta 6

**La partición del sistema EFI (ESP) que utiliza el arranque UEFI:**

A) Se ubica siempre en el sector 0 del disco, en formato MBR
B) Debe estar cifrada obligatoriamente con la clave del TPM
C) Está formateada en FAT32 y contiene los archivos `.efi` de arranque

<details><summary>Respuesta</summary>

**Correcta: C) Está formateada en FAT32 y contiene los archivos `.efi` de arranque** UEFI sustituye a la BIOS heredada, trabaja con tabla de particiones GPT y localiza los cargadores como archivos dentro de la ESP, en lugar de leer un sector de arranque.

*Referencia: §1.2.1 [UEFI-SPEC]*
</details>

---

### Pregunta 7

**¿Cuál es la función del Arranque Seguro (*Secure Boot*)?**

A) Verificar la firma digital de cada componente de la cadena de arranque antes de ejecutarlo
B) Cifrar el contenido del disco duro para impedir su lectura si se extrae
C) Realizar una copia de seguridad automática del sector de arranque en cada inicio

<details><summary>Respuesta</summary>

**Correcta: A) Verificar la firma digital de cada componente de la cadena de arranque antes de ejecutarlo** Impide que se cargue código no confiable —como un *rootkit*— antes que el sistema operativo. Un núcleo o un controlador sin firmar detiene el arranque, lo que a veces se manifiesta justo después de una actualización.

*Referencia: §1.2.1 [UEFI-SPEC]*
</details>

---

### Pregunta 8

**¿Para qué sirve el `initramfs` (o `initrd`) en un sistema Linux?**

A) Para almacenar los registros del sistema durante el arranque
B) Para aportar en memoria los controladores imprescindibles que permiten montar el sistema de archivos raíz real
C) Para sustituir permanentemente al sistema de archivos raíz en sistemas sin disco

<details><summary>Respuesta</summary>

**Correcta: B) Para aportar en memoria los controladores imprescindibles que permiten montar el sistema de archivos raíz real** Si el `initramfs` no incluye el controlador correcto —por ejemplo, el del RAID o el del cifrado—, el núcleo arranca pero no encuentra la raíz y se produce un *kernel panic*: avería clásica tras actualizar el núcleo.

*Referencia: §1.2.1 [RH-DOC] [GRUB-DOC]*
</details>

---

### Pregunta 9

**¿Cuál es la diferencia esencial entre un proceso y un hilo?**

A) El hilo puede ejecutarse en modo núcleo y el proceso no
B) El proceso es siempre más rápido de crear que el hilo
C) El proceso posee el espacio de direcciones y los recursos; el hilo es la unidad de planificación y comparte ese espacio

<details><summary>Respuesta</summary>

**Correcta: C) El proceso posee el espacio de direcciones y los recursos; el hilo es la unidad de planificación y comparte ese espacio** Por eso cambiar de hilo dentro de un proceso es más barato que cambiar de proceso, y por eso un hilo que corrompe memoria puede afectar a todos sus hermanos.

*Referencia: §2.1 [SILBERSCHATZ]*
</details>

---

### Pregunta 10

**Ante un servicio que no responde, ¿cuál es la secuencia correcta de terminación?**

A) Enviar primero `SIGTERM` y, solo si no responde, `SIGKILL`
B) Enviar directamente `SIGKILL`, que es el método limpio
C) Enviar `SIGKILL` y a continuación `SIGTERM` para confirmar

<details><summary>Respuesta</summary>

**Correcta: A) Enviar primero `SIGTERM` y, solo si no responde, `SIGKILL`** `SIGTERM` (15) pide terminar y permite al proceso cerrar archivos y guardar estado; `SIGKILL` (9) lo mata sin que pueda capturarlo. Matar así un gestor de bases de datos puede exigir después una recuperación.

*Referencia: §2.1 [MAN-PAGES]*
</details>

---

### Pregunta 11

**Un proceso «zombi» es aquel que:**

A) Consume el 100 % de la CPU sin realizar trabajo útil
B) Ha terminado, pero su proceso padre no ha recogido su código de salida
C) Está bloqueado en una operación de entrada/salida que no responde

<details><summary>Respuesta</summary>

**Correcta: B) Ha terminado, pero su proceso padre no ha recogido su código de salida** Ocupa una entrada en la tabla de procesos pero no consume CPU. La acumulación de zombis indica un programa padre mal escrito. El proceso cuyo padre muere antes que él es el «huérfano», adoptado por el PID 1.

*Referencia: §2.1 [SILBERSCHATZ] [MAN-PAGES]*
</details>

---

### Pregunta 12

**Un servidor presenta CPU de usuario muy baja, porcentaje de espera de E/S muy alto y valores de intercambio (`si`/`so`) constantemente elevados. ¿Qué está ocurriendo?**

A) Un ataque de denegación de servicio sobre la interfaz de red
B) Una saturación del procesador por exceso de hilos activos
C) Hiperpaginación (*thrashing*): el sistema dedica más tiempo a intercambiar páginas que a trabajar

<details><summary>Respuesta</summary>

**Correcta: C) Hiperpaginación (*thrashing*): el sistema dedica más tiempo a intercambiar páginas que a trabajar** La solución no es un disco más rápido, sino reducir el grado de multiprogramación o ampliar la memoria física. Ampliar el espacio de intercambio solo cambia el síntoma.

*Referencia: §2.1 [SILBERSCHATZ]*
</details>

---

### Pregunta 13

**Un «fallo de página» (*page fault*) se produce cuando:**

A) El proceso accede a una página que no está presente en memoria física y el núcleo debe traerla
B) La tabla de páginas se corrompe y hay que reiniciar el sistema
C) Dos procesos intentan escribir simultáneamente en el mismo marco de página

<details><summary>Respuesta</summary>

**Correcta: A) El proceso accede a una página que no está presente en memoria física y el núcleo debe traerla** Es un mecanismo normal de la memoria virtual, no un error: el núcleo trae la página, actualiza la tabla y reanuda la instrucción. El problema aparece cuando la tasa de fallos se dispara.

*Referencia: §2.1 [SILBERSCHATZ] [TANENBAUM]*
</details>

---

### Pregunta 14

**¿Qué aporta el diario (*journaling*) de un sistema de archivos?**

A) Comprime los archivos poco usados para ahorrar espacio
B) Permite recuperar la coherencia en segundos tras un corte, repitiendo o descartando las operaciones incompletas anotadas previamente
C) Registra qué usuario ha accedido a cada archivo, a efectos de auditoría

<details><summary>Respuesta</summary>

**Correcta: B) Permite recuperar la coherencia en segundos tras un corte, repitiendo o descartando las operaciones incompletas anotadas previamente** Un sistema sin diario, como FAT32, obliga a una comprobación completa del volumen y puede perder datos. La auditoría de accesos es cosa del registro de eventos, no del diario.

*Referencia: §2.2 [SILBERSCHATZ]*
</details>

---

### Pregunta 15

**Se ha ejecutado `lvextend` para ampliar un volumen lógico, pero `df -h` sigue mostrando el tamaño anterior. ¿Qué falta?**

A) Reiniciar el servidor para que el núcleo relea la tabla de particiones
B) Volver a crear el grupo de volúmenes desde cero
C) Ampliar el sistema de archivos que reside dentro del volumen (`resize2fs`, `xfs_growfs`)

<details><summary>Respuesta</summary>

**Correcta: C) Ampliar el sistema de archivos que reside dentro del volumen (`resize2fs`, `xfs_growfs`)** Ampliar en LVM son dos pasos: primero el volumen lógico y después el sistema de archivos. Ninguno de los dos exige reiniciar: ambos pueden hacerse en caliente.

*Referencia: §2.2.1 [LVM-DOC] [RH-DOC]*
</details>

---

### Pregunta 16

**En un sistema de cuotas de disco, el límite blando (*soft*):**

A) Puede superarse temporalmente durante un periodo de gracia, con avisos al usuario
B) Impide cualquier escritura en el momento en que se alcanza
C) Se aplica solo a los administradores del sistema

<details><summary>Respuesta</summary>

**Correcta: A) Puede superarse temporalmente durante un periodo de gracia, con avisos al usuario** El que impide la escritura sin excepción es el límite duro (*hard*). Las cuotas evitan que un solo usuario o proceso agote un volumen compartido y provoque una caída, que es una incidencia de disponibilidad.

*Referencia: §2.2.1 [MAN-PAGES] [ENS]*
</details>

---

### Pregunta 17

**En Windows, si se elimina una cuenta de usuario y se vuelve a crear con el mismo nombre:**

A) Conserva todos sus permisos, porque las ACL guardan el nombre de la cuenta
B) Pierde todos sus permisos, porque se genera un SID nuevo y las ACL guardan el SID, no el nombre
C) Conserva los permisos solo si se recrea en la misma unidad organizativa

<details><summary>Respuesta</summary>

**Correcta: B) Pierde todos sus permisos, porque se genera un SID nuevo y las ACL guardan el SID, no el nombre** Por eso **renombrar** una cuenta es seguro (conserva el SID) y **borrarla y recrearla** no lo es. Es un error clásico en la gestión de altas y bajas.

*Referencia: §3.1 [MS-AD]*
</details>

---

### Pregunta 18

**En una lista de control de acceso (ACL) de Windows, si un usuario tiene concedido el permiso de lectura por pertenecer a un grupo y denegado explícitamente ese mismo permiso por otra entrada:**

A) Prevalece el permiso concedido, por ser más específico
B) El sistema solicita al administrador que resuelva el conflicto
C) Prevalece la denegación explícita y el acceso se rechaza

<details><summary>Respuesta</summary>

**Correcta: C) Prevalece la denegación explícita y el acceso se rechaza** Es la regla básica de evaluación de ACL: la denegación explícita gana sobre el permiso. Los permisos, además, se heredan del contenedor padre salvo que se rompa expresamente la herencia.

*Referencia: §3.1 [MS-AD]*
</details>

---

### Pregunta 19

**El orden de precedencia en la aplicación de las directivas de grupo (GPO) es:**

A) Local, Sitio, Dominio y Unidad organizativa, prevaleciendo la última aplicada
B) Unidad organizativa, Dominio, Sitio y Local, prevaleciendo la primera aplicada
C) Alfabético por nombre de la directiva, sin relación con la estructura del directorio

<details><summary>Respuesta</summary>

**Correcta: A) Local, Sitio, Dominio y Unidad organizativa, prevaleciendo la última aplicada** Es la regla conocida como LSDUO (o LSDOU): gana la directiva más cercana al objeto, salvo bloqueos de herencia o directivas marcadas como obligatorias.

*Referencia: §3.1 [MS-GPO]*
</details>

---

### Pregunta 20

**Dentro del modelo AAA, ¿a qué pregunta responde la autorización?**

A) ¿Quién eres?
B) ¿Qué hiciste?
C) ¿Qué puedes hacer?

<details><summary>Respuesta</summary>

**Correcta: C) ¿Qué puedes hacer?** La autenticación responde a «¿quién eres?» y la auditoría o trazabilidad, a «¿qué hiciste?». Son tres funciones distintas y consecutivas, y las tres son exigibles en el Esquema Nacional de Seguridad.

*Referencia: §3.1.1 [ENS]*
</details>

---

### Pregunta 21

**¿Cuál de estas combinaciones constituye una autenticación multifactor?**

A) Contraseña más pregunta de seguridad
B) Contraseña más código generado por una aplicación en el teléfono
C) Contraseña más repetición de la contraseña en un segundo campo

<details><summary>Respuesta</summary>

**Correcta: B) Contraseña más código generado por una aplicación en el teléfono** Combina «algo que sabes» con «algo que tienes», es decir, factores de **categorías distintas**. Contraseña y pregunta de seguridad son ambos «algo que sabes», por lo que no constituyen multifactor.

*Referencia: §3.1.1 [ISO27002] [ENS]*
</details>

---

### Pregunta 22

**El modelo de control de acceso basado en roles (RBAC) se caracteriza porque:**

A) Los permisos se asignan a roles y las personas se adscriben a esos roles
B) El propietario de cada recurso decide discrecionalmente quién accede
C) La política la impone el sistema mediante etiquetas de seguridad inalterables por el usuario

<details><summary>Respuesta</summary>

**Correcta: A) Los permisos se asignan a roles y las personas se adscriben a esos roles** Es el modelo recomendado en organizaciones grandes porque el alta y la baja se reducen a añadir o retirar el rol. La opción B describe el modelo discrecional (DAC) y la C, el obligatorio (MAC).

*Referencia: §3.1.1 [SILBERSCHATZ]*
</details>

---

### Pregunta 23

**¿Qué diferencia hay entre `systemctl start apache2` y `systemctl enable apache2`?**

A) Ninguna: son sinónimos en systemd
B) `start` habilita el arranque automático y `enable` lo arranca en ese momento
C) `start` lo arranca en ese momento y `enable` lo habilita para el próximo inicio del sistema

<details><summary>Respuesta</summary>

**Correcta: C) `start` lo arranca en ese momento y `enable` lo habilita para el próximo inicio del sistema** Son operaciones independientes: `enable --now` hace ambas. El equivalente conceptual en Windows es la diferencia entre el **estado** del servicio y su **tipo de inicio**.

*Referencia: §3.2 [SYSTEMD] [MS-WINSERVER]*
</details>

---

### Pregunta 24

**¿Qué significa la línea de `cron` siguiente: `30 2 * * 1`?**

A) Cada 30 minutos durante las dos primeras horas del día 1 de cada mes
B) Los lunes a las 02:30
C) El día 30 de febrero, a la hora 1 (entrada inválida)

<details><summary>Respuesta</summary>

**Correcta: B) Los lunes a las 02:30** Los cinco campos son, en este orden: minuto, hora, día del mes, mes y día de la semana (0-7, con 0 y 7 = domingo). Aquí: minuto 30, hora 2, cualquier día del mes, cualquier mes, día de la semana 1 (lunes).

*Referencia: §3.2 [MAN-PAGES]*
</details>

---

### Pregunta 25

**¿Cuál es la medida del anexo II del ENS que exige mantener un inventario actualizado de todos los elementos del sistema y se aplica en las tres categorías?**

A) `op.exp.1` — Inventario de activos
B) `mp.info.6` — Copias de seguridad
C) `op.cont.2` — Plan de continuidad

<details><summary>Respuesta</summary>

**Correcta: A) `op.exp.1` — Inventario de activos** Es la medida fundacional: sin inventario no puede haber análisis de riesgos, ni gestión de parches, ni recuperación fiable. Se aplica en categoría BÁSICA, MEDIA y ALTA sin excepción.

*Referencia: §4.1 [ENS]*
</details>

---

### Pregunta 26

**Reiniciar un servicio caído para devolver el servicio al usuario y, días después, investigar por qué se caía cada martes, corresponde respectivamente a:**

A) Gestión de cambios y gestión de configuración
B) Gestión de problemas y gestión de incidencias
C) Gestión de incidencias y gestión de problemas

<details><summary>Respuesta</summary>

**Correcta: C) Gestión de incidencias y gestión de problemas** La incidencia busca **restablecer** el servicio cuanto antes, aunque sea con una solución temporal; el problema busca eliminar la **causa subyacente**. Son objetivos distintos y sucesivos.

*Referencia: §4.1 [ITIL] [ISO20000]*
</details>

---

### Pregunta 27

**Un sistema tiene la dimensión de disponibilidad valorada en nivel ALTO y todas las demás en nivel BAJO. ¿Cuál es su categoría según el ENS?**

A) BÁSICA, porque predominan las dimensiones de nivel bajo
B) ALTA, porque basta con que una dimensión alcance el nivel ALTO
C) MEDIA, como resultado de promediar los niveles de las cinco dimensiones

<details><summary>Respuesta</summary>

**Correcta: B) ALTA, porque basta con que una dimensión alcance el nivel ALTO** La categoría no se promedia: manda la dimensión más alta. Es MEDIA cuando alguna alcanza el nivel MEDIO y ninguna lo supera, y BÁSICA cuando alguna alcanza el nivel BAJO y ninguna lo supera.

*Referencia: §4.2.1 [ENS]*
</details>

---

### Pregunta 28

**¿Cuáles son las cinco dimensiones de seguridad del anexo I del ENS?**

A) Disponibilidad, integridad, confidencialidad, autenticidad y trazabilidad
B) Disponibilidad, integridad, confidencialidad, interoperabilidad y accesibilidad
C) Confidencialidad, integridad, disponibilidad, eficiencia y economía

<details><summary>Respuesta</summary>

**Correcta: A) Disponibilidad, integridad, confidencialidad, autenticidad y trazabilidad** Mnemotécnica: D-I-C-A-T. La interoperabilidad y la accesibilidad son exigencias reales, pero pertenecen al Esquema Nacional de Interoperabilidad y a la normativa de accesibilidad, no a las dimensiones del ENS.

*Referencia: §4.2.1 [ENS]*
</details>

---

### Pregunta 29

**Respecto a la diferenciación de responsabilidades del artículo 11 del ENS, es cierto que:**

A) El responsable del sistema y el responsable de la seguridad deben ser necesariamente la misma persona
B) Solo se exige designar un responsable de la seguridad, y los demás papeles son opcionales
C) La responsabilidad de la seguridad debe estar diferenciada de la responsabilidad sobre la explotación del sistema

<details><summary>Respuesta</summary>

**Correcta: C) La responsabilidad de la seguridad debe estar diferenciada de la responsabilidad sobre la explotación del sistema** El ENS distingue cuatro papeles: responsable de la información, del servicio, de la seguridad y del sistema. Quien administra no puede ser, a la vez, quien decide y supervisa si esa administración es segura.

*Referencia: §4.2.1 [ENS]*
</details>

---

### Pregunta 30

**Sobre la auditoría de la seguridad prevista en el ENS:**

A) Debe realizarse mensualmente en todos los sistemas, con independencia de su categoría
B) Es una auditoría regular ordinaria al menos cada dos años, y extraordinaria ante modificaciones sustanciales; los sistemas de categoría BÁSICA requieren autoevaluación
C) Solo se realiza cuando se produce un incidente de seguridad con impacto acreditado

<details><summary>Respuesta</summary>

**Correcta: B) Es una auditoría regular ordinaria al menos cada dos años, y extraordinaria ante modificaciones sustanciales; los sistemas de categoría BÁSICA requieren autoevaluación** La auditoría extraordinaria, además, reinicia el cómputo del plazo de dos años para la siguiente ordinaria.

*Referencia: §4.2.1 [ENS]*
</details>

---

### Pregunta 31

**El artículo 21 del ENS, «Integridad y actualización del sistema», exige:**

A) Autorización formal previa para incluir o modificar cualquier elemento físico o lógico del catálogo de activos, y evaluación y monitorización permanentes
B) Que todas las actualizaciones se apliquen automáticamente en el plazo de 24 horas desde su publicación
C) Que el sistema se reinstale íntegramente cada doce meses

<details><summary>Respuesta</summary>

**Correcta: A) Autorización formal previa para incluir o modificar cualquier elemento físico o lógico del catálogo de activos, y evaluación y monitorización permanentes** La monitorización permanente permite adecuar el estado de seguridad atendiendo a deficiencias de configuración, vulnerabilidades identificadas y actualizaciones que afecten al sistema.

*Referencia: §4.2.1 [ENS]*
</details>

---

### Pregunta 32

**¿Qué exige el artículo 32 del RGPD en relación con las copias de seguridad?**

A) Que las copias se conserven exactamente durante cinco años
B) Que las copias se almacenen siempre fuera del territorio de la Unión Europea
C) La capacidad de restaurar la disponibilidad y el acceso a los datos personales de forma rápida tras un incidente, y la verificación regular de la eficacia de las medidas

<details><summary>Respuesta</summary>

**Correcta: C) La capacidad de restaurar la disponibilidad y el acceso a los datos personales de forma rápida tras un incidente, y la verificación regular de la eficacia de las medidas** Es decir: copiar **y** probar la restauración no es una buena práctica opcional, sino una obligación legal.

*Referencia: §4.2 [RGPD]*
</details>

---

### Pregunta 33

**Sustituir un disco cuyo recuento de sectores reasignados está creciendo, antes de que llegue a fallar, es un ejemplo de mantenimiento:**

A) Correctivo, porque el disco presenta un defecto
B) Preventivo, porque actúa sobre un fallo latente antes de que se manifieste
C) Adaptativo, porque adapta el sistema a un hardware nuevo

<details><summary>Respuesta</summary>

**Correcta: B) Preventivo, porque actúa sobre un fallo latente antes de que se manifieste** El criterio que separa los tipos de mantenimiento es el momento y la causa: el correctivo es reactivo (ya ha fallado) y el preventivo, proactivo. Guiado por telemetría S.M.A.R.T., se denomina además predictivo.

*Referencia: §5.1 [ISO14764] [SMART-DOC]*
</details>

---

### Pregunta 34

**El mantenimiento «evolutivo» del enunciado oficial se corresponde, en la norma ISO/IEC 14764, con:**

A) El mantenimiento perfectivo más el adaptativo
B) El mantenimiento correctivo más el preventivo
C) Únicamente el mantenimiento correctivo de emergencia

<details><summary>Respuesta</summary>

**Correcta: A) El mantenimiento perfectivo más el adaptativo** El perfectivo mejora rendimiento o mantenibilidad sin corregir ningún fallo; el adaptativo acomoda cambios del entorno (nueva versión soportada, hardware nuevo, cambio normativo). Ninguno responde a un fallo ya producido.

*Referencia: §5.1 [ISO14764]*
</details>

---

### Pregunta 35

**Respecto al mantenimiento de una unidad de estado sólido (SSD):**

A) Debe desfragmentarse semanalmente para mantener el rendimiento
B) No debe desfragmentarse: la operación adecuada es TRIM u optimización
C) Debe formatearse a bajo nivel cada seis meses

<details><summary>Respuesta</summary>

**Correcta: B) No debe desfragmentarse: la operación adecuada es TRIM u optimización** Desfragmentar una SSD no mejora nada y consume ciclos de escritura, acortando su vida. TRIM informa al dispositivo de qué bloques ya no contienen datos válidos.

*Referencia: §5.1 [MS-PERF]*
</details>

---

### Pregunta 36

**¿Qué es una «línea base» (*baseline*) en monitorización de sistemas?**

A) El valor máximo que un contador puede alcanzar antes de generar una alarma
B) El límite contractual de disponibilidad fijado en el acuerdo de nivel de servicio
C) La medición del comportamiento normal del sistema con la que se comparan las mediciones posteriores

<details><summary>Respuesta</summary>

**Correcta: C) La medición del comportamiento normal del sistema con la que se comparan las mediciones posteriores** Sin línea base, afirmar que un servidor «va lento» no es verificable. Conviene rehacerla tras cada cambio importante y desglosarla por franja horaria y día de la semana.

*Referencia: §5.2 [MS-PERF]*
</details>

---

### Pregunta 37

**Una disponibilidad comprometida del 99,9 % anual equivale aproximadamente a una caída máxima de:**

A) Unas 8 horas y 46 minutos al año
B) Unos 5 minutos al año
C) Unos 3 días y 15 horas al año

<details><summary>Respuesta</summary>

**Correcta: A) Unas 8 horas y 46 minutos al año** Los «cinco nueves» (99,999 %) equivalen a unos 5 minutos anuales y el 99 % («dos nueves»), a unos 3 días y 15 horas. Las paradas planificadas y comunicadas suelen quedar excluidas del cómputo.

*Referencia: §5.2 [ISO20000]*
</details>

---

### Pregunta 38

**Los indicadores MTBF y MTTR miden, respectivamente:**

A) El coste medio de un fallo y el coste medio de una reparación
B) El tiempo medio entre fallos (fiabilidad) y el tiempo medio de reparación (capacidad de recuperación)
C) El número medio de incidencias por usuario y por servicio

<details><summary>Respuesta</summary>

**Correcta: B) El tiempo medio entre fallos (fiabilidad) y el tiempo medio de reparación (capacidad de recuperación)** La disponibilidad puede expresarse como MTBF ÷ (MTBF + MTTR): se mejora espaciando los fallos o reparando más rápido, y lo segundo suele ser más barato.

*Referencia: §5.2 [ISO20000]*
</details>

---

### Pregunta 39

**Al dimensionar un sistema en la gestión de capacidad, lo correcto es:**

A) Tomar el valor mínimo registrado, para no sobredimensionar la inversión
B) Tomar la media aritmética del uso diario a lo largo del año
C) Tomar un percentil alto de la carga (por ejemplo, el percentil 95) y considerar los picos previsibles del calendario

<details><summary>Respuesta</summary>

**Correcta: C) Tomar un percentil alto de la carga (por ejemplo, el percentil 95) y considerar los picos previsibles del calendario** La media oculta los picos, y son los picos los que tiran el servicio: apertura de plazos, campañas de tributos o convocatorias de empleo público.

*Referencia: §5.2 [ISO20000]*
</details>

---

### Pregunta 40

**Un servidor Linux muestra muy poca memoria «libre» pero mucha memoria «disponible». La interpretación correcta es:**

A) Es normal y deseable: el sistema usa la memoria sobrante como caché de disco y la cede cuando hace falta
B) El servidor está a punto de agotar la memoria y hay que reiniciarlo
C) Hay una fuga de memoria en el núcleo que exige actualizarlo

<details><summary>Respuesta</summary>

**Correcta: A) Es normal y deseable: el sistema usa la memoria sobrante como caché de disco y la cede cuando hace falta** La métrica que hay que vigilar es la memoria **disponible** y, sobre todo, la tasa de intercambio (`si`/`so`), no la memoria «libre».

*Referencia: §5.2.1 [MAN-PAGES]*
</details>

---

### Pregunta 41

**Mantener en producción un sistema operativo que ha alcanzado su fin de vida (EOL) implica:**

A) Un ahorro admisible siempre que el sistema no esté publicado en Internet
B) Que las nuevas vulnerabilidades descubiertas quedarán sin corregir, lo que en el sector público supone un incumplimiento del ENS
C) Que el fabricante sigue publicando parches de seguridad, aunque no funcionales

<details><summary>Respuesta</summary>

**Correcta: B) Que las nuevas vulnerabilidades descubiertas quedarán sin corregir, lo que en el sector público supone un incumplimiento del ENS** Si es inevitable convivir con él temporalmente, hay que documentar la excepción con su análisis de riesgo, medidas compensatorias (aislamiento, restricción de accesos, vigilancia reforzada) y fecha límite de migración.

*Referencia: §6.1 [ENS]*
</details>

---

### Pregunta 42

**En versionado semántico, el paso de la versión 4.2.7 a la 5.0.0 indica:**

A) Una simple corrección de errores, sin riesgo apreciable
B) Funcionalidad nueva compatible con la versión anterior
C) Cambios incompatibles con la versión anterior, que exigen pruebas completas antes de producción

<details><summary>Respuesta</summary>

**Correcta: C) Cambios incompatibles con la versión anterior, que exigen pruebas completas antes de producción** En `MAYOR.MENOR.PARCHE`, el incremento de la cifra mayor anuncia ruptura de compatibilidad; el de la menor, funcionalidad compatible; y el del parche, corrección de errores.

*Referencia: §6.1 [SEMVER]*
</details>

---

### Pregunta 43

**¿Qué diferencia hay entre CVE y CVSS?**

A) CVE es el identificador único y público de una vulnerabilidad; CVSS es la puntuación de su gravedad
B) CVE es la puntuación de gravedad; CVSS es el catálogo de fabricantes afectados
C) Son dos nombres del mismo sistema, según se use en Europa o en Estados Unidos

<details><summary>Respuesta</summary>

**Correcta: A) CVE es el identificador único y público de una vulnerabilidad; CVSS es la puntuación de su gravedad** Regla mnemotécnica: **CVE identifica, CVSS puntúa**. La prioridad real de parcheo combina la puntuación con la exposición del activo, su criticidad y la existencia de explotación activa.

*Referencia: §6.1 [CVE] [NIST-CVSS]*
</details>

---

### Pregunta 44

**En la escala CVSS, una vulnerabilidad se considera de gravedad CRÍTICA cuando su puntuación se sitúa entre:**

A) 7,0 y 8,9
B) 9,0 y 10,0
C) 4,0 y 6,9

<details><summary>Respuesta</summary>

**Correcta: B) 9,0 y 10,0** Las bandas son: baja (0,1-3,9), media (4,0-6,9), alta (7,0-8,9) y crítica (9,0-10,0). La puntuación ordena la prioridad, pero no la determina por sí sola.

*Referencia: §6.1 [NIST-CVSS]*
</details>

---

### Pregunta 45

**Ante una vulnerabilidad de día cero (*zero-day*) que afecta a un servicio publicado, la actuación correcta es:**

A) Esperar sin actuar hasta que el fabricante publique el parche oficial
B) Apagar definitivamente el servicio y no volver a prestarlo
C) Aplicar mitigaciones temporales —deshabilitar la función afectada, filtrar accesos, reforzar la vigilancia— y documentarlas hasta que exista parche

<details><summary>Respuesta</summary>

**Correcta: C) Aplicar mitigaciones temporales —deshabilitar la función afectada, filtrar accesos, reforzar la vigilancia— y documentarlas hasta que exista parche** Un día cero es una vulnerabilidad conocida y explotada sin corrección disponible: no actuar equivale a aceptar el riesgo sin medida compensatoria alguna.

*Referencia: §6.1 [NIST80040]*
</details>

---

### Pregunta 46

**¿Cuál es el primer paso del proceso de gestión de parches según la metodología del NIST?**

A) Inventariar los activos y el software instalado
B) Desplegar el parche en el entorno de producción crítica
C) Redactar el informe de cumplimiento para la auditoría

<details><summary>Respuesta</summary>

**Correcta: A) Inventariar los activos y el software instalado** Sin inventario no se sabe qué hay que parchear. La secuencia completa es: inventariar, identificar, priorizar, probar, desplegar y verificar y documentar.

*Referencia: §6.2 [NIST80040] [ENS]*
</details>

---

### Pregunta 47

**El despliegue de actualizaciones «por anillos» consiste en:**

A) Aplicar el parche simultáneamente en todo el parque para reducir la ventana de exposición
B) Aplicarlo en oleadas sucesivas —laboratorio, piloto, producción no crítica y producción crítica— con verificación entre etapas
C) Instalar el parche solo en las máquinas que el usuario solicite expresamente

<details><summary>Respuesta</summary>

**Correcta: B) Aplicarlo en oleadas sucesivas —laboratorio, piloto, producción no crítica y producción crítica— con verificación entre etapas** El anillo piloto debe ser **representativo** del parque: si deja fuera un modelo de equipo o un software departamental, el fallo aparecerá en el despliegue masivo.

*Referencia: §6.2 [NIST80040] [MS-WSUS]*
</details>

---

### Pregunta 48

**El refuerzo R2 de la medida `op.exp.4` del ENS exige que, antes de aplicar configuraciones, parches y actualizaciones de seguridad:**

A) Se comunique la intervención al Centro Criptológico Nacional
B) Se obtenga la conformidad expresa de todos los usuarios afectados
C) Se prevea un mecanismo para revertirlos en caso de aparición de efectos adversos

<details><summary>Respuesta</summary>

**Correcta: C) Se prevea un mecanismo para revertirlos en caso de aparición de efectos adversos** Es la formulación normativa de la regla de oro del parcheo: no se aplica en producción un cambio que no se sepa deshacer. El refuerzo R1 de la misma medida exige la prueba previa en un entorno equivalente al de producción.

*Referencia: §6.2.1 [ENS]*
</details>

---

### Pregunta 49

**En el protocolo syslog, ¿qué relación hay entre el número de severidad y la gravedad del mensaje?**

A) Cuanto menor es el número, más grave es el mensaje: 0 es «emergencia» y 7 es «depuración»
B) Cuanto mayor es el número, más grave es el mensaje: 7 es «emergencia» y 0 es «depuración»
C) El número indica el subsistema emisor y no guarda relación con la gravedad

<details><summary>Respuesta</summary>

**Correcta: A) Cuanto menor es el número, más grave es el mensaje: 0 es «emergencia» y 7 es «depuración»** El subsistema emisor lo indica la **facilidad** (`auth`, `cron`, `kern`…), no la severidad. Filtrar «severidad 3 o inferior» significa quedarse con los errores y todo lo más grave.

*Referencia: §7.1 [RFC5424]*
</details>

---

### Pregunta 50

**¿Por qué es imprescindible la sincronización horaria (NTP) en la gestión de registros?**

A) Porque los registros solo se escriben en horario laboral
B) Porque el protocolo syslog rechaza mensajes con marca de tiempo
C) Porque sin una hora común entre sistemas no es posible correlacionar los eventos de varias máquinas

<details><summary>Respuesta</summary>

**Correcta: C) Porque sin una hora común entre sistemas no es posible correlacionar los eventos de varias máquinas** Un reloj desincronizado, además, provoca fallos de autenticación en protocolos que dependen de marcas de tiempo y resta valor probatorio a los registros.

*Referencia: §7.1 [RFC5905] [NIST80092]*
</details>

---

### Pregunta 51

**¿Cuál es la razón principal para centralizar los registros en un servidor distinto del auditado?**

A) Reducir el consumo de disco del servidor de aplicaciones
B) Impedir que quien comprometa una máquina pueda borrar las huellas de su actividad
C) Cumplir el requisito de interoperabilidad del ENI en materia de formatos

<details><summary>Respuesta</summary>

**Correcta: B) Impedir que quien comprometa una máquina pueda borrar las huellas de su actividad** Es una medida de seguridad, no de ahorro: el atacante que obtiene privilegios en un sistema intenta borrar sus registros, y no debe poder hacerlo en el repositorio central.

*Referencia: §7.1 [NIST80092] [ENS]*
</details>

---

### Pregunta 52

**Ante una incidencia que ha dejado sin servicio a la sede electrónica, el orden de actuación correcto es:**

A) Contener y restablecer el servicio primero, y analizar la causa raíz después
B) Analizar exhaustivamente la causa raíz antes de tocar nada, para no perder información
C) Notificar a los medios de comunicación antes de intervenir técnicamente

<details><summary>Respuesta</summary>

**Correcta: A) Contener y restablecer el servicio primero, y analizar la causa raíz después** Restablecer y averiguar la causa son objetivos distintos y sucesivos. Quedarse depurando con el servicio caído es el error típico. La preservación de evidencias, cuando hay sospecha de incidente de seguridad, se compatibiliza aislando el sistema en lugar de apagarlo precipitadamente.

*Referencia: §7.2 [ITIL] [NIST80061]*
</details>

---

### Pregunta 53

**Varios servicios de un servidor fallan de forma aparentemente aleatoria, no se puede iniciar sesión gráfica y la base de datos ha pasado a solo lectura. La primera comprobación debe ser:**

A) Reinstalar el sistema operativo desde la imagen corporativa
B) Sustituir la tarjeta de red por si estuviera defectuosa
C) El espacio libre en disco y en inodos de los sistemas de archivos

<details><summary>Respuesta</summary>

**Correcta: C) El espacio libre en disco y en inodos de los sistemas de archivos** El disco lleno es la causa número uno de incidencias «misteriosas», y `df -h` junto con `df -i` la resuelven en segundos. Un sistema de archivos puede además quedarse sin inodos aun teniendo espacio libre.

*Referencia: §7.2 [MAN-PAGES]*
</details>

---

### Pregunta 54

**Las fases de la gestión de incidentes de seguridad según el NIST son:**

A) Detección, facturación, sustitución y archivo
B) Preparación; detección y análisis; contención, erradicación y recuperación; y lecciones aprendidas
C) Auditoría, sanción, publicación y cierre

<details><summary>Respuesta</summary>

**Correcta: B) Preparación; detección y análisis; contención, erradicación y recuperación; y lecciones aprendidas** A ello se añade, en el sector público, la notificación del incidente conforme al procedimiento del ENS y, si hay datos personales comprometidos, la notificación de la brecha conforme al RGPD.

*Referencia: §7.2 [NIST80061] [ENS]*
</details>

---

### Pregunta 55

**En un equipo Windows con el almacén de componentes dañado, el orden correcto de reparación es:**

A) Ejecutar `DISM /RestoreHealth` para reparar el almacén y después `sfc /scannow` para reparar los archivos del sistema
B) Ejecutar `sfc /scannow` primero y `DISM` solo si el equipo no arranca
C) Formatear la partición del sistema, porque no hay reparación posible

<details><summary>Respuesta</summary>

**Correcta: A) Ejecutar `DISM /RestoreHealth` para reparar el almacén y después `sfc /scannow` para reparar los archivos del sistema** `sfc` toma los archivos de reemplazo del almacén de componentes: si ese almacén está corrupto, `sfc` no puede reparar nada. De ahí el orden.

*Referencia: §8.1 [MS-WINRE]*
</details>

---

### Pregunta 56

**Respecto a la utilidad `fsck` de comprobación del sistema de archivos:**

A) Debe ejecutarse siempre con el sistema de archivos montado en lectura y escritura, para que pueda corregir en caliente
B) Solo puede ejecutarse desde el gestor de arranque, nunca desde un medio de rescate
C) No debe ejecutarse sobre un sistema de archivos montado en lectura y escritura: se ejecuta desde un medio de rescate, en modo de emergencia o programada para el siguiente arranque

<details><summary>Respuesta</summary>

**Correcta: C) No debe ejecutarse sobre un sistema de archivos montado en lectura y escritura: se ejecuta desde un medio de rescate, en modo de emergencia o programada para el siguiente arranque** Comprobar y reparar un sistema de archivos montado y activo puede destruir datos.

*Referencia: §8.1 [MAN-PAGES]*
</details>

---

### Pregunta 57

**Un servidor Linux arranca pero se queda colgado al iniciar los servicios. ¿Qué mecanismo permite entrar con una sesión de administrador y los servicios detenidos para diagnosticarlo?**

A) Ejecutar `fsck` desde el gestor de arranque GRUB
B) Arrancar en `rescue.target` (o `emergency.target`), editando temporalmente la entrada de GRUB
C) Reinstalar el gestor de arranque con `grub-install`

<details><summary>Respuesta</summary>

**Correcta: B) Arrancar en `rescue.target` (o `emergency.target`), editando temporalmente la entrada de GRUB** `rescue.target` monta el sistema de archivos y ofrece una sesión de administrador sin arrancar los servicios; `emergency.target` es aún más mínimo. El equivalente en Windows es el modo seguro.

*Referencia: §8.1 [SYSTEMD] [GRUB-DOC]*
</details>

---

### Pregunta 58

**El RPO (*Recovery Point Objective*) de un servicio expresa:**

A) La cantidad de datos que se admite perder, medida en tiempo, y determina la frecuencia de las copias
B) El tiempo máximo que el servicio puede permanecer caído antes de restablecerse
C) El porcentaje de disponibilidad comprometido en el acuerdo de nivel de servicio

<details><summary>Respuesta</summary>

**Correcta: A) La cantidad de datos que se admite perder, medida en tiempo, y determina la frecuencia de las copias** El RPO mira hacia atrás (pérdida de datos) y el RTO hacia delante (tiempo sin servicio). Ambos los fija el responsable del servicio a partir del análisis de impacto, no el técnico.

*Referencia: §8.2 [NIST80034] [ISO22301]*
</details>

---

### Pregunta 59

**Para restaurar un sistema protegido con copia total semanal y copias incrementales diarias se necesita:**

A) Únicamente la última copia incremental
B) La copia total y la última copia incremental
C) La copia total y todas las copias incrementales posteriores, en orden

<details><summary>Respuesta</summary>

**Correcta: C) La copia total y todas las copias incrementales posteriores, en orden** La incremental copia lo cambiado desde la última copia de cualquier tipo: si se pierde o corrompe un eslabón, la cadena se rompe. Con copias **diferenciales** bastaría la total más la última diferencial.

*Referencia: §8.2 [NIST80034]*
</details>

---

### Pregunta 60

**Según la medida `mp.info.6` del ENS y sus refuerzos, respecto a las copias de seguridad:**

A) Basta con acreditar que el trabajo de copia finaliza sin errores en el registro de la herramienta
B) Los procedimientos de copia y de restauración deben probarse regularmente, y al menos una copia debe almacenarse separada, en lugar diferente
C) Todas las copias deben conservarse en el mismo centro de proceso de datos, para agilizar la recuperación

<details><summary>Respuesta</summary>

**Correcta: B) Los procedimientos de copia y de restauración deben probarse regularmente, y al menos una copia debe almacenarse separada, en lugar diferente** El objetivo es que un mismo incidente no pueda afectar a la vez al repositorio original y a la copia. Una copia nunca restaurada no es una copia: es una suposición.

*Referencia: §8.2 [ENS] [NIST80034]*
</details>

