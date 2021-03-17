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

#### Desventajas

* El código puede volverse confuso al instanciar muchos tipos de subclases

#### Estructura

![](https://upload.wikimedia.org/wikipedia/commons/4/43/W3sDesign_Factory_Method_Design_Pattern_UML.jpg)

#### Ejemplo

##### Lenguaje escogido: Javascript

En este ejemplo seremos dueños de una tienda de vehículos de todo tipo, en nuestro inventario tenemos por ahora:

* Bicicleta -> 2 ruedas, manual
* Motocicletas -> 2 ruedas, combustión
* Autos -> 4 ruedas, combustión
* Auto eléctrico -> 4 ruedas, eléctrico

Como todos son vehículos creamos una clase Vehicle de la que hereden las demás subclases:

    //Vehicle
    class Vehicle {
     constructor (wheeler, type, motor){
       this._wheeler = wheeler;
       this._type = type;
       this._motor = motor;
     }
     get wheeler(){
       return this._wheeler;
     }
     get type(){
      return this._type; 
     }
     get motor(){
      return this._motor; 
     }
     description(){
       return `Tengo ${this.wheeler} ruedas, un motor de tipo ${this.motor} y soy un ${this.type}`;
     }
    }
    //Bike
    class Bike extends Vehicle{
      constructor() {
        super(2, 'Bicicleta', 'manual');
      }
    }
    
    //Motorcycle
    class Motorcycle extends Vehicle{
      constructor() {
        super(2, 'Motocicleta', 'combustion');
      }
    }
    
    //Car
    class Car extends Vehicle{
      constructor() {
        super(4, 'Auto', 'combustion');
      }
    }
    
    //Electric Car
    class ElectricCar extends Vehicle{
      constructor() {
        super(6, 'Auto eléctrico', 'electric');
      }
    }
    
    import { Bike, Motorcycle, Car, ElectricCar}

Ahora crearemos la clases que nos permita instanciar cada vehículo, dependiendo de los parámetros enviados.

    import { Bike, Motorcycle, Car, ElectricCar } from "./Vehicle";
    
    class VehicleFactory {
      createVehicle(wheeler, motor){
        if(wheeler === 2 && motor === 'manual') {
          return new Bike();
        }
        
        if(wheeler === 2 && motor === 'combustion') {
          return new Motorcycle();
        }
        
        if(wheeler === 4 && motor === 'combustion') {
          return new Car();
        }
        
        if(wheeler === 4 && motor === 'electric') {
          return new ElectricCar();
        }
        
        console.log('Error')
      }
    }

### Abstract Factory

#### Nivel de aplicación

Objetos

#### Definición

Este patrón crea diferentes familias de objetos, por lo que podemos considerarlo como un super-factory; dado que implementa uno o varios Factory.

#### Cuando utilizarlo

Se recomienda su uso cuando existen varias familias de objetos, nos podemos dar cuenta por que estaremos creando varios grupos del patrón Factory.

#### Beneficios

* Cumple con el principio de responsabilidad única
* Se pueden desarrollar interfaces más pequeñas o segmentadas.
* Se cumple el principio abierto/cerrado

#### Desventajas

* El mantenimiento del código puede volverse muy complicado ya que se introducen muchas nuevas interfaces y clases junto con el patrón.

#### Estructura

![](https://44r0n.github.io/images/AbstractFactoryPattern.png)

#### Ejemplo

##### Lenguaje escogido: Javascript

Volvemos a nuestra tienda de vehículos, en esta ocasión vamos a vender motos y autos y los vamos a dividir de esta manera: 

Autos

* Sedan
* Deportivo
* Camioneta
* Clásico

Motos

* Deportiva
* Motoneta
* Clásica
* Cuadrón

Como vimos hemos dividido a los vehículos en 2 familias los autos y las motos, lo que haces es seguir el patrón Factory dentro de cada familia resultando MotoFactory y CarFactory; luego creamos un Factory para crear vehículos de cada familia obteniendo VehicleAbstractFactory.

    ///Vehículos
    class Vehicle {
      constructor(type, model) {
        this._model = model;
        this._type = type;
      }
      get model(){
        return this._model;
      }
      get type(){
        return this._type;
      }
      description(){
        return `Soy un ${this.type} de clase ${this.model}`
      } 
    }
    
    export default Vehicle;

    ///Auto
    import Vehicle from "./Vehicle";
    
    class CarType1 extends Vehicle {
      constructor() {
        super("auto", "sedan");
      }
    }
    
    class CarType2 extends Vehicle {
      constructor() {
        super("auto", "deportivo");
      }
    }
    
    class CarType3 extends Vehicle {
      constructor() {
        super("auto", "camioneta");
      }
    }
    
    class CarType4 extends Vehicle {
      constructor() {
        super("auto", "clasico");
      }
    }
    
    export { CarType1, CarType2, CarType3, CarType4 };

    ///Motos
    import Vehicle from "./Vehicle";
    
    class MotoType1 extends Vehicle {
      constructor() {
        super("moto", "deportiva");
      }
    }
    
    class MotoType2 extends Vehicle {
      constructor() {
        super("moto", "motoneta");
      }
    }
    
    class MotoType3 extends Vehicle {
      constructor() {
        super("moto", "clasica");
      }
    }
    
    class MotoType4 extends Vehicle {
      constructor() {
        super("moto", "cuadron");
      }
    }
    
    export { MotoType1, MotoType2, MotoType3, MotoType4 };

    ///Factory para autos
    import { CarType1, CarType2, CarType3, CarType4 } from "./Car";
    
    class CarFactory {
      create(model) {
        switch (model) {
          case "sedan":
            return new CarType1();
          case "deportivo":
            return new CarType2();
          case "camioneta":
            return new CarType3();
          case "clasico":
            return new CarType4();
          default:
            console.log("Modelo no encontrado ", model);
            break;
        }
      }
    }
    
    export default CarFactory;

    ///Factory para motos
    import { MotoType1, MotoType2, MotoType3, MotoType4 } from "./Moto";
    
    class MotoFactory {
      create(model) {
        switch (model) {
          case "deportiva":
            return new MotoType1();
          case "motoneta":
            return new MotoType2();
          case "clasica":
            return new MotoType3();
          case "cuadron":
            return new MotoType4();
          default:
            console.log("Modelo no encontrado ", model);
            break;
        }
      }
    }
    
    export default MotorcycleFactory;

    ///Factory para todas las familias de vehículos
    import CarFactory from "./CarFactory";
    import MotoFactory from "./MotoFactory";
    
    class VehicleAbstractFactory {
      createType(type) {
        if (type === "auto") {
          return new CarFactory();
        } else if (type === "moto") {
          return new MotoFactory();
        } else {
          console.log("Error type");
        }
      }
    }
    
    export default VehicleAbstractFactory;
    

## Patrones Estructurales

Los patrones de diseño estructurales se refieren a la composición de clases y objetos, nos ayuda a simplificar la relación entre objetos, estos patrones nos ayudan a que si hay cambios, sean mínimos y no afecten a toda la aplicación; esto quiere decir que podemos agregar nueva funcionalidad o actualizar sin modificar nuestra aplicación completa.

### Decorator

#### Nivel de aplicación

Objetos

#### Definición

El patrón Decorator responde a la necesidad de añadir dinámicamente funcionalidad a un Objeto. Esto nos permite no tener que crear sucesivas clases que hereden de la primera incorporando la nueva funcionalidad, sino otras que la implementan y se asocian a la primera.

#### Cuando utilizarlo

Cuando se necesite agregar comportamientos adicionales a los objetos en tiempo de ejecución sin romper el código, y no sea posible extender el comportamiento de un objeto usando la herencia.

#### Beneficios

* Extender comportamientos sin crear nuevas subclases
* Agregar o quitar comportamientos durante la ejecucción
* Se puede usar múltiples decoradores para envolver un objeto

#### Desventajas

* Cuando la interfaz de componentes es compleja hace más difícil obtener un decorador correcto.
* El desempeño decae si existen demasiados decoradores
* Los decoradores pueden complicar el proceso de creación de instancia de objeto, ya que no solo tienen que crear una instancia del componente, si no que también envolverlo en varios decoradores

#### Estructura

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Decorator_UML_class_diagram.svg/758px-Decorator_UML_class_diagram.svg.png)

#### Ejemplo

##### Lenguaje escogido: Javascript

Nos acaban de contratar para trabajar en Subway, el menú de esta semana es Sándwich de Queso, Sándwich de Pollo y Sándwich de Jamón. Obviamente cada sándwich tiene un precio distinto. Con esto podemos crear una clase Sandwich y las subclases CheeseSubway, ChickenSubway, HamSubway y entre sus métodos estaría la descripción del precio dependiendo del tipo de sándwich.

    ///Sándwich
    class Sandwich {
      constructor() {
        this._drescription = "Sándwich desconocido";
        this._price = 0;
      }
      set price(price) {
        this._price = price;
      }
      get price() {
        return this._price;
      }
      get drescription() {
        return this._drescription;
      }
      getSandwich() {
        return `Su orden es un Sándwich de : ${this.description} el precio total es: ${this.price}`;
      }
    }
    
    export default Sandwich;
    ///Sándwich de Queso
    
    import Sandwich from "./Sandwich";
    class CheeseSubway extends Sandwich {
      constructor(){
        super();
        this.description = 'CheeseSubway';
        this.price = 3;
      }
    }
    
    export default CheeseSubway;
    ///Sándwich de pollo
    
    import ChickenSubway from "./ChickenSubway ";
    class ChickenSubway extends Sandwich {
      constructor(){
        super();
        this.description = 'ChickenSubway';
        this.price = 5;
      }
    }
    
    export default ChickenSubway;
    ///Sándwich de Jamón
    
    import Sandwich from "./Sandwich";
    class HamSubway extends HamSubway {
      constructor(){
        super();
        this.description = 'HamSubway ';
        this.price = 4;
      }
    }
    
    export default HamSubway ;

Pero espera un momento esto es un Subway, y el cliente puede modificar su sándwich, oh no! y ahora quien podrá ayudarnos. La primera idea que se te puede pasar por la cabeza es modificar la clase Sandwich y agregar métodos y atributos para poder colocarle: huevos, tomate, queso, tocino o lechuga, bien problema resulto, espera un momento esto trae otra serie de problemas como:

> * Por cada ingrediente debemos agregar otra propiedad y nuevos métodos
> * Modificar el método get price por cada ingrediente, el exceso de ingredientes no es gratis sabes no podemos regalar hojas de lechuga
> * Y si alguien quiere 3 lonchas de queso???
> * Ni hablar del principio de abierto cerrado

Antes de empezar a llorar recordemos que tenemos patrones de diseño, en este caso usaremos el Decorator. Para que una subclase cumpla como decorador, esta debe tener el mismo supertipo que el objeto al que van a decorar, esto quiere decir que extienden de la clase principal; ahora para cumplir con los principios de SOLID vamos a generar un super decorador, quien es el que va a extender de la clase principal, algo así:

    ///Super decorador de Sándwich
    
    import Sandwich  from "./Sandwich";
    
    class SandwichDecorator extends Sandwich {
      constructor(sandwich) {
        super();
        this.sandwich = sandwich;
      }
    }
    
    export default SandwichDecorator;
    ///Super decorador de Sándwich
    
    import SandwichDecorator from "./SandwichDecorator";
    
    class BaconDecorator extends SandwichDecorator {
      constructor(sandwich) {
        super(sandwich);
      }
      get description() {
        return this.sandwich.description + " con tócino";
      }
      get price() {
        return this.sandwich.price + 9;
      }
    }
    
    class HamDecorator extends SandwichDecorator {
      get description() {
        return this.sandwich.description + " con jamón";
      }
      get price() {
        return this.sandwich.price + 15;
      }
    }
    
    class MeatDecorator extends SandwichDecorator {
      constructor(sandwich) {
        super(sandwich);
      }
      get description() {
        return this.sandwich.description + " con carne";
      }
      get price() {
        return this.burger.price + 20;
      }
    }
    
    class EggDecorator extends SandwichDecorator {
      constructor(sandwich) {
        super(sandwich);
      }
      get description() {
        return this.sandwich.description + " con huevo";
      }
      get price() {
        return this.sandwich.price + 12;
      }
    }
    
    class PickleDecorator extends SandwichDecorator {
      constructor(sandwich) {
        super(sandwich);
      }
      get description() {
        return this.sandwich.description + " con pepinillos";
      }
      get price() {
        return this.sandwich.price + 5;
      }
    }
    
    class CheeseDecorator extends SandwichDecorator {
      constructor(sandwich) {
        super(sandwich);
      }
      get description() {
        return this.sandwich.description + " con queso";
      }
      get price() {
        return this.sandwich.price + 9;
      }
    }
    
    export {
      CheeseDecorator,
      BaconDecorator,
      EggDecorator,
      HamDecorator,
      MeatDecorator,
      PickleDecorator
    };

## Patrones de comportamiento

Los patrones de diseño de comportamiento mejoran la comunicación y responsabilidad entre objetos, nos ayudan a que se tenga toda la información sincronizada.

### Strategy

#### Nivel de aplicación

Objeto

#### Definición

Strategy es un patrón de diseño de comportamiento que te permite definir una familia de algoritmos, colocar cada uno de ellos en una clase separada y hacer sus objetos intercambiables.

#### Cuando utilizarlo

Cuando ser quiera utilizar distintas variantes de un algoritmo dentro de un objeto y poder cambiar de un algoritmo a otro durante el tiempo de ejecución. O cuando tengas muchas clases similares que sólo se diferencien en la forma en que ejecutan cierto comportamiento.

#### Beneficios

* Intercambiar algoritmos usados dentro de un objeto durante el tiempo de ejecución
* Aislar los detalles de implementación de un algoritmo del código que lo utiliza
* Sustituyes la herencia por composición

#### Desventajas

* Los clientes deben conocer las diferencias entre estrategias para poder seleccionar la adecuada
* Si sólo tienes un par de algoritmos que raramente cambian, no hay una razón real para complicar el programa en exceso con nuevas clases e interfaces que vengan con el patrón

#### Estructura

#### ![](http://codigolinea.com/wp-content/uploads/2015/03/strategy-uml.png)  
Ejemplo

##### Lenguaje escogido: Dart

Bienvenido al año 1987 Capcom ha lanzado un juego llamado Street Fighter les ha ido medianamente bien así que quieren sacar la secuela. En esta nueva versión el personaje puede tener cuatro movimientos: patear, golpear, esquivar y saltar. Todos los personajes tienen los movimientos de esquivar y golpear pero patear y saltar son opcionales. Tu como viajero en el tiempo que ya sabe sobre programación orientada a objetos y patrones de diseño has sido contratado para programar el comportamiento de los personajes. El primer instinto es crear la clase Fighter y que el resto de personajes hereden de Fighter.

¿Mmm, pero qué pasa si un personaje no realiza un movimiento de salto? Todavía hereda el comportamiento de salto de la superclase. Aunque puede anular el salto para no hacer nada en ese caso. Pero es posible que tenga que hacerlo para muchas clases existentes y ocuparse de eso también para las clases futuras. Esto también dificultaría el mantenimiento. Entonces no podemos usar la herencia aquí.

Por suerte eres todo un pro de los patrones de diseño vienes del siglo XXI cuando ya se han resuelto muchos de estos problemas, así que puedes aplicar el patrón de Strategy. Lo primero es identificar los comportamientos que puedan variar entre diferentes clases en el futuro y separarlos. En nuestro caso saltar y patear tendremos que sacarlos de Fighter y crear un nuevo conjunto de clases para representar cada comportamiento.

La clase Fighter ahora delegará su comportamiento de patadas y saltos en lugar de utilizar los métodos de patadas y saltos definidos en la clase Fighter o su subclases.

    ///Peleador Génerico
    abstract class Fighter {
      KickBehavior kickBehavior;
      JumpBehavior jumpBehavior;
    
      Fighter(this.kickBehavior, this.jumpBehavior);
    
      setKickStrategy(KickBehavior kickBehavior){
        this.kickBehavior = kickBehavior;
      }
      
      setJumpStrategy(JumpBehavior jumpBehavior){
        this.jumpBehavior = jumpBehavior;
      }
    
      void kick() {
        kickBehavior.kick();
      }
    
      void jump() {
        jumpBehavior.jump();
      }
    
      void display();
    
      void dodge() {
        print("Esquiva");
      }
    
      void punch() {
        print("Golpea");
      }
    }
    ///Comportamiento de patada
    
    abstract class KickBehavior {
       void kick();
    }
    
    class LightningKick implements KickBehavior {
        @override
        void kick() {
            print ("Hadouken")
        }
    }
    
    class TornadoKick implements KickBehavior {
        @override
        void kick(){
            print ("Tatsumaki Senpuu Kyaku")
        }
    }
    ///Comportamiento del salto
    
    abstract class JumpBehavior{
       void kick();
    }
    
    class OneJump implements JumpBehavior{
        @override
        void jump() {
            print ("Shoryuken")
        }
    }
    
    class DoubleJump implements JumpBehavior{
        @override
        void jump(){
            print ("Shinkuu Hadouken")
        }
    }
    ///Luchador Ryu
    
    class Ryu extends Fighter {
       Ryu (KickBehavior kickBehavior, JumpBehavior jumpBehavior) : 
          super(kickBehavior, jumpBehavior);
    
       @override
       void display(){
          print("¡Debes vencer a mi Puño del Dragón para tener una oportunidad!")
       }
    
       @override
       void dodge(){}
    }
    ///Luchador Ken
    
    class ken extends Fighter {
       Ken (KickBehavior kickBehavior, JumpBehavior jumpBehavior) : 
          super(kickBehavior, jumpBehavior);
    
       @override
       void display(){
          print("¡Atácame si te atreves, te aplastaré!")
       }
    
       @override
       void dodge(){}
    }
    ///Implementar
    
    main(){
    
       JumpBehavior oneJump = OneJump();
       JumpBehavior dobleJump = DobleJump();
       KickBehavior lightningKick = LightningKick();
       KickBehavior tornadoKick = TornadoKick();
    
       Fighter ryu = Ryu(tornadoKick, oneJump);
       ryu.display();
    
       ryu.punch();
       ryu.kick();
       ryu.jump();
    
       ryu.setJumpStrategy(DobleJump);
       ryu.setKickStrategy(lightningKick);
       
       ryu.dodge();
       ryu.kick();
       ryu.jump();
    }

Si te has quedado hasta aquí y quieres saber más tengo para ti una serie de videos que puedes revisar:

* [👨‍💻 Patrones de Diseño | Resumen en 9 Minutos (más o menos)](https://youtu.be/pG_qsHnX0Ok)
* [Patrones de Diseño - BettaTech](https://www.youtube.com/watch?v=3qTmBcxGlWk&list=PLJkcleqxxobUJlz1Cm8WYd-F_kckkDvc8)
* [Introducción a los patrones de diseño - Vida MRR](https://youtu.be/1QUhp7QIWv0)

Por ultimó te dejo el enlace a mi repositorio en Github para que puedas ver con mayor detenimiento y a todo color el uso de estos patrones.

* [Design Pattern](https://github.com/jonarosero/DesignPattern)