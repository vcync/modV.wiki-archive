# modV.TextControl()

A Text Control adds a HTML Input to a Module's generated control panel.

```JavaScript
const TextControl = new modV.TextControl({
  variable: 'message',      // String: local variable to write input value to
  label: 'Type something',  // String: label for control
  default: 'modV'           /* (optional) String: initiates local variable within Module
                                 (in this case "this.message") */
});
```

### TextControl key commands
TextControls can be reset with ```ctrl+click``` on Windows and Linux and with ```⌘+click``` on Mac to their default value if set.

### TextControl.makeNode()

### TextControl.getID()

### TextControl.getSettings()