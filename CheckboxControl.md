# modV.CheckboxControl()

A Checkbox Control adds a HTML Input with checkbox type to a Module's generated control panel.

```JavaScript
const CheckboxControl = new modV.CheckboxControl({
  variable: 'fillOrLine',    // String: local variable to write input value to
  label: 'Fill/Line',        // String: label for control
  checked: true              /* (optional) Boolean: initiates local variable within Module
                                (in this case "this.fillOrLine") */
});
```

### CheckboxControl key commands
CheckboxControls can be reset with ```ctrl+click``` on Windows and Linux and with ```⌘+click``` on Mac to their initial checked value if set.

### CheckboxControl.makeNode()

### CheckboxControl.getID()

### CheckboxControl.getSettings()