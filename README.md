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
   
     ![image](https://user-images.githubusercontent.com/87882802/183325204-8f2f51da-7ca6-463d-803b-f1df17534fa2.png)
 
-   Ejemplo con el código modificado:

     ![image](https://user-images.githubusercontent.com/87882802/183325249-23bdc198-02bd-4c2b-9290-eed4ab3b3548.png)
     
-   2. Mostrar en un diagrama de árbol gráficamente la estructura final para los datos
ingresados. (4 puntos)
-   Árbol de máximo 4
    -   Ingresaremos el primer valor el cual es: www.cs.princeton.edu 

       ![image](https://user-images.githubusercontent.com/87882802/183325434-64dca4af-aaa9-4a93-b9c4-f9e8f0f44aba.png)
    -   Ingresaremos el siguiente valor que es: www.cs.princeton.edu
    -   Como el árbol es de orden 4 lo podremos unir dentro del mismo nodo
    
       ![image](https://user-images.githubusercontent.com/87882802/183326090-cd2c4a87-c46e-4993-bb1f-362d3601e05c.png)
    -   Ingresaremos el valor: www.princeton.edu
    -   Como el árbol es de orden 4 lo podremos unir dentro del mismo nodo

      ![image](https://user-images.githubusercontent.com/87882802/183326115-c92b2bc4-c035-483c-a1e0-1fbc62aa0731.png)
    -   Ingresaremos el valor: www.yale.edu
    -   Como superaría el tamaño establecido lo dividiremos en dos nodos hijos.
      ![image](https://user-images.githubusercontent.com/87882802/183326146-53bb16f5-2071-4fcb-9bbd-94c10178b25b.png)
    -   Ingresaremos el valor: www.simpsons.com 
    -   Por orden de valores ira al segundo nodo hijo.
      ![image](https://user-images.githubusercontent.com/87882802/183326184-71131f79-7124-4c3d-8e54-2223a4cbc90b.png)
    -   Ingresaremos el valor: www.apple.com
    -   Por orden de valores ira al primer nodo hijo.
      ![image](https://user-images.githubusercontent.com/87882802/183326215-dd3453bc-2df0-4cd6-84bd-b5abb470e474.png)
    -   Ingresaremos el valor: www.amazon.com
    -   Por orden este valor también ira al primer nodo hijo.
      ![image](https://user-images.githubusercontent.com/87882802/183326251-f5d8efa0-5680-4b34-8341-274ff93830c7.png)
    -   Ingresaremos el valor: www.ebay.com
    -   Por orden este valor no puede ingresar en los nodos hijos por el espacio, se creará otro nodo.
      ![image](https://user-images.githubusercontent.com/87882802/183326297-8f07ebb6-c3c0-437a-a30e-9b9868befda5.png)
    -   Ingresaremos el valor: www.cnn.com
    -   Por orden y espacio en los nodos haremos una restructuración en la raíz subiremos los valores de la izquierda de cada nodo hijo a la raíz y separaremos los nodos.
      ![image](https://user-images.githubusercontent.com/87882802/183326334-7cea422e-d3e4-42bd-be2b-63f5fe8c3ae2.png)
    -   Ingresaremos el valor: www.google.com
    -   Lo ubicamos en el tercer nodo.
      ![image](https://user-images.githubusercontent.com/87882802/183326363-2510f52d-eee1-4658-b114-f9f4c09f7eb9.png)
    -   Ingresaremos el valor: www.nytimes.com
    -   Lo ubicamos en el tercer nodo por el orden.
      ![image](https://user-images.githubusercontent.com/87882802/183326406-a4be26d7-0fec-499c-897b-fd3633580291.png)
    -   Ingresaremos el valor: www.microsoft.com
    -   Este valor iría en el tercer nodo hijo, pero como ya no entraría por espacio, restructuraremos el árbol, ponemos el segundo nodo hijo en el nivel 1 y de ahí creamos 3 nodos hijos mas
      ![image](https://user-images.githubusercontent.com/87882802/183326444-c5dd784e-0ae2-4218-9b38-b2358e9bc36d.png)
    -   Ingresaremos el valor: www.dell.com    
    -   Este valor iría en el primer nodo del tercer nivel, por el orden
      ![image](https://user-images.githubusercontent.com/87882802/183326476-d7eba4b0-85e9-429e-af35-f38ced8b01d3.png)
    -   Ingresaremos el valor: www.slashdot.org
    -   Este valor iría en el tercer nodo hijo del tercer nivel.
      ![image](https://user-images.githubusercontent.com/87882802/183326504-97d9555f-e7c9-4990-bc0e-1dfa183ea944.png)
    -   Ingresaremos el valor: www.weather.com
    -   Este valor iría en el tercer nodo hijo, del tercer nivel, pero como no hay espacio, restructuraríamos el árbol.
      ![image](https://user-images.githubusercontent.com/87882802/183326542-c2c948c0-2755-4375-a35a-ec175fb0de56.png)
    -   Ingresaremos el valor: www.yahoo.com
    -   Este valor iría en el tercer nodo hijo, del tercer nivel, pero como no hay espacio, restructuraríamos el árbol.
      ![image](https://user-images.githubusercontent.com/87882802/183326583-11ba1975-76a2-4d1e-95ee-25f3738004b7.png)

-   3. El método toString() del árbol, retorna lo siguiente. ¿Por qué están entre paréntesis
ciertas claves? (4 puntos)

    -   Las claves que están entre paréntesis, vienen a ser el primer valor de cada nodo. Y se da cada vez que en nuestro toString(), cambiemos de nodo.

-   4. Agregar un nodo adicional (www.youtube.com, 134.24.13.78) y mostrarlo paso a paso. (3 puntos)

    -   Ingresaremos el valor: www.youtube.com
    -   Primero buscaremos su lugar en el árbol, ese valor seria en el cuarto nodo del ultimo nivel 
 
      ![image](https://user-images.githubusercontent.com/87882802/183326653-5e81c83d-d9bc-40f5-8802-0c016b7c4429.png)

    -   Como se puede observar en ese nodo se excede la cantidad de valores dentro de ese nodo, así que se haría una restructuración del árbol.
    -   Primero moveremos el www.yahoo.com
 
      ![image](https://user-images.githubusercontent.com/87882802/183326683-7f18c74c-c47a-451e-9cc7-ca3dee13ea6d.png)

    -   Cómo podemos ver el segundo nodo del primer nivel está lleno haci que volveremos a hacer una restructuración del árbol.
 
      ![image](https://user-images.githubusercontent.com/87882802/183326712-92827b76-acbc-41fb-9e40-693e45ef061c.png)

