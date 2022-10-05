# __Reflexió__

## __• Sobre el codi de les activitats__

### __- Indica com accedeixes als diferents elements de la interfície__

Para acceder a los diferentes elementos de la interfície he tenido que crear los enlaces dentro del __onCreate__ de la siguiente manera:

``` kotlin
val casillaUsuario = findViewById<TextView>(R.id.editTextTextUsername)
val casillaPwd = findViewById<TextView>(R.id.editTextTextPassword)
val botonLogin = findViewById<Button>(R.id.btLogin)
val textoIntentosRestantes = findViewById<TextView>(R.id.textViewAttempts)
```

Para poder realizar esta declaración es necesario tener previamente asignado un ID a cada elemento del layout, para comprenderlo podemos seccionar la declaración en:

- "val casillaUsuario": Nombre de variable estática
- "findViewById": Función
- "TextView": Tipo de elemento del layout, ejemplos: "Button", "TextView", "ImageView", etc.
- "R.id.editTextTextUsername": Referencia del directorio resources "R", hacia el archivo de id's almacenadas ".id", en referencia a la id declarada ".editTextTextUsername"

### __- Indica com has realitzat la navegació entre una activitat i altra__

Para poder realizar la navegación entre páginas traspasando la variable del nombre del usuario hay que seguir varios pasos.

En primer lugar, tenemos que asegurarnos de tener declarada la nueva página en el archivo de "AndroidMainfest.xml"

```xml
<activity
    android:name=".MainActivityScreen"
    android:exported="false"
/>
```

La etiqueta esta declarada justo debajo de la etiqueta "activity" de la página principal, ambas anidadas en la etiqueda de "application"

Una vez tenemos declaramos la página, desde la página donde queremos navegar tenemos que implementar la funcionalidad de "intent"

Para ello necesitaremos imporatar la siguiente libreria:
```kotlin
import android.content.Intent
```

```kotlin
intent = Intent(this, MainActivityScreen::class.java).apply{
    intent.putExtra("USUARIO_LOGIN", casillaUsuario.text.toString())
    startActivity(intent)
}
```

Nuevamente, este códgio a grandes rasgos se puede seccionar en los diferentes apartados:

- "intent = Intent(this, MainActivityScreen::class.java).apply{": Declaramos el intent indicando a que página queremos navegar, en este caso "MainActivityScreen"
- "intent.putExtra("USUARIO_LOGIN", casillaUsuario.text.toString())": Insertamos la variable que queremos transferir, la sintaxis es "nombreKey", "valorAsignado"
- "startActivity(intent)": Lanzamos la navegación

Por último, necesitamos recuperar la variable en la página de destino, para ello tendremos que declarar el siguiente código en dicha página:

```kotlin
val usuarioLogin = intent.getStringExtra("USUARIO_LOGIN")
```

Esta variable se declara dentro del onCreate. Como se puede ver, declaramos una variable recuperando la variable transferida a través de la key

## __• Sobre el fitxer Manifest, investiga el següent:__

### __- Quantes activitats apareixen configurares? Mostra-les i indica les principals diferències entre elles i què signifiquen.__

Este es el contenido de mi Mainfest:
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.ieseljust.pmdm.formulariologin">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.FormularioLogin"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <!-- Declaro la nueva página -->
        <activity
            android:name=".MainActivityScreen"
            android:exported="false"
        />
    </application>

</manifest>
```

Como se puede observar, tenemos dos actividades creadas, una es la de la página principal del login (android:name=".MainActivity"), y la otra es la de la página secundaria donde vamos a navegar (android:name=".MainActivityScreen")

Para la configuración que he necesitado realizar la única diferencia esque la página secundaria a diferencia de la principal solo puede ser lanzada por páginas de la propia APP, no esta permitida por ninguna APP/actividad externa al marcar "android:exported" a "false", en la siguiente pregunta se explica que significa dicho "android:exported"

### __- Observa l’atribut android:exported en elles i investiga en la documentació d’Android què significa i quines repercusions té el seu valor en l’aplicació.__

El atributo de "android:exported" permite(true) o deniega(false) que cualquier APP externa pueda acceder e incluso lanzar esta propia actividad

## __• Sobre les traduccions realitzades:__

### __- Examina la carpeta dels recursos de tipus String, tant en la vista d’Android com en la vista dels fitxers del projecte. Hi ha nous fitxers, carpetes o recursos? Quin nom tenen i què contenen cadascun?__

Tras realizar la configuración de manera gráfica en el proyecto, desde la vista del explorador de archivos en modo "Android" se nos generar diferentes archivos por cada uno de los idiomas que hemos declarado, la ruta donde se almacenan los estos archivos es "res > values > strings"

Estos archivos se diferencian según la región declarada, por ejemplo "es_ES" -> "Español de España", "ca_ES" -> "Catalán de España", "it_IT" -> "Italiano de Italia", etc.

Si contenplamos la estructura de estos archivos podemos observar que es casi idéntica, lo único que cambia es el valor que tiene asignado cada key, a continuación os expongo un par de ejemplos

Español:
```xml
<string name="nombreUsuario">Nombre usuario</string>
```

Valenciano:
```xml
<string name="nombreUsuario">Nom usuari</string>
```

La estructura esta simplemente creada por la key de acceso y el valor en cada correspondiente idioma