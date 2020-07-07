modV.on('eventID', value1, value2...)

| Event ID         | Values                                   |
| ---------------- | ---------------------------------------- |
| moduleRegister | Module[Module2D, Module3D, ModuleShader] |
| controlUpdate    | Control[Control, \*Control, CustomControl]        |
| layerAdd         | Layer[Layer], index[Integer]             |
| layerRemove      | Layer[Layer], index[Integer]             |
| layerReorder     | Layer[Layer], oldIndex[Integer], newIndex[Integer] |
| midiInput        | ??? (currently set to scope of modV.MIDIInstance - will most likely deprecate in favour of MIDI events being handled solely by a plugin) |



Layer.on('eventID', value1, value2...)

| Event ID        | Values                                   |
| --------------- | ---------------------------------------- |
| moduleAdd       | Module[Module2D, Module3D, ModuleShader], index[Integer] |
| moduleRemove    | Module[Module2D, Module3D, ModuleShader], index[Integer] |
| moduleReorder   | Module[Module2D, Module3D, ModuleShader], index[Integer] |
| enabledSet         | enabled[Boolean]                         |
| nameChange      | name[String]                             |
| clearingSet     | value[Boolean]                           |
| alphaSet        | value[Float]                             |
| enabledSet      | value[Boolean]                           |
| inheritSet      | value[Boolean]                           |
| inheritFromSet  | layerIndex[Integer]                      |
| pipelineSet     | value[Boolean]                           |
| drawToOutputSet | value[Boolean]                           |
| lockedSet          | value[Boolean]                           |
| blendingSet        | value[String]                            |