<div align="center">
<table>
    <theader>
        <tr>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/epis.png?raw=true" alt="EPIS" style="width:50%; height:auto"/></td>
            <th>
                <span style="font-weight:bold;">UNIVERSIDAD NACIONAL DE SAN AGUSTIN</span><br />
                <span style="font-weight:bold;">FACULTAD DE INGENIERÍA DE PRODUCCIÓN Y SERVICIOS</span><br />
                <span style="font-weight:bold;">DEPARTAMENTO ACADÉMICO DE INGENIERÍA DE SISTEMAS E INFORMÁTICA</span><br />
                <span style="font-weight:bold;">ESCUELA PROFESIONAL DE INGENIERÍA DE SISTEMAS</span>
            </th>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/abet.png?raw=true" alt="ABET" style="width:50%; height:auto"/></td>
        </tr>
    </theader>
    <tbody>
        <tr><td colspan="3"><span style="font-weight:bold;">Formato</span>: INFORME DE LABORATORIO</td></tr>
        <tr><td><span style="font-weight:bold;">Aprobación</span>:  2022/03/01</td><td><span style="font-weight:bold;">Código</span>: GUIA-PRLD-001</td><td><span style="font-weight:bold;">Página</span>: 1</td></tr>
    </tbody>
</table>
</div>
<div align="center">
<span style="font-weight:bold;">GUÍA DE LABORATORIO</span><br />
</div>

<table>
<theader>
<tr><th colspan="6">INFORMACIÓN BÁSICA</th></tr>
</theader>
<tbody>
<tr><td>ASIGNATURA:</td><td colspan="5">Estructura de Datos y Algoritmos</td></tr>
<tr><td>TÍTULO DE LA PRÁCTICA:</td><td colspan="5">Arboles B</td></tr>
<tr>
<td>NÚMERO DE PRÁCTICA:</td><td>06</td><td>AÑO LECTIVO:</td><td>2022 A</td><td>NRO. SEMESTRE:</td><td>III</td>
</tr>
<tr>
<td>FECHA INICIO::</td><td>03-Agosto-2022</td><td>FECHA FIN:</td><td>07-Agosto-2022</td><td>DURACIÓN:</td><td>02 horas</td>
</tr>
<tr><td colspan="6">RECURSOS:
    <ul>
        <li>Weiss M., Data Structures & Algorithm Analysis Using Java, 2010, Addison-Wesley.
        <li> Capítulo 4. Representación de conjuntos mediante arboles, Departamento de Informática y Sistemas Área de Lenguajes y Sistemas, Universidad de Murcia, pag.168
        <li> https://www.cs.usfca.edu/~galles/visualization/BTree.html
        <li> https://ccia.ugr.es/~jfv/ed1/tedi/cdrom/docs/arb_B.htm
    </ul>    
</td>
</<tr>
  <tr><td colspan="6">ALUMNO:
<ul>
<li>Frank's Vilca Quispe - fvilcaqui@unsa.edu.pe</li>
</ul>
</td>
</<tr>
<tr><td colspan="6">DOCENTES:
<ul>
<li>Richart Smith Escobedo Quispe - rescobedoq@unsa.edu.pe</li>
</ul>
</td>
</<tr>
</tdbody>
</table>
#
   ## SOLUCION Y RESULTADOS
#

## I. SOLUCION DE EJERCICIOS/PROBLEMAS

-   Ejercicio 1:
   -   Modificar el método de obtención de valor dado una clave (5 puntos)
   -   Nuestro código de búsqueda de un valor, es el siguiente:
   -   Este método será el que nos deriva a la búsqueda de nuestro valor, en aquí solo necesitaremos el key para que nos devuelva el valor. 
            
              public Value get(Key key) { 
        
        -   En caso que nuestro Key sea null, ósea simplemente no exista daremos el mensaje "argument to get() is null". 
        
                   if (key == null) throw new IllegalArgumentException("argument to get() is null");
        
        -   En caso si exista un valor en key llamaremos el método “search”, el cual nos       devolverá el valor de la key.
                     
                     return search(root, key, height);
                   }
	    
        -   Este es el método search el cual recorrerá todo el árbol y nos devolverá el valor.   
	            
                 private Value search(Node x, Key key, int ht) {
        
        -   Nuestro Nodo le pondremos él “.children” para así poder ingresar a los valores que tiene y ese valor le daremos a “children” para trabajar mejor.
	            
                    Entry[] children = x.children;
        
        -   ht es la altura del árbol y solo cuando sea cero podremos continuar con esta parte del código
	                
                    if (ht == 0) {
        
        -   Este “for” nos servira para poder recorrer todos los valores de children.
	                     
                         for (int j = 0; j < x.m; j++) {
        
        -   Compararemos todos children[j].key con nuestra key con ayuda del método “eq”, y cuando sean iguales devolveremos el valor de esa key con ayuda del “.value”.
	                         
                             if (eq(key, children[j].key)) 
	                              return (Value)children[j].val;
	                      }
	                 } else {
         
         -   En caso a la altura del árbol no sea cero continuaremos con esta parte.
         -   Usaremos un for para dar un recorrido a los valores de nuestro nodo. 
	      
                          for (int j = 0; j < x.m; j++) {
         
         -   Utilizaremos un if con las condiciones que, si el valor de un número mayor a j es                                                                                      igual a la cantidad de nuestros valores del nodo, y que si, el valor de nuestra key es menor a “children[j+1].key”.
	                    
                              if (j+1 == x.m || less(key, children[j+1].key))
        
        -   Una vez cumplida cualquiera de las condiciones retornaremos un llamado del método “search” pero disminuyendo el nivel, e ingresando a otro nodo que este guardado dentro de children[j], ósea caminaremos por el valor y ahora buscaremos el valor en un nivel inferior.
	                   
                                  return search(children[j].next, key, ht-1);
	                          }
	                       }
        
        -   En caso no se encuentre ningún valor retornara null.
	    
                         return null;
	                }

         -   Como el código anterior solo me devuelve el primer valor que encuentre de la key, modificaremos algunas partes para que me devuelva todos los valores que tenga la key.
         -   Utilizaremos el método “getComplete” para que al igual que nuestro código anterior nos derive al método “searchComplete” o me envié un mensaje de que no hay el valor de key.
         
 	    public String getComplete(Key key) {
	          if (key == null) throw new IllegalArgumentException("argument to get() is null");
	               return searchComplete(root, key, height);
	    }
              
         -   El primer cambio es que este método ya no devolverá value si no un String.
	    
        private String searchComplete(Node x, Key key, int ht) {
	            Entry[] children = x.children;
        
        -   Crearemos el String “resp” donde se guardarán los valores que encontremos.
	            
                String resp = "";
	             if (ht == 0) {
	                 for (int j = 0; j < x.m; j++) {
	                    if (eq(key, children[j].key)) 
         
         -   Una vez encontrado el valor ya no lo devolveremos defrente, sino que lo guardaremos en resp y que no pare el for, sino que siga buscando por si encuentra otro valor de nuestra key.
 	     
                         resp = (String)(Value)children[j].val + "  " +resp;
	              }
         
         -   Cuando termine todo el for recien devolveremos nuestros valores encontrados.
	              
                  return resp;	     
                 } else {
	                for (int j = 0; j < x.m; j++) {
	                    if (j+1 == x.m || less(key, children[j+1].key))
	             return searchComplete(children[j].next, key, ht-1);
	                }
	             }
	            return null;
	        }

-   Ejemplo con el código antes de modificarlo:
 
-   Ejemplo con el código modificado:
 


