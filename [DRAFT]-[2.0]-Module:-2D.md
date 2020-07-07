As I write the 2.0 Plugin format, I feel Modules should also update to a loose Object structure.

This plays nicely with keeping state secular also, which should be useful when modV is updated to use OffscreenCanvas. 

```JavaScript
import Meyda from 'meyda';

export default {
  name: 'Waveform',
  author: '2xAA',
  version: '1.0.0',
  audioFeatures: ['buffer'],
  type: '2d',
  
  props: {
    strokeWeight: {
      label: 'Stroke',
      type: 'int',
      min: 1,
      max: 30,
      default: 1,
      strict: true,
    },

    maxHeight: {
      label: 'Height',
      type: 'float',
      min: 1,
      max: 100,
      default: 75,
    },

    windowing: {
      type: 'enum',
      enum: [
        { label: 'Rectangular (no window)', value: 'rect' },
        { label: 'Hanning', value: 'hanning', selected: true },
        { label: 'Hamming', value: 'hamming' },
        { label: 'Blackman', value: 'blackman' },
        { label: 'Sine', value: 'sine' },
      ],
    },

    color: {
      type: 'vec4',

      // explicitly define a control
      control: {
        type: 'palette',

        // pass options to the control
        options: {
          colors: [
            [255, 0, 0, 1],
            [0, 255, 0, 1],
            [0, 0, 255, 1],
          ],
        },
      },
    },
  },

  // Vue.js-like data handling?
  data() {
    return {

    };
  },

  draw({ canvas, context, features }) {
    const { width, height } = canvas;
    const bufferLength = features.buffer.length;
    const buffer = Meyda.windowing(features.buffer, this.windowing);

    context.lineWidth = this.strokeWeight;
    context.strokeStyle = this.colour;
    context.beginPath();

    const sliceWidth = width / bufferLength;
    let x = 0;

    for (let i = 0; i < bufferLength; i += 1) {
      const v = (buffer[i] / 100) * this.maxHeight;
      const y = (height / 2) + ((height / 2) * v);

      if (i === 0) {
        context.moveTo(x, y);
      } else {
        context.lineTo(x, y);
      }

      x += sliceWidth;
    }

    context.lineTo(width, height / 2);
    context.stroke();
  },
};
```