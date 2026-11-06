 <img width="1280" height="400" alt="Super Mario Kart – Fullscreen Edition" src="https://github.com/user-attachments/assets/838b9ed3-0d4c-4db8-a1d1-c81326d3d1ab" />

# Super Mario Kart – Fullscreen Edition (USA)

**Una auténtica versión a pantalla completa del modo para un jugador de Super Mario Kart, con cámara de horizonte amplio, minimapa flotante, escenarios adaptados en los 20 circuitos y una profunda revisión de la lógica del juego para ajustarla a la nueva perspectiva.**

[![Super Mario Kart – Fullscreen Edition v3.0](https://img.youtube.com/vi/BO4YEe-mxVU/hqdefault.jpg)](https://youtu.be/BO4YEe-mxVU)

Por **Psicopompo** · ROM USA · Parches IPS y BPS · Versión actual: **v3.0**

---

## ¿Por qué existe este proyecto?

Super Mario Kart es un juego magnífico, pero su modo para un jugador siempre ha tenido una limitación: la carrera ocupa únicamente una parte de la pantalla, mientras que la zona inferior está reservada para un mapa o un espejo retrovisor heredados del diseño de pantalla dividida para dos jugadores.

El primer paso parecía evidente: eliminar ese recorte para que la carrera pudiera aprovechar los 256×224 píxeles de la pantalla completa.

<img width="256" height="224" alt="Super Mario Kart original" src="https://github.com/user-attachments/assets/720198e8-d8f6-41bf-bf2d-a980b2fca2e2" /> <img width="256" height="224" alt="Super Mario Kart a pantalla completa" src="https://github.com/user-attachments/assets/d136ed1b-e4a8-4a49-a6e6-9b72715bc234" />

Pero eso era solo el principio.

La cámara seguía apuntando a la posición original, el kart continuaba dibujándose para el diseño anterior y tanto las sombras como los rivales, las colisiones, los objetos, el HUD y los efectos de pantalla seguían asumiendo que la parte inferior de la imagen estaba ocupada por otra cosa.

**No bastaba con quitar el mapa.** Había que modificar la propia referencia de la cámara y adaptar todo lo que dependía de ella.

## La idea que hizo avanzar el proyecto

Al principio, el proyecto intentaba solucionar las consecuencias una por una: mover el kart, corregir la sombra, ajustar los efectos, las colisiones, los rivales, los objetos…

Cada arreglo parecía descubrir otra parte del juego que todavía utilizaba las coordenadas antiguas.

Entonces surgió una idea que cambió el rumbo del proyecto: **el jugador 2 ya contaba con buena parte de la lógica de coordenadas de pantalla necesaria para colocar un kart en la posición que buscábamos para la nueva vista del jugador 1. ¿Por qué no reutilizar esa lógica?**

Eso no resolvió todos los problemas, pero proporcionó una base mucho mejor que intentar corregir cada efecto secundario por separado. Permitió ahorrar tiempo y concentrarse en los problemas más profundos de cámara y proyección.

## La cámara

La cámara y el sistema de proyección originales estaban diseñados en torno al DSP-1 y a la distribución de pantalla original del juego.

Mover simplemente a Mario hacia abajo no funciona. El sprite cambia de posición, pero la carretera, la sombra, los rivales y los cálculos de colisión siguen perteneciendo a la proyección anterior. El resultado es un kart que parece flotar sobre el suelo.

<img width="256" height="224" alt="Ajuste de cámara" src="https://github.com/user-attachments/assets/88b90047-53c8-4df4-9b2a-4bf06d72206f" /> <img width="256" height="224" alt="Distribución de la proyección" src="https://github.com/user-attachments/assets/8207c45b-d0fb-4497-a037-a163d21f01aa" />

La solución fue cambiar la propia referencia de la cámara. **El kart permanece en su nueva posición en pantalla mientras el escenario proyectado se acerca a él**, de una forma similar al efecto visual que se produce al acelerar en el juego original.

Esto resultó especialmente importante en la parrilla de salida. Al ampliar la vista de carrera hasta ocupar las 224 líneas, la parrilla quedaba demasiado lejos de Mario: el kart estaba en la posición deseada, pero los rivales y la marca pintada en el suelo seguían situados según la proyección antigua. Volver a mover el kart no era la solución. Había que recuperar la relación correcta entre el escenario y el kart.

**El kart permanece donde debe estar; el mundo se acerca a él.**

La versión 1.2 perfeccionó esta relación. La proyección del suelo se realineó con la posición del kart en pantalla, de modo que el punto de la pista situado debajo del vehículo coincide con el lugar donde realmente tocan sus ruedas. Esto también corrigió las colisiones con paredes, bordes de pista y precipicios, que antes se activaban demasiado pronto.

La versión 2.0 introdujo una segunda opción de cámara: la **cámara de horizonte amplio**, activada por defecto en los 20 circuitos. Ofrece una vista más abierta, con su propio horizonte, y también se utiliza durante la introducción de las carreras, el zoom de salida y el giro de la línea de meta.

La versión 3.0 conserva ambas opciones de cámara e introduce una nueva arquitectura interna: **el DSP-1 ha sido sustituido por el chip de expansión SA-1**. La cámara alternativa sigue pudiéndose seleccionar durante la carrera.

Ambas perspectivas mantienen la proyección a pantalla completa y las correcciones desarrolladas en versiones anteriores. La segunda cámara no es un modo de juego independiente, sino una vista alternativa construida sobre la misma base de pantalla completa.

## Novedades y cambios

- **Migración a SA-1.** El hack ha sido migrado del DSP-1 original al chip de expansión SA-1. Se trata de un importante cambio arquitectónico y constituye la base de esta nueva versión.
- **Pantalla completa real en 1P.** La vista de carrera aprovecha los 256×224 píxeles.
- **Minimapa flotante.** Un nuevo minimapa muestra el trazado del circuito durante las carreras sin renunciar a la vista ampliada. Se presenta como una superposición sobre la imagen, en lugar de ocupar una zona independiente de la pantalla.
- **Dos perspectivas de cámara.** La cámara de horizonte amplio y la cámara alternativa a pantalla completa pueden intercambiarse durante la partida.
- **Escenarios adaptados en los 20 circuitos.** Los cielos se amplían para evitar franjas negras y saltos de color. Las zonas recién visibles se rellenan utilizando el tono de la banda de degradado adyacente. Las nubes de Koopa Beach aparecen a las tres alturas de la parrilla de salida y los pilares de Ghost Valley se recortan correctamente.
- **Fondos mejorados.** Se han perfeccionado los degradados del cielo y se han realizado correcciones gráficas adicionales.
- **Nueva referencia de cámara.** El kart, la carretera, los rivales, los objetos, las sombras y la lógica de colisiones mantienen su coherencia con la nueva proyección.
- **Colisiones alineadas con el kart.** Las colisiones con paredes, bordes de pista y precipicios se producen donde el kart realmente los toca, en lugar de hacerlo antes de tiempo.
- **HUD reajustado.** El espacio adicional permite reorganizar los indicadores de posición, número de coches y monedas sin las limitaciones del diseño original.
- **Tablas y rótulos centrados.** La tabla LAP TIME y las caras de la clasificación se desplazan hacia abajo. También se recolocan Game Over, ROUND 1, Ranked Out y los menús RETRY / END.
- **Corrección de efectos dependientes de la posición.** Plátanos, humo de aplastamiento, Monty Moles, monedas perdidas y otros efectos vinculados a la antigua posición del kart se adaptan al nuevo diseño.
- **Rescate de Lakitu adaptado.** Cuando el jugador cae de la pista, Lakitu entra en escena, recoge el kart con su caña y su moneda y lo devuelve al circuito, igual que en el juego original.
- **Escalado de rivales perfeccionado.** Se conservan los once dibujos originales de los rivales, cuyos tamaños se seleccionan mediante una nueva distribución geométrica elegida tras comparar las distintas alternativas en movimiento. El tamaño normal del jugador no cambia.
- **Mejoras de rendimiento.** Se han introducido nuevas optimizaciones, junto con la migración a SA-1.
- **Modo 2P conservado.** La lógica de pantalla completa está restringida al modo para un jugador. El modo de dos jugadores mantiene la distribución y el comportamiento originales de pantalla dividida.
- **Otras correcciones gráficas y de jugabilidad.** Se han solucionado diversos problemas relacionados con artefactos visuales, posición de sprites, representación de fondos y otras inconsistencias.

## El mapa y el espejo retrovisor

La idea original era conservar ambos como pequeñas superposiciones sobre la vista de carrera a pantalla completa.

Sin embargo, el mapa y el espejo retrovisor originales son representaciones Mode 7 secundarias. Mantenerlos en su forma original habría obligado a volver a dividir la pantalla por la mitad.

Eso iba directamente en contra del objetivo de conseguir una vista de carrera limpia y a pantalla completa.

La versión 3.0 introduce una solución diferente: **un minimapa flotante que aparece durante las carreras**, permitiendo consultar el trazado del circuito sin sacrificar la vista ampliada.

El espejo retrovisor original sigue eliminado durante las carreras a pantalla completa.

El mapa de los resultados de Time Trial continúa visible, incluyendo la información BEST 5 / BEST LAP.

El modo para dos jugadores conserva su presentación original de pantalla dividida.

## Cómo se desarrolló: arreglar algo y romper otra cosa

El proyecto terminó siendo mucho más complejo que mover un sprite y cambiar unas cuantas coordenadas.

El juego combina DSP-1, Mode 7, HDMA, OAM, ordenación de profundidad de sprites, rutinas de colisión, límites de coordenadas de pantalla, ventanas de color y otros sistemas que asumían la distribución original del modo para un jugador.

Prácticamente cada corrección importante abría la puerta a otro problema.

Los rivales podían atravesar a Mario porque el código de colisiones seguía utilizando el antiguo rango de profundidad. Las tuberías podían volverse casi invisibles para la detección de colisiones. Los objetos podían desaparecer demasiado pronto porque la nueva cámara los llevaba más allá de los límites de visibilidad originales. Algunos sprites podían saltar del borde inferior de la pantalla al superior porque la SNES almacena su coordenada Y en 8 bits. Lakitu, las sombras, el humo, las monedas, los plátanos y otros efectos podían seguir vinculados a la antigua posición del jugador.

El rescate de Lakitu es un buen ejemplo. Su secuencia espera a que la coordenada Y alcance determinados valores elegidos para el rango de pantalla original. Con la vista ampliada, su trayectoria atraviesa valores negativos, por lo que esas esperas —y la moneda que lleva— nunca llegaban a completarse. Hubo que adaptar las comprobaciones sin alterar su velocidad ni su secuencia.

También fue necesario investigar el orden OAM de los karts para entender por qué algunos rivales se superponían incorrectamente. Algunas soluciones experimentales funcionaban visualmente, pero consumían demasiados ciclos de CPU y provocaban ralentizaciones en la versión NTSC. Esos enfoques tuvieron que descartarse y sustituirse por soluciones mucho más económicas.

Por eso, el desarrollo se apoyó en un proceso continuo de pruebas de regresión. **Decenas de estados de guardado reproducibles**, que cubrían salidas de carrera, copas, colisiones, efectos, Time Trial, Ranked Out, Game Over, pantallas de reintento, créditos, modo 2P y otras situaciones, se reprodujeron y compararon fotograma a fotograma después de cada cambio.

En la versión 1.4, la nueva distribución de tamaños de los rivales se comprobó mediante **3.360 fotogramas comparados**. La cámara, el cronómetro, los campos de posición y velocidad y los sprites del jugador coincidieron con la referencia anterior. Una prueba independiente de 360 fotogramas en pantalla dividida también coincidió en sus imágenes completas.

La versión 2.0 incorporó pruebas de regresión específicas para la nueva cámara y los escenarios adaptados. En bsnes, el modo attract desde un arranque en frío se comparó con la ROM original durante **2.950 fotogramas**, con resultados idénticos salvo por la firma del hack. **Veintisiete estados reales de carrera**, comparados durante 120 fotogramas cada uno, no mostraron diferencias de representación.

El rendimiento se comprobó por separado. En una prueba de Time Trial en Bowser Castle 1, desde un arranque en frío y con giros bruscos programados a alta velocidad, la ROM USA original, la v1.5 y la v2.0 produjeron los mismos ciclos de reloj (11.640 de 12.000) y los mismos tiempos siguiendo la misma trayectoria.

La versión 3.0 lleva el proyecto un paso más allá con la migración a SA-1, el nuevo minimapa flotante, optimizaciones adicionales y pruebas ampliadas de compatibilidad con flashcarts.

Una corrección no se consideraba terminada simplemente porque funcionase en una captura de pantalla. Tenía que superar el resto de las pruebas.

## Desarrollo

Este proyecto se ha desarrollado mediante una colaboración iterativa entre una persona y una IA, basada en la interacción continua, la exploración conjunta y la retroalimentación mutua.

El proceso de desarrollo ha consistido en investigar posibilidades, explorar distintos enfoques, evaluar resultados, resolver problemas y perfeccionar soluciones mediante ciclos repetidos de experimentación y pruebas. Las ideas evolucionaron, los planteamientos se ajustaron y las soluciones mejoraron a lo largo de todo el proceso.

El resultado final refleja esta colaboración continuada, en la que el valor no reside en una contribución aislada, sino en cómo la interacción entre la persona y la IA ha dado forma al desarrollo en su conjunto.

## Aplicación del parche

Se necesita una ROM limpia y sin cabecera de **Super Mario Kart (USA)**.

| ROM | Tamaño | CRC32 |
| --- | ---: | --- |
| Original (USA, limpia y sin cabecera) | 524.288 bytes | `CD80DB86` |
| Parcheada (v3.0) | 4.194.304 bytes | No facilitado |

La ROM resultante ocupa **4 MB (4.194.304 bytes)**.

Su checksum corregido en la cabecera SNES es:

- Checksum: `AE16`
- Complemento del checksum: `51E9`

Se incluyen dos parches:

- `SMK_Fullscreen_USA.bps` — **recomendado**; verifica la ROM de entrada antes de aplicar el parche.
- `SMK_Fullscreen_USA.ips` — no verifica la ROM de entrada.

El parche IPS se ha verificado contra la ROM final utilizando un decodificador propio, pero no se ha probado con herramientas de parcheo de terceros como Flips o Lunar IPS.

Aplica **un solo parche** sobre una copia de tu ROM limpia. No apliques ninguno de los dos parches sobre una versión que ya esté parcheada.

La versión PAL no es compatible.

No se incluye ninguna ROM del juego.

## Requisitos

El juego necesita un emulador o flashcart con soporte para **SA-1**.

Emuladores recomendados:

- **Mesen**
- **bsnes**

## Compatibilidad con flashcarts

La compatibilidad ha sido probada por jugadores utilizando:

- **FXPAK Pro**
- **SD2SNES con firmware oficial**

**Guardado en flashcarts:** después de guardar, vuelve a un menú y espera un momento antes de apagar la consola. Así das tiempo al flashcart para escribir los datos de guardado en la tarjeta SD.

El LED rojo del flashcart puede permanecer encendido durante la partida. Este comportamiento se ha observado durante las pruebas y no ha ocasionado ningún problema.

## Problemas conocidos

- **FXPAK Pro:** ocasionalmente pueden aparecer dos pequeños píxeles blancos en la zona oscura del lado izquierdo de la pantalla en Ghost Valley.
- **Parpadeo de fondos:** pueden producirse parpadeos ocasionales durante momentos especialmente exigentes.
- **Firmware SD2SNES no oficial:** se ha informado de congelaciones aleatorias en un clon que utilizaba el firmware `sd2SNES+`. Este problema no se ha reportado con el firmware oficial.

Estos problemas siguen bajo investigación. Esta versión mejora la compatibilidad y corrige varios problemas gráficos que llevaban tiempo presentes, aunque todavía quedan algunas imperfecciones.

## Historial de versiones

- **v3.0** – Actualización importante. Migra el hack de DSP-1 a SA-1, introduce un minimapa flotante durante las carreras y añade una perspectiva de cámara alternativa que puede seleccionarse durante la partida. Mejora los degradados del cielo y los gráficos de los fondos, incorpora nuevas optimizaciones de rendimiento, corrige diversos problemas gráficos y de jugabilidad y añade compatibilidad probada con FXPAK Pro y SD2SNES con firmware oficial.

- **v2.0** – Introduce la cámara de horizonte amplio, activada por defecto en los 20 circuitos, con cambio mediante SELECT durante la carrera entre la nueva cámara y la clásica. La nueva vista también se utiliza en la introducción, el zoom de salida y el giro de la línea de meta. Los escenarios se adaptan en los 20 circuitos, incluyendo cielos ampliados, rellenos de degradado sin cortes, nubes de Koopa Beach a las tres alturas de la parrilla de salida y pilares recortados correctamente en Ghost Valley. Corrige la cara duplicada del jugador después de ganar, el parpadeo de las montañas durante la carga, las líneas negras y azules intermitentes en Ghost Valley, el umbral de colisión de las manchas de aceite y la alineación del rótulo ROUND. Resincroniza el modo attract y reduce los ciclos de CPU sin modificar el resultado visual. Incluye todas las mejoras de la v1.5.

- **v1.5** – Corrige la pantalla de resultados de Time Trial. Los resultados muestran ahora correctamente todas las vueltas, los tiempos destacados, TOTAL y el mapa con BEST 5 / BEST LAP, mientras la carrera permanece a pantalla completa y se conserva la distribución de resultados del Grand Prix.

- **v1.4** – Introduce una nueva distribución geométrica para los once tamaños originales de los rivales, seleccionada tras comparar las distintas alternativas en movimiento. El tamaño normal del jugador no cambia. La corrección lateral de la parrilla de salida se aplica ahora desde el comienzo de la aproximación de la cámara, conservando el zoom y la órbita completos. Corrige la sombra de Lakitu en pantalla completa y en ambas vistas de pantalla dividida.

- **v1.3** – Lakitu ya no aparece en la parte inferior de la pantalla: su cabeza y su nube se ocultan mientras desciende desde arriba o sale hacia arriba, y se eliminan los restos que quedaban al inicio y después de un rescate. En 2P, la moneda de Lakitu y las monedas perdidas se dibujan a la altura correcta. Reduce la carga de CPU en 1P.

- **v1.2** – Realinea la proyección del suelo con la posición del kart en pantalla, de modo que la pista situada debajo del vehículo coincide con el lugar donde se dibuja. Corrige el rescate de Lakitu después de caer de la pista y reduce las ralentizaciones calculando una sola vez por fotograma la comprobación de pantalla completa.

- **v1.1** – Corrige píxeles blancos sueltos en la banda de transición de la imagen. La tabla LAP TIME y las caras de la clasificación se desplazan otros 5 píxeles hacia abajo.

- **v1.0** – Lanzamiento inicial.

## Estado y limitaciones

- **Solo USA.** La versión PAL no es compatible.
- **224 líneas / 60 Hz NTSC.**
- Requiere un emulador o flashcart con soporte para **SA-1**.
- Emuladores recomendados: **Mesen y bsnes**.
- Compatibilidad con flashcarts probada en **FXPAK Pro y SD2SNES con firmware oficial**.
- Las copas de 50cc y 100cc se completaron con versiones anteriores. Las versiones posteriores han recibido pruebas de regresión adicionales estado por estado, comparaciones fotograma a fotograma, mediciones de rendimiento y sesiones de juego, pero esto no garantiza que todos los modos estén libres de errores.
- Los objetos de los circuitos, como las tuberías, siguen utilizando las reglas originales de carga por secciones. Con la nueva referencia de cámara, algunos límites de aparición y desaparición resultan más visibles.
- El modo para dos jugadores conserva su comportamiento original de pantalla dividida y no utiliza la cámara a pantalla completa de 1P.
- El minimapa flotante está disponible durante las carreras a pantalla completa. El espejo retrovisor original sigue eliminado.
- Todavía quedan algunas imperfecciones gráficas. Consulta la sección **Problemas conocidos**.
- Los informes de errores son bienvenidos. Incluye el emulador o modelo de flashcart, la versión del firmware, el modo de juego y un estado de guardado que permita reproducir el problema.

## Créditos y aviso legal

- **Psicopompo** — dirección del proyecto, investigación, análisis, diseño de soluciones, pruebas y validación.

Super Mario Kart © Nintendo.

Este es un proyecto no oficial realizado por aficionados y no está afiliado a Nintendo ni cuenta con su aprobación.

No se distribuyen datos del juego. Debes proporcionar tu propia ROM obtenida legalmente.
