# modV.RangeControl()

A Range Control adds a HTML Input with Range type to a Module's generated control panel.

```JavaScript
const RangeControl = new modV.RangeControl({
  variable: 'amount',    // String: local variable within Module to write input value to
  label: 'Amount',       // String: label displayed for the control
  min: 0,                // Number: minimum number in range
  max: 30,               // Number: maximum number in range
  varType: 'int',        // String: must be "int" or "float"
  step: 1,               // Number: the amount to increment on each step
  default: 25            /* (optional) Number: initiates local variable within Module
                            (in this case "this.amount") */
});
```

### RangeControl key commands
RangeControls can be reset with ```ctrl+click``` on Windows and Linux and with ```⌘+click``` on Mac to their default value if set.

RangeControls can be made to have a finer grain of control by holding ```ctrl``` while dragging the slider, for further reduction of the step value press ```shift``` and ```ctrl``` in unison whilst dragging.

### RangeControl.makeNode()

### RangeControl.getID()

### RangeControl.getSettings()