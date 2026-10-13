 <img width="1280" height="400" alt="Super-Mario-Kart-Logo" src="https://github.com/user-attachments/assets/838b9ed3-0d4c-4db8-a1d1-c81326d3d1ab" />

# Super Mario Kart – Fullscreen Edition (USA)

**Una vista de pantalla completa de verdad para el modo de 1 jugador de Super Mario Kart, con cámara de horizonte amplio, decorados adaptados en los 20 circuitos y un replanteo completo de la lógica del juego en torno a la vista ampliada.**

Por **Psicopompo** · ROM USA · IPS y BPS · Versión actual: **v2.0**

[![Super Mario Kart in Fullscreen!](https://img.youtube.com/vi/2ajlZI5xrAw/hqdefault.jpg)](https://youtu.be/2ajlZI5xrAw)

---

## Por qué existe

Super Mario Kart es un juego precioso que siempre ha jugado su modo de 1 jugador con una mano atada a la espalda. La carrera se dibuja en una parte recortada de la pantalla, mientras que la zona inferior queda reservada para un mapa o un retrovisor heredados del diseño a pantalla partida del modo 2 jugadores.

El primer paso obvio es quitar el recorte que parte la imagen para que el suelo en modo 7 pueda usar las 256×224 píxeles completas.

Pero eso es solo el principio.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-031613" src="https://github.com/user-attachments/assets/29a52de2-30c4-401c-be1a-4015c5d3c60a" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-030909" src="https://github.com/user-attachments/assets/2534d407-c5a0-4448-8118-df31ec4ef981" />

La cámara sigue apuntando a la posición antigua, el kart se sigue dibujando para la distribución antigua, y la sombra, los rivales, las colisiones, los objetos, el HUD y los efectos de pantalla siguen dando por hecho que la parte inferior de la imagen es otra cosa.

**Esto no es solo «quitar el mapa».** Se cambia la propia referencia de la cámara, y todo lo que depende de ella tiene que seguirla.

## La idea que hizo avanzar el proyecto

Al principio el proyecto intentó resolver las consecuencias una a una: mover el kart, arreglar la sombra, arreglar los efectos, arreglar las colisiones, arreglar los rivales, arreglar los objetos…

Cada arreglo parecía destapar otra parte del juego que seguía usando las coordenadas antiguas.

Y entonces llegó la idea que cambió la dirección del proyecto: **el Jugador 2 ya tenía buena parte de la lógica de espacio de pantalla necesaria para colocar un kart alrededor de la posición que queríamos para la nueva vista de 1 jugador. ¿Por qué no reutilizar esa lógica para el Jugador 1?**

No lo resolvió todo por sí sola, pero proporcionó una base mucho mejor que pelear cada efecto secundario por separado. Eso ahorró muchísimo tiempo y permitió concentrarse en los problemas más profundos de cámara y proyección.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-040214" src="https://github.com/user-attachments/assets/fb3a2e64-65fb-4b7d-831a-8ecceedea7ad" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-041627" src="https://github.com/user-attachments/assets/1b3b37c2-3698-4f0c-b0d7-8d9ef875a610" />

## La cámara

El suelo en modo 7 lo proyecta el DSP-1 de la SNES a partir de un punto de foco asociado al kart.

Simplemente dibujar a Mario más abajo en la pantalla no funciona. El sprite se moverá, pero la carretera, la sombra, los rivales y los cálculos de colisión siguen perteneciendo a la proyección antigua. El resultado es un kart que parece flotar separado del suelo.

La solución fue cambiar la propia referencia de la cámara. **El kart se queda en su nueva posición de pantalla mientras el escenario proyectado se acerca a él**, de forma parecida al efecto visual que se produce al acelerar en el juego original.

Esto resultó especialmente importante en la parrilla de salida. Tras ampliar el área de modo 7 hasta llenar las 224 líneas, la parrilla quedaba demasiado por delante de Mario: el kart estaba en la posición deseada, pero los rivales y la marca pintada de la parrilla se habían quedado atrás en la proyección antigua. Volver a mover el kart no era la respuesta. Había que traer el propio escenario de vuelta a la relación correcta con el kart.

Por eso el punto de foco efectivo del DSP-1 se desplaza hacia delante a lo largo de la dirección de la vista, y la cámara transiciona gradualmente a su nueva posición al empezar la carrera en lugar de cambiar de golpe.

**El kart se queda donde le corresponde; el mundo es el que se acerca a él.**

La versión 1.2 refinó esta relación. El punto del circuito que el juego trata como la posición del kart seguía situado unas 37 filas de pantalla por encima de los pies del kart (en el juego original está unas 6 filas por encima), así que las colisiones con muros, bordes y fosos saltaban demasiado pronto. Ahora la proyección del suelo está realineada con la posición del kart en pantalla, de modo que el punto bajo el kart se dibuja donde el kart toca realmente el suelo.

La versión 2.0 introduce una segunda opción de cámara: la **cámara de horizonte amplio**, activada por defecto en los 20 circuitos. Ofrece una vista más abierta y alta, con horizonte propio, y también se usa durante la intro, el zoom de salida y el giro de meta. Pulsa **SELECT durante la carrera** para alternar al vuelo entre la cámara de horizonte amplio y la clásica. SELECT no tiene efecto en los menús.

Ambas opciones de cámara conservan la proyección a pantalla completa y las correcciones desarrolladas en las versiones anteriores. La cámara nueva no es un modo aparte del juego: es una vista alternativa construida sobre la misma base de pantalla completa.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-032540" src="https://github.com/user-attachments/assets/70bff508-ffa6-4a1e-886f-15d4369451b0" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-032728" src="https://github.com/user-attachments/assets/cd414d84-033b-4867-8f5c-935351be6fb6" />

## Qué cambia

* **Pantalla completa real en 1P.** La vista de carrera usa las 256×224 píxeles completas.
* **Dos vistas de cámara.** La nueva cámara de horizonte amplio está activada por defecto en los 20 circuitos. Pulsa SELECT durante la carrera para alternar entre ella y la cámara clásica a pantalla completa. La vista nueva también cubre la intro, el zoom de salida y el giro de meta.
* **Decorados adaptados en los 20 circuitos.** Los cielos se extienden para evitar bandas negras y saltos de color. Las zonas que quedan a la vista se rellenan usando el tono de la franja adyacente del degradado. Las nubes de Koopa Beach aparecen en las tres alturas desde la parrilla de salida, y los pilares de Ghost Valley se recortan correctamente.
* **Nueva referencia de cámara.** El kart, la carretera, los rivales, los objetos, las sombras y la lógica de colisión se mantienen coherentes con la nueva proyección.
* **Colisiones alineadas con el kart.** Las colisiones con muros, bordes del circuito y fosos ocurren donde el kart las toca de verdad, no antes.
* **Reubicación del HUD.** El espacio extra permite reorganizar los dígitos de posición, el contador de coches y el contador de monedas sin las limitaciones de la distribución original. El dígito pequeño de posición se mueve unos 8 píxeles a la izquierda, y el dígito grande de posición final se traslada al espacio nuevo.
* **Tablas y carteles centrados.** La tabla de LAP TIME y las caras de la clasificación se bajan 25 píxeles. Game Over, ROUND 1, Ranked Out y los menús RETRY / END también se reposicionan. El cartel ROUND se corrige en la v2.0.
* **Efectos dependientes de la posición, corregidos.** Plátanos, humo de aplastamiento, Monty Moles, monedas perdidas y otros efectos que estaban atados a la posición antigua del kart se mueven para encajar con la nueva distribución de cámara.
* **El rescate de Lakitu funciona a pantalla completa.** Tras caerse del circuito, Lakitu entra en escena, recoge el kart con la moneda y lo devuelve a la pista, como en el juego original. Se evita que su cabeza, su nube y los «tres pelos» sobrantes aparezcan en el borde inferior de la pantalla durante su entrada, el rescate y su salida.
* **Escalado de rivales refinado.** Se conservan los once dibujos originales de los rivales, pero sus tamaños se eligen según una nueva distribución geométrica escogida tras comparar las alternativas en movimiento. El tamaño normal del jugador no cambia.
* **Alineación de la parrilla refinada.** La corrección lateral de la parrilla de salida se aplica desde el comienzo del acercamiento de la cámara. El zoom y la órbita completos de la introducción se conservan intactos.
* **Sombras de Lakitu corregidas.** Su sombra se corrige a pantalla completa y en las dos vistas de pantalla partida, y se mantiene la corrección anterior del cuerpo que asomaba por abajo.
* **Rendimiento ajustado.** La comprobación que decide si se aplica la lógica de pantalla completa se calcula una vez por fotograma en lugar de decenas de veces. En la escena más pesada medida (el rescate de Lakitu), los fotogramas con retraso bajaron del 18 % a prácticamente cero respecto a la build anterior a esa optimización. La v1.3 recorta la carga aún más: en la salida de carrera más pesada medida, el pico de carga de CPU bajó del 95,7 % al 90,5 % (original: 89 %), y no se midió ningún fotograma con retraso en los primeros 1.061 fotogramas de las salidas de las copas Champiñón, Flor y Estrella (50cc). La v2.0 reduce aún más los ciclos de CPU sin cambiar el resultado renderizado.
* **2P conservado.** La lógica de pantalla completa se restringe a 1P. La rama de 2 jugadores mantiene la lógica original del juego mediante puertas dedicadas, y los efectos secundarios que se filtraban al 2P se corrigieron uno a uno. La moneda de Lakitu y las monedas perdidas en 2P se dibujan a la altura correcta en lugar de 88 píxeles demasiado abajo tras jugar una carrera de 1P en la misma sesión.
* **Problemas gráficos secundarios corregidos.** Parpadeo de los créditos, texto de reintento en 2P, artefactos de Time Trial, una bola suelta detrás de Mario al empezar Time Trial, la sombra de Lakitu durante la secuencia de rescate, sprites en el borde inferior, parpadeo del contador de monedas y vidas, y varios problemas más fueron localizados y corregidos. La v2.0 corrige además la cara duplicada del jugador al ganar, el parpadeo de montañas durante la carga, las líneas negras y azules intermitentes en Ghost Valley y el umbral de colisión de la mancha de aceite.
* **Attract mode corregido.** El attract mode se resincroniza en la v2.0, conservando el renderizado original salvo por la firma del hack.
* **Pantalla de título.** Se añadió una línea discreta en blanco, `Fullscreen Edition · Psicopompo`, bajo el copyright de Nintendo. La línea de copyright original también se desplazó 2 píxeles a la derecha para centrarla.

<p align="center">
  <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo)-261012-030213" src="https://github.com/user-attachments/assets/ed38c50b-da13-445b-9caf-d51ff9f34569" />
  <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo)-261012-030211" src="https://github.com/user-attachments/assets/ce5ef69c-f19b-4fdf-bc26-9e0ffd75e452" />
