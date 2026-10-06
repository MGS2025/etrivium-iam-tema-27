# Tema 27 — Catálogo de Diagramas

> **Título oficial**: Administración del Sistema operativo y software de base. Funciones y responsabilidades. Actualización, mantenimiento y reparación del sistema operativo.
>
> **Versión**: v1.0
> **Fecha**: 2026-08-20
> **Autor**: ETRIVIUM
> **Formato**: SVG inline (zero-dependencias, escalable, imprimible, accesible con role/aria-label)
> **Paleta**: Ayuntamiento de Madrid #0055a0 (primario) + #d13c3c (alertas) + #2d8659 (ventajas) + #e89822 (callouts)
> **Nota técnica**: las clases CSS de cada SVG llevan sufijo numérico único (`.t1`, `.h1`…) para evitar colisiones de estilos entre los 14 diagramas embebidos en la misma página.

---

## Índice de diagramas

| ID | Título | Sección | Tipo | Formato |
|---|---|---|---|---|
| D1 | Las capas del software de base | §1.1 | Capas | 680×330 |
| D2 | Arquitecturas de núcleo: monolítico, micronúcleo e híbrido | §1.1.1 | Comparativa | 680×340 |
| D3 | La cadena de arranque y dónde falla | §1.2.1 | Flujo | 680×320 |
| D4 | Procesos, hilos y estados de ejecución | §2.1 | Flujo de estados | 680×350 |
| D5 | Memoria virtual, intercambio e hiperpaginación | §2.1 | Esquema anotado | 680×320 |
| D6 | La pila de almacenamiento: del disco al punto de montaje | §2.2.1 | Capas | 680×350 |
| D7 | Identidad y permisos: Linux frente a Windows | §3.1 | Comparativa | 680×340 |
| D8 | AAA y modelos de control de acceso | §3.1.1 | Flujo + tabla visual | 680×310 |
| D9 | Servicios, demonios y tareas programadas | §3.2 | Bloques | 680×340 |
| D10 | El ENS aplicado a la administración de sistemas | §4.2.1 | Esquema normativo | 680×390 |
| D11 | Los cuatro tipos de mantenimiento (ISO/IEC 14764) | §5.1 | Matriz | 680×330 |
| D12 | Diagnóstico por recurso: qué métrica mirar | §5.2.1 | Tabla visual | 680×340 |
| D13 | Ciclo de gestión de parches y anillos de despliegue | §6.2 | Flujo | 680×372 |
| D14 | Recuperación: RPO, RTO, tipos de copia y regla 3-2-1 | §8.2 | Línea temporal + esquema | 680×390 |

---

## D1 · Las capas del software de base

**Sección**: §1.1 — Concepto, funciones y clasificación del software de base
**Propósito**: Situar cada componente del software de base en su capa y fijar la frontera entre modo núcleo y modo usuario.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 336" role="img" aria-label="Capas del software de base, de abajo arriba: hardware, firmware UEFI, núcleo del sistema operativo con controladores, bibliotecas y servicios del sistema, middleware y aplicaciones. La frontera entre modo núcleo y modo usuario se cruza mediante llamadas al sistema">
  <style>.t1{font:700 11.5px system-ui,sans-serif;fill:#fff}.s1{font:9.5px system-ui,sans-serif;fill:#fff}.h1{font:700 13px system-ui,sans-serif;fill:#0055a0}.k1{font:700 10px system-ui,sans-serif;fill:#0055a0}.d1{font:9.5px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h1">Las capas del software de base</text>
  <rect x="60" y="32" width="470" height="40" rx="5" fill="#2d8659"/>
  <text x="295" y="49" text-anchor="middle" class="t1">APLICACIONES</text>
  <text x="295" y="65" text-anchor="middle" class="s1">Padrón · sede electrónica · ofimática · navegador</text>
  <rect x="60" y="78" width="470" height="40" rx="5" fill="#5a9e7a"/>
  <text x="295" y="95" text-anchor="middle" class="t1">MIDDLEWARE</text>
  <text x="295" y="111" text-anchor="middle" class="s1">servidor web · servidor de aplicaciones · SGBD</text>
  <rect x="60" y="124" width="470" height="42" rx="5" fill="#e89822"/>
  <text x="295" y="141" text-anchor="middle" class="t1">BIBLIOTECAS, UTILIDADES Y SERVICIOS DEL SISTEMA</text>
  <text x="295" y="158" text-anchor="middle" class="s1">glibc y DLL · systemd y servicios · gestor de paquetes · copias</text>
  <line x1="20" y1="176" x2="660" y2="176" stroke="#d13c3c" stroke-width="2" stroke-dasharray="6 4"/>
  <text x="24" y="190" class="k1">Frontera de privilegio: se cruza mediante LLAMADAS AL SISTEMA</text>
  <rect x="60" y="198" width="470" height="42" rx="5" fill="#0055a0"/>
  <text x="295" y="215" text-anchor="middle" class="t1">NÚCLEO DEL SISTEMA OPERATIVO</text>
  <text x="295" y="232" text-anchor="middle" class="s1">procesos · memoria · archivos · E/S · protección · controladores</text>
  <rect x="60" y="246" width="470" height="34" rx="5" fill="#004077"/>
  <text x="295" y="268" text-anchor="middle" class="t1">FIRMWARE (UEFI / BIOS)</text>
  <rect x="60" y="286" width="470" height="32" rx="5" fill="#555"/>
  <text x="295" y="307" text-anchor="middle" class="t1">HARDWARE</text>
  <rect x="546" y="198" width="112" height="82" rx="5" fill="none" stroke="#0055a0" stroke-width="2"/>
  <text x="602" y="222" text-anchor="middle" class="k1">MODO</text>
  <text x="602" y="238" text-anchor="middle" class="k1">NÚCLEO</text>
  <text x="602" y="258" text-anchor="middle" class="d1">privilegiado</text>
  <text x="602" y="272" text-anchor="middle" class="d1">(anillo 0)</text>
  <rect x="546" y="32" width="112" height="134" rx="5" fill="none" stroke="#2d8659" stroke-width="2"/>
  <text x="602" y="86" text-anchor="middle" class="k1">MODO</text>
  <text x="602" y="102" text-anchor="middle" class="k1">USUARIO</text>
  <text x="602" y="122" text-anchor="middle" class="d1">restringido</text>
  <text x="670" y="332" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: SILBERSCHATZ; STALLINGS]</text>
</svg>
```

---

## D2 · Arquitecturas de núcleo: monolítico, micronúcleo e híbrido

**Sección**: §1.1.1 — Modelos de arquitectura
**Propósito**: Mostrar de un vistazo qué corre en modo núcleo en cada modelo, que es la única diferencia estructural entre ellos.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Comparación de tres arquitecturas de núcleo: monolítico con todos los servicios en modo núcleo, micronúcleo con servicios en modo usuario comunicados por paso de mensajes, e híbrido o modular como compromiso. Se indican ejemplos, ventajas e inconvenientes de cada uno">
  <style>.t2{font:700 11px system-ui,sans-serif;fill:#fff}.s2{font:9.5px system-ui,sans-serif;fill:#fff}.h2{font:700 13px system-ui,sans-serif;fill:#0055a0}.k2{font:700 10.5px system-ui,sans-serif;fill:#0055a0}.d2{font:9.5px system-ui,sans-serif;fill:#444}.g2{font:700 9.5px system-ui,sans-serif;fill:#2d8659}.r2{font:700 9.5px system-ui,sans-serif;fill:#d13c3c}</style>
  <text x="340" y="20" text-anchor="middle" class="h2">¿Cuánto código se ejecuta en modo núcleo?</text>
  <text x="118" y="42" text-anchor="middle" class="k2">MONOLÍTICO</text>
  <text x="340" y="42" text-anchor="middle" class="k2">MICRONÚCLEO</text>
  <text x="562" y="42" text-anchor="middle" class="k2">HÍBRIDO / MODULAR</text>
  <rect x="20" y="52" width="196" height="24" rx="4" fill="#ddd"/>
  <text x="118" y="69" text-anchor="middle" class="d2">Aplicaciones</text>
  <rect x="242" y="52" width="196" height="24" rx="4" fill="#ddd"/>
  <text x="340" y="69" text-anchor="middle" class="d2">Aplicaciones</text>
  <rect x="464" y="52" width="196" height="24" rx="4" fill="#ddd"/>
  <text x="562" y="69" text-anchor="middle" class="d2">Aplicaciones</text>
  <rect x="242" y="82" width="196" height="46" rx="4" fill="#2d8659"/>
  <text x="340" y="100" text-anchor="middle" class="t2">Servidores en modo usuario</text>
  <text x="340" y="118" text-anchor="middle" class="s2">archivos · red · controladores</text>
  <rect x="20" y="82" width="196" height="122" rx="4" fill="#0055a0"/>
  <text x="118" y="104" text-anchor="middle" class="t2">NÚCLEO</text>
  <text x="118" y="126" text-anchor="middle" class="s2">planificador · memoria</text>
  <text x="118" y="144" text-anchor="middle" class="s2">sistemas de archivos</text>
  <text x="118" y="162" text-anchor="middle" class="s2">pila de red</text>
  <text x="118" y="180" text-anchor="middle" class="s2">controladores</text>
  <text x="118" y="198" text-anchor="middle" class="s2">TODO va aquí dentro</text>
  <rect x="242" y="134" width="196" height="70" rx="4" fill="#0055a0"/>
  <text x="340" y="156" text-anchor="middle" class="t2">MICRONÚCLEO</text>
  <text x="340" y="176" text-anchor="middle" class="s2">planificación · memoria</text>
  <text x="340" y="194" text-anchor="middle" class="s2">comunicación (IPC)</text>
  <rect x="464" y="82" width="196" height="122" rx="4" fill="#0055a0"/>
  <text x="562" y="104" text-anchor="middle" class="t2">NÚCLEO + MÓDULOS</text>
  <text x="562" y="126" text-anchor="middle" class="s2">base siempre cargada</text>
  <text x="562" y="146" text-anchor="middle" class="s2">+ módulos que entran y</text>
  <text x="562" y="164" text-anchor="middle" class="s2">salen en caliente</text>
  <text x="562" y="188" text-anchor="middle" class="s2">lsmod · modprobe</text>
  <text x="118" y="224" text-anchor="middle" class="g2">+ Rápido: llamadas a función</text>
  <text x="118" y="240" text-anchor="middle" class="r2">− Un fallo tumba el sistema</text>
  <text x="340" y="224" text-anchor="middle" class="g2">+ Robusto y aislado</text>
  <text x="340" y="240" text-anchor="middle" class="r2">− Sobrecarga de mensajes</text>
  <text x="562" y="224" text-anchor="middle" class="g2">+ Rápido y extensible</text>
  <text x="562" y="240" text-anchor="middle" class="r2">− Aislamiento limitado</text>
  <rect x="20" y="252" width="196" height="26" rx="4" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="118" y="269" text-anchor="middle" class="d2">Unix, BSD</text>
  <rect x="242" y="252" width="196" height="26" rx="4" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="340" y="269" text-anchor="middle" class="d2">MINIX 3, QNX, L4, Mach</text>
  <rect x="464" y="252" width="196" height="26" rx="4" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="562" y="269" text-anchor="middle" class="d2">Linux, Windows NT, XNU</text>
  <rect x="90" y="290" width="500" height="30" rx="5" fill="none" stroke="#d13c3c" stroke-width="2"/>
  <text x="340" y="310" text-anchor="middle" class="k2">Atención: Linux es MONOLÍTICO MODULAR, no un micronúcleo</text>
  <text x="670" y="336" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: TANENBAUM; SILBERSCHATZ]</text>
</svg>
```

