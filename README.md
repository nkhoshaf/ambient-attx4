#Ambient
Driver for the ambient-attx4 Tessel ambient (light and sound detecting) module.

Use the Ambient module to gather data about the ambient light and sound levels.

The module currently supports 'streams' of light levels and sound levels, as well as trigger levels for light and sound levels. You can use triggers to get notified when, for example, a light turns on or somebody claps.

All the values received and used for triggers are between 0.0 and 1.0.

You'll notice that the light readings seem to be logarithmic - when making the ambient light brighter, the reading will increase slowly and then get faster. That's a property of the photodiode itself.

##TODO
Make functions to trigger when light/sound drops below a level (currently supports "light turned on" but not "light turned off")

##Installation
```sh
npm install ambient-attx4
```

##Example
```js
/*********************************************
This ambient module example reports sound and
light levels to the console, and console.logs
whenever a specified light or sound level
trigger is met.
*********************************************/

var tessel = require('tessel');
var ambientPort = tessel.port('a');

// Import the ambient library and use designated port
require('ambient-attx4').use(ambientPort, function(err, ambient) {

  // If there was a problem
  if (err) {
    // Report it and return
    return console.log("Error initializing:", err);
  }

 // Get a stream of light data
  ambient.on('light', function(data) {
    console.log("Got some  light: ", data);
  });

  // Get a stream of sound level data
  ambient.on('sound', function(data) {
    console.log("Got some  sound: ", data);
  });

  // Set trigger levels
  // The trigger value is a float between zero to 1
  ambient.setLightTrigger(0.15);

  ambient.on('light-trigger', function(data) {
    console.log("Our light trigger was hit:", data);

    // Clear the trigger so it stops firing
    ambient.clearLightTrigger();
  });


  // Set a sound level trigger
  // The trigger is a float between 0 and 1
  // Basically any sound will trip this trigger
  ambient.setSoundTrigger(0.001);

  ambient.on('sound-trigger', function(data) {

    console.log("Something happened with sound: ", data);

    // Clear it
    ambient.clearSoundTrigger();
  });
});

setInterval(function() {}, 200);
```

##Methods

##### * `ambient.clearLightTrigger(callback(err, triggerVal))` Clears trigger listener for light trigger.

##### * `ambient.clearSoundTrigger(callback(err, triggerVal))` Clears trigger listener for sound trigger.

##### * `ambient.getLightBuffer(callback(err, data))` Gets the last 20 light readings.

##### * `ambient.getLightLevel(callback(err, data))` Gets a single data point of light level.

##### * `ambient.getSoundBuffer(callback(err, data))` Gets the last 20 sound readings.

##### * `ambient.getSoundLevel(callback(err, data))` Gets a single data point of sound level.

##### * `ambient.setLightTrigger(triggerVal, callback(err, triggerVal))` Sets a trigger to emit a 'light-trigger' event when triggerVal is reached. `triggerVal` is a float between 0 and 1.0.

##### * `ambient`.setSoundTrigger(triggerVal, callback(err, triggerVal))` Sets a trigger to emit a 'sound-trigger' event when triggerVal is reached. `triggerVal` is a float between 0 and 1.0.

##Events

##### * `ambient.on('error', callback(err))` Emitted upon error.

##### * `ambient.on('light', callback(lightData))` Get a stream of light data.

##### * `ambient.on('light-trigger', callback(lightTriggerValue))` Emitted upon crossing light trigger threshold.

##### * `ambient.on('ready', callback())` Emitted upon first successful communication between the Tessel and the module.

##### * `ambient.on('sound', callback(soundData))` Get a stream of sound level data.

##### * `ambient.on('sound-trigger', callback(soundTriggerValue))` Emitted upon crossing sound trigger threshold.

## License

MIT
APACHE
