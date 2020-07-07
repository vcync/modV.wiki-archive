```JavaScript
import controlPanelComponent from './ControlPanel';
import galleryTabComponent from './Gallery';
import store from './store'; // the store module for the plugin


export default {
  name: 'Plugin Name',
  controlPanelComponent,
  galleryTabComponent,
  store,
  storeName: 'myAwesomeStoreName', // optional: if not set, the plugin name will be converted to camelCase  
  
  /**
   * Called when plugin is enabled
   */
  on() {
  
  },

  /**
   * Called when plugin is disabled
   */
  off() {
  
  },
  
  presetData: {
    /**
     * Data to save to a preset
     */
    save() {
      const { assignments, devices } = store.state.midiAssignment;

      return {
        assignments,
        devices,
      };
    },
    
    /**
     * Saved plugin data loaded from a previously saved preset
     * 
     * @param{any} data - the previously saved data
     */
    load(data) {
      
    },
  },

  pluginData: {
   /**
     * Save plugin data to a project
     */
    save() {
      return {
        data: 'to save',
      };
    },
    
    /**
     * Load saved data from data saved to a project.
     * 
     * @param{any} data - the previously saved data
     */
    load(data) {
      console.log('data loaded', data.data === 'to save');
    },
  },
  
  /**
   * Resize method
   *
   * @param{Object} canvas - The modV output canvas
   */
  resize(canvas) {
    
  },

  /**
   * Only called when added to modV.
   */
  install(Vue, store) {
    // Vue.component(controlPanelComponent.name, controlPanelComponent);

    store.subscribe((mutation) => {
      if (mutation.type === 'windows/setSize') {
        
      }
    });
  },

  /* process
   * Called once every frame.
   * Useful for plugins which need to process data away from modV
   */
  process({ delta }) {
    // this.delta = delta;
  },

  /* processValue
   * Called once every frame.
   * Allows access of each value of every active Module.
   * (see expression plugin for an example)
   */
  processValue({ currentValue, moduleName, controlVariable }) {

  },

  /**
   * Called once every frame.
   * Allows access of each frame drawn to the screen.
   *
   * @param{Object} canvas - The modV output canvas
   */
  processFrame({ canvas }) {
    
  },
};

```