---

## D3 · La cadena de arranque y dónde falla

**Sección**: §1.2.1 — Gestores de arranque, cargadores, controladores y bibliotecas
**Propósito**: Encadenar los seis eslabones del arranque y asociar a cada uno su síntoma de fallo, que es la base del diagnóstico de §8.1.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 320" role="img" aria-label="Cadena de arranque en seis eslabones: firmware UEFI, gestor de arranque, cargador del núcleo, núcleo e initramfs, proceso inicial systemd o wininit, y servicios y sesión. Bajo cada eslabón se indica el síntoma característico cuando falla y la reparación correspondiente">
  <style>.t3{font:700 10px system-ui,sans-serif;fill:#fff}.s3{font:9px system-ui,sans-serif;fill:#fff}.h3{font:700 13px system-ui,sans-serif;fill:#0055a0}.k3{font:700 10px system-ui,sans-serif;fill:#0055a0}.d3{font:9px system-ui,sans-serif;fill:#444}.a3{font:700 9px system-ui,sans-serif;fill:#d13c3c}</style>
  <text x="340" y="20" text-anchor="middle" class="h3">La cadena de arranque: cada eslabón, su síntoma de fallo</text>
  <rect x="14" y="34" width="102" height="46" rx="5" fill="#0055a0"/>
  <text x="65" y="53" text-anchor="middle" class="t3">1 · FIRMWARE</text>
  <text x="65" y="70" text-anchor="middle" class="s3">UEFI / BIOS · POST</text>
  <rect x="126" y="34" width="102" height="46" rx="5" fill="#0055a0"/>
  <text x="177" y="53" text-anchor="middle" class="t3">2 · GESTOR</text>
  <text x="177" y="70" text-anchor="middle" class="s3">GRUB 2 · BCD</text>
  <rect x="238" y="34" width="102" height="46" rx="5" fill="#0055a0"/>
  <text x="289" y="53" text-anchor="middle" class="t3">3 · CARGADOR</text>
  <text x="289" y="70" text-anchor="middle" class="s3">lee el núcleo</text>
  <rect x="350" y="34" width="102" height="46" rx="5" fill="#0055a0"/>
  <text x="401" y="53" text-anchor="middle" class="t3">4 · NÚCLEO</text>
  <text x="401" y="70" text-anchor="middle" class="s3">+ initramfs</text>
  <rect x="462" y="34" width="102" height="46" rx="5" fill="#0055a0"/>
  <text x="513" y="53" text-anchor="middle" class="t3">5 · PROCESO 1</text>
  <text x="513" y="70" text-anchor="middle" class="s3">systemd · wininit</text>
  <rect x="574" y="34" width="92" height="46" rx="5" fill="#2d8659"/>
  <text x="620" y="53" text-anchor="middle" class="t3">6 · SERVICIOS</text>
  <text x="620" y="70" text-anchor="middle" class="s3">y sesión</text>
  <path d="M116 57 L126 57" stroke="#666" stroke-width="2"/>
  <path d="M228 57 L238 57" stroke="#666" stroke-width="2"/>
  <path d="M340 57 L350 57" stroke="#666" stroke-width="2"/>
  <path d="M452 57 L462 57" stroke="#666" stroke-width="2"/>
  <path d="M564 57 L574 57" stroke="#666" stroke-width="2"/>
  <text x="340" y="104" text-anchor="middle" class="k3">Si se detiene aquí, el síntoma es…</text>
  <rect x="14" y="114" width="102" height="70" rx="5" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="65" y="132" text-anchor="middle" class="a3">Sin imagen</text>
  <text x="65" y="148" text-anchor="middle" class="d3">no detecta el</text>
  <text x="65" y="162" text-anchor="middle" class="d3">disco, pitidos</text>
  <text x="65" y="178" text-anchor="middle" class="d3">→ hardware</text>
  <rect x="126" y="114" width="102" height="70" rx="5" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="177" y="132" text-anchor="middle" class="a3">Sin dispositivo</text>
  <text x="177" y="148" text-anchor="middle" class="d3">de arranque</text>
  <text x="177" y="162" text-anchor="middle" class="d3">→ bootrec</text>
  <text x="177" y="178" text-anchor="middle" class="d3">→ grub-install</text>
  <rect x="238" y="114" width="102" height="70" rx="5" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="289" y="132" text-anchor="middle" class="a3">Núcleo no</text>
  <text x="289" y="148" text-anchor="middle" class="d3">encontrado</text>
  <text x="289" y="162" text-anchor="middle" class="d3">→ entrada</text>
  <text x="289" y="178" text-anchor="middle" class="d3">anterior</text>
  <rect x="350" y="114" width="102" height="70" rx="5" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="401" y="132" text-anchor="middle" class="a3">Kernel panic</text>
  <text x="401" y="148" text-anchor="middle" class="d3">no halla la raíz</text>
  <text x="401" y="162" text-anchor="middle" class="d3">→ regenerar</text>
  <text x="401" y="178" text-anchor="middle" class="d3">initramfs</text>
  <rect x="462" y="114" width="102" height="70" rx="5" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="513" y="132" text-anchor="middle" class="a3">Pantalla negra</text>
  <text x="513" y="148" text-anchor="middle" class="d3">o bucle</text>
  <text x="513" y="162" text-anchor="middle" class="d3">→ rescue.target</text>
  <text x="513" y="178" text-anchor="middle" class="d3">→ modo seguro</text>
  <rect x="574" y="114" width="92" height="70" rx="5" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="620" y="132" text-anchor="middle" class="a3">Arranca sin</text>
  <text x="620" y="148" text-anchor="middle" class="d3">red o servicio</text>
  <text x="620" y="162" text-anchor="middle" class="d3">→ systemctl</text>
  <text x="620" y="178" text-anchor="middle" class="d3">--failed</text>
  <rect x="14" y="200" width="652" height="42" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="340" y="219" text-anchor="middle" class="k3">Arranque Seguro (Secure Boot): el firmware verifica la FIRMA DIGITAL de cada eslabón</text>
  <text x="340" y="236" text-anchor="middle" class="d3">Un núcleo o controlador sin firmar detiene el arranque: es una avería «nueva» tras actualizar</text>
  <rect x="14" y="252" width="652" height="42" rx="5" fill="#fff6e8" stroke="#e89822"/>
  <text x="340" y="271" text-anchor="middle" class="k3">UEFI + GPT + partición ESP (FAT32) frente a BIOS heredada + MBR</text>
  <text x="340" y="288" text-anchor="middle" class="d3">MBR: máximo 2 TiB y 4 particiones primarias · GPT: hasta 128 particiones y sin ese límite</text>
  <text x="670" y="314" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: UEFI-SPEC; GRUB-DOC; MS-WINRE]</text>
