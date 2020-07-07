# modV.PaletteControl()

Palette Control adds a modV Palette Control to a Module's generated control panel.

```JavaScript
const PaletteControl = new modV.PaletteControl({
  variable: 'color',    /* String: local variable to write input value to.
                           Also initiates local variable within Module (in this case
                           "this.color") with the first color in the 'colors'
                           array below */
                   
  label: 'Palette',     // String: label for control
  colors: [             // Array: RGB colour values (0-255) as ints. [RED, GREEN, BLUE]
    [122,121,120],
    [135,203,172],
    [144,255,220],
    [141,228,255],
    [138,196,255]
  ],
  timePeriod: 500       /* Integer: the default number of milliseconds to cycle from one
                           color to the next */
});
```

### PaletteControl.makeNode()

### PaletteControl.getID()

### PaletteControl.getSettings()