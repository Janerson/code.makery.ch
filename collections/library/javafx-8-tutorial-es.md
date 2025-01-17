---
layout: article
title: "JavaFX 8 Tutorial"
date: 2014-09-17 00:00
updated: 2014-09-17 00:00
slug: javafx-8-tutorial/es
canonical: /java/javafx-8-tutorial-intro/
github: https://github.com/marcojakob/code.makery.ch/edit/master/collections/library/javafx-8-tutorial-es.md
description: "Este tutorial en siete partes  describe el diseño, programación y publicación de una aplicación de contactos con JavaFX."
image: /assets/library/javafx-8-tutorial/addressapp.png
published: true
prettify: true
comments: false
sidebars:
- header: "Artículos en esta serie"
  body:
  - text: "Introducción"
    link: /library/javafx-8-tutorial/es/
    paging: Intro
    active: true
  - text: "Parte 1: Scene Builder"
    link: /library/javafx-8-tutorial/es/part1/
    paging: 1
  - text: "Parte 2: Modelo y TableView"
    link: /library/javafx-8-tutorial/es/part2/
    paging: 2
  - text: "Parte 3: Interacción con el usuario"
    link: /library/javafx-8-tutorial/es/part3/
    paging: 3
  - text: "Parte 4: Hojas de estilo CSS"
    link: /library/javafx-8-tutorial/es/part4/
    paging: 4
  - text: "Parte 5: Persistencia de datos con XML"
    link: /library/javafx-8-tutorial/es/part5/
    paging: 5
  - text: "Parte 6: Gráficos estadísticos"
    link: /library/javafx-8-tutorial/es/part6/
    paging: 6
  - text: "Parte 7: Publicación con e(fx)clipse"
    link: /library/javafx-8-tutorial/es/part7/
    paging: 7
- header: Lenguajes
  body:
  - text: English
    link: /java/javafx-8-tutorial-intro/
    icon-css: fa fa-fw fa-globe
  - text: Português
    link: /library/javafx-8-tutorial/pt/
    icon-css: fa fa-fw fa-globe
  - text: Español
    link: /library/javafx-8-tutorial/es/
    icon-css: fa fa-fw fa-globe
    active: true
---

<div class="alert alert-warning">
  <i class="fa fa-language"></i> This page is beeing translated to Spanish. If you'd like to help out please read <a href="/library/how-to-contribute/" class="alert-link">how to contribute</a>.
</div>

JavaFX proporciona a los desarrolladores de Java una nueva plataforma gráfica.  JavaFX 2.0 se publicó en octubre del 2011 con la intención de reemplazar a Swing en la creación de nuevos interfaces gráficos de usario (IGU). Cuando empecé a enseñar JavaFX en 2011 era una tecnología muy incipiente todavía. No había libros sobre JavaFX que fueran **adecuados para estudiantes de programación noveles**, así es que empecé a escribir una serie de tutoriales muy detallados sobre JavaFX.

![JavaFX Logo](/assets/java/javafx-2-tutorial-intro/javafx-logo.png)

El tutorial te guía a lo largo del diseño, programación y publicación de una aplicación de contactos (libreta de direcciones) mediante JavaFX. Este es el aspecto que tendrá la aplicación final:

![Screenshot AddressApp Part 1](/assets/java/javafx-2-tutorial-intro/addressapp01.png)


## Lo que aprenderás

* Creando un nuevo projecto JavaFX
* Usando Scene Builder para diseñar la interfaz de usuario
* Estructurando una aplicación con el patrón Modelo Vista Controlador (MVC)
* Uso de `ObservableLists` para la actualización automática de la interfaz de usuario
* Uso de `TableView` y respuesta a cambios de selección en la table
* Creación de un diálogo personalizado para editar personas
* Validando la entrada del usuario
* Aplicando estilos mediante CSS
* Persistencia de datos mediante XML
* Guardando el último archivo abierto en las preferencias del usuario
* Crenado un gráfico JavaFX para mostrar estadísticos
* Publicación de una aplicación JavaFX nativa

Después de completar esta serie de tutoriales deberías estar preparado para construir aplicaciones sofisticadas con JavaFX.

## Como usar este tutorial

Hay dos formas de utilizarlo

* **máximo-aprendizaje*** Creando tu propio proyecto JavaFX desde cero.
* **máxima-rápidez** Importa el código fuente de una parte del tutorial en tu entorno de desarrollo (es un proyecto Eclipse, pero puedes usar otros entornos, como Netbeans, con ligeras modificaciones). Después revisa el tutorial para entender el código. Este enfoque también resulta útil si te quedas atascado en la creación de tu propio código.


¡ Espero que te diviertas y aprendas mucho ! Empieza en  [Part 1: Scene Builder](/library/javafx-8-tutorial/es/part1/).