# CLASE_5_DOCKER
Imagen de docker basada en nginx personalizada con index.html  como página por defecto:
1. Crear un dockerfile
Para ello se crea un nuevo directorio con el comando: 
mkdir -p nginx-image
Una vez dentro del directorio creado, se crea el dockerfile con el comando:
touch Dockerfile
Ya tenemos un dockerfile vacío. Para agregar el contenido utilizamos el editor de texto: 
sudo nano Dockerfile 
El contenido que se agrega al dockerfile es el siguiente: 
FROM nginx:alphine
COPY index.html /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

2. Crear el archivo index.html con el contenido de su preferencia para personalizar la imagen
En este caso el contenido fue el siguiente:
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>MY FIRST DEMO DOCKER CONTAINER</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/kognise/water.css@latest/dist/dark.min.css">
</head>
<body>

    <h1>HELLO, THIS IS MY NGINX WEB. MY NAME IS ROXANA REIGOSA.</h1>
    <p>This content is being served by an Nginx container.</p>

</body>
</html>
3. Crear la imagen
Se utiliza para esto el comando: 
sudo docker build -t miimagen

4.Crear un docker-compose para levantar el contenedor con esa imagen 
El docker- compose es un archivo .yml que tendrá el siguiente contenido:
version: '3.7'
services:
  web:
    image:miimagen 
    ports:
      - "8000:80"
    volumes:
      - ./app:/usr/share/nginx/html

Una vez creado el archivo utilizar el siguiente comando para ejecutarlo: 
docker-compose up -d