</svg>
```

---

## D4 · Procesos, hilos y estados de ejecución

**Sección**: §2.1 — Gestión de procesos, hilos y memoria principal
**Propósito**: Fijar el ciclo de estados de un proceso y la diferencia entre proceso e hilo, con los estados patológicos que el administrador debe reconocer.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 350" role="img" aria-label="Ciclo de estados de un proceso: nuevo, preparado, en ejecución, bloqueado y terminado, con las transiciones de admisión, despacho, expropiación, petición de entrada y salida y fin. A la derecha, la diferencia entre proceso e hilo. Debajo, los estados patológicos zombi, huérfano y espera ininterrumpible">
  <style>.t4{font:700 10.5px system-ui,sans-serif;fill:#fff}.s4{font:9px system-ui,sans-serif;fill:#fff}.h4{font:700 13px system-ui,sans-serif;fill:#0055a0}.k4{font:700 10px system-ui,sans-serif;fill:#0055a0}.d4{font:9px system-ui,sans-serif;fill:#444}.e4{font:8.5px system-ui,sans-serif;fill:#0055a0}</style>
  <defs>
    <marker id="a4" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#0055a0"/></marker>
    <marker id="r4" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#d13c3c"/></marker>
    <marker id="o4" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#e89822"/></marker>
  </defs>
  <text x="340" y="20" text-anchor="middle" class="h4">Estados de un proceso · proceso frente a hilo</text>
  <text x="117" y="40" text-anchor="middle" class="e4">admisión</text>
  <text x="253" y="40" text-anchor="middle" class="e4">despacho</text>
  <text x="389" y="40" text-anchor="middle" class="e4">fin</text>
  <rect x="16" y="46" width="86" height="34" rx="5" fill="#888"/>
  <text x="59" y="68" text-anchor="middle" class="t4">NUEVO</text>
  <rect x="132" y="46" width="106" height="34" rx="5" fill="#0055a0"/>
  <text x="185" y="68" text-anchor="middle" class="t4">PREPARADO</text>
  <rect x="268" y="46" width="106" height="34" rx="5" fill="#2d8659"/>
  <text x="321" y="68" text-anchor="middle" class="t4">EN EJECUCIÓN</text>
  <rect x="404" y="46" width="86" height="34" rx="5" fill="#888"/>
  <text x="447" y="68" text-anchor="middle" class="t4">TERMINADO</text>
  <path d="M102 63 L128 63" stroke="#0055a0" stroke-width="2" marker-end="url(#a4)"/>
  <path d="M238 57 L264 57" stroke="#0055a0" stroke-width="2" marker-end="url(#a4)"/>
  <path d="M264 72 L238 72" stroke="#d13c3c" stroke-width="2" marker-end="url(#r4)"/>
  <path d="M374 63 L400 63" stroke="#0055a0" stroke-width="2" marker-end="url(#a4)"/>
  <text x="253" y="96" text-anchor="middle" class="e4">expropiación (fin de quantum)</text>
  <path d="M350 82 L350 132" stroke="#e89822" stroke-width="2" marker-end="url(#o4)"/>
  <path d="M150 132 L150 82" stroke="#0055a0" stroke-width="2" marker-end="url(#a4)"/>
  <text x="392" y="112" text-anchor="middle" class="e4">pide E/S</text>
  <text x="108" y="112" text-anchor="middle" class="e4">llega la E/S</text>
  <rect x="110" y="136" width="290" height="34" rx="5" fill="#e89822"/>
  <text x="255" y="158" text-anchor="middle" class="t4">BLOQUEADO / EN ESPERA (de E/S o de un evento)</text>
  <rect x="506" y="46" width="158" height="126" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="585" y="65" text-anchor="middle" class="k4">PROCESO vs HILO</text>
  <text x="585" y="86" text-anchor="middle" class="d4">El PROCESO posee el espacio</text>
  <text x="585" y="100" text-anchor="middle" class="d4">de direcciones y los recursos</text>
  <text x="585" y="120" text-anchor="middle" class="d4">El HILO es la unidad de</text>
  <text x="585" y="134" text-anchor="middle" class="d4">planificación y lo comparte</text>
  <text x="585" y="156" text-anchor="middle" class="d4">Cambiar de hilo es más barato</text>
  <text x="340" y="194" text-anchor="middle" class="k4">Estados patológicos que hay que saber reconocer</text>
  <rect x="16" y="206" width="210" height="76" rx="5" fill="#d13c3c"/>
  <text x="121" y="227" text-anchor="middle" class="t4">ZOMBI</text>
  <text x="121" y="246" text-anchor="middle" class="s4">Terminó, pero el padre no ha</text>
  <text x="121" y="261" text-anchor="middle" class="s4">recogido su código de salida</text>
  <text x="121" y="276" text-anchor="middle" class="s4">Ocupa entrada, no consume CPU</text>
  <rect x="234" y="206" width="210" height="76" rx="5" fill="#e89822"/>
  <text x="339" y="227" text-anchor="middle" class="t4">HUÉRFANO</text>
  <text x="339" y="246" text-anchor="middle" class="s4">Su padre murió antes que él</text>
  <text x="339" y="261" text-anchor="middle" class="s4">El proceso inicial (PID 1)</text>
  <text x="339" y="276" text-anchor="middle" class="s4">lo adopta</text>
  <rect x="452" y="206" width="212" height="76" rx="5" fill="#7a3b8f"/>
  <text x="558" y="227" text-anchor="middle" class="t4">ESPERA ININTERRUMPIBLE (D)</text>
  <text x="558" y="246" text-anchor="middle" class="s4">Bloqueado en una E/S que no</text>
  <text x="558" y="261" text-anchor="middle" class="s4">responde. Carga media altísima</text>
  <text x="558" y="276" text-anchor="middle" class="s4">con la CPU ociosa</text>
  <rect x="70" y="294" width="540" height="30" rx="5" fill="none" stroke="#0055a0" stroke-width="2"/>
  <text x="340" y="314" text-anchor="middle" class="k4">SIGTERM (15) pide terminar y permite cerrar bien · SIGKILL (9) mata sin remedio</text>
  <text x="670" y="344" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: SILBERSCHATZ; MAN-PAGES]</text>
</svg>
```

---

## D5 · Memoria virtual, intercambio e hiperpaginación

**Sección**: §2.1 — Gestión de procesos, hilos y memoria principal
**Propósito**: Explicar la traducción de direcciones y el fallo de página, y fijar la firma diagnóstica de la hiperpaginación.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 320" role="img" aria-label="Esquema de memoria virtual: el proceso emite una dirección virtual, la unidad de gestión de memoria la traduce con la tabla de páginas y la caché de traducción TLB; si la página no está en memoria física se produce un fallo de página y se trae del espacio de intercambio. Abajo, la firma diagnóstica de la hiperpaginación">
  <style>.t5{font:700 10.5px system-ui,sans-serif;fill:#fff}.s5{font:9px system-ui,sans-serif;fill:#fff}.h5{font:700 13px system-ui,sans-serif;fill:#0055a0}.k5{font:700 10px system-ui,sans-serif;fill:#0055a0}.d5{font:9px system-ui,sans-serif;fill:#444}.e5{font:8.5px system-ui,sans-serif;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h5">Memoria virtual: traducción, fallo de página e intercambio</text>
  <rect x="16" y="40" width="120" height="52" rx="5" fill="#2d8659"/>
  <text x="76" y="61" text-anchor="middle" class="t5">PROCESO</text>
  <text x="76" y="80" text-anchor="middle" class="s5">dirección virtual</text>
  <rect x="176" y="40" width="140" height="52" rx="5" fill="#0055a0"/>
  <text x="246" y="61" text-anchor="middle" class="t5">MMU + TLB</text>
  <text x="246" y="80" text-anchor="middle" class="s5">tabla de páginas</text>
  <rect x="356" y="40" width="140" height="52" rx="5" fill="#0055a0"/>
  <text x="426" y="61" text-anchor="middle" class="t5">MEMORIA FÍSICA</text>
  <text x="426" y="80" text-anchor="middle" class="s5">marcos de página</text>
  <rect x="536" y="40" width="128" height="52" rx="5" fill="#e89822"/>
  <text x="600" y="61" text-anchor="middle" class="t5">INTERCAMBIO</text>
  <text x="600" y="80" text-anchor="middle" class="s5">swap · pagefile.sys</text>
  <path d="M136 66 L172 66" stroke="#666" stroke-width="2"/>
  <path d="M316 66 L352 66" stroke="#666" stroke-width="2"/>
  <path d="M496 66 L532 66" stroke="#d13c3c" stroke-width="2" stroke-dasharray="4 3"/>
  <text x="154" y="60" text-anchor="middle" class="e5">virtual</text>
  <text x="334" y="60" text-anchor="middle" class="e5">física</text>
  <text x="514" y="36" text-anchor="middle" class="e5">fallo de página</text>
  <rect x="16" y="108" width="318" height="76" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="175" y="127" text-anchor="middle" class="k5">Fallo de página (page fault)</text>
  <text x="175" y="146" text-anchor="middle" class="d5">La página no está en memoria física: el núcleo la trae</text>
  <text x="175" y="161" text-anchor="middle" class="d5">de disco, actualiza la tabla y reanuda la instrucción</text>
  <text x="175" y="176" text-anchor="middle" class="d5">Reemplazo: LRU · FIFO · reloj (anomalía de Belady en FIFO)</text>
  <rect x="346" y="108" width="318" height="76" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="505" y="127" text-anchor="middle" class="k5">Fragmentación</text>
  <text x="505" y="146" text-anchor="middle" class="d5">INTERNA: se desperdicia espacio dentro de la unidad</text>
  <text x="505" y="161" text-anchor="middle" class="d5">asignada (la última página nunca se llena del todo)</text>
  <text x="505" y="176" text-anchor="middle" class="d5">EXTERNA: huecos libres dispersos e inservibles</text>
  <rect x="16" y="198" width="648" height="86" rx="5" fill="#d13c3c"/>
  <text x="340" y="219" text-anchor="middle" class="t5">HIPERPAGINACIÓN (THRASHING): el sistema intercambia más de lo que trabaja</text>
  <text x="180" y="243" text-anchor="middle" class="s5">SÍNTOMA</text>
  <text x="180" y="260" text-anchor="middle" class="s5">CPU de usuario baja</text>
  <text x="180" y="275" text-anchor="middle" class="s5">%wa alto · si/so constantes</text>
  <text x="400" y="243" text-anchor="middle" class="s5">CAUSA</text>
  <text x="400" y="260" text-anchor="middle" class="s5">Demasiados procesos para</text>
  <text x="400" y="275" text-anchor="middle" class="s5">la memoria disponible</text>
  <text x="580" y="243" text-anchor="middle" class="s5">SOLUCIÓN</text>
  <text x="580" y="260" text-anchor="middle" class="s5">Añadir memoria o bajar la</text>
  <text x="580" y="275" text-anchor="middle" class="s5">multiprogramación</text>
  <text x="340" y="304" text-anchor="middle" class="d5">Un disco más rápido no lo arregla: solo hace el mismo error más deprisa</text>
  <text x="670" y="314" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: SILBERSCHATZ; TANENBAUM]</text>
