# Crear un componente

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

8. No incluya espacios en el nombre de la propiedad porque hará referencia al componente por este nombre cuando escriba una fórmula. Por ejemplo, **ComponentName.PropertyName**.

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

   ![Imagen 5](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab1/picture-5.png)
   
10. En el componente, inserte un control vertical en blanco Gallery y seleccione Diseño en el panel de propiedades como Título.
11.  

