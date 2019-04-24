---
layout: post
title: Inyección de dependencias con ejemplos
---

    public  class  Start  {
    
    public  static  void  main(String[]  args)  {
    
    //Usamos una puerta con cerradura de llave
    
    ObjetoPuertaLlave puertaLlave  =  new  ObjetoPuertaLlave();
    
    puertaLlave.abrir();
    
    //Usamos una puerta con cerradura de código
    
    ObjetoPuertaCodigo puertaCodigo  =  new  ObjetoPuertaCodigo();
    
    puertaCodigo.abrir();
    
    }
    
    }

Se crea un nuevo objeto “puerta” que tenga una “cerradura” de tipo “llave” por un lado y otro que tenga una cerradura de tipo “código”.


    public  class  ObjetoPuertaLlave  {
    
    private  ObjetoCerraduraLlave cerradura;
    
    public  ObjetoPuertaLlave(){
    
    cerradura  =  new  ObjetoCerraduraLlave();
    
    }
    
    public  void  abrir(){
    
    cerradura.accionar();
    
    }
    
    }

/
  

    public class ObjetoCerraduraLlave{ public void accionar() { System.out.println("Cerradura con Llave"); } }
    
    public  class  ObjetoCerraduraLlave{
    
    public  void  accionar()  {
    
    System.out.println("Cerradura con Llave");
    
    }
    
    }

/

    public  class  ObjetoPuertaCodigo  {
    
    private  ObjetoCerraduraCodigo cerradura;
    
    public  ObjetoPuertaCodigo(){
    
    cerradura  =  new  ObjetoCerraduraCodigo();
    
    }
    
    public  void  abrir(){
    
    cerradura.accionar();
    
    }
    
    }

/

    public  class  ObjetoCerraduraCodigo{
    
    public  void  accionar()  {
    
    System.out.println("Cerradura con Código");
    
    }
    
    }

Al ejecutar debe aparecer esto:

    Cerradura con Llave
    
    Cerradura con  Código

Hagamos esto mismo utilizando la <strong> inyección de dependencias: </strong>

Para ello solo usaremos una clase puerta:


    public  class  ObjetoPuerta  {
    
    private  CerraduraInterface cerradura;
    
    public  ObjetoPuerta(CerraduraInterface cerraduraGeneric){
    
    cerradura  =  cerraduraGeneric;
    
    }
    
    public  void  usar(){
    
    cerradura.accionar();
    
    }
    
    }
    
Esta clase puerta tiene un atributo que es una interface. Esto es a groso modo la inyección de dependencias, en la que en lugar de invocar instancias nuevas de objetos desde la propia clase, se invocan desde fuera de esta. Estas instancias serán pasadas como parámetros. De esta manera, este ObjetoPuerta nos servirá para representar cualquier puerta que tenga una cerradura siempre y cuando ese objeto cerradura implemente la interface que contiene ObjetoPuerta como atributo.


    public  interface  CerraduraInterface  {
    
    void  accionar();
    
    }

/


    public  class  ObjetoCerraduraLlave  implements  CerraduraInterface{
    
    @Override
    
    public  void  accionar()  {
    
    System.out.println("Cerradura con Llave");
    
    }
    
    }

/


    public  class  ObjetoCerraduraCodigo  implements  CerraduraInterface{
    
    @Override
    
    public  void  accionar()  {
    
    System.out.println("Cerradura con Código");
    
    }
    
    }
/

    public  class  Start  {
    
    public  static  void  main(String[]  args)  {
    
    ObjetoCerraduraLlave llave  =  new  ObjetoCerraduraLlave();
    
    ObjetoPuerta puerta  =  new  ObjetoPuerta(llave);
    
    puerta.usar();
    
    ObjetoCerraduraCodigo codigo  =  new  ObjetoCerraduraCodigo();
    
    puerta  =  new  ObjetoPuerta(codigo);
    
    puerta.usar();
    
    }
    
    }

Obtendríamos la siguiente salida:

  


    Cerradura con Llave
    
    Cerradura con  Código
Como se puede ver, la salida es la misma en ambos casos. La diferencia es que si quisiéramos añadir una puerta con cerradura de tipo “_Reconocimiento_dactilar_“, en el primer caso habría que crear un nuevo tipo de puerta que tuviera como atributo un objeto de tipo _CerraduraDactilar_ y ya tendríamos tres objetos distintos cuya única diferencia es el tipo de un atributo. Vamos, que esta no es la mejor manera de optimizar un poco el código.

Fuente: [https://entreunosyceros.net/inyeccion-de-dependencias/](https://entreunosyceros.net/inyeccion-de-dependencias/)


