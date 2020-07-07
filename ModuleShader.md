ModuleShader utilises the WebGL API, specifically GLSL.

Take a look at the [Kaleidoscope module](https://github.com/2xAA/modV/blob/master/modules/Kaleidoscope.js) for a simple example of ModuleShader.

*For now, modV's ModuleShaders only really focus on the Fragment Shader.  
The Vertex Shader can be used, but only a 2 poly rectangle is available.  
For Vertex Shaders, you can use Module3D with THREE.js.*

## Using ModuleShader

To create a module using ModuleShader, we must first initialise a new instance

```JavaScript
class myModule extends modV.ModuleShader {
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
  name: 'My Module',        // REQUIRED: Name of the Module
  author: '2xAA',           // Author of Module
  version: 0.1,             // Version of Module
  meyda: [],                // Audio features passed to the Module as Uniform variables
  scripts: [],              /* Array of String paths to JS files your module requires.
                               This delays the registering of the module until all
                               external scripts are loaded. These scripts are not
                               sandboxed, so be selective with the files you load in */

  uniforms: {},             // Three.JS style Uniform variables (thanks Mr. Doob!)
  shaderFile: ""            /* REQUIRED: String path to HTML file within modules directory 
                               with shader script tags */
};
```

### settings.info.shaderFile

A ModuleShader requires a HTML file with the following script tags within the body tag for successful Shader compilation:

The Vertex Shader:

```HTML
<script id="vertexshader" type="x-shader/x-vertex">
  varying vec2 Vertex_UV;
  attribute vec2 a_position, a_texCoord;
  uniform vec2 u_resolution;
  void main() {
    vec2 zeroToOne = a_position / u_resolution;
    vec2 zeroToTwo = zeroToOne * 2.0;
    vec2 clipSpace = zeroToTwo - 1.0;
    gl_Position = vec4(clipSpace * vec2(1, -1), 0, 1);
    Vertex_UV = a_texCoord;
  }
</script>
```

The Fragment Shader:

```HTML
<script id="fragmentshader" type="x-shader/x-fragment">
  precision mediump float;
  uniform sampler2D u_modVCanvas;
  varying vec2 Vertex_UV;
  void main() {
    gl_FragColor = texture2D(u_modVCanvas, Vertex_UV);
  }
</script>

```

### Module2D.add()
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

### Register Module
To finish adding your Module to modV you must register it to the modV instance like so:

```JavaScript
modV.register(myModule);
```

This must be done outside of the class.

### File Format
Modules must be saved as JavaScript files in the 'module' folder with the extension '.modV.js' for modV to discover them.

### Available Uniforms

Currently, modV provides the following Uniform variables as standard:

| Variable | Info |
|---|---|
| u_delta | The Delta value from modV's main requestAnimationFrame loop (uniform1f) |
| u_time | The same as u_delta (uniform1f) (for compatibility, need to find a list of common uniforms) |
| u_modVCanvas | modV's main Canvas as a sampler location (uniform1i) (for use with sampler2D) |
| a_position | Vertex Position (vertexAttribPointer) |
| u_resolution | modV's current Canvas resolution as vec2. width,height (uniform2f) |