</svg>
```

---

## D6 · La pila de almacenamiento: del disco al punto de montaje

**Sección**: §2.2.1 — Volúmenes lógicos, cuotas de disco y dispositivos de bloques
**Propósito**: Ordenar las capas que separan el disco físico del directorio en el que trabaja el usuario, y situar en ellas LVM y las cuotas.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 350" role="img" aria-label="Pila de almacenamiento de abajo arriba: dispositivo físico, dispositivo de bloques, particiones, gestor de volúmenes lógicos con volumen físico, grupo de volúmenes y volumen lógico, sistema de archivos y punto de montaje. A la derecha se explican las cuotas de disco con límite blando y límite duro">
  <style>.t6{font:700 10.5px system-ui,sans-serif;fill:#fff}.s6{font:9px system-ui,sans-serif;fill:#fff}.h6{font:700 13px system-ui,sans-serif;fill:#0055a0}.k6{font:700 10px system-ui,sans-serif;fill:#0055a0}.d6{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h6">De la cabeza del disco al directorio del usuario</text>
  <rect x="16" y="34" width="420" height="34" rx="5" fill="#2d8659"/>
  <text x="226" y="49" text-anchor="middle" class="t6">PUNTO DE MONTAJE · /srv/expedientes o D:\</text>
  <text x="226" y="63" text-anchor="middle" class="s6">lo que ve el usuario y la aplicación</text>
  <rect x="16" y="74" width="420" height="40" rx="5" fill="#0055a0"/>
  <text x="226" y="90" text-anchor="middle" class="t6">SISTEMA DE ARCHIVOS · ext4 · XFS · NTFS · ReFS</text>
  <text x="226" y="106" text-anchor="middle" class="s6">archivos, directorios, inodos, permisos y diario (journaling)</text>
  <rect x="16" y="120" width="420" height="92" rx="5" fill="#e89822"/>
  <text x="226" y="138" text-anchor="middle" class="t6">GESTOR DE VOLÚMENES LÓGICOS (LVM)</text>
  <rect x="28" y="148" width="126" height="52" rx="4" fill="#fff"/>
  <text x="91" y="168" text-anchor="middle" class="k6">PV</text>
  <text x="91" y="186" text-anchor="middle" class="d6">volumen físico</text>
  <rect x="163" y="148" width="126" height="52" rx="4" fill="#fff"/>
  <text x="226" y="168" text-anchor="middle" class="k6">VG</text>
  <text x="226" y="186" text-anchor="middle" class="d6">grupo de volúmenes</text>
  <rect x="298" y="148" width="126" height="52" rx="4" fill="#fff"/>
  <text x="361" y="168" text-anchor="middle" class="k6">LV</text>
  <text x="361" y="186" text-anchor="middle" class="d6">volumen lógico</text>
  <rect x="16" y="218" width="420" height="34" rx="5" fill="#0055a0"/>
  <text x="226" y="240" text-anchor="middle" class="t6">PARTICIONES · tabla GPT o MBR</text>
  <rect x="16" y="258" width="420" height="34" rx="5" fill="#004077"/>
  <text x="226" y="280" text-anchor="middle" class="t6">DISPOSITIVO DE BLOQUES · /dev/sda · PhysicalDrive0</text>
  <rect x="16" y="298" width="420" height="32" rx="5" fill="#555"/>
  <text x="226" y="319" text-anchor="middle" class="t6">DISPOSITIVO FÍSICO · HDD · SSD · LUN de cabina</text>
  <rect x="450" y="34" width="214" height="118" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="557" y="53" text-anchor="middle" class="k6">CUOTAS DE DISCO</text>
  <text x="557" y="74" text-anchor="middle" class="d6">Límite BLANDO (soft): se puede</text>
  <text x="557" y="88" text-anchor="middle" class="d6">superar durante un periodo</text>
  <text x="557" y="102" text-anchor="middle" class="d6">de gracia, con avisos</text>
  <text x="557" y="122" text-anchor="middle" class="d6">Límite DURO (hard): la escritura</text>
  <text x="557" y="136" text-anchor="middle" class="d6">falla, sin excepción</text>
  <rect x="450" y="162" width="214" height="90" rx="5" fill="#f0f4f8" stroke="#2d8659"/>
  <text x="557" y="181" text-anchor="middle" class="k6">VENTAJAS DE LVM</text>
  <text x="557" y="197" text-anchor="middle" class="d6">Redimensionar EN CALIENTE</text>
  <text x="557" y="211" text-anchor="middle" class="d6">Instantáneas (snapshots)</text>
  <text x="557" y="225" text-anchor="middle" class="d6">Agregar varios discos en uno</text>
  <text x="557" y="239" text-anchor="middle" class="d6">Windows: Espacios de almacenamiento</text>
  <rect x="450" y="262" width="214" height="68" rx="5" fill="#d13c3c"/>
  <text x="557" y="281" text-anchor="middle" class="t6">AMPLIAR SON DOS PASOS</text>
  <text x="557" y="300" text-anchor="middle" class="s6">1) lvextend  → agranda el volumen</text>
  <text x="557" y="316" text-anchor="middle" class="s6">2) resize2fs → agranda el sistema</text>
  <text x="670" y="344" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: LVM-DOC; RH-DOC; MAN-PAGES]</text>
</svg>
```

---

## D7 · Identidad y permisos: Linux frente a Windows

**Sección**: §3.1 — Administración de usuarios, grupos y directivas de seguridad
**Propósito**: Poner en paralelo los dos modelos de identidad y permisos, con las reglas clave de cada uno.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Comparación del modelo de identidad y permisos de Linux, basado en UID, GID y permisos rwx con sudo y PAM, frente al de Windows, basado en SID, listas de control de acceso, Active Directory y directivas de grupo. Debajo, los cinco principios comunes de gestión de cuentas exigidos por el Esquema Nacional de Seguridad">
  <style>.t7{font:700 11px system-ui,sans-serif;fill:#fff}.s7{font:9px system-ui,sans-serif;fill:#fff}.h7{font:700 13px system-ui,sans-serif;fill:#0055a0}.k7{font:700 10px system-ui,sans-serif;fill:#0055a0}.d7{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h7">Dos modelos de identidad, los mismos principios</text>
  <rect x="16" y="34" width="316" height="30" rx="5" fill="#0055a0"/>
  <text x="174" y="54" text-anchor="middle" class="t7">LINUX / UNIX</text>
  <rect x="348" y="34" width="316" height="30" rx="5" fill="#004077"/>
  <text x="506" y="54" text-anchor="middle" class="t7">WINDOWS</text>
  <rect x="16" y="70" width="316" height="46" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="174" y="88" text-anchor="middle" class="k7">Identidad: UID y GID</text>
  <text x="174" y="106" text-anchor="middle" class="d7">/etc/passwd · /etc/group · /etc/shadow (con sal)</text>
  <rect x="348" y="70" width="316" height="46" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="506" y="88" text-anchor="middle" class="k7">Identidad: SID</text>
  <text x="506" y="106" text-anchor="middle" class="d7">único e irrepetible · cuentas locales o de dominio</text>
  <rect x="16" y="122" width="316" height="60" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="174" y="140" text-anchor="middle" class="k7">Permisos: tres ternas rwx</text>
  <text x="174" y="158" text-anchor="middle" class="d7">propietario · grupo · otros — chmod y chown</text>
  <text x="174" y="174" text-anchor="middle" class="d7">especiales: SUID · SGID · sticky · ACL POSIX</text>
  <rect x="348" y="122" width="316" height="60" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="506" y="140" text-anchor="middle" class="k7">Permisos: ACL con entradas ACE</text>
  <text x="506" y="158" text-anchor="middle" class="d7">de permiso o de denegación · herencia del padre</text>
  <text x="506" y="174" text-anchor="middle" class="d7">la DENEGACIÓN explícita prevalece</text>
  <rect x="16" y="188" width="316" height="58" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="174" y="206" text-anchor="middle" class="k7">Elevación y política</text>
  <text x="174" y="224" text-anchor="middle" class="d7">sudo (registra cada orden) · PAM (módulos)</text>
  <text x="174" y="240" text-anchor="middle" class="d7">política en ficheros de /etc</text>
  <rect x="348" y="188" width="316" height="58" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="506" y="206" text-anchor="middle" class="k7">Elevación y política</text>
  <text x="506" y="224" text-anchor="middle" class="d7">UAC · Active Directory (dominio, bosque, UO)</text>
  <text x="506" y="240" text-anchor="middle" class="d7">GPO con precedencia L-S-D-UO (gana la última)</text>
  <rect x="16" y="256" width="648" height="60" rx="5" fill="#2d8659"/>
  <text x="340" y="275" text-anchor="middle" class="t7">PRINCIPIOS COMUNES EXIGIDOS POR EL ENS</text>
  <text x="105" y="295" text-anchor="middle" class="s7">Cuentas nominales</text>
  <text x="240" y="295" text-anchor="middle" class="s7">Mínimo privilegio</text>
  <text x="375" y="295" text-anchor="middle" class="s7">Separación de funciones</text>
  <text x="510" y="295" text-anchor="middle" class="s7">Baja inmediata al cesar</text>
  <text x="622" y="295" text-anchor="middle" class="s7">Doble factor</text>
  <text x="340" y="311" text-anchor="middle" class="s7">La cuenta de administración nunca es la cuenta de trabajo diario</text>
  <text x="670" y="334" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: POSIX; MS-AD; MS-GPO; ENS]</text>
