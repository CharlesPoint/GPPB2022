
En este laboratorio vamos a escribir nuestro propio componente de código personalizado: un mensaje Hola mundo que será similar al mostrado en la siguiente imagen:

![Imagen 1](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-1.png)

Este componente escuchará los cambios provenientes de la aplicación host y permitirá al usuario realizar cambios que luego se envían a la aplicación host.

Siga los siguientes pasos:

# PASO 1: Crear un nuevo proyecto de componente

Para crear un nuevo proyecto de componente, siga estos pasos:

1. Cree un directorio en el que se creará el componente (por ejemplo C:\source\hello-pcf).  Para crear su propio directorio, usará un símbolo del sistema (abrir la ventana **como Administrador**. En el directorio de origen, cree un directorio que se llame **hello-pcf** y luego vaya a ese directorio con el comando _cd hello-PCF_:

2. Inicialice el proyecto de componente mediante Power Apps CLI a través del siguiente comando:

```
pac pcf init --namespace SampleNamespace --name HelloPCF --template field
```

En la siguiente imagen se muestra un ejemplo del resultado que debería ver.

![Imagen 2](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-2.png)

3. Instalar las herramientas de compilación del proyecto mediante el comando `npm install`. En caso que aparezca alguna advertencia, puede ignorarlas sin problema.

![Imagen 3](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-3.png)

4. Abrir el nuevo proyecto en un entorno de desarrollador. Puede usar Visual Studio, Visual Studio Code o cualquier otro entorno que prefiera. En este ejemplo utilizararemos Visual Studio Code, que proporciona una forma de abrir una nueva ventana desde un directorio en un símbolo del sistema a través del código de comando.

![Imagen 4](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-4.png)

# PASO 2: Actualizar el manifiesto del componente de código

En este paso vamos a actualizar el archivo de manifiesto para representar con precisión su control.

1. Cambie las propiedades _version, display-name-key_ y _description-key_ que aparecen en el nodo HelloPCF, archivo ControlManifest.Input.xml para obtener valores más significativos. En este ejemplo, cambiará las propiedades a **1.0.0**, **Hello PCF** y **Says hello**, respectivamente:

```
<control namespace="SampleNamespace" constructor="HelloPCF" version="1.0.0" display-name-key="Hello PCF" description-key="Says hello" control-type="standard">
```

2. Reemplace la propiedad de ejemplo con su propia propiedad **Name** personalizada.

```
<property name="Name" display-name-key="Name" description-key="A name" of-type="SingleLine.Text" usage="bound" required="true" />
```

3. Actualice el nodo <resources> para incluir una referencia a un archivo CSS denominado _hello-pcf.css_ que va a crear. Coloque este archivo en una carpeta de CSS. El nodo será similar al mostrado en el siguiente ejemplo:
  
```
<css path="css/hello-pcf.css" order="1" />
```
  
4. Una vez que haya realizado las actualizaciones, guarde los cambios. Su archivo de manifiesto debería ser similar al mostrado en el siguiente ejemplo:
  
```
<?xml version="1.0" encoding="utf-8" ?>
<manifest>
  <control namespace="SampleNamespace" constructor="HelloPCF" version="1.0.0" display-name-key="Hello PCF" description-key="Says hello" control-type="standard">
    <property name="Name" display-name-key="Name" description-key="A name" of-type="SingleLine.Text" usage="bound" required="true" />
    <resources>
      <code path="index.ts" order="1"/>
      <css path="css/hello-pcf.css" order="1" />
    </resources>
  </control>
</manifest>
```
  
# Agregar estilo al componente de código
  
Para agregar estilo al componente de código, siga estos pasos:

1. Cree una nueva subcarpeta CSS en la carpeta HelloPCF.

2. Cree un nuevo archivo hello-pcf.css en la subcarpeta de CSS.

3. Agregue el siguiente contenido de estilo al archivo hello-pcf.css:
  
```
.SampleNamespace\.HelloPCF {
  font-size: 1.5em;
}
```
