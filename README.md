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
<br>
En nuestro caso 
<br>
docker history mi-ubuntu


