Es posible lograr este efecto usando **FontForge** y las **ligaduras contextuales** de **OpenType**, aunque tiene sus limitaciones.

### Funcionamiento

Las ligaduras son una característica de las tipografías OpenType que permite que una secuencia de caracteres se reemplace por un solo glifo o por una secuencia de glifos diferentes. En este caso, no estás creando una ligadura tradicional (como la 'f' y la 'i' que se unen para formar un solo glifo 'fi'), sino una **sustitución contextual**.

Para lograr que `*` se vea como `→` en el contexto `*letra`, necesitarías crear una regla en FontForge que le diga al motor de renderizado de la tipografía que:

* **Identifique la secuencia:** Un espacio, un asterisco y una letra (o cualquier otro carácter que quieras).
* **Sustituya solo el asterisco:** Dentro de esa secuencia, sustituya el glifo del asterisco `*` por el glifo de la flecha `→`.

### Limitaciones

* **Aplicación:** Esta sustitución ocurre a nivel de **renderizado de tipografía** en la pantalla. El texto subyacente sigue siendo `int *pointer`. Cuando selecciones, copies y pegues el texto, seguirás obteniendo `int *pointer`. Esto es ideal para código, ya que no cambia la semántica del programa.
* **Compatibilidad:** No todos los programas y motores de renderizado de texto son compatibles con las características avanzadas de OpenType como las **ligaduras contextuales**. IDEs de programación como Visual Studio Code, Sublime Text o Neovim suelen tener una buena compatibilidad, especialmente si la fuente se carga correctamente y se habilita la característica. Sin embargo, editores de texto más simples o navegadores web con configuraciones por defecto podrían no aplicar la sustitución.

### Pasos Generales en FontForge

1.  **Crea el glifo de la flecha:** Asegúrate de que tu tipografía tenga un glifo para la flecha (`→`). Si no, puedes dibujarlo o importarlo.
2.  **Crea la sustitución en la tabla GPOS/GSUB:** Dentro de FontForge, usarías el menú `Element` > `Font Info` > `GSUB` (Sustitución de glifos). Aquí, definirías una tabla de sustitución contextual. La sintaxis es compleja, pero en esencia le dirías:
    * **Contexto anterior:** Un espacio.
    * **Glifo a sustituir:** El glifo del asterisco `*`.
    * **Contexto posterior:** Una clase de caracteres que incluya todas las letras (y otros caracteres que desees).
    * **Sustitución:** Reemplaza el asterisco por el glifo de la flecha `→`.

Es un proceso avanzado que requiere entender la lógica de las **características OpenType** y cómo se implementan en FontForge. El resultado es una tipografía que visualmente **mejora la legibilidad del código** sin cambiar el texto real, lo cual es la principal ventaja de esta técnica. 
