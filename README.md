<h3>Paso 1</h3>

En este paso vamos a ejecutar un contenedor de una imagen de ubuntu y vamosa acceder a 
su terminal y para ejecutar los comandos necesarios para instalar curl y comprobar que
ha sido instalado correctamente.

Empezamos
Vamos a descargar la imagen primero y luego acceder a su terminal por el tamaño de ubuntu es un problema. Para ello usamos Docker pull en principio.

<img width="1262" height="336" alt="1_Captura" src="https://github.com/user-attachments/assets/002748bd-2248-4fb8-9116-260469642c36" />

Luego ejecutamos un contenedor permitiendo el acceso a su terminal quedandose la linea de comandos para aceptar comandos dentro del contenedor.

<img width="929" height="165" alt="Captura de pantalla_2026-04-26_09-45-20" src="https://github.com/user-attachments/assets/4b0a13bf-a28f-4bcf-bfb6-95d72d7e2868" />

Instalamos  curl:

<img width="1925" height="1080" alt="Captura de pantalla_2026-04-26_09-47-01" src="https://github.com/user-attachments/assets/e3232d6a-fffc-4818-b8fc-77f954d05b09" />

<img width="1298" height="716" alt="Captura de pantalla_2026-04-26_09-45-55" src="https://github.com/user-attachments/assets/88260503-32aa-4e5a-80ea-b2b3d7b2bc8a" />

Comprobamos que funciona:
curl --version

<img width="1300" height="702" alt="Captura de pantalla_2026-04-26_09-47-57" src="https://github.com/user-attachments/assets/c33ac566-48ae-4e40-afa4-b16828420db8" />

<h4>Pregunta</h4>
¿Con qué comando podrías guardar los cambios del contenedor como una nueva imagen?

docker commit [id_contenedor] [nombre_imagen:versión]

<h3>Paso 2</h3>
Crea un Dockerfile que haga lo mismo automáticamente que el paso anterior.
Aqui tenemos el fichero Dockerfile
<img width="1180" height="516" alt="2_Captura de pantalla_2026-04-26_10-11-02" src="https://github.com/user-attachments/assets/e943df8b-6436-4c38-8f44-7bfe85b8fe10" />

Ahora ejecutamos el comando para crear la imagen con las capas incluidas en Dockerfile

<img width="1304" height="575" alt="2_Captura de pantalla_2026-04-26_10-17-19" src="https://github.com/user-attachments/assets/e48b8961-4732-4dba-bb68-c5d9d93aa968" />

Ejecutamos la imagen en un contenedor 
<img width="1133" height="146" alt="2_Captura de pantalla_2026-04-26_10-22-44" src="https://github.com/user-attachments/assets/d230c6bc-e24e-4053-88f9-883b1f5bf99e" />

Comprobamos  que curl está instalado.
<img width="1933" height="329" alt="2_Captura de pantalla_2026-04-26_10-23-46" src="https://github.com/user-attachments/assets/f3c8d4f3-82d4-4087-a3bf-4503261203f9" />

<h4>Pregunta</h4>

¿Qué comando permite ver las capas de una imagen Docker?
<br>
docker history [nombre_imagen] 

docker run -d  --name postgres-demo -e POSTGRES_PASSWORD=123 -v postgres-vol:/var/lib/postgresql/ postgres

<br>
En nuestro caso 
<br>
docker history mi-ubuntu

<h3>Paso 3</h3>
Volúmenes persistentes

Vamos a ejecutar un contenedor de postgres que use un volumen Docker montado en /var/lib/postgresql/data.

En este caso vamos a crear el volumen a la vez que ejecutamos el contenedor.
Además la ruta del volumen en el contenedor la he tenido que cambiar por un cambio reciente en la versión de postgre

docker run -d  --name postgres-demo -e POSTGRES_PASSWORD=123 -v postgres-vol:/var/lib/postgresql/ postgres

<img width="1893" height="48" alt="3_Captura de pantalla_2026-04-26_11-53-13" src="https://github.com/user-attachments/assets/c4937ac3-31a2-42fa-a6d7-94a45f0424bb" />

