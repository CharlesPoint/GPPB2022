
En este laboratorio vamos a escribir nuestro propio componente de código personalizado: un mensaje Hola mundo que será similar al mostrado en la siguiente imagen:

![Imagen 1](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-1.png)

Este componente escuchará los cambios provenientes de la aplicación host y permitirá al usuario realizar cambios que luego se envían a la aplicación host.

Siga los siguientes pasos:

# PASO 1: Crear un nuevo proyecto de componente

Para crear un nuevo proyecto de componente, siga estos pasos:

1. Cree un directorio en el que se creará el componente (por ejemplo C:\source\hello-pcf).  Para crear su propio directorio, usará un símbolo del sistema (abrir la ventana **como Administrador**. En el directorio de origen, cree un directorio que se llame **hello-pcf** y luego vaya a ese directorio con el comando _cd hello-PCF_:

![Imagen 2](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-2.png)

2. Inicialice el proyecto de componente mediante Power Apps CLI a través del siguiente comando:

```
pac pcf init --namespace SampleNamespace --name HelloPCF --template field
```

En la siguiente imagen se muestra un ejemplo del resultado que debería ver.

![Imagen 2](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-3.png)

3. Instalar las herramientas de compilación del proyecto mediante el comando `npm install`. En caso que aparezca alguna advertencia, puede ignorarlas sin problema.

![Imagen 3](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-4.png)

4. Abrir el nuevo proyecto en un entorno de desarrollador. Puede usar Visual Studio, Visual Studio Code o cualquier otro entorno que prefiera. En este ejemplo utilizararemos Visual Studio Code, que proporciona una forma de abrir una nueva ventana desde un directorio en un símbolo del sistema a través del código de comando.

![Imagen 4](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-5.png)


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

4. Guarde el archivo hello-pcf.css:
  
# PASO 3: Crear el componente de código

Para poder implementar la lógica de su componente, debe ejecutar una compilación en su componente. Esto asegura que se generen los tipos de TypeScript correctos para que coincidan con las propiedades en su documento ControlManifest.xml.

Vuelva al símbolo del sistema y cree el proyecto mediante el siguiente comando.
  
 ```
 npm run build
 ```
 
![Imagen 2](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-6.png)
  
El componente se compila en el directorio carpeta out/controls/HelloPCF. Entre los artefactos de compilación se incluyen:
 
- **bundle.js:** código de origen del componente compilado.

- **ControlManifest.xml:** archivo de manifiesto del componente real que se carga en la organización de Microsoft Dataverse.
  
# PASO 4: Implementar la lógica del componente del código
  
Para implementar la lógica del componente de código, siga estos pasos:
  
1. Abra index.ts en Visual Studio Code o su editor de código preferido.

2. Encima del método _constructor_, introduzca las siguientes variables privadas:
  
 ```
  // The PCF context object
private context: ComponentFramework.Context<IInputs>;

// The wrapper div element for the component
private container: HTMLDivElement;

// The callback function to call whenever your code has made a change to a bound or output property
private notifyOutputChanged: () => void;

// Flag to track if the component is in edit mode or not
private isEditMode: boolean;

// Tracks the event handler so we can destroy it when done
private buttonClickHandler: EventListener;

// Tracking variable for the name property
private name: string | null;
```
  
3. Reemplace el método _init_ por la siguiente lógica: 
  
```
  public init(
  context: ComponentFramework.Context<IInputs>,
  notifyOutputChanged: () => void,
  state: ComponentFramework.Dictionary,
  container: HTMLDivElement
) {
  // Track all the things
  this.context = context;
  this.notifyOutputChanged = notifyOutputChanged;
  this.container = container;
  this.isEditMode = false;
  this.buttonClickHandler = this.buttonClick.bind(this);

  // Create the span element to hold the hello message
  const message = document.createElement("span");
  message.innerText = `Hello ${this.isEditMode ? "" : context.parameters.Name.raw}`;

  // Create the textbox to edit the name
  const textbox = document.createElement("input");
  textbox.type = "text";
  textbox.style.display = this.isEditMode ? "block" : "none";
  if (context.parameters.Name.raw) {
    textbox.value = context.parameters.Name.raw;
  }

  // Wrap the two above elements in a div to box out the content
  const messageContainer = document.createElement("div");
  messageContainer.appendChild(message);
  messageContainer.appendChild(textbox);

  // Create the button element to switch between edit and read modes
  const button = document.createElement("button");
  button.textContent = this.isEditMode ? "Save" : "Edit";
  button.addEventListener("click", this.buttonClickHandler);

  // Add the message container and button to the overall control container
  this.container.appendChild(messageContainer);
  this.container.appendChild(button);
}
```

```  
4. Agregue un método _buttonClick_ debajo de _init_ con la siguiente lógica:
  
 // The event handler for the button's click event
public buttonClick() {
  // Get our controls via DOM queries
  const textbox = this.container.querySelector("input")!;
  const message = this.container.querySelector("span")!;
  const button = this.container.querySelector("button")!;

  // If not in edit mode, copy the current name value to the textbox
  if (!this.isEditMode) {
    textbox.value = this.name ?? "";
  } else if (textbox.value != this.name) {
    // if in edit mode, copy the textbox value to name and call the motify callback
    this.name = textbox.value;
    this.notifyOutputChanged();
  }

  // flip the mode flag
  this.isEditMode = !this.isEditMode; 

  // Set up the new output based on changes
  message.innerText = `Hello ${this.isEditMode ? "" : this.name}`;

  textbox.style.display = this.isEditMode ? "inline" : "none";
  textbox.value = this.name ?? "";

  button.textContent = this.isEditMode ? "Save" : "Edit";
}
```  

 5. Reemplace el método _updateView_ con lo siguiente:
  
 ```
 public updateView(context: ComponentFramework.Context<IInputs>): void {
  // Checks for updates coming in from outside
  this.name = context.parameters.Name.raw;
  const message = this.container.querySelector("span")!;
  message.innerText = `Hello ${this.name}`;
}
```
 
6. Sustituya _getOuptuts_ con el siguiente método:

```
public getOutputs(): IOutputs {
  return {
    // If our name variable is null, return undefined instead
    Name: this.name ?? undefined
  };
}
```  
7. Sustituya el método destroy con la siguiente lógica:
  
```  
public destroy() {
  // Remove the event listener we created in init
  this.container.querySelector("button")!.removeEventListener("click", this.buttonClickHandler);
}
``` 
  
8. Después de haber realizado las actualizaciones, el archivo index.ts debe ser similar al mostrado en el siguiente ejemplo:

```
import {IInputs, IOutputs} from "./generated/ManifestTypes";

export class HelloPCF implements ComponentFramework.StandardControl<IInputs, IOutputs> {
  // The PCF context object
  private context: ComponentFramework.Context<IInputs>;

  // The wrapper div element for the component
  private container: HTMLDivElement;

  // The callback function to call whenever your code has made a change to a bound or output property
  private notifyOutputChanged: () => void;

  // Flag to track if the component is in edit mode or not
  private isEditMode: boolean;

  // Tracks the event handler so we can destroy it when done
  private buttonClickHandler: EventListener;

  // Tracking variable for the name property
  private name: string | null;

  /**
  * Empty constructor.
  */
  constructor()
  {

  }

  /**
  * Used to initialize the control instance. Controls can kick off remote server calls and other initialization actions here.
  * Data-set values are not initialized here, use updateView.
  * @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to property names defined in the manifest, as well as utility functions.
  * @param notifyOutputChanged A callback method to alert the framework that the control has new outputs ready to be retrieved asynchronously.
  * @param state A piece of data that persists in one session for a single user. Can be set at any point in a controls life cycle by calling 'setControlState' in the Mode interface.
  * @param container If a control is marked control-type='standard', it will receive an empty div element within which it can render its content.
  */
  public init(context: ComponentFramework.Context<IInputs>, notifyOutputChanged: () => void, state: ComponentFramework.Dictionary, container:HTMLDivElement)
  {
    // Track all the things
    this.context = context;
    this.notifyOutputChanged = notifyOutputChanged;
    this.container = container;
    this.isEditMode = false;
    this.buttonClickHandler = this.buttonClick.bind(this);

    // Create the span element to hold the hello message
    const message = document.createElement("span");
    message.innerText = `Hello ${this.isEditMode ? "" : context.parameters.Name.raw}`;

    // Create the textbox to edit the name
    const textbox = document.createElement("input");
    textbox.type = "text";
    textbox.style.display = this.isEditMode ? "block" : "none";
    if (context.parameters.Name.raw) {
      textbox.value = context.parameters.Name.raw;
    }

    // Wrap the two above elements in a div to box out the content
    const messageContainer = document.createElement("div");
    messageContainer.appendChild(message);
    messageContainer.appendChild(textbox);

    // Create the button element to switch between edit and read modes
    const button = document.createElement("button");
    button.textContent = this.isEditMode ? "Save" : "Edit";
    button.addEventListener("click", this.buttonClickHandler);

    // Add the message container and button to the overall control container
    this.container.appendChild(messageContainer);
    this.container.appendChild(button);
  }

  // The event handler for the button's click event
  public buttonClick() {
    // Get our controls via DOM queries
    const textbox = this.container.querySelector("input")!;
    const message = this.container.querySelector("span")!;
    const button = this.container.querySelector("button")!;

    // If not in edit mode, copy the current name value to the textbox
    if (!this.isEditMode) {
      textbox.value = this.name ?? "";
    } else if (textbox.value != this.name) {
      // if in edit mode, copy the textbox value to name and call the motify callback
      this.name = textbox.value;
      this.notifyOutputChanged();
    }

    // flip the mode flag
    this.isEditMode = !this.isEditMode; 

    // Set up the new output based on changes
    message.innerText = `Hello ${this.isEditMode ? "" : this.name}`;

    textbox.style.display = this.isEditMode ? "inline" : "none";
    textbox.value = this.name ?? "";

    button.textContent = this.isEditMode ? "Save" : "Edit";
  }

  /**
  * Called when any value in the property bag has changed. This includes field values, data-sets, global values such as container height and width, offline status, control metadata values such as label, visible, etc.
  * @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to names defined in the manifest, as well as utility functions
  */
  public updateView(context: ComponentFramework.Context<IInputs>): void
  {
    // Checks for updates coming in from outside
    this.name = context.parameters.Name.raw;
    const message = this.container.querySelector("span")!;
    message.innerText = `Hello ${this.name}`;
  }

  /** 
  * It is called by the framework prior to a control receiving new data. 
  * @returns an object based on nomenclature defined in manifest, expecting object[s] for property marked as “bound” or “output”
  */
  public getOutputs(): IOutputs
  {
    return {
      // If our name variable is null, return undefined instead
      Name: this.name ?? undefined
    };
  }

  /** 
  * Called when the control is to be removed from the DOM tree. Controls should use this call for cleanup.
  * i.e. cancelling any pending remote calls, removing listeners, etc.
  */
  public destroy(): void
  {
    // Remove the event listener we created in init
    this.container.querySelector("button")!.removeEventListener("click", this.buttonClickHandler);
  }
}
```
  
# PASO 5: Volver a crear y ejecutar el componente de código
  
Para volver a crear y ejecutar el componente de código, siga estos pasos:
  
1. Ahora que ha implementado la lógica del componente, vuelva al símbolo del sistema para volver a crearla mediante este comando:

```
npm run build
```

![Imagen 7](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-7.png)
  
2. Ejecute `npm start` para ejecutar el componente en la herramienta de ejecución de pruebas del nodo. También puede habilitar el modo de observación para garantizar que cualquier cambio en los siguientes activos se realice automáticamente sin tener que reiniciar la herramienta de ejecución de pruebas mediante el comando `npm start watch`.
  
- Archivo index.ts.

- Archivo ControlManifest.Input.xml.

- Bibliotecas importadas en index.ts.

- Todos los recursos enumerados en el archivo de manifiesto

![Imagen 8](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-8.png)
  
3. Vaya a la dirección de hospedaje en una ventana del navegador (la ventana posiblemente aparecerá automáticamente, pero también puede hacer referencia a la dirección que se encuentra en la ventana del comando) para observar el control en la herramienta de ejecución de pruebas.
  
![Imagen 9](https://github.com/CharlesPoint/GPPB2022/blob/main/Images/Lab2/picture-9.jpg)