</svg>
```

---

## D8 · AAA y modelos de control de acceso

**Sección**: §3.1.1 — Autenticación, autorización y control de acceso local
**Propósito**: Separar las tres funciones que se confunden (autenticar, autorizar y auditar) y enumerar los cuatro modelos de control de acceso.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 316" role="img" aria-label="Las tres funciones AAA: autenticación que responde a quién eres, autorización a qué puedes hacer y auditoría a qué hiciste. Debajo, los tres factores de autenticación y los cuatro modelos de control de acceso: discrecional, obligatorio, basado en roles y basado en atributos">
  <style>.t8{font:700 11px system-ui,sans-serif;fill:#fff}.s8{font:9px system-ui,sans-serif;fill:#fff}.h8{font:700 13px system-ui,sans-serif;fill:#0055a0}.k8{font:700 10px system-ui,sans-serif;fill:#0055a0}.d8{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h8">Autenticación, autorización y auditoría: tres cosas distintas</text>
  <rect x="16" y="34" width="196" height="64" rx="5" fill="#0055a0"/>
  <text x="114" y="55" text-anchor="middle" class="t8">1 · AUTENTICACIÓN</text>
  <text x="114" y="74" text-anchor="middle" class="s8">¿QUIÉN ERES?</text>
  <text x="114" y="90" text-anchor="middle" class="s8">contraseña · certificado · biometría</text>
  <rect x="242" y="34" width="196" height="64" rx="5" fill="#2d8659"/>
  <text x="340" y="55" text-anchor="middle" class="t8">2 · AUTORIZACIÓN</text>
  <text x="340" y="74" text-anchor="middle" class="s8">¿QUÉ PUEDES HACER?</text>
  <text x="340" y="90" text-anchor="middle" class="s8">permisos · ACL · grupos · roles</text>
  <rect x="468" y="34" width="196" height="64" rx="5" fill="#e89822"/>
  <text x="566" y="55" text-anchor="middle" class="t8">3 · AUDITORÍA</text>
  <text x="566" y="74" text-anchor="middle" class="s8">¿QUÉ HICISTE?</text>
  <text x="566" y="90" text-anchor="middle" class="s8">registro · retención · protección</text>
  <path d="M212 66 L240 66" stroke="#666" stroke-width="2"/>
  <path d="M438 66 L466 66" stroke="#666" stroke-width="2"/>
  <rect x="16" y="110" width="648" height="52" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="340" y="128" text-anchor="middle" class="k8">Los tres FACTORES de autenticación (multifactor = factores de categorías DISTINTAS)</text>
  <text x="130" y="150" text-anchor="middle" class="d8">Algo que SABES (contraseña, PIN)</text>
  <text x="340" y="150" text-anchor="middle" class="d8">Algo que TIENES (tarjeta, token, certificado)</text>
  <text x="560" y="150" text-anchor="middle" class="d8">Algo que ERES (biometría)</text>
  <text x="340" y="184" text-anchor="middle" class="k8">Los cuatro modelos de control de acceso</text>
  <rect x="16" y="196" width="156" height="72" rx="5" fill="#0055a0"/>
  <text x="94" y="216" text-anchor="middle" class="t8">DAC · discrecional</text>
  <text x="94" y="236" text-anchor="middle" class="s8">Decide el PROPIETARIO</text>
  <text x="94" y="253" text-anchor="middle" class="s8">del recurso</text>
  <rect x="180" y="196" width="156" height="72" rx="5" fill="#004077"/>
  <text x="258" y="216" text-anchor="middle" class="t8">MAC · obligatorio</text>
  <text x="258" y="236" text-anchor="middle" class="s8">Lo impone el SISTEMA</text>
  <text x="258" y="253" text-anchor="middle" class="s8">por etiquetas (SELinux)</text>
  <rect x="344" y="196" width="156" height="72" rx="5" fill="#2d8659"/>
  <text x="422" y="216" text-anchor="middle" class="t8">RBAC · por roles</text>
  <text x="422" y="236" text-anchor="middle" class="s8">Permisos al ROL y</text>
  <text x="422" y="253" text-anchor="middle" class="s8">personas al rol</text>
  <rect x="508" y="196" width="156" height="72" rx="5" fill="#7a3b8f"/>
  <text x="586" y="216" text-anchor="middle" class="t8">ABAC · por atributos</text>
  <text x="586" y="236" text-anchor="middle" class="s8">Sujeto + recurso +</text>
  <text x="586" y="253" text-anchor="middle" class="s8">contexto (hora, lugar)</text>
  <rect x="90" y="272" width="500" height="24" rx="5" fill="none" stroke="#d13c3c" stroke-width="2"/>
  <text x="340" y="289" text-anchor="middle" class="k8">Las contraseñas no se guardan: se guarda su resumen con SAL</text>
  <text x="670" y="311" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: SILBERSCHATZ; ISO27002; ENS]</text>
</svg>
```

---

## D9 · Servicios, demonios y tareas programadas

**Sección**: §3.2 — Gestión de servicios, demonios y tareas programadas
**Propósito**: Equiparar los mecanismos de las dos familias de sistemas y fijar la sintaxis de `cron`.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Gestión de servicios y demonios en systemd frente a servicios de Windows, con la distinción entre arrancar ahora y habilitar en el arranque. Debajo, la sintaxis de los cinco campos de cron y las buenas prácticas de las tareas programadas">
  <style>.t9{font:700 11px system-ui,sans-serif;fill:#fff}.s9{font:9px system-ui,sans-serif;fill:#fff}.h9{font:700 13px system-ui,sans-serif;fill:#0055a0}.k9{font:700 10px system-ui,sans-serif;fill:#0055a0}.d9{font:9px system-ui,sans-serif;fill:#444}.m9{font:700 10px ui-monospace,monospace;fill:#0055a0}</style>
  <text x="340" y="20" text-anchor="middle" class="h9">Servicios y tareas programadas: el trabajo que corre solo</text>
  <rect x="16" y="34" width="316" height="112" rx="5" fill="#0055a0"/>
  <text x="174" y="54" text-anchor="middle" class="t9">LINUX · systemd</text>
  <text x="174" y="74" text-anchor="middle" class="s9">Unidades: .service · .timer · .target · .mount</text>
  <text x="174" y="92" text-anchor="middle" class="s9">systemctl status | restart | enable --now</text>
  <text x="174" y="110" text-anchor="middle" class="s9">systemctl list-units --failed</text>
  <text x="174" y="132" text-anchor="middle" class="s9">Registro integrado: journalctl -u servicio</text>
  <rect x="348" y="34" width="316" height="112" rx="5" fill="#004077"/>
  <text x="506" y="54" text-anchor="middle" class="t9">WINDOWS · Administrador de servicios</text>
  <text x="506" y="74" text-anchor="middle" class="s9">services.msc · sc · Get-Service · Restart-Service</text>
  <text x="506" y="92" text-anchor="middle" class="s9">Tipo de inicio: automático · manual · deshabilitado</text>
  <text x="506" y="110" text-anchor="middle" class="s9">Cuenta de ejecución con privilegios mínimos</text>
  <text x="506" y="132" text-anchor="middle" class="s9">Dependencias y acción ante fallo</text>
  <rect x="16" y="154" width="648" height="30" rx="5" fill="#d13c3c"/>
  <text x="340" y="174" text-anchor="middle" class="t9">start = arrancar AHORA · enable = arrancar en el PRÓXIMO INICIO · son cosas distintas</text>
  <rect x="16" y="194" width="380" height="82" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="206" y="212" text-anchor="middle" class="k9">Los cinco campos de cron</text>
  <text x="206" y="234" text-anchor="middle" class="m9">min(0-59) hora(0-23) día-mes(1-31) mes(1-12) día-sem(0-7)</text>
  <text x="206" y="254" text-anchor="middle" class="d9">30 2 * * *  → todos los días a las 02:30</text>
  <text x="206" y="269" text-anchor="middle" class="d9">*/15 * * * *  → cada quince minutos · 0 y 7 = domingo</text>
  <rect x="408" y="194" width="256" height="82" rx="5" fill="#f0f4f8" stroke="#2d8659"/>
  <text x="536" y="212" text-anchor="middle" class="k9">Windows: Programador de tareas</text>
  <text x="536" y="232" text-anchor="middle" class="d9">Desencadenadores: hora, inicio de sesión,</text>
  <text x="536" y="247" text-anchor="middle" class="d9">evento del registro, conexión de red</text>
  <text x="536" y="266" text-anchor="middle" class="d9">Equivalente moderno en Linux: .timer</text>
  <rect x="16" y="286" width="648" height="38" rx="5" fill="#2d8659"/>
  <text x="340" y="304" text-anchor="middle" class="t9">Una tarea programada bien hecha</text>
  <text x="340" y="319" text-anchor="middle" class="s9">idempotente · registra su resultado · avisa TAMBIÉN si falla · usa bloqueo · corre con cuenta de servicio</text>
  <text x="670" y="336" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: SYSTEMD; MAN-PAGES; MS-WINSERVER]</text>
