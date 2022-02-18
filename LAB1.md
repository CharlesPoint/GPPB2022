## LAB 1 : Crear Componentes en Power Apps

# PASO 1: Crear el componente

1. Inicie sesión en [Power Apps](https://make.powerapps.com/)

2. Seleccione **Aplicaciones** y seleccione **Aplicación de lienzo desde cero**.

3. Proporcione un nombre de aplicación, seleccione cualquier diseño y luego seleccione **Crear**.

4. En la **Vista de árbol**, seleccione **Componentes** y luego seleccione **Nuevo componente** para crear un nuevo componente.

  ![Imagen 1](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-1.png)

5. Seleccione el nuevo componente en el panel izquierdo, seleccione los puntos suspensivos (...) y luego seleccione **Cambiar nombre**. Escriba o pegue el nombre como **MenuComponent**.

6. En el panel de la derecha, establezca el ancho del componente como **150** y su altura como **250** y luego seleccione **Nueva propiedad personalizada**. También puede establecer el alto y el ancho en cualquier otro valor, según corresponda.

  ![Imagen 2](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-2.png)

7. En los cuadros **Nombre para mostrar**, **Nombre de la propiedad** y **Descripción**, escriba o pegue texto como _Items_.

  ![Imagen 3](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-3.png)

   No incluya espacios en el nombre de la propiedad porque hará referencia al componente por este nombre cuando escriba una fórmula. Por ejemplo, **ComponentName.PropertyName**.

   El nombre para mostrar aparece en la pestaña **Propiedades** del panel derecho si selecciona el componente. Un nombre para mostrar descriptivo le ayuda a usted y a otros creadores a comprender el propósito de esta propiedad. La **Descripción** aparece en una información sobre herramientas si coloca el cursor sobre el nombre de esta propiedad en la pestaña **Propiedades**.
   
8. En el lista **Tipo de datos**, seleccione **Tabla** y, a continuación, seleccione **Crear**.

  ![Imagen 4](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-4.png)

   La propiedad **Items** se establece en un valor predeterminado según el tipo de datos que especificó. Puede establecerla en un valor que se adapte a sus necesidades. Si especificó un tipo de datos de **Tabla** o **Registro**, es posible que desee cambiar el valor de la propiedad **Items** para que coincida con el esquema de datos que desea introducir en el componente. En este caso, lo cambiará a una lista de cadenas.

   Puede establecer el valor de la propiedad en la barra de fórmulas si selecciona el nombre de la propiedad en la pestaña **Propiedades** del panel de la derecha.

  ![Imagen 5](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-5.png)
   
   Como muestrala imagen, también puede editar el valor de la propiedad en la pestaña **Avanzada** del panel de la derecha.

9. Establezca la propiedad **Items** del componente en esta fórmula:

   ```
   Table({Item:"SampleText"})
   ```

  ![Imagen 6](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-6.png)
   
10. En el componente, inserte un control vertical en blanco **Gallery** y seleccione **Diseño** en el panel de propiedades como **Título**.

11. Asegúrese de que la lista de propiedades muestre la propiedad **Items** (como lo hace por defecto). Y luego establezca el valor de esa propiedad en esta expresión:

   ```
   MenuComponent.Items
   ```
   
   De esta manera, la propiedad **Items** del control **Gallery** lee y depende de la propiedad de entrada **Items** del componente.
   
12. Opcional: configure la propiedad **BorderThickness** del control **Gallery** en **1** y su propiedad **TemplateSize** en **50**. También puede actualizar los valores del grosor del borde y el tamaño de la plantilla en cualquier otro valor, según corresponda.

# PASO 2: Agregar un componente a una pantalla

A continuación, agregará el componente a una pantalla y especificará una tabla de cadenas para que el componente las muestre.

1. En el panel izquierdo, seleccione la lista de pantallas y luego seleccione la pantalla predeterminada.

  ![Imagen 7](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-7.png)
  
2. En la pestaña **Insertar**, abra el menú **Componentes** y luego seleccione **MenuComponent**.

  ![Imagen 8](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-8.png)

   El nuevo componente se llama **MenuComponent_1** por defecto.

3. Establezca la propiedad **Items** de **MenuComponent_1** a esta fórmula:

   ```
   Table({Item:"Home"}, {Item:"Admin"}, {Item:"About"}, {Item:"Help"})
   ```

   Esta instancia se debería parecer a la siguiente imagen, pero puede personalizar el texto y otras propiedades de cada instancia.
  
  ![Imagen 9](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-9.png)
  
# PASO 3 : Crear y usar la propiedad de salida

Hasta ahora, hemos creado un componente y se ha añadido a una aplicación. A continuación, crearemos una propiedad de salida que refleje el elemento que el usuario selecciona en el menú.

1. Abra la lista de componentes y luego seleccione **MenuComponent**.

2. En el panel de la derecha, seleccione la pestaña **Propiedades** y luego **Nueva propiedad personalizada**.

3. En los cuadros **Nombre para mostrar**, **Nombre de la propiedad** y **Descripción**, escriba o pegue **Seleccionado**.

4. Debajo **Tipo de propiedad**, seleccione **Salida** y luego seleccione **Crear**.

 ![Imagen 10](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-10.png)
 
 5. En la pestaña **Avanzada**, establezca el valor de la propiedad **Selected** en esta expresión, ajustando el número en el nombre de la galería si es necesario:

   ```
   Gallery1.Selected.Item
   ```

  ![Imagen 11](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-11.png)
  
  6. En la pantalla predeterminada de la aplicación, agregue una etiqueta y configure su propiedad Text en esta expresión, ajustando el número en el nombre del componente si es necesario:

    ```
   MenuComponent_1.Selected
   ```
  
   **MenuComponent_1** es el nombre predeterminado de una instancia, no el nombre de la definición del componente. Puede cambiar el nombre de cualquier instancia.
  
  7. Mientras mantiene presionada la tecla Alt, seleccione cada elemento en el menú.
  
  El control **Label** refleja el elemento de menú que seleccionó más recientemente.
  
  ## Scope
  
  Hay ocasiones en las que un componente puede querer compartir un origen de datos o una variable con su host. Especialmente cuando el componente solo está diseñado para usarse en una aplicación en particular. Para estos casos, puede acceder directamente a la información a nivel de la aplicación activando el conmutador Acceder al alcance de la aplicación en el panel de propiedades del componente:
  
   ![Imagen 12](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-12.png)



  
