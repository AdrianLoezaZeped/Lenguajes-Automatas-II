# Notas de la clase
Un compilador en la entrada revisa si tiene errores o marca un error en base a unas reglas gramaticales 

Reglas gramaticales:

* Reglas lexicas(Se escriben Mayusculas)
  * Correcta formacion de palabras(Tokens)
* Reglas Sintacticas(Se escriben Minusculas)
  * Correcta formacion de frases (Revisa el orden en la que se forman los tokens como se dice en el compilador)
    
 ## Ejemplo de uso de reglas gramaticales
```
grammar ordenes;

indicaciones : orden+                       ; 	    REGLAS SINTACTICAS
orden	     : APODO ACCION';'              ;

APODO:  ('amor'   | 'vida' | 'cuchurrumin' |        REGLAS LEXICAS
       'canijo' | 'perro'| 'fidel') ;

ACCION: ('barre' |'limpia' |'lava' |'resuelve' |'plancha' |'cocina' |'seca' |'trapea');

WS:(''|'\n'|'\r'|'\t')+ { $channel=HIDDEN; } ;
```
Si no esta correcto algo marca un error, de lo contrario no marca ningun error