</svg>
```

---

## D10 · El ENS aplicado a la administración de sistemas

**Sección**: §4.2.1 — Aplicación del Esquema Nacional de Seguridad
**Propósito**: Traducir el Real Decreto 311/2022 a lo que significa para quien administra el sistema: dimensiones, categorías, responsables y medidas concretas.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 390" role="img" aria-label="Esquema Nacional de Seguridad aplicado a la administración de sistemas: cinco dimensiones de seguridad, tres categorías, cuatro responsables diferenciados, tres grupos de medidas del anexo dos y las medidas concretas de explotación, continuidad y copias de seguridad que afectan a este tema">
  <style>.t10{font:700 10.5px system-ui,sans-serif;fill:#fff}.s10{font:9px system-ui,sans-serif;fill:#fff}.h10{font:700 13px system-ui,sans-serif;fill:#0055a0}.k10{font:700 10px system-ui,sans-serif;fill:#0055a0}.d10{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h10">Real Decreto 311/2022 (ENS) — lo que obliga al administrador</text>
  <text x="340" y="40" text-anchor="middle" class="k10">Las cinco DIMENSIONES de seguridad (anexo I)</text>
  <rect x="16" y="48" width="124" height="34" rx="5" fill="#0055a0"/>
  <text x="78" y="70" text-anchor="middle" class="t10">Disponibilidad</text>
  <rect x="148" y="48" width="124" height="34" rx="5" fill="#0055a0"/>
  <text x="210" y="70" text-anchor="middle" class="t10">Integridad</text>
  <rect x="280" y="48" width="124" height="34" rx="5" fill="#0055a0"/>
  <text x="342" y="70" text-anchor="middle" class="t10">Confidencialidad</text>
  <rect x="412" y="48" width="124" height="34" rx="5" fill="#0055a0"/>
  <text x="474" y="70" text-anchor="middle" class="t10">Autenticidad</text>
  <rect x="544" y="48" width="120" height="34" rx="5" fill="#0055a0"/>
  <text x="604" y="70" text-anchor="middle" class="t10">Trazabilidad</text>
  <rect x="16" y="92" width="316" height="70" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="174" y="110" text-anchor="middle" class="k10">CATEGORÍA del sistema: manda la más alta</text>
  <text x="174" y="127" text-anchor="middle" class="d10">ALTA: alguna dimensión en nivel ALTO</text>
  <text x="174" y="141" text-anchor="middle" class="d10">MEDIA: alguna en MEDIO y ninguna superior</text>
  <text x="174" y="155" text-anchor="middle" class="d10">BÁSICA: alguna en BAJO y ninguna superior</text>
  <rect x="348" y="92" width="316" height="70" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="506" y="110" text-anchor="middle" class="k10">Cuatro RESPONSABLES diferenciados (art. 11)</text>
  <text x="506" y="127" text-anchor="middle" class="d10">de la Información · del Servicio · de la Seguridad</text>
  <text x="506" y="141" text-anchor="middle" class="d10">y del Sistema (el administrador)</text>
  <text x="506" y="155" text-anchor="middle" class="d10">Seguridad y explotación NO en la misma persona</text>
  <text x="340" y="182" text-anchor="middle" class="k10">Las medidas del anexo II que caen sobre este tema</text>
  <rect x="16" y="192" width="210" height="30" rx="5" fill="#004077"/>
  <text x="121" y="212" text-anchor="middle" class="t10">MARCO ORGANIZATIVO [org]</text>
  <rect x="234" y="192" width="210" height="30" rx="5" fill="#0055a0"/>
  <text x="339" y="212" text-anchor="middle" class="t10">MARCO OPERACIONAL [op]</text>
  <rect x="452" y="192" width="212" height="30" rx="5" fill="#2d8659"/>
  <text x="558" y="212" text-anchor="middle" class="t10">MEDIDAS DE PROTECCIÓN [mp]</text>
  <rect x="16" y="230" width="428" height="106" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="230" y="248" text-anchor="middle" class="k10">Explotación [op.exp] y continuidad [op.cont]</text>
  <text x="230" y="268" text-anchor="middle" class="d10">op.exp.1 Inventario de activos · op.exp.2 Configuración de seguridad</text>
  <text x="230" y="284" text-anchor="middle" class="d10">op.exp.3 Gestión de la configuración · op.exp.5 Gestión de cambios</text>
  <text x="230" y="300" text-anchor="middle" class="d10">op.exp.7 Gestión de incidentes · op.exp.8 Registro de la actividad</text>
  <text x="230" y="320" text-anchor="middle" class="d10">op.cont.1 a 4: análisis de impacto, plan, pruebas y medios alternativos</text>
  <rect x="456" y="230" width="208" height="106" rx="5" fill="#e89822"/>
  <text x="560" y="249" text-anchor="middle" class="t10">op.exp.4</text>
  <text x="560" y="266" text-anchor="middle" class="s10">Mantenimiento y</text>
  <text x="560" y="281" text-anchor="middle" class="s10">actualizaciones de seguridad</text>
  <text x="560" y="301" text-anchor="middle" class="s10">R1 · pruebas en preproducción</text>
  <text x="560" y="317" text-anchor="middle" class="s10">R2 · mecanismo para revertir</text>
  <text x="560" y="331" text-anchor="middle" class="s10">= el corazón de este tema</text>
  <rect x="16" y="344" width="648" height="30" rx="5" fill="#d13c3c"/>
  <text x="340" y="364" text-anchor="middle" class="t10">mp.info.6 Copias de seguridad · R1 obliga a PROBAR la restauración · auditoría al menos cada 2 años</text>
  <text x="670" y="386" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: ENS (RD 311/2022)]</text>
</svg>
```

---

## D11 · Los cuatro tipos de mantenimiento (ISO/IEC 14764)

**Sección**: §5.1 — Estrategias de mantenimiento preventivo, correctivo y evolutivo
**Propósito**: Ordenar los cuatro tipos por causa y momento, y mostrar su correspondencia con la terminología del enunciado oficial.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 330" role="img" aria-label="Los cuatro tipos de mantenimiento de la norma ISO 14764: correctivo tras un fallo, preventivo antes del fallo, perfectivo para mejorar y adaptativo para acomodar cambios del entorno. Se muestra su correspondencia con la terminología preventivo, correctivo y evolutivo del enunciado oficial y una lista de tareas preventivas típicas">
  <style>.t11{font:700 11px system-ui,sans-serif;fill:#fff}.s11{font:9px system-ui,sans-serif;fill:#fff}.h11{font:700 13px system-ui,sans-serif;fill:#0055a0}.k11{font:700 10px system-ui,sans-serif;fill:#0055a0}.d11{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h11">¿Ha fallado ya? La pregunta que clasifica el mantenimiento</text>
  <rect x="16" y="34" width="322" height="26" rx="4" fill="#0055a0"/>
  <text x="177" y="53" text-anchor="middle" class="t11">RESPONDE A UN FALLO</text>
  <rect x="346" y="34" width="318" height="26" rx="4" fill="#2d8659"/>
  <text x="505" y="53" text-anchor="middle" class="t11">NO RESPONDE A NINGÚN FALLO</text>
  <rect x="16" y="68" width="156" height="94" rx="5" fill="#d13c3c"/>
  <text x="94" y="88" text-anchor="middle" class="t11">CORRECTIVO</text>
  <text x="94" y="108" text-anchor="middle" class="s11">Reactivo: ya ha fallado</text>
  <text x="94" y="126" text-anchor="middle" class="s11">Reinstalar un servicio</text>
  <text x="94" y="141" text-anchor="middle" class="s11">corrupto, corregir una</text>
  <text x="94" y="156" text-anchor="middle" class="s11">configuración errónea</text>
  <rect x="180" y="68" width="158" height="94" rx="5" fill="#e89822"/>
  <text x="259" y="88" text-anchor="middle" class="t11">PREVENTIVO</text>
  <text x="259" y="108" text-anchor="middle" class="s11">Proactivo: aún no falla</text>
  <text x="259" y="126" text-anchor="middle" class="s11">Sustituir un disco con</text>
  <text x="259" y="141" text-anchor="middle" class="s11">sectores reasignados,</text>
  <text x="259" y="156" text-anchor="middle" class="s11">ampliar un volumen al 80 %</text>
  <rect x="346" y="68" width="156" height="94" rx="5" fill="#0055a0"/>
  <text x="424" y="88" text-anchor="middle" class="t11">PERFECTIVO</text>
  <text x="424" y="108" text-anchor="middle" class="s11">Mejorar lo que ya va bien</text>
  <text x="424" y="126" text-anchor="middle" class="s11">Ajustar parámetros,</text>
  <text x="424" y="141" text-anchor="middle" class="s11">automatizar una tarea</text>
  <text x="424" y="156" text-anchor="middle" class="s11">manual, reorganizar</text>
  <rect x="510" y="68" width="154" height="94" rx="5" fill="#7a3b8f"/>
  <text x="587" y="88" text-anchor="middle" class="t11">ADAPTATIVO</text>
  <text x="587" y="108" text-anchor="middle" class="s11">Cambia el entorno</text>
  <text x="587" y="126" text-anchor="middle" class="s11">Migrar a una versión</text>
  <text x="587" y="141" text-anchor="middle" class="s11">soportada, adaptarse a</text>
  <text x="587" y="156" text-anchor="middle" class="s11">nuevo hardware o norma</text>
  <rect x="346" y="170" width="318" height="28" rx="4" fill="none" stroke="#2d8659" stroke-width="2"/>
  <text x="505" y="189" text-anchor="middle" class="k11">El enunciado oficial los llama, juntos, EVOLUTIVO</text>
  <rect x="16" y="170" width="322" height="28" rx="4" fill="none" stroke="#0055a0" stroke-width="2"/>
  <text x="177" y="189" text-anchor="middle" class="k11">Predictivo = preventivo guiado por telemetría (S.M.A.R.T.)</text>
  <rect x="16" y="208" width="648" height="96" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="340" y="226" text-anchor="middle" class="k11">Tareas preventivas típicas de un sistema operativo</text>
  <text x="176" y="246" text-anchor="middle" class="d11">Rotación y purga de registros</text>
  <text x="176" y="262" text-anchor="middle" class="d11">Limpieza de temporales y núcleos viejos</text>
  <text x="176" y="278" text-anchor="middle" class="d11">Vigilancia del espacio libre (80 % / 90 %)</text>
  <text x="176" y="294" text-anchor="middle" class="d11">Salud del hardware: S.M.A.R.T., memoria</text>
  <text x="500" y="246" text-anchor="middle" class="d11">Verificar copias Y probar restauración</text>
  <text x="500" y="262" text-anchor="middle" class="d11">Retirar servicios y puertos innecesarios</text>
  <text x="500" y="278" text-anchor="middle" class="d11">Comprobar la sincronización horaria (NTP)</text>
  <text x="500" y="294" text-anchor="middle" class="d11">SSD: TRIM, nunca desfragmentar</text>
  <text x="670" y="324" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: ISO14764; SMART-DOC; RFC5905]</text>
