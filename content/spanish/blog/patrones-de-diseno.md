+++
categories = ["Software y Tecnología"]
date = 2021-03-01T13:00:00Z
description = "Descripción breve de los patrones de diseño "
image = "/images/1.png"
title = "Patrones de Diseño"
type = "post"

+++
# **¿Qué son?**

Son técnicas para resolver problemas recurrentes del diseño de software. Esa es la respuesta usual cuando preguntas a un informático, pero que quiere decir con esto. Partamos por lo básico el informático, el ingeniero en sistemas, el desarrollador, el programador, etc lo que hacen es resolver problemas y por mucho de que cada trabajo sea único, y de que el problema al que te enfrentes sea especifico, alguien en alguna parte del mundo ya ha solucionado algo muy parecido a lo que tienes y ha creado una receta, un plan de acción con la descripción del problema y como resolverlo, eso es un **patrón de diseño**.

**_No reinventar la rueda ni el agua tibia_**

![](https://pbs.twimg.com/media/CPBVSG6WcAAIZKg.jpg)

El uso de **Patrones de Diseño** no es exclusivo de los que trabajamos en el área informática, el ser humano ha venido resolviendo problemas desde que apareció hace 300.000 años en África. Y nos gusta muy poco volver a hacer las cosas que ya hicimos, es por eso que siempre dejamos escribiendo las cosas para facilitarnos la vida en el futuro. Un ejemplo en arquitectura es el **ARCO** como elemento estructural de soporte, el arco nace a la par de las primeras civilizaciones en Mesopotamia, en la cultura del valle del Indo; y es un elemento de diseño que los arquitectos siguen usando hoy en día para resolver problemas como soporte y estética de las construcciones.

![](https://www.construyehogar.com/wp-content/uploads/2014/11/Fachada-de-casa-moderna-tipo-arco.jpg)

# Clasificación

Ahora que ya entendemos que son los Patrones de Diseño, importancia y beneficio de su uso podemos empezar revisando los que existen en el área de la informática, siendo más específicos en el desarrollo de software. Los patrones de diseño más utilizados se clasifican en tres categorías principales, cada patrón de diseño individual conforma un total de 23 patrones de diseño. Las tres categorías principales son:

**1. Creacionales**: Soluciona los problemas con la creación de objetos.

> 1. Factory
> 2. Abstract Factory
> 3. Singleton
> 4. Builder Patterns
> 5. Prototype

**2. Estructurales**: Describe cómo los objetos se componen para formar estructuras complejas.

> 1. Decorator
> 2. Bridge
> 3. Facade
> 4. Flyweight
> 5. Composite
> 6. Proxy
> 7. Adapter

**3. Comportamentales**: Establece soluciones relacionadas con el comportamiento de la aplicación respecto a la interacción con objetos y clases.

>  1. Strategy
>  2. Command
>  3. Interpreter
>  4. Iterator
>  5. Medaitor
>  6. Memento
>  7. Chain of responsability
>  8. Observer
>  9. State
> 10. Template
> 11. Visitor

Sabiendo cuales son los principales patrones de diseño, demos un vistazo rápido por 6 de ellos.

## Patrones Creacionales

Los patrones de diseño de creación están basados en la creación de nuevos objetos que de manera controlada nos ayuda a resolver un problema; dicho de otra manera son los que nos facilitan la creación de nuevos objetos de tal forma que su creación pueda ser desacoplada de la implementación de nuestra aplicación.

### Factory

#### Nivel de aplicación

Clases

#### Definición

Este patrón define una interfaz para crear un objeto, pero permite que las subclases decidan qué clase instanciar; básicamente tenemos una clase genérica que delega la instancia a las subclases mediante un constructor virtual.

#### Cuando utilizarlo

Cuando se necesita administrar colecciones de objetos que son diferentes pero que tienen propiedades o características muy parecidas.

Beneficios

* Cumple con el principio de responsabilidad única
* Cumple con el principio de abierto/cerrado

### Desventajas

* El código puede volverse confuso al instanciar muchos tipos de subclases

### Estructura