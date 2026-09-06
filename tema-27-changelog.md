# Tema 27 — Changelog

> **Título oficial**: Administración del Sistema operativo y software de base. Funciones y responsabilidades. Actualización, mantenimiento y reparación del sistema operativo.

---

## v1.1 — 2026-09-06 — Ficha de extensión y tiempo de estudio

**Estado**: sin cambios de contenido. Solo se añade información sobre el propio tema.

**Motivo**: petición del IAM (Jesús Cuadrado, 02-09-2026) al validar el Tema 30. Acepta la extensión de los temas «compuestos» a condición de que se informe de «su extensión en palabras y tiempo estimado de estudio». Al revisarlo se vio que ese dato solo aparecía en 16 de los 40 temas, y que faltaba justo en los más largos.

### Alcance

- Ficha bajo la cabecera del tema, y al final de la pestaña Índice donde esa pestaña existe:
  - **Extensión**: ~17.500 palabras · 14 diagramas · 60 preguntas de test
  - **Tiempo estimado de estudio**: 16-18 horas (primera vuelta completa, sin contar repasos)
- La cifra de palabras de la tabla de entregables se sincroniza con la ficha, para que el tema no muestre dos recuentos distintos.
- Las horas salen de una fórmula común a los 40 temas, para que sean comparables entre sí: contenido a 1.500 palabras/hora (ritmo de estudio activo), diagramas a una hora por cada cinco y test a dos minutos por pregunta. Se publica como intervalo de dos horas.
- Generado con `_tools-qa/ficha_estudio.py`, idempotente y reejecutable tras cualquier regeneración con `build_tNN.py`.

---

## v1.0 — 2026-08-20 — Primera versión

**Estado**: pendiente de validación por María y Ana, y de revisión técnica del IAM (Jesús Cuadrado).

**Motivo**: desarrollo del Tema 27, dentro de la serie de temas técnicos generados desde cero, replicando la estructura y el formato de los Temas 1, 11, 17-24 ya consolidados.

### Alcance de la v1.0

| Entregable | Cantidad |
|---|---|
| Contenido teórico | ~16.700 palabras · 8 secciones · 31 epígrafes numerados |
| Diagramas SVG inline | 14 (accesibles con `role`/`aria-label`, clases con sufijo único anti-colisión) |
| Banco de preguntas tipo test | 60 preguntas A/B/C con explicación y referencia, balanceadas **20/20/20** (verificado por el generador) |
| Casos prácticos | 3 (puesta en servicio de un servidor de la Sede; ventana de mantenimiento y parche crítico; caída del Padrón, diagnóstico y recuperación) · 10 puntos cada uno |
| Fuentes Tier 1 | 26 referencias canónicas y normativas (Silberschatz, Tanenbaum, Stallings, POSIX, FHS, UEFI, RFC, NIST, ISO/IEC, ENS, ENI, RGPD) |

### Decisiones de generación