</svg>
```

---

## D12 · Diagnóstico por recurso: qué métrica mirar

**Sección**: §5.2.1 — Análisis de métricas y ajuste del sistema
**Propósito**: Asociar cada recurso con sus métricas, su herramienta y el síntoma de saturación, para poder recorrer los cuatro recursos con método.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 340" role="img" aria-label="Tabla visual de diagnóstico por recurso: para CPU, memoria, almacenamiento y red se indican las métricas clave, la herramienta de Linux y de Windows y el síntoma de saturación. Debajo, la advertencia de que sin línea base no hay diagnóstico posible">
  <style>.t12{font:700 10.5px system-ui,sans-serif;fill:#fff}.s12{font:9px system-ui,sans-serif;fill:#fff}.h12{font:700 13px system-ui,sans-serif;fill:#0055a0}.k12{font:700 9.5px system-ui,sans-serif;fill:#0055a0}.d12{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h12">Los cuatro recursos: qué mirar y qué significa</text>
  <rect x="16" y="32" width="104" height="26" rx="4" fill="#0055a0"/>
  <text x="68" y="50" text-anchor="middle" class="t12">RECURSO</text>
  <rect x="124" y="32" width="216" height="26" rx="4" fill="#0055a0"/>
  <text x="232" y="50" text-anchor="middle" class="t12">MÉTRICAS CLAVE</text>
  <rect x="344" y="32" width="164" height="26" rx="4" fill="#0055a0"/>
  <text x="426" y="50" text-anchor="middle" class="t12">HERRAMIENTA</text>
  <rect x="512" y="32" width="152" height="26" rx="4" fill="#0055a0"/>
  <text x="588" y="50" text-anchor="middle" class="t12">SÍNTOMA DE SATURACIÓN</text>
  <rect x="16" y="62" width="104" height="58" rx="4" fill="#2d8659"/>
  <text x="68" y="88" text-anchor="middle" class="t12">CPU</text>
  <text x="68" y="106" text-anchor="middle" class="s12">cálculo</text>
  <rect x="124" y="62" width="216" height="58" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="232" y="80" text-anchor="middle" class="d12">% usuario / % sistema / % espera E/S</text>
  <text x="232" y="96" text-anchor="middle" class="d12">carga media frente a nº de núcleos</text>
  <text x="232" y="112" text-anchor="middle" class="d12">cambios de contexto e interrupciones</text>
  <rect x="344" y="62" width="164" height="58" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="426" y="86" text-anchor="middle" class="d12">top · uptime · mpstat</text>
  <text x="426" y="104" text-anchor="middle" class="d12">Monitor de rendimiento</text>
  <rect x="512" y="62" width="152" height="58" rx="4" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="588" y="86" text-anchor="middle" class="d12">Carga media &gt;&gt; núcleos</text>
  <text x="588" y="104" text-anchor="middle" class="d12">y cola de ejecución larga</text>
  <rect x="16" y="124" width="104" height="58" rx="4" fill="#e89822"/>
  <text x="68" y="150" text-anchor="middle" class="t12">MEMORIA</text>
  <text x="68" y="168" text-anchor="middle" class="s12">espacio de trabajo</text>
  <rect x="124" y="124" width="216" height="58" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="232" y="142" text-anchor="middle" class="d12">memoria DISPONIBLE (no «libre»)</text>
  <text x="232" y="158" text-anchor="middle" class="d12">tasa de intercambio si/so</text>
  <text x="232" y="174" text-anchor="middle" class="d12">fallos de página mayores</text>
  <rect x="344" y="124" width="164" height="58" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="426" y="148" text-anchor="middle" class="d12">free · vmstat</text>
  <text x="426" y="166" text-anchor="middle" class="d12">Available MBytes</text>
  <rect x="512" y="124" width="152" height="58" rx="4" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="588" y="148" text-anchor="middle" class="d12">Hiperpaginación:</text>
  <text x="588" y="166" text-anchor="middle" class="d12">si/so altos y CPU ociosa</text>
  <rect x="16" y="186" width="104" height="58" rx="4" fill="#0055a0"/>
  <text x="68" y="212" text-anchor="middle" class="t12">DISCO / E/S</text>
  <text x="68" y="230" text-anchor="middle" class="s12">persistencia</text>
  <rect x="124" y="186" width="216" height="58" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="232" y="204" text-anchor="middle" class="d12">espacio libre Y inodos libres</text>
  <text x="232" y="220" text-anchor="middle" class="d12">IOPS, MB/s, latencia y cola</text>
  <text x="232" y="236" text-anchor="middle" class="d12">% de utilización del dispositivo</text>
  <rect x="344" y="186" width="164" height="58" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="426" y="210" text-anchor="middle" class="d12">df -h · df -i · iostat -xz</text>
  <text x="426" y="228" text-anchor="middle" class="d12">Avg. Disk sec/Transfer</text>
  <rect x="512" y="186" width="152" height="58" rx="4" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="588" y="210" text-anchor="middle" class="d12">Latencia creciente y</text>
  <text x="588" y="228" text-anchor="middle" class="d12">utilización cerca del 100 %</text>
  <rect x="16" y="248" width="104" height="44" rx="4" fill="#7a3b8f"/>
  <text x="68" y="268" text-anchor="middle" class="t12">RED</text>
  <text x="68" y="284" text-anchor="middle" class="s12">ver Tema 30</text>
  <rect x="124" y="248" width="216" height="44" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="232" y="266" text-anchor="middle" class="d12">ancho de banda, errores,</text>
  <text x="232" y="282" text-anchor="middle" class="d12">descartes y retransmisiones</text>
  <rect x="344" y="248" width="164" height="44" rx="4" fill="#f0f4f8" stroke="#ccc"/>
  <text x="426" y="274" text-anchor="middle" class="d12">ip -s link · ss · netstat</text>
  <rect x="512" y="248" width="152" height="44" rx="4" fill="#fdeaea" stroke="#d13c3c"/>
  <text x="588" y="274" text-anchor="middle" class="d12">Descartes y reintentos</text>
  <rect x="16" y="300" width="648" height="26" rx="5" fill="#0055a0"/>
  <text x="340" y="318" text-anchor="middle" class="t12">Sin LÍNEA BASE no hay diagnóstico: «va lento» solo significa algo comparado con algo</text>
  <text x="670" y="336" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: MAN-PAGES; MS-PERF]</text>
</svg>
```

---

## D13 · Ciclo de gestión de parches y anillos de despliegue

