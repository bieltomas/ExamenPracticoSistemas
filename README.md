# ExamenPracticoSistemas

## 1.Introducción

Mi proyecto trata de una aplicación destinada a la gestión de stock y almacenes llamada GAI.

Primero instalaremos docker-compose dirigiéndonos a la consola y introduciendo el comando `sudo apt install docker-compose` 

![image](https://user-images.githubusercontent.com/91564872/172453616-d6ff7369-5903-4b01-8a52-b5730c37fca5.png)


## 2.Configuración del archivo docker-compose.yml

Primer nos dirigiremos a la consola y mediante el comando `touch docker-compose.yml` crearemos el archivo

![image](https://user-images.githubusercontent.com/91564872/172448561-caa60784-400c-4eb4-801b-fbd0a961c446.png)

A continuación, crearemos un directorio nuevo que llamaremos "DOCKER" para introducir todos los archivos necesarios:

![image](https://user-images.githubusercontent.com/91564872/172448999-e487dd26-e720-4f0b-9928-5ceb13f0dc93.png)

En esta carpeta tambien introduciremos el archivo `.war` de nuestro proyecto.

![image](https://user-images.githubusercontent.com/91564872/172453973-22343416-ccc9-41c0-bb30-935653f326d8.png)


Ahora modificaremos el archivo .yml de la siguiente manera:

![image](https://user-images.githubusercontent.com/91564872/172452469-8778260b-6478-441e-af83-7db1f98b37ac.png)

Primero declararemos las imagenes que vamos a usar como se puede ver en `image:` que en este caso son tomcat, MySQL y phpmyadmin. 

Tomcat y phpmydamin dependen de la base de datos es decir de mysql, así que será la primera que configuraremos. En `volume:` le daremos las indicaciones para que ejecute nuestra base de datos desde MySQL al iniciarse. A continuación usaremos `environment:` para declarar el usuario root, su contraseña y el nombre de la base de datos que queremos iniciar. Finalmente en `ports:` le asignaremos el puerto que va ocupar, en este caso el 3306:3306.

Pasamos a phpmyadmin. Tras declarar que depende de la base de datos y la declaración de `image:` que nos sirve para indicar que imagen descargaremos y configuraremos, le asignaremos su puerto mediante `ports:` que en este caso es el 8081:80. Finalmente usaremos `environment:` como he mencionado anteriormente para declarar la contraseña del usuario root. Es muy importante recordar esta contraseña ya que sino luego no podremos utilizar el phpmyadmin.

Finalmente con tomcat, declararemos su dependencia de la base de datos, en `volumes:` introduciremos la ruta del archivo `.war` del proyecto. Le asignaremos su puerto debidamente en `ports:` (el 8082:8080) y finalmente en `enviroment:` declararemos el usuario y contraseña del root como en los dos casos anteriores (importante recordar contraseña).

## 3.Pasos para el despliegue de la aplicación

Nos dirigiremos desde la consola al directorio donde se encuentra nuestro docker-compose que en este caso es DOCKER, y introduciremos el comando `sudo docker-compose up` que nos ayuda a construir la imagen, tras lo cual creará y lanzará los contenedores Docker.

![image](https://user-images.githubusercontent.com/91564872/172455258-1d602b8c-9268-4889-969b-765f0011891d.png)

Despues de procesar la construccion de la imagen usaremos el comando `sudo docker ps` para comprobar que todo ha funcionado perfectamente.

![image](https://user-images.githubusercontent.com/91564872/172455527-2d3ecf90-cb9c-4bd9-83c6-4055e30e837b.png)


## 4.Preparación y subida de la imagen a dockerhub.

Primero de todo iniciaremos sesión en DockerHub mediante `sudo docker login` y nuestras credenciales.

![image](https://user-images.githubusercontent.com/91564872/172456368-88805616-91af-434b-bd4c-878c2ef94d26.png)

Ahora revisaremos las imagenes que tenemos mediante `sudo docker images`.

![image](https://user-images.githubusercontent.com/91564872/172456582-f176a3fd-9859-4b97-8f2f-e4748b504336.png)

De las imágenes que tenemos vamos a seleccionar las que queremos subir al repositorio remoto (). Tambien les vamos a añadir una etiqueta mediante `docker tag`.

![image](https://user-images.githubusercontent.com/91564872/172457654-647861b1-d2ee-42cf-af21-1d5e485664e5.png)

![image](https://user-images.githubusercontent.com/91564872/172457611-902e9958-8b55-4074-987f-00854750fedb.png)

![image](https://user-images.githubusercontent.com/91564872/172457793-3f5d12b4-28d5-45bc-a54e-d7323578d455.png)

Ahora usaremos `docker push` y el nombre que les hemos aignado para subirlas.

![image](https://user-images.githubusercontent.com/91564872/172458108-2c24b416-1392-46d4-96ae-4a3dfdaef069.png)

![image](https://user-images.githubusercontent.com/91564872/172458176-0b15a439-6534-4480-8811-d422d011ce97.png)

![image](https://user-images.githubusercontent.com/91564872/172458321-edfcb85c-f9d0-4308-aa04-bd28b67a7aae.png)

Ahora todo seria dirgirse a nuestro repositorio de DockerHub y a nuestra pagina para comprobar que todo se ha funcionado perfectamente.

![image](https://user-images.githubusercontent.com/91564872/172459827-aa95e7a7-1956-4086-aaec-8fba4c169481.png)

![image](https://user-images.githubusercontent.com/91564872/172460279-528b4ec1-9664-4d50-96a9-8d745531d45b.png)


## 5.Conclusiones

La verdad que la subida ha sido muy tediosa al principio pero una vez entendido el funcionamiento de Docker y DockerHub todo ha sido mas sencillo.

## 6.Annexos

Links de las 3 capas a DockerHub: 

https://hub.docker.com/repository/docker/bieltomas/gai.phpmyadmin

https://hub.docker.com/repository/docker/bieltomas/gai.mysql

https://hub.docker.com/repository/docker/bieltomas/gai.tomcat
