As I write the 2.0 Plugin and Module formats, I feel Layers also update to a loose Object structure.

```JavaScript
  /**
   * @typedef {Object} Layer
   * @property {String}  name                   Name of the Layer
   * @property {Number}  position               Position of the Layer
   * @property {Array}   modules                The draw order of the Modules contained within the Layer
   * @property {Boolean} enabled                Indicates whether the Layer should be drawn
   * @property {Number}  alpha                  The level of opacity, between 0 and 1, the Layer should
   *                                            be muxed at
   * @property {Boolean} inherit                Indicates whether the Layer should inherit from another
   *                                            Layer at redraw
   * @property {Number}  inheritFrom            The target Layer to inherit from, -1 being the previous
   *                                            Layer in modV#layers, 0-n being the index of another Layer
   *                                            within modV#layers
   * @property {Boolean} pipeline               Indicates whether the Layer should render using pipeline
   *                                            at redraw
   * @property {Boolean} clearing               Indicates whether the Layer should clear before redraw
   * @property {String}  compositeOperation     The {@link Blendmode} the Layer muxes with
   *
   * @example
   * const Layer = {
   *   name: 'Layer',
   * 
   *   position: 0,
   * 
   *   modules: [
   *     'Module Name',
   *     'Another Module Name',
   *     'Waveform',
   *   ],
   * 
   *   enabled: true,
   * 
   *   alpha: 1,
   * 
   *   inherit: true,
   * 
   *   inheritFrom: -1,
   * 
   *   pipeline: false,
   * 
   *   clearing: false,
   * 
   *   compositeOperation: 'normal',
   * };
   **/
```