</p>
<p align="center"><sub><span style="color: white;">Las dos cámaras seleccionables.</span></sub></p>

## Mapa y retrovisor: fuera, a propósito

La idea original era conservar ambos como pequeños recuadros sobre la vista de carrera completa.

Sin embargo, los dos son renderizados secundarios en modo 7, y conservarlos suponía volver a partir el fotograma a media pantalla. Eso iba directamente en contra del objetivo de una vista de carrera limpia a pantalla completa e introducía una colección nueva de problemas de tiempos, HDMA y renderizado.

Por tanto, el mapa y el retrovisor se dejaron fuera de las carreras a pantalla completa. **El mapa de resultados de Time Trial sigue visible**, incluida la información de BEST 5 / BEST LAP.

**Una vista de carrera limpia a pantalla completa ganó frente a un compromiso recargado.**

El modo 2 jugadores conserva la presentación original a pantalla partida.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-003628" src="https://github.com/user-attachments/assets/3c5f4f1a-1f72-4f38-85d1-d4f236b2507d" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261003-013030" src="https://github.com/user-attachments/assets/513fa905-178b-40e1-984c-91c2062df0cf" />

## Cómo se construyó: arreglos que rompían otras cosas

Esto resultó ser mucho más profundo que mover un sprite y cambiar unas coordenadas.

