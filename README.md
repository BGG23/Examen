<sub>Belén Gamero García 07/06/2022</sub>

# Examen

## Introduccion 

- Se trata de un proyecto final relacionado con pokemon, en la web pudes iniciar sesion y crear tu propio equipo pokemon con los movimientos que quieras.

## docker-compose

Tenemos que realizar un archivo **.yml** para hacer el Docker-Compose.

<sup>Resultado:</sup> 

```
version: '3.3'
services:
  db:
    image: mysql:8.0
    volumes:
      - ./test:/var/lib/mysql
      - ./BD:/docker-entrypoint-initdb.d
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: pokedexdb
      MYSQL_USER: fran
      MYSQL_PASSWORD: 123456Fran
    ports:
      - 3307:3306
  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin/phpmyadmin
    ports:
      - '8081:80'
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: root
  web:
    depends_on:
      - db
    image: tomcat:10.0
    volumes:
      - ./PokemonFBM.war:/usr/local/tomcat/webapps/PokemonFBM.war
    ports:
      - '8080:8080'
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: pokedexdb
      MYSQL_USER: fran
      MYSQL_PASSWORD: 123456Fran
```

## Pasos para el despliegue de la aplicación.

En mi caso ya lo prepare para realizar esta parte del examen y solo debo realizar unos comandos

Lo primero a realizar es un clon del github donde ya tenemos todo lo relacionado con base de datos, java, HTML, CSS y JavaSCRIPT

![image](https://user-images.githubusercontent.com/91567318/172449724-9d043610-1e03-46f0-8ffb-1f277912a0e1.png)

Despues de esto se nos creara una carpeta que contiene todo lo anterior la cual inicaremos desde terminal

![image](https://user-images.githubusercontent.com/91567318/172449934-5d138750-423b-4aa4-92dc-00c1b035a9b8.png)

Ahora introducimos un **sudo su** para iniciar como root, actualizaremos todo con un **git pull**

![image](https://user-images.githubusercontent.com/91567318/172450374-247605a9-00db-40d6-835b-9ecd11152718.png)

tendremos que situarnos en la rama **test2** y se puede hacer de dos formas

1. desde terminal: **git checkout test2**

![image](https://user-images.githubusercontent.com/91567318/172450637-8371c1d9-12ef-4345-8dac-989f5a4dea92.png)

2. desde VisualStudio Code:

Iniciaremos el programa y clicaremos en la esquina inferior izquierda

![image](https://user-images.githubusercontent.com/91567318/172450911-2188f646-ae70-4d69-aecb-1056973848cc.png)

al clicar se nos habrira la barra de busqueda en la cual nos salen todas las ramas posibles, solo seleccionamos la indicada

![image](https://user-images.githubusercontent.com/91567318/172451314-407428c7-e9e5-4d45-a62e-a28ed4db0508.png)

## Preparación y subida de la imagen a dockerhub.
Despues de lo enterior en la misma terminal introducimos **docker-compose up -d**

![image](https://user-images.githubusercontent.com/91567318/172451904-5ec03ab2-5067-4ab3-8efa-8f372cbdf5f6.png)

cuando ya este listo iremos al navegador y buscamos **localhost:8081** esto nos iniciara el PHP en el cual tenemos que introducior el usuario (pruebas) con la contraseña (123456)

![image](https://user-images.githubusercontent.com/91567318/172452522-c15e3201-ef12-4563-8e65-013e7bccb5d1.png)

al ver que esto funciona solo tendremos que ir a la web **localhost:8080/PokemonFBM**

![image](https://user-images.githubusercontent.com/91567318/172452811-e47faaa5-c7e8-4da4-8d13-9555858a0f90.png)

para ver que todo funciona nos registraremos e iniciaremos sesion

![image](https://user-images.githubusercontent.com/91567318/172453113-263e79c7-51ce-40bc-9a7b-a16e0a02c6a9.png)

como podemos ver funciona crrectamente 

![image](https://user-images.githubusercontent.com/91567318/172453432-1f8a7587-6bc7-428a-9050-63f191487194.png)

## Conclusiones

- Se que no es el despliegue como tal pero en mi equipo tubimos muchos problemas desde el inicio y al conseguirlo al final lo acabamos haciendo de esta forma en los ordenadores donde no se realizo la practica previa al examen. En este ordenador Ubunto 20.04 no realice la practica por posibles problemas de compativilidad pero estube en todo el proceso con mis compañeros por videollamada.
