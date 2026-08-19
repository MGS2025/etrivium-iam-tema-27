# Tema 27 — Checklist de Validación

> **Título oficial**: Administración del Sistema operativo y software de base. Funciones y responsabilidades. Actualización, mantenimiento y reparación del sistema operativo.
> **Versión**: v1.0 — Pendiente validación
> **Fecha**: 2026-08-20
> **Revisores**: María y Ana (eTrivium) · revisión técnica IAM (Jesús Cuadrado)
> **Instrucciones**: marcar cada ítem. Los cambios no se guardan en la web (imprimir o exportar a PDF si se desea fijarlos).

---

## 1. Cobertura del temario oficial

- [ ] **Fundamentos del software de base**: concepto, funciones y clasificación; arquitecturas monolítica, micronúcleo y modular — §1.1
- [ ] **Componentes del software de base**: gestores de arranque, cargadores, controladores y bibliotecas del sistema — §1.2
- [ ] **Gestión de recursos**: procesos, hilos y memoria principal — §2.1
- [ ] **Almacenamiento, archivos y E/S**: volúmenes lógicos, cuotas y dispositivos de bloques — §2.2
- [ ] **Funciones operativas**: usuarios, grupos y directivas; autenticación, autorización y control de acceso local; servicios, demonios y tareas programadas — §3
- [ ] **Responsabilidades organizativas**: documentación, inventario y procedimientos operativos; marco legal y gobernanza; aplicación del ENS — §4
- [ ] **Mantenimiento**: estrategias preventiva, correctiva y evolutiva; monitorización, capacidad y ajuste — §5
- [ ] **Actualizaciones**: ciclo de vida y versiones; despliegue de parches; evaluación de impacto, entornos de prueba y marcha atrás — §6
- [ ] **Diagnóstico**: análisis de registros y auditoría de eventos; identificación y aislamiento de anomalías — §7
- [ ] **Reparación y recuperación**: técnicas de reparación y arranque de emergencia; copias, restauración y continuidad — §8

## 2. Estructura

- [ ] **Decisión a validar**: el esqueleto oficial tiene **cuatro bloques de primer nivel**; aquí se han desarrollado como **ocho secciones numeradas** (dos por bloque), con la correspondencia explicitada en el Índice y en las Convenciones. La alternativa era numerar en cuatro niveles (`1.1.1.1.`), descartada por ilegible. ¿Se acepta el criterio?
- [ ] El mapa de equivalencias Windows/Linux se ha situado **fuera de la numeración oficial** (en Convenciones) para no añadir epígrafes que el esqueleto no contempla. ¿Conforme?

## 3. Contenido teórico

- [ ] El nivel de profundidad (8 secciones, 31 epígrafes, ~16.700 palabras) es adecuado para C1 (¿hay que ampliar o recortar alguna sección?). **Es el tema más extenso de la serie técnica hasta la fecha**
- [ ] La frontera entre **`start` y `enable`**, entre **incidencia, problema y cambio**, entre **RPO y RTO** y entre **copia diferencial e incremental** queda nítida: son los cuatro pares que más se confunden
- [ ] La decisión de usar **órdenes reales** de Linux (shell) y de Windows (PowerShell y símbolo del sistema) en lugar de pseudocódigo es adecuada (mismo criterio que T21, T23 y T24)
- [ ] La frontera con los Temas 11 (arquitectura), 12 (periféricos y almacenamiento físico), 13 (organizaciones de ficheros), 14 (sistemas operativos), 25 (puesto de usuario y seguridad en el desarrollo), 26 (almacenamiento, virtualización y copias), 28 (virtualización), 29 (control remoto e incidencias con el usuario), 30 (redes de área local), 31 (cloud), 32 (seguridad de sistemas), 36 (seguridad en redes) y 39 (ENS/ENI) está clara y sin duplicidades innecesarias
- [ ] Los ejemplos Ayto Madrid (Sede Electrónica, Padrón, puestos de Distrito) son verosímiles y coherentes entre secciones

## 4. Datos normativos (ENS) — verificados contra el BOE

Los siguientes datos se han extraído del **texto oficial del RD 311/2022 publicado en el BOE de 4 de mayo de 2022** (no de memoria ni de fuentes secundarias). Conviene una segunda lectura por parte de la revisión técnica:

