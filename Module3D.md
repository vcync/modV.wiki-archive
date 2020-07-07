Module3D utilises WebGL via [THREE.js](https://threejs.org/).

Take a look at the [3D Module](https://github.com/2xAA/modV/blob/master/modules/3D.js) for an example of Module3D.

## Module3D

To create a module using Module3D, we must first initialise a new instance

```JavaScript
class myModule extends modV.Module3D {
  constructor() {
    super(settings);
  }

  init() {

  }

  resize() {

  }

  draw() {

  }
}
```

In our settings object we provide information about our Module.

We must provide the Module info.

### settings.info

```JavaScript
settings.info = {
  name: 'My Module',        // Name of the Module
  author: '2xAA',           // Author of Module
  version: 0.1,             // Version of Module
  meyda: [],                // Audio features
  previewWithOutput: false  // Show Gallery preview with current output mixed or not
  scripts: []               /* Array of String paths to JS files your module requires.
                               This delays the registering of the module until all
                               external scripts are loaded. These scripts are not
                               sandboxed, so be selective with the files you load in */
};
```

### Module3D.init()
The init function is passed 4 arguments:

|Argument |Type           |Info |
|---    |---            |---  |
|canvas   |[HTMLCanvasElement](https://developer.mozilla.org/en/docs/Web/API/HTMLCanvasElement)     |Main Canvas drawn to within modV|
|scene    |[THREE.Scene](https://threejs.org/docs/#Reference/Scenes/Scene)      |New Scene generated for the Module|
|material |[Three.MeshBasicMaterial](https://threejs.org/docs/?q=material#Reference/Materials/MeshBasicMaterial)      |Using the modV Canvas texture as a map and the sides set to ```THREE.DoubleSide```|
|texture  |[Three.Texture](https://threejs.org/docs/?q=text#Reference/Textures/Texture)|modV's main Canvas as a Texture|

```JavaScript
init(canvas, scene, material, texture) {
  
  const camera;
  // code to set up camera...
  
  this.geometry = new THREE.SphereGeometry( 5, 32, 32 );
  this.sphere = new THREE.Mesh(this.geometry, material);
  scene.add(this.sphere);

  this.setScene(scene);
  this.setCamera(camera);
}
```

### Module3D.draw()
The draw function is passed 5 arguments:

|Argument |Type           |Info |
|---    |---            |---  |
|scene    |[THREE.Scene](https://threejs.org/docs/#Reference/Scenes/Scene)      |The Scene set by setScene() or the Scene generated on the Module's creation|
|camera   |[THREE.Camera](https://threejs.org/docs/?q=camera#Reference/Cameras/Camera)      |The Camera set by setCamera() or null|
|material |[Three.MeshBasicMaterial](https://threejs.org/docs/?q=material#Reference/Materials/MeshBasicMaterial)      |Using the modV Canvas texture as a map and the sides set to ```THREE.DoubleSide```|
|texture  |[Three.Texture](https://threejs.org/docs/?q=text#Reference/Textures/Texture)|modV's main Canvas as a Texture|
|features |[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)|Features requested by modules returned by Meyda|

```JavaScript
draw(scene, camera, material, texture, features) {
  const obj = this.sphere;
  const scale = this.size + features.rms;

  obj.rotation.x += this.speed * 0.005;
  obj.rotation.y += this.speed * 0.01;
  obj.scale.set(scale, scale, scale);
}
```

### Module3D.resize()
We use the resize function to monitor viewPort size changes. This is useful if you're managing Cameras or another canvas within your Module, for example.

The resize function is passed 5 arguments:

|Argument |Type           |Info |
|---    |---            |---  |
|canvas   |[HTMLCanvasElement](https://developer.mozilla.org/en/docs/Web/API/HTMLCanvasElement)     |Main Canvas drawn to within modV|
|scene    |[THREE.Scene](https://threejs.org/docs/#Reference/Scenes/Scene)      |The Scene set by setScene() or the Scene generated on the Module's creation|
|camera   |[THREE.Camera](https://threejs.org/docs/?q=camera#Reference/Cameras/Camera)      |The Camera set by setCamera() or null|
|material |[Three.MeshBasicMaterial](https://threejs.org/docs/?q=material#Reference/Materials/MeshBasicMaterial)      |Using the modV Canvas texture as a map and the sides set to ```THREE.DoubleSide```|
|texture  |[Three.Texture](https://threejs.org/docs/?q=text#Reference/Textures/Texture)|modV's main Canvas as a Texture|

```JavaScript
resize(canvas, scene, camera, material, texture) {
  const WIDTH = canvas.width;
  const HEIGHT = canvas.height;

  const ratio = WIDTH / HEIGHT;
  const zoom = camera.top;
  const newWidth = zoom * ratio;
  
  // update orthographic camera
  
  camera.left = -Math.abs(newWidth);
  camera.right = newWidth;
  camera.bottom = -Math.abs(zoom);
  
  camera.updateProjectionMatrix();
}
```

### Module3D.setScene(scene)
setScene is used to set the Module's Scene to use while drawing.  
Typically this should be used within the init function, but can be used anywhere within the Module3D Class.

The setScene function recieves 1 argument:

|Argument |Type           |Info |
|---    |---            |---  |
|scene    |[THREE.Scene](https://threejs.org/docs/#Reference/Scenes/Scene)||

### Module3D.getScene()
getScene is used to get the Module's Scene set by setScene() or the Scene generated on the Module's creation.

The getScene function returns:

|Argument |Type           |Info |
|---    |---            |---  |
|scene    |[THREE.Scene](https://threejs.org/docs/#Reference/Scenes/Scene)||

### Module3D.setCamera(camera)
setScene is used to set the Module's Camera to use while drawing.  
Typically this should be used within the init function, but can be used anywhere within the Module3D Class.

The setCamera function recieves 1 argument:

|Argument |Type           |Info |
|---    |---            |---  |
|camera   |[THREE.Camera](https://threejs.org/docs/?q=camera#Reference/Cameras/Camera)|Can be any type of Three compatible camera|

### Module3D.getCamera()
getCamera is used to get the Module's Camera set by setCamera().

The getCamera function returns:

|Argument |Type           |Info |
|---    |---            |---  |
|camera   |[THREE.Camera](https://threejs.org/docs/?q=camera#Reference/Cameras/Camera)|Can be any type of Three compatible camera|

### Module3D.add()
This method allows you to attach UI controls to the Module to modify public variables.  
You can add controls in the contructor function.

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

  const controls = [];
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