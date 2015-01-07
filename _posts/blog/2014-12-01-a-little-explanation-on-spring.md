---
author: juanpintoduran
title: A little explanation on Spring
excerpt:
layout: post
categories:
  - Rails
  - Ruby
tags:
  - hacking
post_format: [ ]
---

#Spring Sucks

Desde **Rails 4.1**, el preloader [Spring](https://github.com/rails/spring) está incluída por defecto en el framework con el fin de hacer más rápido el desarrollo, ya que mantiene a la aplicación corriendo en background y no se tiene que iniciar con cada ejecución de tests, rake tasks o migraciones.

Lamentablemente hemos experimentado algunos "problemas" derivados del uso de spring, y acá documentamos algunos de ellos y como "solucionarlos" o "evadirlos":

## A little explanation

En rails 4.1 los ejecutables de `rails`, `bundler`, `rake` y `spring` que se encuentran dentro de la carpeta `bin/` de tu proyecto vienen `springficados` por defecto, lo que significa que cada vez que ejecutas uno de los comandos de esos ejecutables, la aplicación se pre-carga vía spring.

##Troubleshoot

**rake db:create**
---

Como spring hace preload de la aplicación antes de `rake`, al correr este comando se produce un error circular `database xxxxxxx not found`.

Para evitarlo tenemos 2 opciones:

	bin/rake db:create
	bundle exec rake db:create
	
La primera es (`bin/ejecutable`), de hecho, la nueva forma de hacerlo según el *manual* y es la recomendada a todos los efectos ya que es la única forma de asegurarse que *spring* ejecute los comandos en la aplicación que estamos trabajando ([Referencia](http://stackoverflow.com/a/23251853/2205353)).


## Don't use Spring:

Para decirle a tu ejecutable que no use spring, se le puede pasar `DISABLE_SPRING=1`, así:

- **rails generators**

		DISABLE_SPRING=1 bin/rails g generator

- **rails server or console**

		DISABLE_SPRING=1 bin/rails s
		DISABLE_SPRING=1 bin/rails c

- **rake**

		DISABLE_SPRING=1 bin/rake task

## Turn off Spring:

Para saber que procesos se están ejecutando:

	ps aux |grep spring

y luego:

	kill -9 pid

## Spring Removal from existing project:

Si estás igual de cansado que nosotros de spring, puedes hacer *unspring* de los ejecutables de tu proyecto corriendo:

	bin/spring binstub --remove --all

## Start New Projects without Spring:

Ahora bien, si prefieres iniciar tus proyectos sin `spring` eso es posible ejecutando:

	rails new --skip-spring	