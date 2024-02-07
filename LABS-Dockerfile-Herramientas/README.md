# Laboratorio Dockerfile Tools
En este Lab se genra un Dockerfile un poco más complejo en el cual basandonos en una imagen de Debian vamos a instalar herramientas e linux para hacer tests, esto al ejecutarse el contenedor lo muestra en pantalaa y se elimina.
## Pasos

### Paso 1: Crear el Dockerfile
Crea un nuevo archivo llamado Dockerfile_tools en una nueva carpeta.
Dockerfile_tools:

```Dockerfile
# Usa una imagen base Debian
FROM debian:bullseye

# Actualiza e instala las herramientas
RUN apt-get update && apt-get install -y \
    iputils-ping \
    tcpdump \
    dnsutils \
    curl

# Configura tcpdump para mostrar solo algunas líneas
ENV TCPDUMP_OPTIONS -c 5

# Ejecuta comandos en la creación del contenedor
CMD echo "Resultado de ping a www.google.com:" && ping -c 3 www.google.com && \
    echo "\nResultado de tcpdump en la interfaz local (mostrando solo algunas líneas):" && tcpdump $TCPDUMP_OPTIONS && \
    echo "\nResultado de dig al dominio cnn.com:" && dig cnn.com && \
    echo "\nResultado de curl a www.google.com:" && curl -I www.google.com
```
### Paso 2: Construir la imagen Docker
Abre una terminal, navega hasta la carpeta que contiene tu Dockerfile_tools y ejecuta el siguiente comando:
```bash
docker build -t tu_usuario_docker/nombre_imagen_tools:v1 -f Dockerfile_tools .
```
### Paso 3: Ejecutar el contenedor
Ejecuta el contenedor con el siguiente comando:
```bash
docker run --rm tu_usuario_docker/nombre_imagen_tools:v1
```
Esto imprimirá en la terminal los resultados de los comandos especificados en el CMD del Dockerfile.

¡Listo! Ahora tienes un contenedor Docker que muestra los resultados de ping, tcpdump, dig y curl al ejecutarse. Puedes ajustar el Dockerfile según tus necesidades y agregar más comandos si lo deseas. Podrías pasarles variables de entorno para seleccionar por ejemplo que dominio/ip hacerle ping o curl, etc

## Nota
Se sugiere que hagas los archivos desde 0, cualuier duda pueden usar los que ya están acá como referencia.