El juego combina el DSP-1, el modo 7, HDMA, OAM, la ordenación de profundidad de sprites, las rutinas de colisión, los límites de espacio de pantalla, las ventanas de color y otros cuantos sistemas que daban por hecha la distribución original de 1 jugador.

Casi cada arreglo importante abría otro problema.

Los rivales podían atravesar a Mario porque el código de colisión seguía usando el rango de profundidad antiguo. Las tuberías podían volverse prácticamente invisibles para la detección de colisiones. Los objetos podían desaparecer demasiado pronto porque la cámara nueva los empujaba fuera de los límites de visibilidad originales. Los sprites podían saltar del borde inferior de la pantalla al superior porque la SNES guarda su coordenada Y en 8 bits. Lakitu, las sombras, el humo, las monedas, los plátanos y otros efectos podían quedar todos atados a la posición antigua del jugador.

El rescate de Lakitu es un buen ejemplo. Su guion espera a que su coordenada Y alcance ciertos valores, elegidos para el rango de pantalla original. Con la vista más amplia su recorrido cruza valores negativos, así que esas esperas, y la moneda que lleva, no se completaban nunca. Hubo que adaptar las comprobaciones sin cambiar su velocidad ni su secuencia.

Incluso cuando el rescate ya funcionaba, Lakitu seguía dejando rastros en la parte baja de la pantalla. El rescate empieza con una coordenada Y negativa, así que su cabeza y su nube aparecían en las líneas extra de abajo mientras bajaba desde arriba, y de nuevo al marcharse hacia arriba; ahora esos elementos se ocultan en esos momentos. Arreglar eso destapó un problema más: sus tres trozos de pelo sobrantes se quedaban dibujados en el borde inferior durante el resto de la carrera, porque el juego no reescribe esos huecos de sprite cuando Lakitu termina. Ahora se aparcan fuera de pantalla, lo que de paso limpia los estados guardados creados con versiones anteriores.

