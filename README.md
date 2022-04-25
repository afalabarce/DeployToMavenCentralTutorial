# Tutorial de despliegue a MavenCentral / Deploy to MavenCentral Tutorial

En este repo voy a intentar explicar de la forma más sencilla posible la creación de un proyecto de librería para android enfocado a su despliegue en MavenCentral, a fin de que esté disponible en el buscador de paquetes de Android Studio.

JetBrains, como no, proporciona también un tutorial bastante cómodo de seguir (practicamente lo mismo que esto, pero con menos imágenes)
https://www.jetbrains.com/help/space/publish-artifacts-to-maven-central.html, aunque es para Spaces


Para ganar tiempo, y dejar el entorno preparado, lo primero que debemos hacer es registrarnos en sonatype.

1. Accederemos a la web de incidencias de Sonatype (es un Jira), y nos registraremos como usuario (si no estamos registrados ya).

https://issues.sonatype.org/secure/Dashboard.jspa

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991081-6946097e-e481-4934-9c79-8811b6838d9e.png">

2. Pulsaremos sobre Signup, y comenzaremos el proceso de registro.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991181-911b82e6-3f83-41d3-a62f-29ef55ad06ec.png">

3. Una vez acabado el proceso de registro, se nos notifica.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991205-174882cc-fec4-409a-b858-0b6f799b664a.png">

4. En el primer inicio de sesión, aparece el asistente típico de Jira, en el que configuraremos varios aspectos del sistema.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991244-72e52f09-9f97-4ba0-9fb6-dc895289cc4c.png">

5. Una vez tenemos todo configurado (Idioma y avatar), nos aparece la página principal para Jira, en la que tenemos pocas opciones para elegir.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991338-510ebdfd-5180-4055-a0e8-45d6b2e0de8d.png">

6.  Pulsaremos sobre Crear Incidencia, y seleccionaremos la opción **Community Support - Open Source Project Repository Hosting (OSSRH)** y como tipo de incidencia, **New Project**
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991514-4e862af3-7976-4ab7-bc24-bb1c0947d895.png">

7.  Completaremos **todos* los campos de la incidencia**
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991815-996c8fcf-c2ae-4f6b-8037-d2502bfc639f.png">
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164991832-033eaf60-8424-4f5a-a6ca-b351f532f12c.png">

Como podemos ver, tenemos un asunto, que será el "título" del proyecto, una breve descripción de lo que vamos a subir y a continuación los campos realmente importantes:
- **Group Id**: Es la base para los namespaces del proyecto. **MUY IMPORTANTE** si alojamos nuestro proyecto en GitHub, el package de nuestra librería **debe comenzar sí o sí por com.github**, en mi caso, establezco **com.github.afalabarce**
- **Project URL**: Es la url del proyecto, en mi caso en GitHub.
- **SCM url**: Es la url para la descarga y clonado del proyecto (normalmente la misma que la de Project URL, terminada en .git).
- **Username(s)**: Será la lista de usuarios (separados por ,) que podrán publicar artifacts en MavenCentral, normalmente, salvo que sea un proyecto colaborativo, seremos nosotros mismos.
- **Already Synced to Central**: Puesto que es la primera vez que solicitamos creación de un nuevo proyecto, indicaremos que NO.

8.  Por último, pulsaremos sobre **Crear**, a fin de que se genere la incidencia y nos creen nuestro nuevo proyecto de alojamiento de artifacts. Nos aparece la información necesaria de la incidencia. Cuando esté solucionada, esto es, nuestro proyecto creado, se nos notificará por email.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164992139-70811e7b-f375-4cbc-b067-e972808656fa.png">

**Nota Importante**: Ha cambiado el criterio para asignaciones de GroupIds para GitHub, se nos notifica, por lo que debemos modificar el GroupId de nuestra incidencia, y crear un repo en nuestra cuenta de GitHub con el código que nos propone el bot. En cuanto lo realicemos, la incidencia pasa a abierta.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164993088-4c8a4efd-412a-4c0d-83aa-1c6ad34fa3ad.png">

9. Una vez el Bot (sí, un bot, antes lo hacía un humano y tardaba un par de días) valida todo, se marca la incidencia como resuelta y ya podremos acceder a nexus.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164993587-818dc6af-005b-487b-b4d3-48b1a71ab0cc.png">

Como vemos, el bot nos indica dónde debemos acceder para gestionar nuestros artifacts.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164993695-1f98eaa8-d657-4ae7-96b7-90bde50ed8cc.png">

Además se nos proporciona la siguiente url, con información de interés:
https://central.sonatype.org/publish/publish-guide/#deployment

