Es habitual ejecutar un fragmento de lógica en un intervalo establecido. Imagine que es el propietario de un blog y observa que los suscriptores no están leyendo sus entradas más recientes. Decide que es lo mejor es enviar un correo electrónico una vez por semana para recordarles que visiten su blog. Implementa esta lógica mediante una función de Azure con un desencadenador de temporizador para invocar la función todas las semanas.

Aquí, aprenderá a crear un desencadenador de temporizador y a indicar el desencadenador que se ejecute en un intervalo uniforme.

## <a name="what-is-a-timer-trigger"></a>¿Qué es un desencadenador de temporizador?

Un desencadenador de temporizador es un desencadenador que ejecuta una función en un intervalo uniforme. Para crear un desencadenador de temporizador, debe proporcionar dos fragmentos de información. El primer requisito es un *nombre de parámetro de marca de tiempo*, que es simplemente un identificador para acceder al desencadenador en el código. El segundo requisito es una *programación*, que es una *expresión CRON* que establece el intervalo del temporizador.

## <a name="what-is-a-cron-expression"></a>¿Qué es una expresión CRON?

Una *expresión CRON* es una cadena que consta de seis campos que representan un conjunto de horas.

El orden de los seis campos en Azure es: {second} {minute} {hour} {day} {month} {day of the week}.

Por ejemplo, una *expresión CRON* para crear un desencadenador que se ejecuta cada cinco minutos es como esta:

```
0 */5 * * * *
```

A primera vista, esta cadena puede parecer confusa. Volveremos y desglosaremos estos conceptos cuando echemos un vistazo más profundo a las *expresiones CRON*.

Para crear una *expresión CRON*, debe tener un conocimiento básico de algunos de los caracteres especiales.

| Carácter especial | Significado | Ejemplo |
| ------------- | ------------- | ------------- |
| *      | Selecciona todos los valores de un campo. | Un asterisco "*" en el campo de día de la semana significa *cada* día. |
| .      | Separa los elementos de una lista. | Una coma "1,3" en el capo de día de la semana significa solo los lunes (día 1) y los miércoles (día 3). |
| -      | Especifica un intervalo. | Un guion "10-12" en el campo de hora significa un intervalo que incluya las horas, 10, 11 y 12. |
| /      | Especifica un incremento. | Una barra diagonal "*/10" en el campo de minutos significa un incremento de cada 10 minutos. |

Ahora volveremos al ejemplo original de expresión CRON. Vamos a desglosar campo por campo para intentar comprenderlo mejor.

```
0 */5 * * * *
```

El **primer campo** representa los segundos. Este campo admite los valores de 0 a 59. Dado que el campo contiene un cero, selecciona el primer valor posible, que es un segundo.

El **segundo campo** representa los minutos. El valor "*5" contiene dos caracteres especiales. Primero, el asterisco (*) significa "seleccionar todos los valores dentro del campo". Como este campo representa los minutos, los valores posibles son de 0 a 59. El segundo carácter especial es la barra diagonal (/), que representa un incremento. Cuando se combinan estos caracteres, significa que de todos los valores de 0 a 59, se selecciona cada quinto valor. Una manera más fácil de decirlo es simplemente "cada cinco minutos".

Los **cuatro campos restantes** representan la hora, el día, el mes y día de la semana. Un asterisco en estos campos significa seleccionar todos los valores posibles. En este ejemplo, seleccionamos "cada hora de cada día de cada mes".

Al colocar todos los campos juntos, la expresión se lee como "en el primer segundo, de cada quinto minuto de cada hora, de cada día, de cada mes".

## <a name="how-to-create-a-timer-trigger"></a>Cómo crear un desencadenador de temporizador

Un desencadenador de temporizador se puede crear por completo en Azure Portal. En la función de Azure, seleccione **desencadenador de temporizador** en la lista de tipos de desencadenadores predefinidos. Escriba la lógica que quiere ejecutar. Proporcione un **nombre de parámetro de marca de tiempo** y una **expresión CRON**.

## <a name="summary"></a>Resumen

Un desencadenador de temporizador invoca una función de Azure según una programación uniforme. Para definir la programación de un desencadenador de temporizador, creamos una *expresión CRON*, que es una cadena que representa un conjunto de horas.