También hubo que investigar el orden OAM de los karts para entender por qué algunos rivales se solapaban incorrectamente. Algunos arreglos experimentales funcionaban visualmente pero costaban demasiados ciclos de CPU y provocaban ralentización en la versión NTSC. Esos enfoques hubo que descartarlos y sustituirlos por enganches mucho más baratos.

Perfilar las ralentizaciones mostró que el culpable era uno de esos enganches: la comprobación que decide si se aplica la lógica de pantalla completa la ejecutaban las rutinas de dibujo de sprites entre 40 y 55 veces por fotograma. En la escena más pesada medida (el rescate de Lakitu), la lógica del juego tardaba casi tanto como el propio fotograma. Ahora el resultado de esa comprobación se calcula una vez por fotograma y lo leen directamente las rutinas que más se llaman. La v1.3 va un paso más allá: el código de proyección y de descarte de objetos también lee ese resultado en caché, y los tres envoltorios encadenados que deciden si un objeto está en pantalla se fusionaron en una sola rutina. La conducción normal, las salidas de carrera con los ocho karts y carreras completas en Donut Plains no mostraron retraso.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-040354" src="https://github.com/user-attachments/assets/c0163555-2ec3-4b5d-88d6-7f344ac86a8d" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v2 0) (by Psicopompo)-261012-041922" src="https://github.com/user-attachments/assets/653d7a3b-8982-4892-b8ef-f2c47345538c" />

El trabajo se volvió, por tanto, fuertemente dirigido por regresiones. **Decenas de estados guardados reproducibles** que cubren salidas de carrera, copas, colisiones, efectos, Time Trial, Ranked Out, Game Over, pantallas de reintento, créditos, 2P y otras situaciones se reproducían y comparaban fotograma a fotograma tras cada cambio.

Para la v1.4, la nueva distribución de tamaños de los rivales se comprobó a lo largo de **3.360 fotogramas comparados**. La cámara, el cronómetro, los campos de posición y velocidad y los sprites del jugador coincidían con la referencia anterior, y una prueba de 360 fotogramas a pantalla partida también coincidió en sus imágenes completas. Esto no es una afirmación de cobertura exhaustiva de todos los modos.

La versión 2.0 añadió comprobaciones de regresión dedicadas para la cámara nueva y los decorados adaptados. En bsnes, el attract mode en frío se comparó contra la ROM original a lo largo de **2.950 fotogramas**, con una salida idéntica salvo por la firma del hack. **Veintisiete estados de carrera reales**, comparados durante 120 fotogramas cada uno, no mostraron diferencias de renderizado. El OAM de la cámara de meta también coincidió con la build aprobada, y se ejecutaron pruebas de regresión de varios miles de fotogramas en los circuitos con tratamiento especial de decorado.

El rendimiento se comprobó por separado. En un Time Trial de Bowser Castle 1 arrancado en frío, con giros duros guionizados a alta velocidad, la ROM USA original, la v1.5 y la v2.0 produjeron tics de reloj idénticos (11.640 de 12.000) y los mismos tiempos a lo largo de la misma trayectoria. En un estado de carrera de Bowser Castle 3, la v1.5 y la v2.0 también coincidieron (2.993 de 3.000 tics) y dieron el mismo tiempo final.

El tartamudeo en los giros duros que se observa en estas pruebas es comportamiento nativo del juego, idéntico con y sin el parche. Por ese motivo, la v2.0 no modifica la planificación de la IA ni las físicas.

