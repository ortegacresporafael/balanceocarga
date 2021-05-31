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

## Comprobar que IP tiene cada uno de los contendores donde alojaremos la web

```bash
docker inspect 3e8 (los 3 primeros números del ID del contenedor)
``` 
## Crear el fichero load-balancing.conf en /etc/nginx/conf.d en el contendor que aloja el proxy y eliminar el default.conf

```bash
upstream backend {
        server 192.168.10.11;
        server 192.168.10.12;
    }
	
    server {
        listen      80;
        server_name loadbalancing.example.com;

        location / {
	        proxy_redirect      off;
	        proxy_set_header    X-Real-IP $remote_addr;
	        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
	        proxy_set_header    Host $http_host;
		proxy_pass http://backend;
	}
}
```
## Modificar (si queremos) los archivos html que muestran las páginas, se encuentran en el directorio: /usr/share/nginx/html/index.html

## Reiniciar el contenedor nginx(proxy) para la comprobación final
```bash
/etc/init.d/nginx restart
```

## En el navegador introducir la IP del proxy y actualizar para que cambie entre las webs refernciadas
