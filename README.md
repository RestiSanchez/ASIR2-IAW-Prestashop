# Práctica: Instalación de PrestaShop usando contenedores Docker y Docker Compose

Siguiendo con la práctica 15, haremos exactamente lo mismo pero la diferencia es que en vez de instalar Wordpress instalaremos PrestaShop.

Nuestro archivo docker-compose.yml instalaremos:
- MySQL
- phpmyadmin
- PrestaShop

Habilitaremos los puestos 80 (Apache), 8080 (phpmyadmin) y finalmente el 3306 (mysql).

Constará de dos redes, una capa frontend y otra backend.

## Configuración de docker compose:

Para phpmyadmin y MySQL usaremos el mismo que en la práctica 15.

### PrestaShop

Descargamos la imagen del PrestaShop, añadimos puertos (para este 80:80), le añadiremos la variable de la base de datos del mysql, añadimos los volumenes, sus redes, le decimos que reinicie en caso de que fallase y finalmente que dependa de MySQL para conectarse. 

```
    prestashop:
        image: prestashop/prestashop
        ports:
            - 80:80
        environment:
            - DB_SERVER=${DB_SERVER}
        volumes:
            - prestashop_data:/var/www/html
        networks:
            - frontend-network
            - backend-network
        restart: always
        depends_on: 
            - mysql
```