Un arreglo no se daba por terminado solo porque funcionara en una captura. Tenía que sobrevivir al resto de la batería de pruebas.

<img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223050" src="https://github.com/user-attachments/assets/0e15be06-1bbe-4cb1-9b44-5df626976089" /> <img width="256" height="224" alt="Super Mario Kart - Fullscreen Edition (v1 0) (by Psicopompo)-261002-223113" src="https://github.com/user-attachments/assets/990be6ee-a48a-4e8c-a422-15ec17976c61" />

## Desarrollo

Este proyecto se desarrolló mediante un proceso de **colaboración iterativa entre una persona y una IA**, basado en la interacción continua, la exploración conjunta y la retroalimentación mutua.

El desarrollo implicó investigar distintas posibilidades, explorar enfoques, evaluar resultados, resolver problemas y perfeccionar soluciones mediante sucesivos ciclos de experimentación y pruebas. Las ideas evolucionaron, los planteamientos se ajustaron y las soluciones mejoraron a lo largo del proceso.

El resultado final es fruto de esta colaboración continua, en la que el valor no reside en una contribución aislada, sino en cómo la interacción entre la persona y la IA dio forma al desarrollo en su conjunto.

## Aplicar el parche

Entrada: una ROM limpia de **Super Mario Kart (USA)**, sin cabecera.

| ROM | Tamaño | CRC32 | MD5 | SHA-1 | SHA-256 |
| --- | ---: | --- | --- | --- | --- |
| Original (USA, limpia y sin cabecera) | 524.288 bytes | `CD80DB86` | `7f25ce5a283d902694c52fb1152fa61a` | `47E103D8398CF5B7CBB42B95DF3A3C270691163B` | No facilitado |
| Parcheada (v2.0) | 1.048.576 bytes | `E9B8C210` | `0f4d2c70b6057c8af55f584244d78911` | `3C0A0D7B4E87CD6A54151F0B953A003E9353E65B` | `008a5cedb569d07487b93dbfdb0c09c98f2b30cfecfe41916fee663c5fc9992b` |

Descarga **`Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).zip`** desde las releases. El archivo contiene los parches IPS y BPS, `LÉEME.md`, `README.md` y las notas de cambio en inglés y español. No se incluye ninguna ROM del juego.

* `Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).bps` — **recomendado**; verifica la ROM de entrada. Usa Flips, beat, MultiPatch o RomPatcher.js.
* `Super Mario Kart - Fullscreen Edition (v2.0) (by Psicopompo).ips` — usa cualquier parcheador compatible con IPS.

La salida se expande a 1 MB. El código y los datos nuevos se guardan en el espacio añadido, y el byte de tamaño de ROM se actualiza. El checksum interno está corregido, así que no debería aparecer ningún aviso de checksum en flashcarts compatibles ni en las herramientas de parcheo.

Aplica **un solo parche** a una copia de tu ROM limpia. El parche es acumulativo sobre la ROM original: **no apliques la v2.0 encima de la v1.4 ni de la v1.5**.

La versión PAL no está soportada.

## Historial de versiones

* **v2.0** – Introduce la cámara de horizonte amplio, activada por defecto en los 20 circuitos, con cambio mediante SELECT durante la carrera entre la cámara nueva y la clásica. La vista nueva también cubre la intro, el zoom de salida y el giro de meta. Decorados adaptados en los 20 circuitos, incluidos cielos extendidos, rellenos de degradado sin cortes, nubes de Koopa Beach en las tres alturas desde la parrilla de salida y pilares de Ghost Valley recortados. Corrige la cara duplicada del jugador al ganar, el parpadeo de montañas durante la carga, las líneas negras y azules intermitentes en Ghost Valley, el umbral de colisión nativo de la mancha de aceite y la alineación del cartel ROUND. Resincroniza el attract mode y reduce los ciclos de CPU sin cambiar el resultado renderizado. Conserva todas las mejoras de la v1.5. Validada en bsnes y RetroArch mediante comparación del attract mode, 27 estados de carrera reales, comparación del OAM de la cámara de meta y pruebas de regresión ampliadas. No se afirma haber probado en hardware real.

* **v1.5** – Corrige la pantalla de resultados de Time Trial. Los resultados muestran ahora correctamente todas las vueltas, los tiempos resaltados, TOTAL y el mapa con BEST 5 / BEST LAP, mientras la carrera sigue a pantalla completa y se conserva la distribución de los resultados del Grand Prix. Probada con Time Trial y una carrera normal. Incluye todas las mejoras de la v1.4.

