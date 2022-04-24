# Tutorial de despliegue a MavenCentral / Deploy to MavenCentral Tutorial

En este repo voy a intentar explicar de la forma más sencilla posible la creación de un proyecto de librería para android enfocado a su despliegue en MavenCentral, a fin de que esté disponible en el buscador de paquetes de Android Studio.

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


3. 