- [ ] **Siete principios básicos** (art. 5, desarrollados en arts. 6 a 11): seguridad como proceso integral; gestión basada en riesgos; prevención, detección, respuesta y conservación; líneas de defensa; vigilancia continua; reevaluación periódica; diferenciación de responsabilidades
- [ ] **Art. 11**: cuatro responsables (información, servicio, seguridad y sistema) y separación entre seguridad y explotación
- [ ] **Art. 21** (Integridad y actualización del sistema): autorización formal previa y monitorización permanente
- [ ] **Art. 31**: auditoría ordinaria **al menos cada dos años** y extraordinaria ante modificaciones sustanciales; categoría BÁSICA, **autoevaluación**
- [ ] **Anexo I**: cinco dimensiones (D, I, C, A, T) y tres categorías, determinadas por la dimensión de mayor nivel
- [ ] **Anexo II**: `op.exp.1` Inventario de activos · `op.exp.2` Configuración de seguridad · `op.exp.3` Gestión de la configuración de seguridad · `op.exp.4` **Mantenimiento y actualizaciones de seguridad** (R1 pruebas en preproducción, R2 prevención de fallos) · `op.exp.5` Gestión de cambios · `op.exp.7` Gestión de incidentes · `op.exp.8` Registro de la actividad · `op.cont.1` a `op.cont.4` · `mp.info.6` **Copias de seguridad** (R1 pruebas de recuperación, R2 protección de las copias)
- [ ] Nota de vigencia: el ENS puede ser modificado; **reverificar los códigos y refuerzos antes de cada convocatoria**

## 5. Fuentes

- [ ] Todas las afirmaciones técnicas están respaldadas por fuente Tier 1 (Silberschatz, Tanenbaum, Stallings, POSIX, FHS, UEFI, RFC, NIST, ISO/IEC) o normativa
- [ ] Las referencias inline se corresponden con `tema-27-fuentes.md`
- [ ] Las guías del NIST citadas (SP 800-40 Rev. 4, 800-92, 800-34 Rev. 1, 800-61 Rev. 2) están en su revisión vigente

## 6. Test (60 preguntas)

- [ ] Cada pregunta tiene una sola respuesta correcta e inequívoca
- [ ] Los distractores (A/B/C) son plausibles
- [ ] La distribución de la opción correcta entre A/B/C está equilibrada (**verificada 20/20/20** por el generador)
- [ ] Las explicaciones y referencias de cada respuesta son correctas

## 7. Casos prácticos (3)

- [ ] Realistas y propios del Ayuntamiento (puesta en servicio de un servidor de la Sede; ventana de mantenimiento y parche crítico; caída del Padrón, diagnóstico y recuperación)
- [ ] Soluciones orientativas técnicamente correctas
- [ ] La puntuación de cada caso suma 10 puntos

## 8. Diagramas (14 SVG)

- [ ] Cada diagrama es correcto y legible (también impreso en blanco y negro)
- [ ] Accesibilidad: todos tienen `role="img"` y `aria-label`
- [ ] Sin desbordes de texto ni colisiones de estilo entre SVG (clases con sufijo único, QA de caja contenedora con render en navegador y **pestañas forzadas visibles**)

## 9. Referencias cruzadas a otros temas

- [ ] Validadas contra BOAM 10.032 (T5, T6, T11, T12, T13, T14, T25, T26, T28, T29, T30, T31, T32, T34, T36, T39)
- [ ] Ninguna referencia cruzada cita un enunciado de tema incorrecto

## 10. Calidad editorial

- [ ] Ortografía verificada (tildes y ñ) — sin diacríticos perdidos, también dentro de los `aria-label` de los SVG
- [ ] Coherencia de versión (v1.0) en title, badges, banner y footer del `index.html`
- [ ] El `index.html` abre, navega entre las 8 pestañas y el motor de test funciona
- [ ] Las listas anidadas del Contenido se muestran con sus niveles (sin aplanar)
- [ ] Los bloques de órdenes de shell, PowerShell y `crontab` se muestran correctamente formateados, sin markdown crudo

---

## Observaciones abiertas

_(Espacio para anotaciones de María, Ana y la revisión IAM.)_

- Pendiente confirmar si conviene **desarrollar más la parte de bastionado** (`op.exp.2`: retirada de cuentas estándar, mínima funcionalidad, seguridad por defecto) con guías CCN-STIC concretas, o si al existir el Tema 32 el nivel actual es suficiente.
- Pendiente confirmar la **frontera con el Tema 26**: aquí se ha tratado la copia de seguridad desde la perspectiva del administrador del sistema operativo (qué se copia, con qué frecuencia, cómo se restaura y cómo se prueba), dejando al T26 las políticas, los sistemas y los procedimientos de respaldo en toda su extensión, incluida la copia de sistemas virtuales. ¿Es la división correcta?
- Pendiente confirmar si la parte de **gestión del servicio** (incidencia / problema / cambio, ANS, MTBF y MTTR) debe mantenerse aquí o remitirse al Tema 29, que trata la gestión de la resolución de incidencias con el usuario final.
- Junto al Tema 24 (móvil) y al Tema 31 (cloud), este es un tema **sensible a la obsolescencia** en su parte de producto (versiones, herramientas de despliegue) y **muy sensible a los cambios normativos** en su parte de ENS: conviene fijar una revisión de vigencia antes de cada convocatoria.
