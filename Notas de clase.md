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

## Ejemplo de compilador
```
import org.antlr.runtime.*;

public class Test {
    public static void main(String[] args) throws Exception {
        ANTLRInputStream input = new ANTLRInputStream(System.in);
        ordenesLexer lexer = new ordenesLexer(input);
        CommonTokenStream tokens = new CommonTokenStream(lexer);
        ordenesParser parser = new ordenesParser(tokens);
        parser.indicaciones();   
    }
}
```
### Se procede a realizar la primer practica de compilar el ejemplo
<img width="1059" height="518" alt="image" src="https://github.com/user-attachments/assets/2543f09c-82d6-4fc6-9320-9494e166aebe" />

1. En el paso numero uno se crean los archivos (Parse, tokens, lexer)
2. Se revisan que se crearon los archivos
3. Se compila el archivo de compilador para crear los .class
4. Se corre el archivo Test(Sin java para revisar que se creo correctamente los archivos .class)
5. Se procede a poner ejemplos que se encuentran el codigo de ordenes y no marca error de algun tipo

<img width="971" height="187" alt="image" src="https://github.com/user-attachments/assets/7f0f45ee-064e-4887-9439-73e95c6d7924" />

Aqui genere debido a que la accion de "coje" es algo que no declare en el codigo de ordenes.g 
# Gramatica
En la gramatica hay dos tipos de simbolos
* Terminales (ε,a,b) en minuscula y no se puede sustiuir
* No terminales (A,B,S) en mayuscula y se puede sustituir

S---> A|B|S
A--->aA|ε
B--->bB|ε
Derivar significa sustituir los no terminales en funcion de las reglas gramaticales buscando que en los nodos del arbol formado haga puros simbolos terminales, mediante un arbol de derivacion que analiza parte por parte de lo que esta declarado en el codigo fuente
### Ejemplo
S---> A|B
A--->aA|ε
B--->bB|ε

aaabb 

Es correcta en funcion de la gramatica?


![Imagen de WhatsApp 2025-09-02 a las 11 30 52_610b0959](https://github.com/user-attachments/assets/df47e1dd-3851-4c8b-b8b9-89d422c9ee55)

Es correcta la gramatica basado en la derivacion

## Basado en el codigo de ordenes
```
grammar ordenes;

(no terminales)indicaciones : orden+                       ; 	    REGLAS SINTACTICAS
(no terminales)orden	     : APODO ACCION';'              ;

(no terminales)APODO:  ('amigo'   | 'vida' | 'cuchurrumin' |        REGLAS LEXICAS
       'canijo' | 'perro'| 'fidel') ;

(no terminales)ACCION: ('barre' |'limpia' |'lava' |'resuelve' |'plancha' |'cocina' |'seca' |'trapea');

WS:(''|'\n'|'\r'|'\t')+ { $channel=HIDDEN; } ;
```
### Programa de Prueba
fidel barre;

amigo limpia;

amigo barre;

![Imagen de WhatsApp 2025-09-02 a las 11 41 33_570780e8](https://github.com/user-attachments/assets/75edcce1-6b79-4c10-a471-03a9b8ffc04c)

Basado en el arbol de derivacion las expresiones si corresponden a la gramatica del codigo, lo circulado son simbolos terminalese que es en lo que debe terminar


