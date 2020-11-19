# Java basico


![]()

Manual basico de Java


# Indice

<!--ts-->
   * [Strings y variables](#Strings)
   * [ControlFlujo](#ControlFlujo)      
   * [Clases](#Clases)
   * [Referencias](#Referencias)   
   * [configurationFile](#configurationFile)
   * [handlers](#handlers)
   * [roles](#roles)
   * [ansible Container](#ansible_container)

<!--te-->


Strings
--------

Cadenas

```Java
        String nombre="Karla";
        String apellido="Esparza";
        
        System.out.println("Concatenacion:" + nombre + apellido);
        
        System.out.println("Nueva linea: \n" + nombre + " " + apellido);
        
        System.out.println("Tabulador: \t" + nombre + " " + apellido);
        
        System.out.println("Retroceso:\b" + nombre + " " + apellido);
        
        System.out.println("Retorno de carro: \r" + nombre + " " + apellido);
        
        System.out.println("Comilla simple: \'" + nombre + " " + apellido + "\'");
        
        System.out.println("Comilla doble: \"" + nombre + " " + apellido + "\"");
```
Operadores

```Java
 System.out.println("Operadores Aritmeticos:");
        int a = 1 + 2;
        int b = a * 4;
        int c = b / 2;
        int d = c - a;
        int e = -d;
        System.out.println("a = " + a);
        System.out.println("b = " + b);
        System.out.println("c = " + c);
        System.out.println("d = " + d);
        System.out.println("e = " + e);

        System.out.println("\nOperador Módulo (residuo):");
        System.out.println("x mod 10 = " + a % 2);

        System.out.println("\nOperador Compuesto:");
        //a = a + 4
        a += 2;
        b -= 4;
        c *= a;
        System.out.println("a = " + a);
        System.out.println("b = " + b);
        System.out.println("c = " + c);

        System.out.println("\nOperador Incremento:");
        //int a = a + 1;
        //Puede reescribierse como
        a++;
        System.out.println("a = " + a);

        //Preincremento/decremento (se incrementa antes de asignar el valor)
        c = ++a;
        //Postincremento/decremento (se incrementa despues de asignar el valor)
        //La siguiente vez que se evalua b, es cuando se incrementa
        d = b++;
        System.out.println("b = " + b);
        System.out.println("c = " + c);
        System.out.println("d = " + d);

        System.out.println("\nOperador relacional:");
        //a es menor que b
        boolean res = a < b;
        System.out.println("res = " + res);

        System.out.println("\nOperador Ternario:");
        int min = (a < b) ? a : b;
        System.out.println("min = " + min);

        System.out.println("\nOperador de Asignación:");
        int i, j, k;
        //cadena de asignación
        i = j = k = 100; // valor de x, y, and z igual a 100
        System.out.println("i = " + i);
        System.out.println("j = " + j);
        System.out.println("k = " + k);
```

Variables

```Java
        //Variables boolean, declaracion
        boolean bool1;
        //inicializacion
        bool1 = true;
        //Declaracion e inicializacion
        boolean bool2 = false;
        System.out.println("Valor bool1:" + bool1);
        System.out.println("Valor bool2:" + bool2);
        System.out.println("");
    
        //Variables byte
        byte b1 = 10;
        //Literal en hexadecimal
        byte b2 = 0xa;
        System.out.println("Valor byte1:" + b1);
        System.out.println("Valor byte2:" + b2);
        System.out.println("");
        
        //Variables short
        short s1 = 2;
        System.out.println("Valor char1:" + s1);
        System.out.println("");

        char ch1 = 65, ch2 = 'A';
        System.out.println("Valor char1:" + ch1);
        System.out.println("Valor char2:" + ch2);
        System.out.println("");
        
        //Variable enteras
        int decimal = 100;
        int octal = 0144;//Valor octal inicia con 0
        int hexa = 0x64;//Valor hexadecimal onicia con 0x
        System.out.println("Valor int decimal:" + decimal);
        System.out.println("Valor int octal:" + octal);
        System.out.println("Valor int hexadecimal:" + hexa);
        System.out.println();
        
        //Variables long
        long long1 = 10, long2 = 20L;
        System.out.println("Valor long1:" + long1);
        System.out.println("Valor long2:" + long2);
        System.out.println();
        
        //Variables float
        float f1 = 15, f2 = 22.3F;
        System.out.println("Valor float1:" + f1);
        System.out.println("Valor float2:" + f2);
        System.out.println();

        //Variables double
        double d1 = 11.0, d2 = 30.15D;
        System.out.println("Valor long1:" + d1);
        System.out.println("Valor long2:" + d2);
        System.out.println();
```

```Java
        System.out.println("Primer Ejemplo Procedencia Operadores");
        int x = 5;
        int y = 10;
        int z = ++x * y--;

        System.out.println("x = " + x);
        System.out.println("y = " + y);
        System.out.println("z = " + z);

        System.out.println("Ejemplo Evaluacion");
        System.out.println(4 + 5 * 6 / 3);
        System.out.println((4 + 5) * (6 / 3));

        System.out.println("Otro Ejemplo Evaluacion");
        System.out.println(1 + 2 - 3 * 4 / 5);
        System.out.println(1 + 2 - (3 * (4 / 5)));

        System.out.println("\nOtro ejemplo");
        //Si detecta una cadena, lo demas lo convierte en cadena
        System.out.println("1 + 2 = " + 1 + 2);
        //Los parentesis rompen esta regla, ya que tiene la mayor prioridad
        System.out.println("(1 + 2) = " + (1 + 2));

        System.out.println("\nOtro ejemplo");
        //El operador + es asociativo a la izquierda
        System.out.println(1 + 2 + "abc");//Detecta una operacion primero
        System.out.println("abc" + 1 + 2);//Detecta una cadena primero
```

```Java

```


```Java

```

ControlFlujo
----------

If
else if

```Java
        //Ejemplo If
        int x = 10;

        if (x < 20) {
            System.out.print("X menos que 20\n");
        }
```


```Java
        int x = 30;
        if (x < 20) {
            System.out.print("X menos que 20\n");
        } else {
            System.out.print("X mayor que 20\n");
        }
```


```Java
        int x = 10;
        if (x == 10) {
            System.out.print("X igual a 10\n");
        } else if (x == 20) {
            System.out.print("X igual a 20\n");
        } else if (x == 30) {
            System.out.print("X igual a 30\n");
        } else {
            System.out.print("X no es igual ni a 10, ni 20 ni 30\n");
        }
```

do while


```Java
        int contador = 0;
        int limite = 10;
        do{
            System.out.println("contador = " + contador);
            contador++;
        }
        while (contador < limite);
```

For

```Java
        int limite = 10;
        for (int contador = 0; contador < limite; contador++) {
            System.out.println("contador = " + contador);
        }
```

while

```Java
       int contador = 0;
        int limite = 10;
        while (contador < limite) {
            System.out.println("contador = " + contador);
            contador++;
        }
```

```Java
        System.out.println("Por favor introduce el número de elementos a iterar:");
        int maxElementos;
        Scanner entradaEscaner = new Scanner(System.in); //Creacion de objeto Scanner para leer datos
        maxElementos = entradaEscaner.nextInt(); //Leemos el valor proporcionado por el usuario
        int contador = 0;//Inicializamos el contador
        while (contador < maxElementos) {
            System.out.println("contador = " + contador);
            contador++;
        }
```




Clases
---------

Persona


```Java
package personas;

public class Persona {

   //Atributos de una clase
    //No es necesario asignar valores
    String nombre;
    String apellidoPaterno;
    String apellidoMaterno;

    //Metodos de la clase
    //Los usaran los objetos de esta clase
    public void desplegarNombre() {
        System.out.println("Nombre : " + nombre);
        System.out.println("Apellido Paterno : " + apellidoPaterno);
        System.out.println("Apellido Materno : " + apellidoMaterno);
    }
}
```

Test
 
```Java
package personas;

public class PersonaPrueba {
    public static void main(String args[]){
        //Creacion de un objeto
        Persona p1 = new Persona();
        
        //LLamando a un metodo del objeto creado
        System.out.println("Valores por default del objeto Persona");
        p1.desplegarNombre();
        
        //Modificar valores
        p1.nombre = "Juan";
        p1.apellidoPaterno = "Esparza";
        p1.apellidoMaterno = "Lara";
        
        //Volvemos a llamar al metodo
        System.out.println("\nNuevos valores del objeto Persona");
        p1.desplegarNombre();
        
    }
}
```

Fecha

```Java

package ejemplofecha;

public class Fecha {

    private int dia;
    private int mes;
    private int anio;

    //Constructor crea los objetos  --> esto anula los setters
    public Fecha(int d, int m, int a) {
        this.dia = d;
        this.mes = m;
        this.anio = a;

    }

    public int getDia() {
        return dia;
    }

    public void setDia(int dia) {
        this.dia = dia;
    }

    public int getMes() {
        return this.mes;
    }

    public void setMes(int mes) {
        this.mes = mes;
    }

    public int getAnio() {
        return anio;
    }

    public void setAnio(int anio) {
        this.anio = anio;
    }

    @Override
    public int hashCode() {
        int hash = 3;
        hash = 97 * hash + this.dia;
        hash = 97 * hash + this.mes;
        hash = 97 * hash + this.anio;
        return hash;
    }

    @Override
    public boolean equals(Object obj) {
        if (obj == null) {
            return false;
        }
        if (getClass() != obj.getClass()) {
            return false;
        }
        final Fecha other = (Fecha) obj;
        if (this.dia != other.dia) {
            return false;
        }
        if (this.mes != other.mes) {
            return false;
        }
        if (this.anio != other.anio) {
            return false;
        }
        return true;
    } 
    
}
```

Test

```Java
package ejemplofecha;

import java.util.Scanner;

public class EjemploFecha {

    public static void main(String[] args) {

        Scanner ftext = new Scanner(System.in);

        System.out.print("Ingrese Dia, Mes, Año: ");
        int dia = ftext.nextInt();
        int mes = ftext.nextInt();
        int anio = ftext.nextInt();
        Fecha f1 = new Fecha(dia, mes, anio);

        System.out.print("Ingrese Dia, Mes, Año: ");
        dia = ftext.nextInt();
        mes = ftext.nextInt();
        anio = ftext.nextInt();
        Fecha f2 = new Fecha(dia, mes, anio);

        //System.out.println("La Fecha1 es: "+f1.toString());
        //System.out.println("La Fecha2 es: "+f2.toString());
        if (f1.equals(f2)) {
            System.out.println("Son igules");

        } else {
            System.out.println("Son diferentes");
        }

        System.out.println(f1);
        System.out.println(f2);

    }

}
```

Aritmetica


```Java
package aritmetica;

public class Aritmetica {
    
    //Atributos de la clase
    int a;
    int b;
    
    //Constructor Vacio
    //Recordar que si agregamos un constructor distinto al vacio
    //ya no se crea este constructor y nosotros debemos crearlo si lo necesitamos
    Aritmetica(){}
    
    //Constructor con 2 argumentos
    Aritmetica( int a , int b){
        //Uso del operador this
        this.a = a;
        this.b = b;
    }
    
    //Este metodo toma los atributos de la clase para hacer la suma
    int sumar(){
        return a + b;
    }
    
    //Metodo restar
    int restar(){
        return a - b;
    }
    
    //Metodo multiplicar
    int multiplicar(){
        return a * b;
    }
    
    //Metodo dividir
    int dividir(){
        return a / b;
    }
    
}
```

```Java
package aritmetica;

public class PruebaAritmetica {
    
    public static void main(String args[]){
        
        //Variables locales
        int operandoA = 6;
        int operandoB = 2;
        
        //Creamos un objeto de la clase Aritmetica enviando argumentos
        Aritmetica obj1 = new Aritmetica(operandoA,operandoB);
        
        //Imprimir operandos
        System.out.println("Operando A:" + operandoA + " y operadoB:" + operandoB);
               
        //Resultado de la suma
        System.out.println("\nResultado suma:" + obj1.sumar() );
        
        //Resultado de la resta
        System.out.println("\nResultado resta:" + obj1.restar());
         
        //Resultado de la multiplicacion
        System.out.println("\nResultado multiplicacion:" + obj1.multiplicar());
        
        //Resultado de la division
        System.out.println("\nResultado division:" + obj1.dividir());   
    }
```

Caja

```Java
package caja;

public class Caja {

    private int ancho;
    private int alto;
    private int profundo;

    public Caja() {
    }

    public Caja(int ancho, int alto, int profundo) {
        this.ancho = ancho;
        this.alto = alto;
        this.profundo = profundo;
    }

    public int calcularVolumen() {
        return ancho * alto * profundo;
    }

    public int calcularVolumen(int ancho, int alto, int profundo) {
        return ancho * alto * profundo;
    }
}
```

```Java
package caja;

public class PruebaCaja {

    public static void main(String args[]) {

        int medidaAncho = 3;
        int medidaAlto = 2;
        int medidaProf = 6;

        Caja caja1 = new Caja();
        int resultado = caja1.calcularVolumen(medidaAncho, medidaAlto, medidaProf);

        System.out.println("resultado de caja 1:" + resultado);

        Caja caja2 = new Caja(2, 4, 6);
        System.out.println("resultado de caja 2:" + caja2.calcularVolumen());
    }
}
```

Definir una clase dentro de otra clase

```Java
package palabrareturnclases;

public class PalabraReturnClases {

    public static void main(String args[]) {
        Suma s = creaObjetoSuma();
        int resultado = s.a + s.b;
        System.out.println("Resultado:" + resultado);
    }

    public static Suma creaObjetoSuma() {
        Suma s = new Suma(3, 4);
        return s;
    }
}

class Suma {
    int a;
    int b;

    Suma(int a, int b) {
        this.a = a;
        this.b = b;
    }
}
```

```Java

```

```Java

```



Referencias
-----------------

```Java
package pasoporreferencia;

public class Persona {
    String nombre;
    
    public void cambiarNombre(String nuevoNombre){
        this.nombre = nuevoNombre;
    }
    
    public String obtenerNombre(){
        return nombre;
    }
}
```


```Java
package pasoporreferencia;

public class PasoPorReferencia {

    public static void main(String[] args) {
        Persona p = new Persona();
        p.cambiarNombre("Juan");
        imprimirNombre(p);//Imprime Juan
        modificarPersona(p);
        imprimirNombre(p);//Imprime Carlos
    }

    public static void modificarPersona(Persona arg){
        arg.cambiarNombre("Carlos");
    }
    
    public static void imprimirNombre(Persona p ){
        System.out.println("Valor recibido :" + p.obtenerNombre());
    }
}
```

Paso por valor

```Java
package pasoporvalor;

public class PasoPorValor {

    public static void main(String[] args) {
        int x = 10;       
        imprimir(x);//Imprime 10
        cambiarValor(x);
        imprimir(x);//Imprime 10
    }
    
    public static void cambiarValor(int i){
        i=200;
    }
    
    public static void imprimir(int arg){
        System.out.println("Valor recibido:" + arg);
    }
    
}
```

```Java

```

```Java

```


handlers
--------

```Java

```
ansible Container
-----------------
```Java

```

roles
-----

```Java

```




