# Docker 
Docker es un gestor de contenedores para implementar servicios.

# Docker compose 
Docker compose es una herramienta que nos proporciona docker para implementar 
varios contenedores de forma simultánea pudiendo especificar múltiples opciones.
El archivo .yml que levanta la infraestructura normalmente se llamará docker-compose.
Debemos estar en el mismo directorio que el compose para poder lanzarlo.

## Comandos instalación de Docker:

```bash
sudo apt-get install docker
sudo apt-get install docker-compose
``` 


## Ejecución del docker-compose (.yml que se adjunta al README)

```bash
docker-compose up -d
```

## Comprobación de la respuesta de cada web (ambas en el mismo puerto) a través de curl:

```bash
curl -H "Host: sitio1.com" localhost
curl -H "Host: sitio2.com" localhost
``` 
