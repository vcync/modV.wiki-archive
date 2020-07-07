As I write the 2.0 Plugin format, I feel Modules should also update to a loose Object structure.

This plays nicely with keeping state secular also, which should be useful when modV is updated to use OffscreenCanvas. 

```JavaScript
import fragmentShader from './Plasma/plasma.frag';

export default {
  name: 'Plasma',
  author: '2xAA',
  version: '1.0.0',
  audioFeatures: [], // returned variables passed to the shader individually as uniforms
  type: 'shader',

  props: {
    u_scale: {
      label: 'Scale',
      type: 'vec2',
      x: {
        min: 1,
        max: 150,
        step: 1,
        default: 50,
      },
      y: {
        min: 1,
        max: 150,
        step: 1,
        default: 50,
      },
    },

    u_timeScale: {
      label: 'Time Scale',
      type: 'float',
      min: 1,
      max: 1000,
      default: 50,
    },
  },

  fragmentShader,
};

```