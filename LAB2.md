
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