**Sección**: §6.2 — Procedimientos de despliegue de parches y actualizaciones
**Propósito**: Encadenar los seis pasos del NIST con los cuatro anillos de despliegue y los mecanismos de marcha atrás.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 372" role="img" aria-label="Ciclo de gestión de parches en seis pasos según el NIST: inventariar, identificar, priorizar, probar, desplegar y verificar. Debajo, los cuatro anillos de despliegue desde laboratorio hasta producción crítica, la escala de gravedad CVSS y los mecanismos de marcha atrás disponibles">
  <style>.t13{font:700 10px system-ui,sans-serif;fill:#fff}.s13{font:9px system-ui,sans-serif;fill:#fff}.h13{font:700 13px system-ui,sans-serif;fill:#0055a0}.k13{font:700 10px system-ui,sans-serif;fill:#0055a0}.d13{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h13">Gestión de parches: seis pasos, cuatro anillos, una marcha atrás</text>
  <rect x="14" y="32" width="104" height="48" rx="5" fill="#0055a0"/>
  <text x="66" y="52" text-anchor="middle" class="t13">1 · INVENTARIAR</text>
  <text x="66" y="69" text-anchor="middle" class="s13">op.exp.1</text>
  <rect x="124" y="32" width="104" height="48" rx="5" fill="#0055a0"/>
  <text x="176" y="52" text-anchor="middle" class="t13">2 · IDENTIFICAR</text>
  <text x="176" y="69" text-anchor="middle" class="s13">boletines · CVE</text>
  <rect x="234" y="32" width="104" height="48" rx="5" fill="#e89822"/>
  <text x="286" y="52" text-anchor="middle" class="t13">3 · PRIORIZAR</text>
  <text x="286" y="69" text-anchor="middle" class="s13">riesgo real</text>
  <rect x="344" y="32" width="104" height="48" rx="5" fill="#e89822"/>
  <text x="396" y="52" text-anchor="middle" class="t13">4 · PROBAR</text>
  <text x="396" y="69" text-anchor="middle" class="s13">preproducción</text>
  <rect x="454" y="32" width="104" height="48" rx="5" fill="#2d8659"/>
  <text x="506" y="52" text-anchor="middle" class="t13">5 · DESPLEGAR</text>
  <text x="506" y="69" text-anchor="middle" class="s13">por anillos</text>
  <rect x="564" y="32" width="102" height="48" rx="5" fill="#2d8659"/>
  <text x="615" y="52" text-anchor="middle" class="t13">6 · VERIFICAR</text>
  <text x="615" y="69" text-anchor="middle" class="s13">y documentar</text>
  <path d="M118 56 L124 56" stroke="#666" stroke-width="2"/>
  <path d="M228 56 L234 56" stroke="#666" stroke-width="2"/>
  <path d="M338 56 L344 56" stroke="#666" stroke-width="2"/>
  <path d="M448 56 L454 56" stroke="#666" stroke-width="2"/>
  <path d="M558 56 L564 56" stroke="#666" stroke-width="2"/>
  <text x="340" y="102" text-anchor="middle" class="k13">Anillos de despliegue: nunca todo a la vez</text>
  <rect x="14" y="112" width="158" height="58" rx="5" fill="#0055a0"/>
  <text x="93" y="132" text-anchor="middle" class="t13">0 · LABORATORIO</text>
  <text x="93" y="150" text-anchor="middle" class="s13">clones de producción</text>
  <text x="93" y="165" text-anchor="middle" class="s13">¿instala sin romper?</text>
  <rect x="180" y="112" width="158" height="58" rx="5" fill="#0055a0"/>
  <text x="259" y="132" text-anchor="middle" class="t13">1 · PILOTO</text>
  <text x="259" y="150" text-anchor="middle" class="s13">grupo representativo</text>
  <text x="259" y="165" text-anchor="middle" class="s13">con el software real</text>
  <rect x="346" y="112" width="158" height="58" rx="5" fill="#e89822"/>
  <text x="425" y="132" text-anchor="middle" class="t13">2 · PRODUCCIÓN</text>
  <text x="425" y="150" text-anchor="middle" class="s13">puestos de usuario</text>
  <text x="425" y="165" text-anchor="middle" class="s13">despliegue masivo</text>
  <rect x="512" y="112" width="154" height="58" rx="5" fill="#d13c3c"/>
  <text x="589" y="132" text-anchor="middle" class="t13">3 · CRÍTICA</text>
  <text x="589" y="150" text-anchor="middle" class="s13">sede, Padrón, bases</text>
  <text x="589" y="165" text-anchor="middle" class="s13">ventana + instantánea</text>
  <rect x="14" y="184" width="322" height="92" rx="5" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="175" y="202" text-anchor="middle" class="k13">Priorizar: CVE identifica, CVSS puntúa</text>
  <text x="175" y="222" text-anchor="middle" class="d13">9,0 – 10,0 CRÍTICA · 7,0 – 8,9 alta</text>
  <text x="175" y="238" text-anchor="middle" class="d13">4,0 – 6,9 media · 0,1 – 3,9 baja</text>
  <text x="175" y="258" text-anchor="middle" class="d13">La prioridad real = CVSS + exposición del activo</text>
  <text x="175" y="272" text-anchor="middle" class="d13">+ criticidad del servicio + explotación activa</text>
  <rect x="344" y="184" width="322" height="92" rx="5" fill="#f0f4f8" stroke="#2d8659"/>
  <text x="505" y="202" text-anchor="middle" class="k13">Mecanismos de marcha atrás</text>
  <text x="505" y="222" text-anchor="middle" class="d13">Instantánea de máquina virtual o de volumen</text>
  <text x="505" y="238" text-anchor="middle" class="d13">Punto de restauración · desinstalar el parche</text>
  <text x="505" y="254" text-anchor="middle" class="d13">Arrancar con el núcleo anterior · revertir driver</text>
  <text x="505" y="270" text-anchor="middle" class="d13">Restaurar desde copia (último recurso: RPO)</text>
  <rect x="14" y="288" width="652" height="30" rx="5" fill="#d13c3c"/>
  <text x="340" y="308" text-anchor="middle" class="t13">Una INSTANTÁNEA no es una copia de seguridad: vive en el mismo almacenamiento</text>
  <rect x="14" y="324" width="652" height="26" rx="5" fill="#0055a0"/>
  <text x="340" y="342" text-anchor="middle" class="t13">Regla de oro: no se aplica en producción un cambio que no se sepa deshacer (op.exp.4 R2)</text>
  <text x="670" y="366" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: NIST80040; NIST-CVSS; ENS; MS-WSUS]</text>
</svg>
```

---

## D14 · Recuperación: RPO, RTO, tipos de copia y regla 3-2-1

**Sección**: §8.2 — Copias de seguridad, restauración y continuidad operativa
**Propósito**: Fijar de un vistazo los dos parámetros que gobiernan el diseño, las tres formas de copiar y la regla de custodia.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 390" role="img" aria-label="Línea temporal de un incidente que sitúa el RPO como pérdida de datos hacia atrás y el RTO como tiempo de recuperación hacia delante. Debajo, comparación de las copias total, diferencial e incremental con su coste de restauración, y la regla 3-2-1 con sus refuerzos de inmutabilidad y prueba de restauración">
  <style>.t14{font:700 10.5px system-ui,sans-serif;fill:#fff}.s14{font:9px system-ui,sans-serif;fill:#fff}.h14{font:700 13px system-ui,sans-serif;fill:#0055a0}.k14{font:700 10px system-ui,sans-serif;fill:#0055a0}.d14{font:9px system-ui,sans-serif;fill:#444}</style>
  <text x="340" y="20" text-anchor="middle" class="h14">RPO mira hacia atrás, RTO mira hacia delante</text>
  <line x1="40" y1="86" x2="640" y2="86" stroke="#444" stroke-width="2"/>
  <circle cx="170" cy="86" r="6" fill="#0055a0"/>
  <circle cx="340" cy="86" r="7" fill="#d13c3c"/>
  <circle cx="560" cy="86" r="6" fill="#2d8659"/>
  <text x="170" y="72" text-anchor="middle" class="k14">Última copia útil</text>
  <text x="340" y="66" text-anchor="middle" class="k14">INCIDENTE</text>
  <text x="560" y="72" text-anchor="middle" class="k14">Servicio restablecido</text>
  <path d="M170 108 L340 108" stroke="#e89822" stroke-width="3"/>
  <path d="M340 130 L560 130" stroke="#2d8659" stroke-width="3"/>
  <text x="255" y="126" text-anchor="middle" class="k14">RPO</text>
  <text x="255" y="140" text-anchor="middle" class="d14">datos que se pierden</text>
  <text x="255" y="154" text-anchor="middle" class="d14">→ fija la FRECUENCIA de copia</text>
  <text x="450" y="148" text-anchor="middle" class="k14">RTO</text>
  <text x="450" y="162" text-anchor="middle" class="d14">tiempo sin servicio</text>
  <text x="450" y="176" text-anchor="middle" class="d14">→ fija la TECNOLOGÍA de recuperación</text>
  <rect x="40" y="186" width="600" height="24" rx="4" fill="#f0f4f8" stroke="#0055a0"/>
  <text x="340" y="203" text-anchor="middle" class="d14">Los dos los fija el responsable del SERVICIO a partir del análisis de impacto; el técnico diseña la solución</text>
  <text x="340" y="232" text-anchor="middle" class="k14">Tres formas de copiar, tres costes de restaurar</text>
  <rect x="16" y="242" width="210" height="76" rx="5" fill="#0055a0"/>
  <text x="121" y="262" text-anchor="middle" class="t14">TOTAL (full)</text>
  <text x="121" y="281" text-anchor="middle" class="s14">Copia todo · ventana larga</text>
  <text x="121" y="298" text-anchor="middle" class="s14">Restaurar: 1 solo paso</text>
  <text x="121" y="313" text-anchor="middle" class="s14">la más simple y segura</text>
  <rect x="234" y="242" width="210" height="76" rx="5" fill="#e89822"/>
  <text x="339" y="262" text-anchor="middle" class="t14">DIFERENCIAL</text>
  <text x="339" y="281" text-anchor="middle" class="s14">Lo cambiado desde la TOTAL</text>
  <text x="339" y="298" text-anchor="middle" class="s14">Restaurar: total + la última</text>
  <text x="339" y="313" text-anchor="middle" class="s14">crece cada día que pasa</text>
  <rect x="452" y="242" width="212" height="76" rx="5" fill="#2d8659"/>
  <text x="558" y="262" text-anchor="middle" class="t14">INCREMENTAL</text>
  <text x="558" y="281" text-anchor="middle" class="s14">Lo cambiado desde la ÚLTIMA</text>
  <text x="558" y="298" text-anchor="middle" class="s14">Restaurar: total + TODA la cadena</text>
  <text x="558" y="313" text-anchor="middle" class="s14">si falta un eslabón, se rompe</text>
  <rect x="16" y="328" width="428" height="42" rx="5" fill="#004077"/>
  <text x="230" y="346" text-anchor="middle" class="t14">REGLA 3-2-1</text>
  <text x="230" y="363" text-anchor="middle" class="s14">3 copias · 2 soportes distintos · 1 fuera de las instalaciones (+ inmutable)</text>
  <rect x="452" y="328" width="212" height="42" rx="5" fill="#d13c3c"/>
  <text x="558" y="346" text-anchor="middle" class="t14">SIN PRUEBA DE RESTAURACIÓN</text>
  <text x="558" y="363" text-anchor="middle" class="s14">no es una copia: es una suposición</text>
  <text x="670" y="384" text-anchor="end" style="font:9.5px system-ui;fill:#666">[Fuente: NIST80034; ISO22301; ENS mp.info.6]</text>
</svg>
```