Ahora vamos a conectarnos a la base de datos del contenedor

<img width="1089" height="88" alt="3_Captura de pantalla_2026-04-26_11-56-12" src="https://github.com/user-attachments/assets/edf15ef6-a334-49e4-959f-8513c461e188" />

Ahora crearemos una tabla que se almacenara en el volumen

<img width="727" height="137" alt="3_Captura de pantalla_2026-04-26_12-00-25" src="https://github.com/user-attachments/assets/68d6d994-ed08-40c4-81f4-bbe440ff180d" />

Insertamos un registro:

<img width="914" height="265" alt="3_Captura de pantalla_2026-04-26_12-02-04" src="https://github.com/user-attachments/assets/f5827200-2407-4a25-925c-0911e62188c5" />

Ahora vamos a comprobar que los datos persisten más allá del contenedor para ello, eliminaremos el contenador y crearemos otro que use el mismo volumen para comprobar que la información persiste y la tabla que creamos con el otro contenedor sigue existiendo y tiene el registro que creamos.

Borramos el contenedor
<img width="1588" height="194" alt="3_1_Captura de pantalla_2026-04-26_16-57-14" src="https://github.com/user-attachments/assets/71ff5eee-3230-48e6-9628-ca45d16f8380" />

Ejecutamos un nuevo contenedor con el mismo volumen
<img width="1644" height="188" alt="3_Captura de pantalla_2026-04-26_12-13-08" src="https://github.com/user-attachments/assets/d998afd0-4e80-4039-a1b2-36f4ea123e06" />

Ahora comprobamos que siguen existiendo los datos
<img width="1487" height="346" alt="3_Captura de pantalla_2026-04-26_12-22-53" src="https://github.com/user-attachments/assets/8cf28209-56d1-4740-b036-401bc59899fe" />


<h3>4. Bind mounts</h3>h3

Ejecuta un contenedor nginx:

    mapea el puerto 80
    monta el archivo en:

/usr/share/nginx/html/index.html

docker run -d \
--name hola-docker-web \
--mount type=bind,source="$(pwd)"/web-content,target=/usr/share/nginx/html/ \
-p 8080:80 nginx

<img width="1257" height="135" alt="4_Captura de pantalla_2026-04-26_17-36-41" src="https://github.com/user-attachments/assets/634d9a22-1511-4f2d-8864-9110d494e377" />

Creamos un fichero html en el directorio bind
<img width="738" height="351" alt="4_Captura de pantalla_2026-04-26_17-37-03" src="https://github.com/user-attachments/assets/6ffa25fd-8745-4cd9-add3-73002419feea" />

Vemos que en si accedemos a localhost en el puerto 8080 se muestra el fichero html que se encuentra en el directorio de mi máquina (Host) que está mapeado con el directorio de publicación de nginx
<img width="875" height="72" alt="4_Captura de pantalla_2026-04-26_17-38-06" src="https://github.com/user-attachments/assets/106f25e6-db6c-48e4-b883-26229a457011" />

Si modificamos el documento en el host se modificará en el contenedor.

<img width="1006" height="124" alt="4_Captura de pantalla_2026-04-26_17-39-58" src="https://github.com/user-attachments/assets/e80975d9-1c12-492b-9632-a17aaaa9f252" />

<img width="825" height="189" alt="4_Captura de pantalla_2026-04-26_17-38-44" src="https://github.com/user-attachments/assets/3b529b11-9dbc-4ac4-93b6-dfc108b7e9d7" />

<h3>6. Creando redes privadas</h3>

Creamos una red con nombre my-net
docker network create my-net
<img width="1074" height="65" alt="6_Captura de pantalla_2026-04-27_21-36-02" src="https://github.com/user-attachments/assets/a855c7c3-2b2e-4cda-9c69-0163ba79bb67" />

<br>

Arranca dos contenedores ubuntu en esa red.
Lo arrancamos de forma interactiva para se queden en estado UP
<br>
docker run -d -it  --name ubuntu-1 --network my-net ubuntu<br>
docker run -d -it  --name ubuntu-2 --network my-net ubuntu

