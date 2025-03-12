<!--
  <<< Author notes: Step 3 >>>
  Start this step by acknowledging the previous step.
  Define terms and link to docs.github.com.
  TBD-step-3-notes.
-->

## Paso 03: Agregar Pruebas

_Ahora, probemos el código común. Una parte esencial será un conjunto de fuentes para pruebas comunes, que tiene la biblioteca de la API kotlin.test como dependencia._

### :keyboard: Actividad: Paso 03

1. En el directorio compartido, abre el archivo `build.gradle.kts`. Agrega un conjunto de fuentes para probar el código común con una dependencia en la biblioteca `kotlin.test`:
    ```gradle
    sourceSets {
      //...
      commonTest.dependencies {
        implementation(libs.kotlin.test)
      }
    }
    ```
1. Una vez que se haya agregado la dependencia, se te pedirá que resincronices el proyecto. Haz clic en Sync Now para sincronizar los archivos de Gradle.
1. El conjunto de fuentes commonTest almacena todas las pruebas comunes. Ahora también necesitas crear un directorio con el mismo nombre en tu proyecto:
    1. Haz clic derecho en el directorio commonMain/src y selecciona **New | Directory**. El IDE presentará una lista de opciones.
    1. Comienza a escribir la ruta commonTest/kotlin para reducir la selección, luego elígela de la lista.
    1. En el directorio `commonTest/kotlin`, crea un nuevo paquete `common.example.search`.
    1. En este paquete, crea el archivo Grep.kt y actualízalo con la siguiente prueba unitaria:
          ```kotlin
          import kotlin.test.Test
          import kotlin.test.assertContains
          import kotlin.test.assertEquals

          class GrepTest {
            companion object {
              val sampleData = listOf(
                "123 abc",
                "abc 123",
                "123 ABC",
                "ABC 123"
              )
            }

            @Test
            fun shouldFindMatches() {
              val resultados = mutableListOf<String>()
              grep(sampleData, "[a-z]+") {
                resultados.add(it)
              }

              assertEquals(2, resultados.size)
              for (resultado in resultados) {
                assertContains(resultado, "abc")
              }
            }
          }
          ```
          Como puedes ver, las anotaciones y afirmaciones importadas no son específicas de la plataforma ni del marco. Cuando ejecutes esta prueba más tarde, un marco específico de la plataforma proporcionará el ejecutor de pruebas.
1. Ejecuta las pruebas: Puedes ejecutar la prueba ejecutando:
    - La función de prueba `shouldFindMatches()` usando el ícono Run en el margen.
    - El archivo de prueba usando su menú contextual.
    - La clase de prueba `GrepTest` usando el ícono **Run** en el margen.
1. Sube los cambios haciendo un commit de los archivos y push a la rama main.
1. Espera unos 20 segundos y luego actualiza esta página (la que estás siguiendo las instrucciones). [GitHub Actions](https://docs.github.com/en/actions) se actualizará automáticamente al siguiente paso.