Hasta este punto, tenemos la primera fase de la creación de un proyecto de librería disponible para su uso a través de MavenCentral.

La segunda fase consiste en preparar nuestro recien creado proyecto para recibir los aar, POM, etc... Recordemos que MavenCentral está diseñado para Maven (que raro, ¿no?), por lo que tendremos nuestros artifacts, con todo lo que ello implica (POM, Paquetes binarios, Código, Documentación, etc, si procede).

Para comenzar con esta segunda fase, accederemos a la url que nos propone en bot, en mi caso:
https://s01.oss.sonatype.org/#welcome

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164992425-1da31638-95f4-4e5e-84bd-652379c878e0.png">

A continuación, los pasos a seguir para preparar nuestro artifact disponible en MavenCentral:

1. Hacemos Login, si nos fijamos en la imagen anterior, arriba a la derecha tenemos el enlace **Login**
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164992477-66d9bd05-a993-462d-a54e-7b5b225c0896.png">

2. Utilizaremos las **mismas credenciales** que en la sección anterior. 
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164993862-9c409df2-8931-4960-b3ea-fc55aedce598.png">

**Importante**: Si intentamos iniciar sesión antes de que se nos haya creado nuestro proyecto (la incidencia no se haya dado por finalizada), se mostrará el siguiente error:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164992552-5b9e5fba-d320-42f6-891b-9bc8d17dc61c.png">

3. Puesto que ya tenemos acceso a Nexus, por ahora lo dejaremos aparcado... y, citando a @mouredev, comenzaremos a picar...

4. Debemos crear una firma gpg, ya que será imprescindible para la firma de nuestros artifacts a la hora de subirlos a MavenCentral, para ello vamos a necesitar las utilidades gpg-tools:
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165032204-1c87f19c-7236-4348-a844-ea46f2bb8e4a.png">
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165032245-40389126-0a03-4085-9af3-67803b900fa6.png">
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165032303-ac332201-d51c-40bb-b9b7-b3f6b914ba14.png">
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165032360-015d9b48-5415-45c7-8571-1d7dd6030a0d.png">
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165032655-db37a9d4-2401-4f8e-84f7-7d4f8b78ee2b.png">

5. Una vez creadas las claves gpg, las exportaremos a la carpeta de nuestro proyecto, a fin de tenerlas a la mano...
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165035091-71a00750-1b96-4b69-aa67-50479897b603.png">
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165035314-fc286e8d-be33-4ffa-9edd-c8ffd91090d8.png">
<img width="1137" alt="image" src="https://user-images.githubusercontent.com/103461358/165035360-d5ce2e93-c726-4994-9a82-b59aa6be834f.png">

```
 % mkdir gpgKeys
 % cd gpgKeys 
 % gpg --output public.pgp --armor --export afalabarce@gmail.com
 % gpg --export-secret-keys -o private.kbx
 Los dos siguientes comandos permiten subir nuestra clave a un keyserver (de ubuntu) utilizado por sonatype para validaciones, sin esto, el proceso de publicación fallará. 1234ABCD es el código de clave pública
 
 % gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 1234ABCD <- sirve para comprobar si la clave existe.
 % gpg --keyserver hkp://keyserver.ubuntu.com --send-keys 1234ABCD <- Envía la clave.
 ```
 **Es muy importante** (en las capturas dejo la creación "estandar"), crear el fichero de claves privadas con el comando ```gpg --export-secret-keys -o private.kbx```ya que de lo contrario, Android Studio nos dará constantemente un error de que no encuentra la cabecera pgp.
 
6. Crearemos un nuevo proyecto para Android Studio, puesto que no vamos a necesitar Activities (o sí, dependerá de lo que vayamos a desarrollar) crearemos el proyecto **sin actividades**. En mi caso, para este tutorial, voy a crear un proyecto para generar un par de Composables que ya había desarrollado en mi vieja cuenta.
<img width="1012" alt="image" src="https://user-images.githubusercontent.com/103461358/164994444-1104d349-883c-40d1-b2eb-6de068e53e2c.png">
<img width="1012" alt="image" src="https://user-images.githubusercontent.com/103461358/164994520-0344bd87-e3e6-49af-a43a-68ac81b91cb0.png">

7. Una vez creado el proyecto, podemos apreciar que Android Studio nos ha creado el proyecto con un módulo de tipo app, esto no nos interesa, por lo que realizaremos las siguientes acciones:
- Agregar un módulo de tipo Librería.
- Eliminar el módulo de tipo app.
<img width="851" alt="image" src="https://user-images.githubusercontent.com/103461358/164994719-c61dcc89-94f3-45dd-bd85-905b32792f6b.png">