1. **Sin material de cliente**: solo el esqueleto `Test_Prompting/temas agosto/27.md`. Desarrollado desde fuentes canónicas y normativa oficial, todas referenciadas.
2. **Mapeo de la estructura del esqueleto** (decisión a validar, anotada en la pestaña Validación): el esqueleto oficial agrupa la materia en **cuatro bloques de primer nivel**, cada uno con dos subbloques, y hasta cuatro niveles de encabezado. Se ha desarrollado como **ocho secciones numeradas** (dos por bloque), con la correspondencia bloque→secciones explicitada en el Índice y en las Convenciones. La alternativa —numerar en cuatro niveles, del tipo `1.1.1.1.`— se descartó por ilegible y por romper con el patrón de tres niveles de toda la serie.
3. **Nada añadido ni suprimido del enunciado**: los 31 epígrafes se corresponden uno a uno con los del esqueleto. El único material fuera de la numeración es el **mapa de equivalencias Windows/Linux**, colocado deliberadamente en «Convenciones» para no inventar epígrafes.
4. **Órdenes reales de shell, PowerShell y `crontab`** (mismo criterio que T21 con Java/Jakarta, T23 con HTML/JS/PHP y T24 con Kotlin/Swift/Dart): la administración de sistemas es una disciplina práctica y el examen pregunta por utilidades concretas; un pseudocódigo agnóstico no serviría.
5. **Datos del ENS verificados contra el BOE, no citados de memoria**: se descargó el **PDF oficial del RD 311/2022 (BOE núm. 106, de 4 de mayo de 2022)** y se extrajo el texto con `pdftotext -layout` para transcribir literalmente los siete principios básicos (art. 5), la diferenciación de responsabilidades (art. 11), la integridad y actualización del sistema (art. 21), la continuidad (art. 26), el régimen de auditoría (art. 31), las cinco dimensiones y las tres categorías del anexo I, y los códigos y refuerzos del anexo II (`op.exp.1` a `op.exp.10`, `op.cont.1` a `op.cont.4` y `mp.info.6`). Los requisitos y refuerzos de **`op.exp.4`** y de **`mp.info.6`** se citan con su redacción literal resumida.
6. **`op.exp.4` como eje normativo del tema**: la medida «Mantenimiento y actualizaciones de seguridad» y sus refuerzos R1 (pruebas en preproducción) y R2 (mecanismo para revertir) son exactamente el enunciado del bloque III traducido a obligación jurídica, y se han usado para articular §6.2 y §6.2.1.
7. **Caso de referencia único para todo el tema**: el parque del **IAM** que sostiene la Sede Electrónica, el Padrón y los puestos de Áreas y Distritos, planteado como supuesto simplificado y no como descripción de una instalación real.
8. **Frontera con temas vecinos** cuidada: los sistemas operativos como tales al **T14**; arquitectura y periféricos a **T11** y **T12**; organizaciones de ficheros a **T13**; puesto de usuario y seguridad en el desarrollo a **T25**; almacenamiento, virtualización de almacenamiento y políticas de copia a **T26**; virtualización a **T28**; gestión de incidencias con el usuario y control remoto a **T29**; administración de redes y gestión de usuarios de red a **T30**; cloud a **T31**; seguridad de sistemas, criptografía y firma a **T32**; seguridad en redes a **T36**; ENS y ENI en su conjunto a **T39**. Además, T5 (deberes del empleado público) y T6 (transparencia) en la parte de responsabilidades.
9. **Anti-colisión de SVG**: las clases CSS de cada diagrama llevan **sufijo numérico único** (`.t1`…`.t14`), evitando el fallo sistémico de estilos que se filtran de un SVG a otro al estar todos embebidos en la misma página (lección de T5).
10. **Distribución A/B/C fijada antes de redactar** y verificada con el generador (lección de T23 y T24): la secuencia de 60 letras se escribió de antemano con exactamente 20 de cada una y `build_t27.py` confirma **20/20/20**.
11. **QA de diagramas con las pestañas forzadas visibles** (lección de T24): el script de comprobación de desbordes activa todas las `.tab-content` antes de medir y deja una sonda de control, porque `getBBox()` devuelve 0×0 en un subárbol con `display:none` y produce un falso «sin desbordes».
12. **Cómputo de extensión medido, no estimado**: la cifra de ~16.700 palabras procede de `wc -w` sobre el `.md`. Con el mismo criterio, T24 arroja ≈12.300, de modo que este tema pasa a ser **el más extenso de la serie técnica**.

### Pendientes para QA / próxima iteración

- Validación de profundidad por María/Ana/IAM (¿alguna sección a ampliar o recortar?).
- Confirmar el criterio de mapeo del esqueleto (cuatro bloques → ocho secciones) y la colocación del mapa Windows/Linux fuera de la numeración.
- Confirmar la frontera con el **Tema 26** en materia de copias de seguridad y con el **Tema 29** en materia de gestión de incidencias.
- Confirmar si conviene desarrollar el **bastionado** (`op.exp.2`) con guías CCN-STIC concretas o si basta el nivel actual dada la existencia del Tema 32.
- **Revisión de vigencia antes de cada convocatoria**: el ENS es modificable y la parte de producto (herramientas de despliegue, versiones) envejece.

### Origen

Generado el 2026-08-20 en el flujo de trabajo de eTrivium, replicando el patrón de los Temas 1 (v2.1), 11 (v3.2), 17-24 (v1.0). `build_t27.py` y `_build_css.txt` persistidos en el repo.
