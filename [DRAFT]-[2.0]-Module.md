```javascript
  /**
   * @typedef {Object} Module
   * @property {Object}   meta So meta
   * @property {String}   meta.name Name of the Module
   * @property {Object}   props     Accepts values of {@link ModuleProp} with the key being the name
   *                                of a variable on the Module's scope. Reserved keys are
   *                                `meta | props | data | init | resize | save | load` and any other
   *                                property defined by the Module type, required or optional.
   * @propert  {Object}   data
   * @property {Function} init
   * @property {Function} resize
   * @property {Function} save
   * @property {Function} load
   **/

  /**
   * @typedef {Module} Module2D
   * @property {String}   meta.type=2d
   * @property {Function} draw
   **/

  /**
   * @typedef {Module} ModuleShader
   * @property {String} meta.type=shader
   * @property {String} fragmentShader
   * @property {String} vertexShader
   **/

  /**
   * @typedef {Module} ModuleIsf
   * @property {String} meta.type=isf
   * @property {String} fragmentShader
   * @property {String} vertexShader
   **/

  /**
   * @typedef {Object} ModuleProp
   * @property {String}            type
   * @property {Function}          set
   * @property {String}            [label]
   * @property {any}               [default]
   * @property {ModulePropControl} control
   **/

  /**
   * @typedef {Object} ModulePropControl
   * @property {String} type
   * @property {Object} [options]
   **/

  /**
   * @typedef {ModuleProp} ModulePropInt
   * @property {String}  type=int
   * @property {Number}  [min=undefined]
   * @property {Number}  [max=undefined]
   * @property {Number}  [default=undefined]
   * @property {Boolean} [strict=false]
   **/

  /**
   * @typedef {ModuleProp} ModulePropFloat
   * @property {String}  type=float
   * @property {Number}  [min=undefined]
   * @property {Number}  [max=undefined]
   * @property {Number}  [default=undefined]
   * @property {Boolean} [strict=false]
   **/

  /**
   * @typedef {ModuleProp} ModulePropEnum
   * @property {String}                     type=float
   * @property {Array<ModulePropEnumItem>}  enum
   **/

  /**
   * @typedef {Object} ModulePropEnumItem
   * @property {String} [label]
   * @property {any} value
   **/

```