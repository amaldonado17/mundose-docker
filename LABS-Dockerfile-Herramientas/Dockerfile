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
