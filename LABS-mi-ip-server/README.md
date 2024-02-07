# Laboratorio Docker - Aplicación PHP "Mi IP"

Este es un laboratorio básico de Docker que muestra cómo crear una aplicación web simple utilizando PHP y ejecutarla dentro de un contenedor Docker.
La aplicación solamente mostrará la ip del server que la ejecuta o la del contenedor en este caso, esto es util cuando balanceamos entre varios contenedores y queremos saber quien es el que responde la solicitud.

## Pasos

### Paso 1: Crear la aplicación en HTML y PHP
1. Crea una carpeta llamada `web-app`.
2. Dentro de `web-app`, crea el archivo: `index.php`

`index.php`:
```php
<?php
    $ip = $_SERVER['SERVER_ADDR'];
?>
<!DOCTYPE html>
<html>
<head>
    <title>IP Display</title>
</head>
<body>
    <h1>Server IP:</h1>
    <p><?php echo $ip; ?></p>
</body>
</html>
```


### Paso 2: Crear el Dockerfile
Crea un archivo llamado Dockerfile en la misma carpeta que tus archivos de la aplicación.
Dockerfile:

```Dockerfile

# Usa una imagen base con soporte para PHP
FROM php:7.4-apache

# Copia los archivos de la aplicación al contenedor
COPY ./web-app/ /var/www/html/
```
### Paso 3: Construir la imagen Docker
Abre una terminal y navega hasta la carpeta que contiene tu Dockerfile.
Ejecuta el siguiente comando para construir la imagen:
```bash
docker build -t nombre_imagen:v1 .
```
### Paso 4: Ejecutar el contenedor
Ejecuta el siguiente comando para ejecutar el contenedor:
```bash
docker run -d -p 8080:80 nombre_imagen:v1
```
### Paso 5: Ver la aplicación en el navegador
Abre tu navegador web y ve a http://ip-server:8080 para ver la aplicación en funcionamiento.


## Nota
Se sugiere que hagas los archivos desde 0, cualuier duda pueden usar los que ya están acá como referencia.
También pueden descargarse la imagen ya hecha de mi dockerhub: 
```bash
docker pull maldoariel/miapp-server:v1
```