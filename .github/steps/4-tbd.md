<!--
  <<< Author notes: Step 4 >>>
  Start this step by acknowledging the previous step.
  Define terms and link to docs.github.com.
  TBD-step-4-notes.
-->

## Paso 04: Agreguemos un test más complicado

_Excelente trabajo, ahora vamos a agregar un test más complicado_

### :keyboard: Actividad: Paso 04

1. En el directorio `commonMain/kotlin`, crea un nuevo directorio `org.kmp.testing`.

1. En este directorio, crea el archivo `CurrentRuntime.kt` y actualízalo con la siguiente implementación:
    ```kotlin
    class CurrentRuntime(val name: String, rawVersion: String?) {
      companion object {
        val versionRegex = Regex("^[0-9]+(\\.[0-9]+)?")
      }

      val version = parseVersion(rawVersion)

      override fun toString() = "$name version $version"

      private fun parseVersion(rawVersion: String?): String {
        val result = rawVersion?.let { versionRegex.find(it) }
        return result?.value ?: "unknown"
      }
    }
    ```
1. En el directorio `commonTest/kotlin`, crea un nuevo paquete `org.kmp.testing`.
1. En este paquete, crea el archivo `CurrentRuntimeTest.kt` y actualízalo con el siguiente test agnóstico de plataforma y framework:
    ```kotlin
    import kotlin.test.Test
    import kotlin.test.assertEquals

    class CurrentRuntimeTest {
      @Test
      fun shouldDisplayDetails() {
        val runtime = CurrentRuntime("MyRuntime", "1.1")
        assertEquals("MyRuntime version 1.1", runtime.toString())
      }

      @Test
      fun shouldHandleNullVersion() {
        val runtime = CurrentRuntime("MyRuntime", null)
        assertEquals("MyRuntime version unknown", runtime.toString())
      }

      @Test
      fun shouldParseNumberFromVersionString() {
        val runtime = CurrentRuntime("MyRuntime", "1.2 Alpha Experimental")
        assertEquals("MyRuntime version 1.2", runtime.toString())
      }

      @Test
      fun shouldHandleMissingVersion() {
        val runtime = CurrentRuntime("MyRuntime", "Alpha Experimental")
        assertEquals("MyRuntime version unknown", runtime.toString())
      }
    }
    ```
1. Ejecuta el nuevo test.
1. Sube los cambios haciendo un commit de los archivos y push a la rama main.
1. Espera unos 20 segundos y luego actualiza esta página (la que estás siguiendo las instrucciones). [GitHub Actions](https://docs.github.com/en/actions) se actualizará automáticamente al siguiente paso.
