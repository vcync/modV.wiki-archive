ModuleScript gives access to the Module2D Canvas and the ModuleShader WebGL context, primarily for operations involving imageData.

Ideally you should not use ModuleScript to draw to either the WebGL or the 2D contexts.

## Using ModuleScript

To create a module using ModuleScript, we must first initialise a new instance

```JavaScript
class myModule extends modV.ModuleScript {
	constructor() {
		super(settings);
	}

	init() {

	}

	resize() {

	}

	loop() {

	}
}
```

In our settings object we provide information about our Module.

We must provide the Module info.

### settings.info

```JavaScript
settings.info = {
	name: 'My Module',			// Name of the Module
	author: '2xAA', 			// Author of Module
	version: 0.1, 				// Version of Module
	meyda: [], 					// Audio features
	previewWithOutput: false 	// Show Gallery preview with current output mixed or not
	scripts: []					/* Array of String paths to JS files your module requires.
								   This delays the registering of the module until all
								   external scripts are loaded. These scripts are not
								   sandboxed, so be selective with the files you load in */
};
```

### ModuleScript.loop()
The loop function is passed 8 arguments:

|Argument	|Type						|Info	|
|---		|---						|---	|
|canvas		|[HTMLCanvasElement](https://developer.mozilla.org/en/docs/Web/API/HTMLCanvasElement)			|Main Canvas drawn to within modV|
|ctx		|[CanvasRenderingContext2D](https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D)	|Context of the main Canvas|
|video		|[HTMLVideoElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLVideoElement)			|The webcam source video element|
|features	|[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)						|Features requested by modules returned by Meyda|
|meyda		|[Meyda](github.com/hughrawlinson/meyda)						|The initialised Meyda object (for Windowing functions mainly)|
|delta		|[DOMHighResTimeStamp](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp)		|Returned by the requestAnimationFrame call|
|bpm		|[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)						|The approximate BPM of the audio source returned from [BeatDetektor](https://github.com/cjcliffe/beatdetektor)|
|kick		|[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)|The Bass Kick detection exposed by [BeatDetektor](https://github.com/cjcliffe/beatdetektor). True if kick, false otherwise.|
|gl		|[WebGLRenderingContext](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext)|Context of the [ModuleShader](https://github.com/2xAA/modV/wiki/ModuleShader) WebGL Canvas|


```JavaScript
loop(canvas, ctx, video, features, meyda, delta, bpm, kick, gl) {
	// Some image process	
};

```

### ModuleScript.init()
We can also set an initialisation function which is called upon the Module's creation in the active list.

The init function is passed 1 argument:

|Argument	|Type						|Info	|
|---		|---						|---	|
|canvas		|[HTMLCanvasElement](https://developer.mozilla.org/en/docs/Web/API/HTMLCanvasElement)			|Main Canvas drawn to within modV|

```JavaScript
init(canvas) {
	// Example code
};
```

### ModuleScript.resize()
We use the resize function to monitor viewPort size changes. This is useful if you're managing another canvas within your Module, for example.

The init function is passed 1 argument:

|Argument	|Type						|Info	|
|---		|---						|---	|
|canvas		|[HTMLCanvasElement](https://developer.mozilla.org/en/docs/Web/API/HTMLCanvasElement)			|Main Canvas drawn to within modV|

```JavaScript
resize(canvas) {
	// ...resize code
};
```

### ModuleScript.add()
This method allows you to attach UI controls to the Module to modify public variables.  
You can add controls in the constructor function.

You may either add controls one by one such as:

```JavaScript
constructor() {
	super(settings);
	
	this.add(new modV.CheckboxControl(controlSettings));
}
```

Or use an array:

```JavaScript
constructor() {
	super(settings);

	var controls = [];
	controls.push(new modV.CheckboxControl(controlSettings));
	controls.push(new modV.RangeControl(otherControlSettings));
	this.add(controls);
}
```
For more information on modV Controls, please check out the Controls page.

### Adding methods
You may add your own custom functions to the class.

Check out the [Balls Module](https://github.com/2xAA/modV/blob/master/modules/Ball.js) for a good example of this.

```JavaScript

	customFunction() {
		alert("I'm a custom function.");
	}
```

### Register Module
To finish adding your Module to modV you must register it to the modV instance like so:

```JavaScript
modV.register(myModule);
```

This must be done outside of the class.

### File Format
Modules must be saved as JavaScript files in the 'module' folder with the extension '.modV.js' for modV to discover them.