* **v1.4** – Nueva distribución geométrica de los once tamaños originales de los rivales, elegida tras comparar las alternativas en movimiento. El tamaño normal del jugador no cambia. La corrección lateral de la parrilla de salida se aplica ahora desde el comienzo del acercamiento de la cámara conservando el zoom y la órbita completos. Corrige la sombra de Lakitu a pantalla completa y en las dos vistas de pantalla partida, manteniendo la corrección anterior del cuerpo en el borde inferior. Los cambios se comprobaron a lo largo de 3.360 fotogramas comparados, con una comparación aparte de 360 fotogramas a pantalla partida. Probada en bsnes y RetroArch y aprobada mediante pruebas visuales.

* **v1.3** – Lakitu ya no asoma por la parte baja de la pantalla: su cabeza y su nube se ocultan mientras baja desde arriba o se marcha hacia arriba (Ghost Valley, las cascadas), y se limpian los trozos sobrantes (los «tres pelos») que quedaban al empezar y tras un rescate. En 2P, la moneda de Lakitu y las monedas perdidas se dibujan a la altura correcta en lugar de 88 píxeles demasiado abajo. Menor carga de CPU en 1P (pico de carga en la salida más pesada medida: 95,7 % → 90,5 %). Incluye todas las correcciones de la v1.2.

* **v1.2** – La proyección del suelo se realinea con la posición del kart en pantalla, de modo que el circuito bajo el kart coincide con donde se dibuja el kart: las colisiones con muros, bordes y fosos ocurren ahora en el sitio correcto (antes saltaban demasiado pronto). Corrige el rescate de Lakitu tras caerse del circuito. Reduce las ralentizaciones calculando la comprobación de pantalla completa una vez por fotograma. Incluye todas las correcciones de la v1.1.

* **v1.1** – Corrige unos píxeles blancos sueltos que aparecían en la banda de transición de la imagen. La tabla de LAP TIME y las caras de la clasificación se bajaron 5 píxeles más.

* **v1.0** – Primera versión.

## Estado y limitaciones

* **Solo USA.** La versión PAL no está soportada.
* **224 líneas / 60 Hz NTSC.**
* Probado en **bsnes** y **RetroArch**. El núcleo SNES9x no se ha probado.
* **Hardware real y flashcarts:** la v2.0 no se ha probado en hardware real ni en flashcarts. Puede que versiones anteriores sí se probaran en hardware, pero eso no establece la compatibilidad de la v2.0.
* La validación de la v2.0 incluye una comparación del attract mode de 2.950 fotogramas contra la ROM original, 27 estados de carrera reales comparados durante 120 fotogramas cada uno, verificación del OAM de la cámara de meta y pruebas de regresión de varios miles de fotogramas en los circuitos con tratamiento especial de decorado.
* Las copas de 50cc y 100cc se completaron con la v1.1. Las versiones posteriores han recibido regresión adicional estado a estado, comparación fotograma a fotograma, mediciones de rendimiento y sesiones de juego, pero esto no garantiza que todos los modos estén libres de fallos. Algunos modos han recibido menos pruebas que otros.
* Los objetos del circuito, como las tuberías, siguen las reglas originales de carga por secciones del juego. Con la nueva referencia de cámara, algunas fronteras de aparición y desaparición se notan más.
* El modo 2 jugadores conserva su comportamiento original a pantalla partida y no usa la cámara de pantalla completa de 1 jugador.
* El mapa y el retrovisor se ocultan durante las carreras a pantalla completa. El mapa de resultados de Time Trial sigue visible.
* Los informes de fallos son bienvenidos. Indica el emulador y el núcleo, el modo de juego y un estado guardado que reproduzca el problema.

## Créditos y aviso

* **Psicopompo** — dirección del proyecto, investigación, análisis, diseño de soluciones, pruebas y validación.
* **Asistente de IA** — análisis de código, herramientas de ingeniería inversa, implementación de parches y automatización de pruebas, bajo la dirección de Psicopompo.

Super Mario Kart © Nintendo.

Este es un proyecto de aficionado no oficial y no está afiliado a Nintendo ni cuenta con su respaldo.

No se distribuyen datos del juego. Debes aportar tu propia ROM obtenida legalmente.