Al final, el proyecto se nos debe quedar así...
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/164995681-86419c70-3dd9-473c-b1b5-77c5d429bdf4.png">

Como vemos, solo nos queda el proyecto de librería, al que deberemos preparar adecuadamente su build.gradle para las particularidades del proyecto, en mi caso, deberé preparar el build.gradle para que soporte JetpackCompose. En otros casos, se agregarán los implementations necesarios para poder desarrollar la funcionalidad necesaria.

8. A continuación, necesitamos preparar tanto el build.gradle del proyecto, como el fichero local.properties (que se excluye del repo git, ya que llevará claves, etc):
     - **Fichero local.properties**. En este fichero guardaremos ciertas variables que nos van a permitir configurar los datos de claves para firma y publicación en sonatype. Muestro el contenido de mi local.properties
```
     ## This file is automatically generated by Android Studio.
     # Do not modify this file -- YOUR CHANGES WILL BE ERASED!
     #
     # This file should *NOT* be checked into Version Control Systems,
     # as it contains information specific to your local configuration.
     #
     # Location of the SDK. This is only used by Gradle.
     # For customization when using a Version Control System, please read the
     # header note.
    sdk.dir=/Users/afalabarce/Library/Android/sdk
    signing.keyId = 1234ABCD # Clave en hexadecimal de nuestra clave privada GPG, se obtiene con gpg --list-secret-keys --keyid-format SHORT
    signing.password = miPasswordGPG
    signing.secretKeyRingFile = /Users/afalabarce/Desarrollo/AndroidStudioProjects/JetpackComposeComponents/gpgKeys/private.kbx
    ossrhUsername = miUsuarioSonatype
    ossrhPassword = miPasswordSonatype
```
     - Fichero build.gradle de proyecto
     Hay que agregar un classpath, a fin de que descargue los plugins para publicación maven.
     Agregaremos al principio una sección buildScript (si no la tiene)
```
     buildscript {
        dependencies {
            classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1'
            // NOTE: Do not place your application dependencies here; they belong
            // in the individual module build.gradle files
        }
     }
```
     - Fichero build.gradle para el módulo aar. En este fichero, hay varias secciones a tener muy en cuenta.
     
        En este build.gradle tendremos un poco más de trabajo, ya que hay que añadir algunas cosas más...
        
        En la sección inicial de plugins, deberemos añadir los plugins necesarios para firmar y publicar en maven, quedando la sección como sigue
```
        plugins {
          id 'com.android.library'
          id 'org.jetbrains.kotlin.android'
          id 'maven-publish' // Support for maven publishing artifacts
          id 'signing' // Support for signing artifacts
        }
```
        
        Una vez tenemos los plugins preparados, agregaremos lo necesario para que se ejecuten las tareas de firma y publicación. Se ha intentado preparar toda esta sección de código para que no haya que escribir nada y todo proceda de parámetros:
```
// Settings for publishing at mavenCentral

ext{
    publishedGroupId = "io.github.afalabarce"
    libraryName = "jetpackcompose"
    artifact = "jetpackcompose"
    libraryDescription = "Another Project for Jetpack Compose Composable Library"
    siteUrl = "https://github.com/afalabarce/jetpackcompose"
    gitUrl = "https://github.com/afalabarce/jetpackcompose.git"
    libraryVersionId = android.defaultConfig.versionCode
    libraryVersionCode = android.defaultConfig.versionName
    developerId = "afalabarce"
    developerName = "Antonio Fdez. Alabarce"
    developerEmail = "afalabarce@gmail.com"
    licenseName = "The Apache Software License, Version 2.0"
    licenseUrl = "http://www.apache.org/licenses/LICENSE-2.0.txt"
    allLicenses = ["Apache-2.0"]
}

task androidSourcesJar(type: Jar) {
    archiveClassifier = 'sources'
    from android.sourceSets.main.java.source
}

artifacts {
    archives androidSourcesJar
}

group = publishedGroupId
version = libraryVersionCode

ext["signing.keyId"] = ''
ext["signing.password"] = ''
ext["signing.secretKeyRingFile"] = ''
ext["ossrhUsername"] = ''
ext["ossrhPassword"] = ''

File secretPropsFile = project.rootProject.file('local.properties')
if (secretPropsFile.exists()) {
    println "Found secret props file, loading props"
    Properties p = new Properties()
    p.load(new FileInputStream(secretPropsFile))
    p.each { name, value ->
        println "Prop: $name -> $value"
        ext[name] = value
    }
}

signing {
    sign publishing.publications
}

publishing {
    publications {
        release(MavenPublication) {
            // The coordinates of the library, being set from variables that
            // we'll set up in a moment
            groupId publishedGroupId
            artifactId artifact
            version libraryVersionCode

            println "groupId: $publishedGroupId"
            println "Artifact: $artifact"
            println "Version: $libraryVersionCode"

            // Two artifacts, the `aar` and the sources
            artifact("$buildDir/outputs/aar/${project.getName()}-release.aar")
            artifact androidSourcesJar

            // Self-explanatory metadata for the most part
            pom {
                name = artifact
                description = libraryDescription
                // If your project has a dedicated site, use its URL here
                url = gitUrl
                licenses {
                    license {
                        name = licenseName
                        url = licenseUrl
                    }
                }
                developers {
                    developer {
                        id = developerId
                        name = developerName
                        email = developerEmail
                    }
                }
                // Version control info, if you're using GitHub, follow the format as seen here
                scm {
                    connection = 'scm:git:github.com/afalabarce/jetpackcompose.git'
                    developerConnection = 'scm:git:ssh://github.com/afalabarce/jetpackcompose.git'
                    url = 'https://github.com/afalabarce/jetpackcompose/tree/master'
                }
                // A slightly hacky fix so that your POM will include any transitive dependencies
                // that your library builds upon
                withXml {
                    def dependenciesNode = asNode().appendNode('dependencies')

                    project.configurations.implementation.allDependencies.each {
                        def dependencyNode = dependenciesNode.appendNode('dependency')
                        dependencyNode.appendNode('groupId', it.group)
                        dependencyNode.appendNode('artifactId', it.name)
                        dependencyNode.appendNode('version', it.version)
                    }
                }
            }
        }
    }
    repositories {
        // The repository to publish to, Sonatype/MavenCentral
        maven {
            // This is an arbitrary name, you may also use "mavencentral" or
            // any other name that's descriptive for you
            name = "sonatype"
            // these urls depend on the configuration provided to the user by sonatype
            def releasesRepoUrl = "https://s01.oss.sonatype.org/service/local/staging/deploy/maven2/"
            def snapshotsRepoUrl = "https://s01.oss.sonatype.org/content/repositories/snapshots/"
            // You only need this if you want to publish snapshots, otherwise just set the URL
            // to the release repo directly
            url = version.endsWith('SNAPSHOT') ? snapshotsRepoUrl : releasesRepoUrl

            // The username and password we've fetched earlier
            credentials {
                username ossrhUsername
                password ossrhPassword
            }
        }
    }
}
```

Una vez tenemos todo configurado, ya sólo nos queda publicar en MavenCentral desde las tareas de gradle:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165049626-e9ebfa17-25ab-4f8c-8246-85feb74d35a8.png">

Por último, y una vez gradle nos da el ok a la subida, podremos comprobar en nexus que todo ha ido bien:

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165049821-e9008ce7-22f7-4d30-a5b0-df82f4883dce.png">

En este punto, ya tenemos nuestro aar subido a MavenCentral, pero aún no ha sido publicado.

Para finalizar, debemos guardar el stage del artifact, a fin de que se publique...
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165050582-c93a7125-e2e9-4182-ba0e-85572839be79.png">

Al pulsar sobre close, nos pide una descripción.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165050760-4bb227ff-6e70-4668-a550-1e4247c4a2bf.png">

Una vez finalizada la publicación, vemos que el estado pasa a Operation in progress, ya solo nos queda esperar.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165051599-93e36009-cf84-4eaa-a5d2-e50efbf41979.png">

Y para terminar, una vez todo está correcto, tan sólo debemos publicar la release.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165059120-67230194-11a2-41de-901f-c2de9ba55624.png">

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165059233-32491285-28d9-4025-a5b1-5c2376be446f.png">

El resultado final, nuestro artifact publicado en el repositorio release de mavenCentral, cuestión de tiempo que aparezca en las búsquedas de librerías de Android Studio. Si tenemos prisa, podemos configurar directamente en build.gradle nuestro recien subido artifact.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/103461358/165060477-ffc713ad-0b05-43cd-becb-dbf96a0f0717.png">

**Y tras una ardua espera de unas 3/4 horas...**
<img width="1009" alt="image" src="https://user-images.githubusercontent.com/103461358/165124042-7a70d2d9-1202-445d-99d1-e7a0a9606e68.png">

Nuestro aporte a la comunidad está disponible para todos! :)

Espero que este tutorial (con todos los posibles errores - que los tendrá seguro -) sirva a la comunidad para extender y proporcionar trabajos que son de sumo interés para todos

Gracias por leer semejante libreto!!
