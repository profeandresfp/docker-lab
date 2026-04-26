<h3>Paso 1</h3>

En este paso vamos a ejecutar un contenedor de una imagen de ubuntu y vamosa acceder a 
su terminal y para ejecutar los comandos necesarios para instalar curl y comprobar que
ha sido instalado correctamente.

Empezamos
Vamos a descargar la imagen primero y luego acceder a su terminal por el tamaño de ubuntu es un problema. Para ello usamos Docker pull en principio.

<img width="1262" height="336" alt="1_Captura" src="https://github.com/user-attachments/assets/002748bd-2248-4fb8-9116-260469642c36" />

Luego ejecutamos un contenedor permieiento el acceso a su terminal quedandose la linea de comandos para aceptar comandos dentro del contenedor.

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