<img width="1301" height="114" alt="6_Captura de pantalla_2026-04-27_21-36-43" src="https://github.com/user-attachments/assets/417f2db4-6ca0-46e1-9832-f9af8d8a0e56" />

Instalamos la herramienta ping
Accedemos al contenedor e instalamos ping
<br>
docker exec -it ubuntu-1 bash <br>
apt-get update && apt-get install -y iputils-ping

<img width="1222" height="458" alt="6_Captura de pantalla_2026-04-27_21-38-43" src="https://github.com/user-attachments/assets/d910adf2-32ac-4852-8c01-d045a7d36f9d" />


Ejecutamos el ping al otro contenedor
Es posible usar el nombre porque Docker tiene un DNS interno
<br>
ping ubuntu-2 
<img width="1084" height="217" alt="6_Captura de pantalla_2026-04-27_21-39-18" src="https://github.com/user-attachments/assets/f75df589-bbe9-44de-86e3-858ce6076623" />


<h4>Pregunta</h4>
¿Los contenedores pueden comunicarse entre sí?
Sí, la forma depende del tipo de red.
También pueden compartir datos mediante volúmenes compartidos.

<h3>9. Docker Compose --- Compartiendo volúmenes</h3>

Crea un fichero: docker-compose.yml
Con dos servicios.<br>
writer<br>
Debe:
    montar un volumen en /app/logs<br>
    escribir un timestamp cada 30 segundos<br>

reader<br>
Debe:<br>
    montar el volumen en modo solo lectura<br>
    mostrar el contenido en consola<br>

Veamos el Contenido del fichero docker-compose.yml que necesitamos
<br>
services:<br>
  writer:<br>
    image: alpine  #distribución linux ligera<br>
    container_name: service-writer #nombre del servicio<br>
    volumes:<br>
      - log-data:/app/logs  #nombre del volumen y ruta<br>
    # Comando: ejecuta un bucle infinito que escribe la fecha en el archivo<br>
    command: ><br>
      sh -c "while true; do <br>
      date >> /app/logs/timestamp.log; <br>
      echo 'Timestamp escrito'; <br>
      sleep 30; <br>
      done"<br>

  reader:<br>
    image: alpine<br>
    container_name: service-reader<br>
    volumes:<br>
      - log-data:/app/logs:ro  # :ro significa Read-Only <br>
    depends_on:  # indica que este servicio depende de writer, es decir reader espera a que writer esté arrancado<br>
      - writer<br>
    # Comando: sigue el archivo en tiempo real<br>
    command: sh -c "tail -f /app/logs/timestamp.log"<br>

volumes:        #definiciónd del volumen utilizado<br>
  log-data:<br>
    driver: local<br>

Seleccionamos la imagen de la distribución linux alpine que es muy ligera para cada servicio.
Cada uno de los servicios referencia al volumen en /app/logs/ 
El servicio writer escribe en el volumen y el servicio reader lee del mismo volumen en el que escribe el servicio writer.
El servicio reader tiene permiso de sólo lectura sobre el volumen.
Se indica aque el servicio reader depende de que se haya cargado el servicio writer.
Se define el volumnen. 

Levantamos los servicios con el argumento -d para que se queden ejectuando en segundo plano.
docker compose up -d
<br>
Comprobamos si se escribe
Miramos el log en el que writer tiene que escribir la hora cada 30 segundos<br>

docker compose logs -f reader

<img width="1461" height="489" alt="9_Captura de pantalla_2026-04-29_16-18-18" src="https://github.com/user-attachments/assets/9c272fa3-e517-40c3-b87f-7a3e38bf3a81" />

Comprobamos que el servicio reader tiene el volumen en solo lectura

<img width="1361" height="65" alt="9_Captura de pantalla_2026-04-29_16-19-35" src="https://github.com/user-attachments/assets/b749dede-b728-4f3d-bdfb-8579b9da896f" />

Vemos que al ejecutar el comando docker exec -it service-reader touch /app/logs/prueba.txt obtenemos un mensaje de error. Read-only file system.







